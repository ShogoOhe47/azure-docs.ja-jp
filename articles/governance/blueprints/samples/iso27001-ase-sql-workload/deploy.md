---
title: ISO 27001 ASE/SQL ワークロード ブループリント サンプルをデプロイする
description: ブループリント アーティファクト パラメーターの詳細を含む ISO 27001 App Service Environment/SQL Database ワークロード ブループリント サンプルのデプロイ手順。
ms.date: 09/08/2021
ms.topic: sample
ms.openlocfilehash: 553218028f610598f1b13cd4daebdb43f1ea1656
ms.sourcegitcommit: f6e2ea5571e35b9ed3a79a22485eba4d20ae36cc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2021
ms.locfileid: "128632103"
---
# <a name="deploy-the-iso-27001-app-service-environmentsql-database-workload-blueprint-sample"></a>ISO 27001 App Service Environment/SQL Database ワークロード ブループリント サンプルをデプロイする

Azure Blueprints ISO 27001 App Service Environment/SQL Database ワークロード ブループリント サンプルをデプロイするには、次の手順を実行する必要があります。

> [!div class="checklist"]
> - [ISO 27001 共有サービス](../iso27001-shared/index.md) ブループリント サンプルをデプロイする
> - サンプルから新しいブループリントを作成する
> - サンプルのコピーを **発行済み** としてマークする
> - ブループリントのコピーを既存のサブスクリプションに割り当てる

Azure サブスクリプションをお持ちでない場合は、開始する前に [無料アカウント](https://azure.microsoft.com/free) を作成してください。

## <a name="deploy-the-iso-27001-shared-services-blueprint-sample"></a>ISO 27001 共有サービス ブループリント サンプルをデプロイする

このブループリント サンプルをデプロイする前に、[ISO 27001 共有サービス](../iso27001-shared/index.md) ブループリント サンプルをターゲット サブスクリプションにデプロイする必要があります。 ISO 27001 共有サービス ブループリント サンプルが正常にデプロイされていないと、このブループリント サンプルはインフラストラクチャとの依存関係を失い、デプロイ中に失敗します。

> [!IMPORTANT]
> このブループリント サンプルは、[ISO 27001 共有サービス](../iso27001-shared/index.md) ブループリント サンプルと同じサブスクリプションに割り当てる必要があります。

## <a name="create-blueprint-from-sample"></a>サンプルからブループリントを作成する

最初に、サンプルをスターターとして使用して環境内に新しいブループリントを作成することにより、ブループリント サンプルを実装します。

1. 左側のウィンドウにある **[すべてのサービス]** を選択します。 **[ブループリント]** を探して選択します。

1. 左側の **[はじめに]** ページで、 _[ブループリントの作成]_ の下にある **[作成]** ボタンを選択します。

1. 検索、 **ISO 27001。ASE/SQL Workload** ブループリント サンプルを _その他のサンプル_ で検索し、**このサンプルを使用する** を選択します。

1. ブループリント サンプルの _[基本]_ を入力します。

   - **[ブループリントの名前]** : ISO 27001 ASE/SQL Workload ブループリント サンプルのコピーの名前を指定します。
   - **[定義の場所]** :省略記号を使用して、サンプルのコピーを保存する管理グループを選択します。

1. ページの上部にある _[アーティファクト]_ タブまたはページの下部にある **[次へ: アーティファクト]** を選択します。

1. ブループリント サンプルを構成するアーティファクトの一覧を確認します。 多くのアーティファクトには、後で定義するパラメーターがあります。 ブループリント サンプルの確認が完了したら、 **[下書きの保存]** を選択します。

## <a name="publish-the-sample-copy"></a>サンプルのコピーを発行する

環境でのブループリント サンプルのコピーの作成が完了しました。 これは **下書き** モードで作成されており、割り当ておよびデプロイの前に **発行** する必要があります。 ブループリント サンプルのコピーは、お使いの環境や必要性に応じてカスタマイズできますが、それが原因で ISO 27001 標準を満たさなくなる場合もあります。

1. 左側のウィンドウにある **[すべてのサービス]** を選択します。 **[ブループリント]** を探して選択します。

1. 左側の **[ブループリントの定義]** ページを選択します。 ブループリント サンプルのコピーを、フィルターを使用して検索し、選択します。

1. ページの上部にある **[ブループリントを発行する]** を選択します。 右側の新しいページで、ブループリント サンプルのコピーの **[バージョン]** を指定します。 このプロパティは、後で変更を加える場合に役立ちます。 **[変更に関するメモ]** (例:「ISO 27001 ブループリント サンプルから発行する最初のバージョン」) を入力します。 次に、ページの下部にある **[発行]** を選択します。

## <a name="assign-the-sample-copy"></a>サンプルのコピーを割り当てる

正常に **発行** されたブループリント サンプルのコピーは、保存先の管理グループ内のサブスクリプションに割り当てることができます。 この手順では、ブループリント サンプルのコピーの各デプロイを一意にするためのパラメーターを指定します。

1. 左側のウィンドウにある **[すべてのサービス]** を選択します。 **[ブループリント]** を探して選択します。

1. 左側の **[ブループリントの定義]** ページを選択します。 ブループリント サンプルのコピーを、フィルターを使用して検索し、選択します。

1. ブループリント定義ページの上部にある **[ブループリントの割り当て]** を選択します。

1. ブループリント割り当て用のパラメーター値を指定します。

   - 基本

     - **サブスクリプション**:ブループリント サンプルのコピーを保存した管理グループ内の 1 つ以上のサブスクリプションを選択します。 複数のサブスクリプションを選択すると、入力したパラメーターを使用して、それぞれに対して割り当てが作成されます。
     - **割り当て名**:名前は、ブループリントの名前に基づいてあらかじめ設定されています。
       必要に応じて変更することも、そのままにしておくこともできます。
     - **[場所]** :マネージド ID を作成するリージョンを選択します。 Azure Blueprint は、この管理対象 ID を使用して、割り当てられたブループリント内にすべての成果物をデプロイします。 詳細については、[Azure リソースの管理対象 ID の概要](../../../../active-directory/managed-identities-azure-resources/overview.md)に関するページをご覧ください。
     - **ブループリント定義ラベル**:ブループリント サンプルのコピーの **発行済み** バージョンを選択します。

   - ロックの割り当て

     お使いの環境のブループリントのロック設定を選択します。 詳細については、[ブループリント リソースのロック](../../concepts/resource-locking.md)に関するページを参照してください。

   - マネージド ID

     既定の _システム割り当て_ マネージド ID オプションはそのままにします。

   - ブループリントのパラメーター

     このセクションで定義するパラメーターは、一貫性を維持するために、ブループリント定義のアーティファクトの多くで使用されます。

     - **組織名**:組織の短縮名を入力します。 このプロパティは、主にリソースの名前付けのために使用されます。
     - **共有サービス サブスクリプション ID**: [ISO 27001 共有サービス](../iso27001-shared/index.md) ブループリント サンプルが割り当てられたサブスクリプション ID。
     - **既定のサブネット アドレス プレフィックス**: 仮想ネットワークの既定のサブネットの CIDR 表記。
       既定値は _10.1.0.0/24_ です。
     - **ワークロードの場所**: アーティファクトをデプロイする場所を決定します。 すべてのサービスがすべての場所で利用できるわけではありません。 このようなサービスをデプロイするアーティファクトには、そのアーティファクトをデプロイする場所についてのパラメーター オプションが用意されています。

   - アーティファクトのパラメーター

     このセクションで定義するパラメーターは、定義対象のアーティファクトに適用されます。 これらのパラメーターはブループリントの割り当て時に定義されるので、[動的パラメーター](../../concepts/parameters.md#dynamic-parameters)です。 アーティファクトのパラメーターとその説明を含む詳しい一覧については、「[アーティファクトのパラメーター表](#artifact-parameters-table)」を参照してください。

1. すべてのパラメーターの入力が完了したら、ページの下部にある **[割り当て]** を選択します。 ブループリントの割り当てが作成され、アーティファクトのデプロイが開始されます。 デプロイに要する時間は、約 1 時間です。 デプロイの状態を確認するには、ブループリントの割り当てを開きます。

> [!WARNING]
> Azure Blueprints サービスと、組み込まれているブループリント サンプルは、**無料** でご利用になれます。 Azure リソースは、[製品ごとに課金](https://azure.microsoft.com/pricing/)されます。 このブループリント サンプルでデプロイされるリソースの実行コストを見積もるには、[料金計算ツール](https://azure.microsoft.com/pricing/calculator/)を使用します。

## <a name="artifact-parameters-table"></a>アーティファクトのパラメーター表

以下の表は、ブループリント アーティファクトのパラメーターの一覧を示しています。

|アーティファクト名|アーティファクトの種類|パラメーター名|説明|
|-|-|-|-|
|Log Analytics resource group (Log Analytics リソース グループ)|Resource group|名前|**[ロック済み]** - **組織名** と `-workload-log-rg` を連結して、リソース グループを一意にします。|
|Log Analytics resource group (Log Analytics リソース グループ)|Resource group|場所|**[ロック済み]** - ブループリントのパラメーターを使用します。|
|Log Analytics テンプレート|Resource Manager テンプレート|サービス階層|Log Analytics ワークスペースの階層を設定します。 既定値は _[PerNode]_ です。|
|Log Analytics テンプレート|Resource Manager テンプレート|ログ保有期間日数|データ保有期間の日数。 既定値は _[365]_ です。|
|Log Analytics テンプレート|Resource Manager テンプレート|場所|Log Analytics ワークスペースを作成するために使用されるリージョン。 既定値は _米国西部 2_ です。|
|Network resource group (ネットワーク リソース グループ)|Resource group|名前|**[ロック済み]** - **組織名** と `-workload-net-rg` を連結して、リソース グループを一意にします。|
|Network resource group (ネットワーク リソース グループ)|Resource group|場所|**[ロック済み]** - ブループリントのパラメーターを使用します。|
|ネットワーク セキュリティ グループ テンプレート|Resource Manager テンプレート|ログ保有期間日数|データ保有期間の日数。 既定値は _[365]_ です。|
|仮想ネットワークとルート テーブルのテンプレート|Resource Manager テンプレート|Azure Firewall のプライベート IP|[Azure Firewall](../../../../firewall/overview.md) のプライベート IP を構成します。 _ISO 27001: 共有サービス_ アーティファクトの **[Azure Firewall サブネット アドレス プレフィックス]** パラメーターに定義されている CIDR 表記の一部にする必要があります。 既定値は _10.0.4.4_ です。|
|仮想ネットワークとルート テーブルのテンプレート|Resource Manager テンプレート|仮想ネットワーク アドレス プレフィックス|Virtual Network の CIDR 表記。 既定値は _10.1.0.0/16_ です。|
|仮想ネットワークとルート テーブルのテンプレート|Resource Manager テンプレート|ADDS IP アドレス|1 番目の ADDS VM の IP アドレス。 この値は、VNET のカスタム DNS として使用されます。|
|仮想ネットワークとルート テーブルのテンプレート|Resource Manager テンプレート|ログ保有期間日数|データ保有期間の日数。 既定値は _[365]_ です。|
|仮想ネットワークとルート テーブルのテンプレート|Resource Manager テンプレート|仮想ネットワーク ピアリング名|ワークロードと共有サービスの間で VNET ピアリングを有効にするために使用される値。|
|Key Vault リソース グループ|Resource group|名前|**[ロック済み]** - **組織名** と `-workload-kv-rg` を連結して、リソース グループを一意にします。|
|Key Vault リソース グループ|Resource group|場所|**[ロック済み]** - ブループリントのパラメーターを使用します。|
|キー コンテナー テンプレート|Resource Manager テンプレート|AAD オブジェクト ID|キー コンテナー インスタンスにアクセスする必要があるアカウントの AAD オブジェクト識別子。 既定値はありませんが、空白のままにしておくことはできません。 Azure portal でこの値を検索するには、 _[サービス]_ で [ユーザー] を検索して選択します。 _[名前]_ ボックスを使用してアカウント名をフィルター処理し、そのアカウントを選択します。 _[ユーザー プロファイル]_ ページで、 _[オブジェクト ID]_ の横にある [クリックしてコピー] アイコンを選択します。|
|キー コンテナー テンプレート|Resource Manager テンプレート|ログ保有期間日数|データ保有期間の日数。 既定値は _[365]_ です。|
|キー コンテナー テンプレート|Resource Manager テンプレート|キー コンテナー SKU|作成されるキー コンテナーの SKU を指定します。 既定値は _[Premium]_ です。|
|キー コンテナー テンプレート|Resource Manager テンプレート|Azure SQL Server 管理者ユーザー名|Azure SQL Server へのアクセスに使用するユーザー名。 **Azure SQL Database テンプレート** 内の同じプロパティの値に一致する必要があります。 既定値は _sql-admin-user_ です。|
|キー コンテナー テンプレート|Resource Manager テンプレート|Azure SQL Server 管理者パスワード|Azure SQL Server 管理者ユーザー名のパスワード|
|Azure SQL Database のリソース グループ|Resource group|名前|**[ロック済み]** - **組織名** と `-workload-azsql-rg` を連結して、リソース グループを一意にします。|
|Azure SQL Database のリソース グループ|Resource group|場所|**[ロック済み]** - ブループリントのパラメーターを使用します。|
|Azure SQL Database テンプレート|Resource Manager テンプレート|Azure SQL Server 管理者ユーザー名|Azure SQL Server のユーザー名。 **キー コンテナー テンプレート** 内の同じプロパティの値に一致する必要があります。 既定値は _sql-admin-user_ です。|
|Azure SQL Database テンプレート|Resource Manager テンプレート|Azure SQL Server 管理者パスワード (キー コンテナー リソース ID)|キー コンテナーのリソース ID。 "/subscriptions/{subscriptionId}/resourceGroups/{orgName}-workload-kv-rg/providers/Microsoft.KeyVault/vaults/{orgName}-workload-kv" を使用し、`{subscriptionId}` を自分のサブスクリプション ID に置き換え、`{orgName}` を **[組織名]** ブループリント パラメーターに置き換えます。|
|Azure SQL Database テンプレート|Resource Manager テンプレート|Azure SQL Server 管理者パスワード (キー コンテナー シークレット名)|SQL Server 管理者のユーザー名。 **[キー コンテナー テンプレート]** のプロパティ **[Azure SQL Server 管理者ユーザー名]** の値に一致する必要があります。|
|Azure SQL Database テンプレート|Resource Manager テンプレート|Azure SQL Server 管理者パスワード (キー コンテナーのシークレット バージョン)|キー コンテナーのシークレット バージョン (新しいデプロイの場合は空のまま)|
|Azure SQL Database テンプレート|Resource Manager テンプレート|ログ保有期間日数|データ保有期間の日数。 既定値は _[365]_ です。|
|Azure SQL Database テンプレート|Resource Manager テンプレート|AAD 管理者オブジェクト ID|Active Directory 管理者として割り当てられたユーザーの AAD オブジェクト ID。既定値はありませんが、空白のままにしておくことはできません。 Azure portal でこの値を検索するには、 _[サービス]_ で [ユーザー] を検索して選択します。 _[名前]_ ボックスを使用してアカウント名をフィルター処理し、そのアカウントを選択します。 _[ユーザー プロファイル]_ ページで、 _[オブジェクト ID]_ の横にある [クリックしてコピー] アイコンを選択します。|
|Azure SQL Database テンプレート|Resource Manager テンプレート|AAD 管理者ログイン|現在、Microsoft アカウント (live.com や outlook.com など) は管理者として設定できません。管理者として設定できるのは、組織内のユーザーとセキュリティ グループだけです。既定値はありませんが、空白のままにしておくことはできません。 Azure portal でこの値を検索するには、 _[サービス]_ で [ユーザー] を検索して選択します。 _[名前]_ ボックスを使用してアカウント名をフィルター処理し、そのアカウントを選択します。 _[ユーザー プロファイル]_ ページで、 _[ユーザー名]_ をコピーします。|
|App Service Environment リソース グループ|Resource group|名前|**[ロック済み]** - **組織名** と `-workload-ase-rg` を連結して、リソース グループを一意にします。|
|App Service Environment リソース グループ|Resource group|場所|**[ロック済み]** - ブループリントのパラメーターを使用します。|
|App Service Environment テンプレート|Resource Manager テンプレート|ドメイン名|サンプルで作成された Active Directory の名前。 既定値は _[contoso.com]_ です。|
|App Service Environment テンプレート|Resource Manager テンプレート|ASE の場所|App Service Environment の場所。 既定値は _米国西部 2_ です。|
|App Service Environment テンプレート|Resource Manager テンプレート|Application Gateway ログ保有期間日数|データ保有期間の日数。 既定値は _[365]_ です。|

## <a name="next-steps"></a>次のステップ

ISO 27001 App Service Environment/SQL Database ワークロード ブループリントのサンプルをデプロイする手順を確認したので、以下の記事に進み、アーキテクチャおよびコントロールのマッピングの詳細を確認します。

> [!div class="nextstepaction"]
> [ISO 27001 App Service Environment/SQL Database ワークロード ブループリント - 概要](./index.md)
> [ISO 27001 App Service Environment/SQL Database ワークロード ブループリント - コントロール マッピング](./control-mapping.md)

ブループリントとその使用方法に関するその他の記事:

- [ブループリントのライフサイクル](../../concepts/lifecycle.md)を参照する。
- [静的および動的パラメーター](../../concepts/parameters.md)の使用方法を理解する。
- [ブループリントの優先順位](../../concepts/sequencing-order.md)のカスタマイズを参照する。
- [ブループリントのリソース ロック](../../concepts/resource-locking.md)の使用方法を調べる。
- [既存の割り当ての更新](../../how-to/update-existing-assignments.md)方法を参照する。
