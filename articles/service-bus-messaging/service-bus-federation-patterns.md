---
title: メッセージ レプリケーション タスクのパターン - Azure Service Bus | Microsoft Docs
description: この記事では、特定のメッセージ レプリケーション タスクのパターンを実装するための詳細なガイダンスを提供します
ms.topic: article
ms.date: 09/28/2021
ms.openlocfilehash: 4effcb9f51532cb2ef87b18b264789c526b57585
ms.sourcegitcommit: e8c34354266d00e85364cf07e1e39600f7eb71cd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/29/2021
ms.locfileid: "129211793"
---
# <a name="message-replication-tasks-patterns"></a>メッセージ レプリケーション タスクのパターン

[フェデレーションの概要](service-bus-federation-overview.md)と[レプリケーター関数の概要](service-bus-federation-replicator-functions.md)に関するページでは、レプリケーション タスクの原理と基本要素について説明しています。この記事を読み進める前にこれらについてよく理解しておくことをお勧めします。

この記事では、概要セクションで強調されているいくつかのパターンの実装ガイダンスについて詳しく説明します。 

## <a name="replication"></a>レプリケーション 

レプリケーション パターンでは、あるキューまたはトピックから次のものに、あるいはキューまたはトピックからイベント ハブのような他の何らかの宛先にメッセージをコピーします。 メッセージは、メッセージ ペイロードを変更することなく転送されます。 

このパターンの実装は、[Azure Service Bus 間でのメッセージ レプリケーション](https://github.com/Azure-Samples/azure-messaging-replication-dotnet/tree/main/functions/config/ServiceBusCopy) サンプルの対象となります。

### <a name="sequences-and-order-preservation"></a>シーケンスと順序の維持

レプリケーション モデルの目的は、ソース キューまたはトピックからターゲット キューまたはトピックへのメッセージの絶対順序を維持することではありませんが、必要に応じて、アプリケーションで必要なメッセージの相対順序を維持することに重点を置いています。 アプリケーションでは、ソース エンティティのセッション サポートを有効にし、[セッション キー](message-sessions.md)が同じである関連メッセージをグループ化することで、これを可能にします。

セッション対応の事前に構築されたレプリケーション関数を使用すると、ソース エンティティから取得されたものと同じセッション ID を持つメッセージ シーケンスが、同じセッション ID で元のシーケンスのバッチとしてターゲット キューまたはトピックに確実に送信されます。 

### <a name="service-assigned-metadata"></a>サービスによって割り当てられたメタデータ 

ソース キューまたはトピックから取得されたメッセージのサービスによって割り当てられたメタデータ、元のエンキュー時刻およびシーケンス番号は、ターゲット キューまたはトピックのサービスによって割り当てられた新しい値に置き換えられますが、サンプルで提供されている既定のレプリケーション タスクでは、元の値は次のユーザー プロパティに保持されます: `repl-enqueue-time` (ISO8601 文字列) と `repl-sequence`。

これらのプロパティは文字列型であり、それぞれの元のプロパティの文字列化された値が含まれています。  複数回メッセージが転送される場合は、直接のソースのサービスによって割り当てられたメタデータが既存のプロパティに追加され、値はセミコロンで区切られます。 

### <a name="failover"></a>[フェールオーバー]

ディザスター リカバリーのためにレプリケーションを使用する場合、Service Bus サービスのリージョンの可用性メッセージから、あるいはネットワークの中断から保護するために、このような障害シナリオでは、あるキューまたはトピックから次のものへのフェールオーバーを実行する必要があります。これにより、プロデューサーやコンシューマーに対して、セカンダリ エンドポイントを使用するように指示されます。

すべてのフェールオーバー シナリオでは、名前空間の必須要素が構造的に同一であることが前提となります。これは、キューとトピックは同じ名前で、共有アクセス署名規則やロールベースのアクセス制御規則が同じ方法で設定されることを意味します。 [名前空間の移動に関するガイダンス](move-across-regions.md)に従い、クリーンアップ手順を省略して、セカンダリ名前空間を作成 (および更新) することができます。

プロデューサーとコンシューマーを強制的に切り替えるには、参照にどの名前空間を使用するかに関する情報をアクセスと更新が容易な場所で利用可能にする必要があります。 プロデューサーまたはコンシューマーは頻繁に発生するまたは永続的なエラーを検出した場合、その場所を確認し、それらの構成を調整する必要があります。 その構成を共有するためのさまざまな方法がありますが、ここでは次の 2 つを取り上げます: DNS とファイル共有。

#### <a name="dns-based-failover-configuration"></a>DNS ベースのフェールオーバー構成

1 つの候補として、制御する DNS で DNS SRV レコードの情報を保持し、それぞれのキューまたはトピックのエンドポイントを指す方法があります。 Message Hubs では、そのエンドポイントを CNAME レコードで直接エイリアス化することが許可されないことにご注意ください。つまり、IP アドレス情報を直接解決するのではなく、エンドポイント アドレスに対して回復力のある参照メカニズムとして DNS を使用します。 

ドメイン `example.com` を所有しているとします。アプリケーションのゾーンは `test.example.com` です。 2 つの代替の Service Bus に対して、ここでさらに入れ子になった 2 つのゾーンとそれぞれの SRV レコードを作成します。 

SRV レコードには、一般的な規則に従って、先頭に `_azure_servicebus._amqp` が付けられ、2 つのエンドポイント レコードが保持されます。1 つはポート 5671 の AMQP over TLS 用で、もう 1 つはポート 443 の AMQP over WebSockets 用です。これらの両方が、ゾーンに対応する名前空間の Service Bus エンドポイントを指しています。

| ゾーン                 | SRV レコード
|----------------------|-------------------------------------------------------------
| `sb1.test.example.com` | **`_azure_servicebus._amqp.sb1.test.example.com`**<br>`1 1 5671 sb1-test-example-com.servicebus.windows.net`<br>`2 2 443 sb1-test-example-com.servicebus.windows.net`
| `sb2.test.example.com` | **`_azure_servicebus._amqp.sb1.test.example.com`**<br>`1 1 5671 sb2-test-example-com.servicebus.windows.net`<br>`2 2 443 sb2-test-example-com.servicebus.windows.net`

次に、アプリケーションのゾーンで、プライマリ キューまたはトピックに対応する下位ゾーンを指す CNAME エントリを作成します。

| CNAME レコード                 | エイリアス
|------------------------------|-------------------------------------------------------------
| `servicebus.test.example.com`  | `sb1.test.example.com`

その後、明示的な CNAME および SRV レコードに対するクエリの実行を許可する DNS クライアントを使用して (Java および .NET の組み込みクライアントで許可されるのは、IP アドレスへの名前のシンプルな解決のみ)、目的のエンドポイントを解決できます。 たとえば、[DnsClient.NET](https://dnsclient.michaco.net/) の場合、参照関数は次のようになります。

``` C#
static string GetServiceBusName(string aliasName)
{
    const string SrvRecordPrefix = "_azure_servicebus._amqp.";
    LookupClient lookup = new LookupClient();

    return (from CNameRecord alias in (lookup.Query(aliasName, QueryType.CNAME).Answers)
            from SrvRecord srv in lookup.Query(SrvRecordPrefix + alias.CanonicalName, QueryType.SRV).Answers
            where srv.Port == 5671
            select srv.Target).FirstOrDefault()?.Value.TrimEnd('.');
}
```

この関数からは、上記のように CNAME で現在エイリアス化されているゾーンのポート 5671 に登録されているターゲット ホスト名が返されます。 

フェールオーバーを実行するには、CNAME レコードを編集し、代替ゾーンを指定する必要があります。 

DNS (具体的には [Azure DNS](../dns/dns-overview.md)) を使用する利点は、Azure DNS の情報がグローバルにレプリケートされるため、単一リージョンの障害に対する回復性があることです。

この手順は、[Service Bus Geo-DR](service-bus-geo-dr.md) の場合と似ていますが、ユーザーが自分で完全に制御でき、アクティブ/アクティブ シナリオでも機能します。

#### <a name="file-share-based-failover-configuration"></a>ファイル共有ベースのフェールオーバー構成

エンドポイント情報の共有に DNS を使用する最もシンプルな代替方法は、プライマリ エンドポイントの名前をプレーンテキスト ファイルに格納し、障害に対して堅牢で、引き続き更新を許可するインフラストラクチャからファイルを提供することです。 

グローバル対応でコンテンツ レプリケーションが可能な高可用性 Web サイト インフラストラクチャを既に実行している場合は、このようなファイルをそこに追加し、切り替えが必要な場合はファイルを再発行します。

## <a name="merge"></a>マージする

マージ パターンには、1 つのターゲットを指す 1 つまたは複数のレプリケーション タスクがあります。また、通常のプロデューサーと同時に、同じターゲットにメッセージが送信される場合もあります。 

このパターンには次のような種類があります。
- 2 つ以上のレプリケーション関数で、別々のソースからメッセージを同時に取得し、それらを同じターゲットに送信する。
- もう 1 つのレプリケーション関数で、ソースからメッセージを取得するが、ターゲットはプロデューサーでも直接使用される。 
- パターンは前述のものだが、メッセージは 2 つ以上のトピック間でミラー化されるため、メッセージの生成場所に関係なく、それらのトピックには同じメッセージが含まれる。

最初の 2 つのパターンの違いはわずかですが、単純なレプリケーション タスクとは異なります。

最後のシナリオでは、既にレプリケートされているメッセージが再度レプリケートされないようにする必要があります。 この手法については、アクティブ/アクティブ サンプルで説明されています。

## <a name="editor"></a>エディター

エディター パターンは[レプリケーション](#replication) パターンに基づいていますが、メッセージは転送される前に変更されます。 そのような変更の例を以下に示します。

- "***コード変換***" - *Apache Avro* 形式または何らかの独自のシリアル化形式を使用して、エンコードされたソースからメッセージ コンテンツ ("本文" または "ペイロード" ともいう) が到着し、そのコンテンツが *JSON* エンコードされることが想定されている場合、コード変換レプリケーション タスクでは、まず *Apache Avro* からメモリ内オブジェクト グラフにペイロードを逆シリアル化してから、そのグラフを、転送中のメッセージに対して *JSON* 形式にシリアル化します。 また、コード変換には **コンテンツの圧縮** とその解除のタスクも含まれます。
- "***変換***" - 構造化データを含むメッセージでは、ダウンストリーム コンシューマーによる使用をより簡単にするために、そのデータのリシェイプが必要となる場合があります。 これには、入れ子構造のフラット化、余分なデータ要素の排除、特定のスキーマに正確に適合させるためのペイロードのリシェイプなどの作業が含まれる場合があります。
- "***バッチ処理***" - ソースからバッチでメッセージ (1 回の転送で複数のメッセージ) が受信される場合がありますが、ターゲットに 1 つずつ転送する必要があります。その逆の場合も同様です。 そのため、タスクで 1 つの入力メッセージの転送に基づいて複数のメッセージが転送されたり、一連のメッセージがまとめて転送されたりする場合があります。 
- "***検証***" - 外部ソースからのメッセージ データは多くの場合、転送する前に一連の規則に準拠しているかどうかを確認する必要があります。 これらの規則はスキーマまたはコードを使用して表すことができます。 準拠していないことが検出されたメッセージは、ログに記録された問題と共に削除されることもあれば、特別なターゲット宛先に転送されてさらに処理されることもあります。   
- "***エンリッチメント***" - 一部のソースから送信されるメッセージ データは、ターゲット システムで使用できるようにするためにさらにコンテキストでのエンリッチメントが必要な場合があります。 これには、参照データを検索し、そのデータをメッセージと共に埋め込んだり、レプリケーション タスクで認識されてはいるもののメッセージには含まれていないソースに関する情報を追加したりする作業が含まれる場合があります。 
- "***フィルター処理***" - ソースから到着する一部のメッセージは、何らかの規則に基づいてターゲットから除外する必要がある場合があります。 フィルターにより、規則に基づいてメッセージがテストされ、その規則と一致しない場合はメッセージが削除されます。 特定の条件を観察し、同じ値の後続のメッセージを削除することによって、重複メッセージをフィルター処理することは、フィルター処理の 1 つの形式です。
- "***ルーティングとパーティション分割***" - レプリケーション タスクによっては、2 つ以上の代替ターゲットが許可される場合があります。また、メッセージのメタデータまたはコンテンツに基づいて特定のメッセージに対して、レプリケーション ターゲットを選択するための規則を定義する場合もあります。 特別な形式のルーティングがパーティション分割であり、その場合、タスクでは規則に基づいて 1 つのレプリケーション ターゲットでパーティションを明示的に割り当てます。
- "***暗号化***" - レプリケーション タスクでは、ソースから到着するコンテンツの暗号化を解除したり、ターゲットに転送されるコンテンツを暗号化したりする必要がある場合があります。また、メッセージで伝達される署名を基準にコンテンツやメタデータの整合性を確認したり、そのような署名を添付したりする必要がある場合があります。 
- "***構成証明***" - レプリケーション タスクでは、特定のチャネルを介して、あるいは特定の時刻にメッセージが受信されたことを証明するメッセージに、デジタル署名で保護される可能性のあるメタデータを添付する場合があります。     
- "***チェーン***" - レプリケーション タスクでは、シーケンスの整合性が保護され、欠落しているメッセージを検出できるように、メッセージのシーケンスに署名を適用する場合があります。

これらのパターンはすべて Azure Functions を使用して実装でき、[Message Hubs トリガー](../azure-functions/functions-bindings-service-bus-trigger.md)を使用してメッセージを取得し、[キューまたはトピックの出力バインド](../azure-functions/functions-bindings-service-bus-output.md)を使用してそれらを配信します。 

## <a name="routing"></a>ルーティング

ルーティング パターンは[レプリケーション](#replication) パターンに基づいていますが、1 つのソースと 1 つのターゲットがあるのではなく、レプリケーション タスクに複数のターゲットがあります。これについては、以下に C# で示します。

``` csharp
[FunctionName("SBRouter")]
public static async Task Run(
    [ServiceBusTrigger("source", Connection = "serviceBusConnectionAppSetting")] Message[] messages,
    [ServiceBus("dest1", Connection = "serviceBusConnectionAppSetting")] QueueClient output1,
    [ServiceBus("dest2", Connection = "serviceBusConnectionAppSetting")] QueueClient output2,
    ILogger log)
{
    foreach (Message messageData in messages)
    {
        // send to output1 or output2 based on criteria 
    }
}
```

ルーティング関数では、メッセージ メタデータやメッセージ ペイロードを考慮し、送信先として使用可能な宛先のいずれかを選択します。

## <a name="next-steps"></a>次のステップ

- [Azure Functions のメッセージ レプリケーター アプリケーション][1]
- [Service Bus 間でのメッセージのレプリケート][2]
- [Azure Event Hubs へのメッセージのレプリケート][3]

[1]: service-bus-federation-replicator-functions.md
[2]: https://github.com/Azure-Samples/azure-messaging-replication-dotnet/tree/main/functions/config/ServiceBusCopy
[3]: https://github.com/Azure-Samples/azure-messaging-replication-dotnet/tree/main/functions/config/ServiceBusCopyToEventHub
