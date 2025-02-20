---
title: 用語集 - LUIS
description: 用語集では、LUIS API サービスの使用中に目にする可能性のある用語について説明します。
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: reference
ms.date: 10/28/2021
ms.openlocfilehash: 25bdf291d7d836523655b131f485721e3a29593b
ms.sourcegitcommit: 702df701fff4ec6cc39134aa607d023c766adec3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2021
ms.locfileid: "131434581"
---
# <a name="language-understanding-glossary-of-common-vocabulary-and-concepts"></a>一般的な用語や概念に関する Language Understanding の用語集
Language Understanding (LUIS) 用語集では、LUIS サービスの使用中に目にする可能性のある用語について説明します。

## <a name="active-version"></a>アクティブなバージョン

アクティブなバージョンとは、LUIS ポータルを使用してモデルに変更を加えたときに更新されるアプリの[バージョン](luis-how-to-manage-versions.md)です。 LUIS ポータルで、変更を加えたいバージョンがアクティブでない場合は、最初にそのバージョンをアクティブとして設定する必要があります。

## <a name="active-learning"></a>アクティブ ラーニング

アクティブ ラーニングは機械学習の手法であり、機械学習モデルを使用して、ラベル付けする有益な新しい例を識別するものです。 LUIS のアクティブ ラーニングとは、現在の予測が不明確なエンドポイント トラフィックから発話を追加してモデルを改善することを指します。 発話のラベルを確認するには、[review endpoint utterances]\(エンドポイント発話の確認\) をクリックします。

関連項目:
* [概念に関する情報](luis-concept-review-endpoint-utterances.md)
* [エンドポイントの発話を確認するチュートリアル](luis-tutorial-review-endpoint-utterances.md)
* [エンドポイントの発話を見直し](luis-how-to-review-endpoint-utterances.md)、LUIS アプリを改善する方法

## <a name="application-app"></a>アプリケーション (アプリ)

LUIS のアプリケーションまたはアプリとは、同じデータ セットに基づいて構築された機械学習モデルのコレクションであり、特定のシナリオの意図とエンティティを予測するために連携して機能します。 各アプリケーションには、個別の予測エンドポイントがあります。

HR ボットを構築している場合は、"休暇の予定を立てる"、"特典について問い合わせる"、"個人情報を更新する" などの一連の意図と、1 つのアプリケーションにグループ化する各意図のエンティティが存在する場合があります。

## <a name="authoring"></a>Authoring

作成は、LUIS ポータルまたはオーサリング API のいずれかを使用して、LUIS アプリを作成、管理、およびデプロイする機能です。

### <a name="authoring-key"></a>オーサリング キー

[オーサリング キー](luis-how-to-azure-subscription.md)はアプリの作成に使用されます。 運用レベルのエンドポイント クエリでは使用されません。 詳細については、「[キーの制限](luis-limits.md#key-limits)」を参照してください。

### <a name="authoring-resource"></a>作成リソース

LUIS の[作成リソース](luis-how-to-azure-subscription.md)は、Azure を通じて利用できる管理可能な項目です。 リソースは、Azure サービスの関連する作成、トレーニング、および公開機能に対するアクセスです。 リソースには、関連する Azure サービスにアクセスするために必要な認証、承認、セキュリティ情報が含まれています。

作成 リソースには、`LUIS-Authoring` という Azure の "種類" があります。

## <a name="batch-test"></a>バッチ テスト

バッチ テストは、ユーザー発話の一貫性のある既知のテスト セットを使用して、現在の LUIS アプリのモデルを検証する機能です。 バッチ テストは、[JSON 形式のファイル](./luis-how-to-batch-test.md#batch-test-file)に定義されます。


関連項目:
* [概念](./luis-how-to-batch-test.md)
* バッチ テストの実行[方法](luis-how-to-batch-test.md)
* [チュートリアル](./luis-how-to-batch-test.md) - バッチ テストの作成と実行

### <a name="f-measure"></a>F メジャー

バッチ テストでは、テストの精度の測定値です。

### <a name="false-negative-fn"></a>検知漏れ (FN)

バッチ テストでは、このデータ ポイントは、アプリが誤ってターゲットの意図/エンティティの不在を予測した発話を表します。

### <a name="false-positive-fp"></a>誤検知 (FP)

バッチ テストでは、このデータ ポイントは、アプリが誤ってターゲットの意図/エンティティの存在を予測した発話を表します。

### <a name="precision"></a>Precision
バッチ テストでは、精度 (陽性予測値とも呼ばれます) は、取得された発話の中にある関連する発話の割合です。

動物バッチ テストの例を使うと、予測された羊の数を動物の総数 (羊と羊以外の両方) で割ったものです。

### <a name="recall"></a>再現率

バッチ テストでは、再現率 (感度とも呼ばれます) は、LUIS が一般化を行う能力です。

動物バッチ テストの例を使うと、予測された羊の数を使用可能な羊の総数で割ったものです。

### <a name="true-negative-tn"></a>真陰性 (TN)

真陰性とは、一致がないことがアプリで正しく予測される場合です。 バッチ テストでは、意図またはエンティティでラベル付けされていない例について、アプリでその意図またはエンティティが予測される場合、真陰性が発生します。

### <a name="true-positive-tp"></a>真陽性 (TP)

真陽性 (TP) 真陽性とは、一致があることがアプリで正しく予測される場合です。 バッチ テストでは、意図またはエンティティでラベル付けされた例について、アプリでその意図またはエンティティが予測される場合、真陽性が発生します。

## <a name="classifier"></a>分類子

分類子は、入力が適合するカテゴリまたはクラスを予測する機械学習モデルです。

分類子の例としては、[意図](#intent)があります。

## <a name="collaborator"></a>コラボレーター

コラボレーターは、概念的には[共同作成者](#contributor)と同じです。 所有者が Azure ロールベースのアクセス制御 (Azure RBAC) で制御されていないアプリにコラボレーターのメール アドレスを追加すると、コラボレーターにアクセスが許可されます。 引き続きコラボレーターを使用している場合は、LUIS アカウントを移行し、LUIS 作成リソースを使用して Azure RBAC で共同作成者を管理する必要があります。

## <a name="contributor"></a>Contributor

共同作成者はアプリの[所有者](#owner)ではありませんが、意図を追加、編集、および削除するための同様のアクセス許可を持っています。 共同作成者は、LUIS アプリへの Azure ロールベースのアクセス制御 (Azure RBAC) を提供します。

関連項目:
* 共同作成者の追加[方法](luis-how-to-collaborate.md#add-contributor-to-azure-authoring-resource)

## <a name="descriptor"></a>記述子

記述子は、以前は機械学習の[特徴](#features)に使用されていた用語です。

## <a name="domain"></a>Domain

LUIS のコンテキストでは、ドメインとはナレッジの一領域です。 ドメインはシナリオに固有のものです。 ドメインによって、ドメインのコンテキストで意味のある特定の言語と用語が使用されます。 たとえば、音楽を再生するアプリケーションを構築している場合、アプリケーションには音楽に固有の用語と言語 ("歌、トラック、アルバム、歌詞、B 面、アーティスト" などの単語) があります。 ドメインの例については、「[事前構築済みのドメイン](#prebuilt-domain)」を参照してください。

## <a name="endpoint"></a>エンドポイント

### <a name="authoring-endpoint"></a>作成エンドポイント

LUIS 作成エンドポイント URL は、アプリを作成、トレーニング、公開する場所です。 エンドポイント URL には、公開されたアプリのリージョンまたはカスタム サブドメインとアプリ ID が含まれています。

プログラムでアプリを作成する方法の詳細については、[開発者向けリファレンス](developer-reference-resource.md#rest-endpoints)を参照してください

### <a name="prediction-endpoint"></a>予測エンドポイント

LUIS 予測エンドポイント URL は、[LUIS アプリ](#application-app)が作成および公開された後に、LUIS クエリを送信する場所です。 エンドポイント URL には、公開されたアプリのリージョンまたはカスタム サブドメインとアプリ ID が含まれています。 エンドポイントは、お使いのアプリの **[[Azure リソース]](luis-how-to-azure-subscription.md)** ページにあります。また、[Get App Info API](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c37) からエンドポイント URL を取得することもできます。

予測エンドポイントに対するアクセスは、LUIS 予測キーを使用して承認されます。

## <a name="entity"></a>Entity

[エンティティ](luis-concept-entity-types.md)は、意図を達成または識別するために使用される情報を説明する発話内の単語です。 エンティティが複雑であり、モデルを使って特定の部分を識別できるようにする場合は、モデルをサブエンティティに分割できます。 たとえば、モデルを使って住所を予測するだけでなく、番地、市区町村、都道府県、郵便番号のサブエンティティも予測することができます。 エンティティは、モデルの特徴としても使用できます。 LUIS アプリからの応答には、予測された意図とすべてのエンティティの両方が含まれます。

### <a name="entity-extractor"></a>エンティティ抽出子

エンティティ抽出子は、単に抽出子と呼ばれることもあり、LUIS でエンティティの予測に使用される機械学習モデルの一種です。

### <a name="entity-schema"></a>エンティティ スキーマ

エンティティ スキーマは、サブエンティティを持つ機械学習エンティティに対して定義する構造です。 予測エンドポイントからは、スキーマで定義されているエンティティとサブエンティティのうち抽出されたものがすべて返されます。

### <a name="entitys-subentity"></a>エンティティのサブエンティティ

サブエンティティは、機械学習エンティティの子エンティティです。

### <a name="non-machine-learning-entity"></a>非機械学習エンティティ

テキストのマッチングを使用してデータを抽出するエンティティ:
* リスト エンティティ
* 正規表現エンティティ

### <a name="list-entity"></a>リスト エンティティ

[リスト エンティティ](reference-entity-list.md)は、固定かつ限定された関連単語セットとそのシノニムを表します。 リスト エンティティは、機械学習エンティティとは異なり、完全一致です。

リスト エンティティの単語がリストに含まれている場合、エンティティは予測されます。 たとえば、"サイズ" というリスト エンティティがあり、リストに "小、中、大" という単語がある場合、コンテキストに関係なく、"小"、"中"、または "大" という単語が使用されるすべての発話に対してサイズ エンティティが予測されます。

### <a name="regular-expression"></a>正規表現

[正規表現エンティティ](reference-entity-regular-expression.md)は正規表現を表します。 正規表現エンティティは、機械学習エンティティとは異なり、完全一致です。
### <a name="prebuilt-entity"></a>事前構築済みのエンティティ

[構築済みのエンティティ](#prebuilt-entity)の事前構築済みモデルのエントリを参照してください

## <a name="features"></a>特徴

機械学習の特徴とは、モデルで特定の概念を認識するために役立つ特性です。 これは LUIS に使用できるヒントですが、厳密な規則ではありません。

この用語は、 **[機械学習特徴](luis-concept-feature.md)** とも呼ばれます。

これらのヒントは、新しいデータを予測する方法を学習するためにラベルと組み合わせて使用されます。 LUIS は、フレーズ リストと他のモデルの使用の両方を特徴としてサポートしています。

### <a name="required-feature"></a>必須の特徴

必須な特徴は、LUIS モデルの出力を制限する方法の 1 つです。 エンティティの特徴が必須とマークされている場合、機械学習モデルで何を予測するかに関係なく、そのエンティティを予測するには、その特徴が例に存在している必要があります。

メニュー注文ボットの数量エンティティで必須とマークした事前構築済みの数値の特徴がある例を考えてみましょう。 ボットで `I want a bajillion large pizzas?` が確認されると、出現するコンテキストに関係なく、bajillion は数量と予測されません。 bajillion は有効な数値ではないため、数値の事前構築済みのエンティティでは予測されません。

## <a name="intent"></a>Intent

[意図](luis-concept-intent.md)は、ユーザーが実行しようとしているタスクまたはアクションを表します。 これは、フライトの予約や請求書の支払いなど、ユーザーの入力で表現される目的または目標です。 LUIS では、発話全体が意図として分類されますが、発話の一部はエンティティとして抽出されます

## <a name="labeling-examples"></a>ラベル付けの例

ラベル付け、またはマーキングは、正または負の例をモデルに関連付けるプロセスです。

### <a name="labeling-for-intents"></a>意図のラベル付け
LUIS では、アプリ内の意図は相互に排他的です。 つまり、発話を意図に追加すると、その意図に対して "_正_" の例と見なされ、他のすべての意図に対しては "_負_" の例と見なされます。 負の例は、アプリのスコープ外の発話を表す "なし" の意図と混同しないでください。

### <a name="labeling-for-entities"></a>エンティティのラベル付け
LUIS では、エンティティを含む意図の例の発話に含まれる単語またはフレーズに、"_正_" の例という [ラベル付け](label-entity-example-utterance.md)をします。 ラベル付けは、その発話に対して何を予測すべき意図を示しています。 ラベル付けされた発話は、意図のトレーニングに使用されます。

## <a name="luis-app"></a>LUIS アプリ

「[アプリケーション (アプリ)](#application-app)」の定義を参照してください。

## <a name="model"></a>モデル

(機械学習された) モデルは、入力データに対して予測を行う関数です。 LUIS では、意図分類子とエンティティ抽出子を総称して "モデル" と呼び、トレーニング、公開、クエリの対象となるモデルのコレクションを "アプリ" と呼びます。

## <a name="normalized-value"></a>正規化された値

[リスト](#list-entity) エンティティに値を追加します。 これらの各値には、1 つ以上のシノニムのリストを含めることができます。 応答では、正規化された値のみが返されます。

## <a name="overfitting"></a>オーバーフィット

オーバーフィットは、モデルが特定の例に固定されていて、適切に一般化できない場合に発生します。

## <a name="owner"></a>所有者

各アプリに、そのアプリを作成した所有者が 1 人います。 所有者は、Azure portal でアプリケーションへのアクセス許可を管理します。

## <a name="phrase-list"></a>フレーズ リスト

[フレーズ リスト](luis-concept-feature.md)は、同じクラスに属し、同様に扱う必要がある値 (単語またはフレーズ) のグループを含む、特定の種類の機械学習特徴です (たとえば、都市や製品の名前)。

## <a name="prebuilt-model"></a>事前構築済みのモデル

[事前構築済みのモデル](luis-concept-prebuilt-model.md)は、意図、エンティティ、またはその両方のコレクションと、ラベル付けされた例です。 これらの一般的な事前構築済みのモデルをアプリに追加すると、アプリに必要なモデル開発作業を減らすことができます。

### <a name="prebuilt-domain"></a>事前構築済みのドメイン

事前構築済みのドメインは、ホーム オートメーション (HomeAutomation)、レストランの予約 (RestaurantReservation) など、特定のドメイン用に構成された LUIS アプリです。 意図、発話、およびエンティティは、このドメインに対して構成されています。

### <a name="prebuilt-entity"></a>事前構築済みのエンティティ

事前構成済みのエンティティは、数値、URL、電子メールなど、一般的な情報の種類のエンティティで、LUIS によって提供されます。 これらは、公開データに基づいて作成されます。 事前構築済みのエンティティは、スタンドアロン エンティティとして、または特徴としてエンティティに追加することを選択できます。

### <a name="prebuilt-intent"></a>事前構築済みの意図

事前構築済みの意図は、一般的な種類の情報に対して LUIS で提供され、独自のラベル付けされた発話例が付属している意図です。

## <a name="prediction"></a>予測

予測は、新しいデータ (ユーザーの発話) を取り込み、トレーニングされ公開されたアプリケーションをそのデータに適用して、検出された意図とエンティティを特定するという、Azure LUIS 予測サービスに対する REST 要求です。

### <a name="prediction-key"></a>予測キー

[予測キー](luis-how-to-azure-subscription.md) (旧称はサブスクリプション キー) は、予測エンドポイントの使用を承認する、Azure で作成した LUIS サービスに関連付けられたキーです。

このキーはオーサリング キーではありません。 予測エンドポイント キーがある場合は、それをオーサリング キーの代わりに、すべてのエンドポイント要求に対して使用してください。 現在の予測キーは、LUIS Web サイトの Azure リソース ページの下部にあるエンドポイント URL 内に表示されます。 これは、subscription-key の名前/値ペアの値です。

### <a name="prediction-resource"></a>予測リソース

LUIS 予測リソースは、Azure を通じて利用できる管理可能な項目です。 リソースは、Azure サービスの関連する予測に対するアクセスです。 リソースには予測が含まれています。

予測 リソースには、`LUIS` という Azure の "種類" があります。

### <a name="prediction-score"></a>予測スコア

[スコア](luis-concept-prediction-score.md)は 0 から 1 の数値であり、システムによって特定の入力発話が特定の意図に一致することの確度がどの程度と判断されているを示す尺度です。 1 に近いスコアは、システムによってその出力の確度が非常に高いと判断されたことを意味し、0 に近いスコアは、入力が特定の出力と一致しない確度が高いと判断されたことを意味します。 中間のスコアは、システムでその判断を下す方法が非常に不確かであることを意味します。

たとえば、一部の顧客のテキストに食品の注文が含まれているかどうかを識別するために使用されるモデルがあるとします。 "1 杯のコーヒーを注文したい" のスコアは 1 (これが注文である確度が高いというシステムの判断)、"私のチームは昨夜ゲームに勝った" のスコアは 0 (これは注文では "ない" 確度が高いというシステムの判断) になる可能性があります。 また、"お茶を飲もう" のスコアは 0.5 (これが注文かどうか不明) になる可能性があります。

## <a name="programmatic-key"></a>プログラム キー

[オーサリング キー](#authoring-key)に名前が変更されました。

## <a name="publish"></a>発行

[公開](luis-how-to-publish-app.md)とは、LUIS のアクティブ バージョンを、ステージングまたは運用[エンドポイント](#endpoint)のいずれかで使用できるようにすることです。

## <a name="quota"></a>Quota

LUIS クォータとは、Azure サブスクリプション レベルの制限です。 LUIS クォータは、1 秒あたりの要求数 (HTTP 状態 429) と 1 か月の要求数合計 (HTTP 状態 403) の両方によって制限できます。

## <a name="schema"></a>スキーマ

スキーマには、意図とエンティティがサブエンティティと共に含まれています。 スキーマは最初に計画され、その後、長期にわたって反復処理されます。 スキーマには、アプリの設定、特徴、発話の例は含まれていません。

## <a name="sentiment-analysis"></a>感情分析
感情分析では、[Language service](../language-service/sentiment-opinion-mining/overview.md) によって得られる発話の正または負の値が提供されます。

## <a name="speech-priming"></a>音声認識の準備

音声認識の準備により、[Speech Services](../speech-service/overview.md) を使用したシナリオで一般的に使用される話し言葉やフレーズの認識が向上します。 音声認識の準備対応アプリケーションの場合、LUIS のラベル付けされたすべての例は、その特定のアプリケーション用にカスタマイズされた音声モデルを作成することで音声認識の精度を向上させるために使用されます。 たとえば、チェス ゲームでは、ユーザーが「Move knight」(ナイトを動かして) と言った場合に、「Move night」(夜を動かして) と解釈されないようにします。 LUIS アプリには、"knight" (ナイト) がエンティティとしてラベル付けした例を含める必要があります。

## <a name="starter-key"></a>スターター キー

初めて LUIS の使用を開始するときに使用する無料のキー。

## <a name="synonyms"></a>シノニム

LUIS の[リスト エンティティ](reference-entity-list.md)では、それぞれシノニムのリストを持つ可能性がある正規化された値を作成できます。 たとえば、小、中、大、特大の正規化された値を持つサイズ エンティティを作成するとします。 次のように、各値のシノニムを作成できます。

|正規化された値| シノニム|
|--|--|
|Small| 小さなもの、8 オンス|
|Medium| 標準、12 オンス|
|Large| 大きなもの、16 オンス|
|Xtra large| 最大のもの、24 オンス|

シノニムのいずれかが入力に含まれる場合、モデルからはエンティティの正規化された値が返されます。

## <a name="test"></a>テスト

LUIS アプリの[テスト](./luis-interactive-test.md)とは、モデル予測を表示することを意味します。

## <a name="timezone-offset"></a>タイムゾーン オフセット

エンドポイントには、[timezoneOffset](luis-concept-data-alteration.md#change-time-zone-of-prebuilt-datetimev2-entity) が含まれています。 これは、事前構築済みエンティティ datetimeV2 から追加または削除する必要がある数値 (分) です。 たとえば、"今何時ですか?" という発話の場合、返される datetimeV2 は、クライアント要求の現在時刻です。 クライアント要求元が、ボットのユーザーと異なるボットまたは他のアプリケーションの場合、ボットとそのユーザーの間のオフセットを渡す必要があります。

「[事前構築済み datetimeV2 エンティティのタイム ゾーンの変更](luis-concept-data-alteration.md?#change-time-zone-of-prebuilt-datetimev2-entity)」を参照してください。

## <a name="token"></a>トークン
[トークン](luis-language-support.md#tokenization)は、LUIS で認識できるテキストの最小単位です。 これは、言語によって若干異なります。

**英語** の場合、トークンは、文字と数字の連続するスパン (スペースや句読点を含まない) です。 スペースはトークンでは "ありません"。

|フレーズ|トークン数|説明|
|--|--|--|
|`Dog`|1|句読点やスペースを含まない 1 つの単語。|
|`RMT33W`|1|レコードのロケーター番号。 数字と文字を含めることはできますが、句読点は含まれません。|
|`425-555-5555`|5|電話番号。 各区切り記号は 1 つのトークンであるため、`425-555-5555` は次のように 5 つのトークンになります。<br>`425`<br>`-`<br>`555`<br>`-`<br>`5555` |
|`https://luis.ai`|7|`https`<br>`:`<br>`/`<br>`/`<br>`luis`<br>`.`<br>`ai`<br>|

## <a name="train"></a>トレーニング

[トレーニング](luis-how-to-train.md)は、前回のトレーニング以降に行われたアクティブなバージョンに対する変更を LUIS に教えるプロセスです。

### <a name="training-data"></a>トレーニング データ

トレーニング データは、モデルのトレーニングに必要な一連の情報です。 これには、スキーマ、ラベル付けされた発話、特徴、およびアプリケーション設定が含まれます。

### <a name="training-errors"></a>トレーニング エラー

トレーニング エラーは、ラベルと一致しないトレーニング データに対する予測です。

## <a name="utterance"></a>発話

[発話](luis-concept-utterance.md)は、会話内の文を表す短いテキストであるユーザー入力です。 "次の火曜日にシアトル行のチケットを 2 枚予約する" などの自然言語フレーズです。 発話の例はモデルをトレーニングするために追加され、実行時には、新しい発話に対してそのモデルを使って予測されます

## <a name="version"></a>Version

LUIS の[バージョン](luis-how-to-manage-versions.md)は、LUIS アプリ ID と公開されたエンドポイントに関連付けられた LUIS アプリケーションの特定のインスタンスです。 LUIS アプリごとに、少なくとも 1 つのバージョンがあります。