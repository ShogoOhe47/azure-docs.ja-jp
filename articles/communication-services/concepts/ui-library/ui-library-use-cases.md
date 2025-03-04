---
title: UI ライブラリのユース ケース
titleSuffix: An Azure Communication Services concept document
description: UI ライブラリと、これがコミュニケーション エクスペリエンスの構築にどのように役立つかを説明します。
author: ddematheu2
manager: chrispalm
services: azure-communication-services
ms.author: dademath
ms.date: 06/30/2021
ms.topic: conceptual
ms.service: azure-communication-services
ms.openlocfilehash: dd338cd0f7d8e39f7f2d72445477991219e8d91c
ms.sourcegitcommit: 98308c4b775a049a4a035ccf60c8b163f86f04ca
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2021
ms.locfileid: "122653331"
---
# <a name="ui-library-use-cases"></a>UI ライブラリのユース ケース

[!INCLUDE [Public Preview Notice](../../includes/public-preview-include.md)]

> [!NOTE]
> UI ライブラリの詳細なドキュメントについては、[UI ライブラリのストーリーブック](https://azure.github.io/communication-ui-library)を参照してください。 そこには、その他の概念説明のドキュメント、クイックスタート、例が記載されています。


UI ライブラリは、通話とチャットの体験を横断する多くのケースをサポートします。
これらの機能は、UI コンポーネントと複合を通じて利用できます。
複合の場合、これらの機能は直接組み込まれており、コンポジットがアプリケーションに統合されたときに公開されます。
UI コンポーネントの場合、これらの機能は UI 機能と基になるステートフル ライブラリの組み合わせによって公開されます。
これらの機能を最大限に活用するには、UI コンポーネントとステートフルな通話およびチャットのクライアント ライブラリを併用することをお勧めします。

## <a name="calling-use-cases"></a>通話のユース ケース

| 領域                | ユース ケース                                              |
| ------------------- | ------------------------------------------------------ |
| 呼び出しの種類          | Teams の会議に参加する                                     |
|                     | グループ ID を使用して Azure Communication Services の通話に参加する   |
| [Teams との相互運用](../teams-interop.md)      | 通話ロビー                                             |
|                     | 文字起こしとレコーディングのアラート バナー               |
| 呼び出しコントロール       | 通話をミュートまたはミュート解除する                                       |
|                     | 通話時のビデオのオンまたはオフ                                   |
|                     | 画面の共有                                         |
|                     | 通話の終了                                               |
| 参加者ギャラリー | リモート参加者がグリッド状に表示される              |
|                     | ローカル ユーザーの通話を通して利用可能なビデオ プレビュー |
|                     | ビデオがオフのときに使用できる既定のアバター            |
|                     | 参加者ギャラリーに表示される共有画面コンテンツ |
| 呼び出しの構成  | マイク デバイスの管理                           |
|                     | カメラ デバイスの管理                               |
|                     | スピーカー デバイスの管理                              |
|                     | ユーザーがビデオを確認するために使用できるローカル プレビュー        |
| 参加者        | 参加者一覧                                     |

## <a name="chat-use-cases"></a>チャットの使用例

| 領域         | ユース ケース                                        |
| ------------ | ------------------------------------------------ |
| チャットの種類   | Teams の会議チャットに参加する                        |
|              | Azure Communication Services のチャット スレッドに参加する |
| チャット アクション | チャット メッセージを送信する                                |
|              | チャット メッセージを受信する                             |
| チャット イベント  | 入力インジケーター                                |
|              | 開封確認メッセージ                                     |
|              | 追加または削除された参加者                        |
|              | チャットのタイトルの変更                               |
| 参加者 | 参加者一覧                               |

## <a name="supported-identities"></a>サポートされている ID

ステートフルなクライアント ライブラリを初期化し、サービスに対して認証を行うには、Azure Communication Services ID が必要です。
認証の詳細については、[認証](../authentication.md)と[アクセス トークン](../../quickstarts/access-tokens.md?pivots=programming-language-javascript)に関するページを参照してください。

## <a name="teams-interop-use-case"></a>Teams との相互運用のユースケース

[Teams との相互運用](../teams-interop.md)のシナリオでは、開発者は UI ライブラリ コンポーネントを使用して、Azure Communication Services を通じて Teams ミーティングに参加することができます。
Teams との相互運用を可能にするために、開発者は、通話とチャットの複合を直接使用するか、UI コンポーネントを使用してカスタム エクスペリエンスを構築することができます。
アプリケーションに通話とチャットの両方の機能を備える場合は、参加者が通話に許可されるまで、チャット クライアントが開始されないようにすることが重要です。
許可されたら、チャット クライアントを開始して、ミーティングのチャット スレッドに参加させることができます。
ガイダンスについては、次の図を参照してください。

:::image type="content" source="../media/teams-interop-pattern.png" alt-text="通話とチャットのための Teams との相互運用パターン":::

Ui コンポーネントを使用して Teams との相互運用のエクスペリエンスを提供する場合、UI ライブラリはエクスペリエンスの重要な部分の例を提供します。
次に例を示します。
- [ロビーの例](https://azure.github.io/communication-ui-library/?path=/story/examples-teams-interop--lobby): 参加者が通話に許可されるまで待機するためのロビーの例。
- [コンプライアンス バナー](https://azure.github.io/communication-ui-library/?path=/story/examples-teams-interop--compliance-banner): 通話が録画されているかどうかをユーザーに表示するバナーの例。
- [Teams テーマ](https://azure.github.io/communication-ui-library/?path=/story/examples-themes--teams): UI ライブラリを Microsoft Teams のように見せるテーマの例。


## <a name="customization"></a>カスタマイズ

UI ライブラリは、開発者がアプリケーションの外観に合わせてコンポーネントを変更するためのパターンを公開します。
これらの機能は、複合と UI コンポーネントの間の主な違いであり、複合はカスタマイズの選択肢が少なく、よりシンプルな統合体験を提供します。

| ユース ケース                                            | 合成 | UI コンポーネント |
| --------------------------------------------------- | ---------- | ------------- |
| Fluent ベースのテーマ                                | X          | X             |
| エクスペリエンス レイアウトがコンポーザブル                     |            | X             |
| CSS スタイル設定を使用してスタイル プロパティを変更可能  |            | X             |
| アイコンは置き換え可能                               |            | X             |
| 参加者のギャラリー レイアウトが変更可能          |            | X             |
| 通話コントロールのレイアウトが変更可能                 | X          | X             |
| データ モデルを挿入してユーザー メタデータを変更可能 | X          | X             |

## <a name="observability"></a>可観測性

UI ライブラリの分離された状態管理アーキテクチャの一部として、開発者はステートフルな通話およびチャット クライアントに直接アクセスすることができます。

開発者はステートフルなクライアントにフックして状態を読み取ったり、イベントを処理したり、UI コンポーネントに渡す動作をオーバーライドしたりすることができます。

| ユース ケース                                  | 合成 | UI コンポーネント |
| ----------------------------------------- | ---------- | ------------- |
| 通話/チャット クライアントの状態にアクセス可能    | X          | X             |
| クライアント イベントにアクセスして処理することが可能 | X          | X             |
| UI イベントにアクセスして処理することが可能     | X          | X             |

## <a name="recommended-architecture"></a>推奨アーキテクチャ

:::image type="content" source="../media/ui-library-architecture.png" alt-text="UI ライブラリで推奨されるクライアントとサーバーのアーキテクチャ":::

複合コンポーネントと基本コンポーネントは、Azure Communication Services のアクセス トークンを使用して初期化されます。 アクセス トークンは、管理対象の信頼できるサービスを介して Azure Communication Services から調達する必要があります。 「[クイック スタート:詳細については、アクセストークンの作成に関するクイックスタート](../../quickstarts/access-tokens.md?pivots=programming-language-javascript)と[信頼できるサービスのチュートリアル](../../tutorials/trusted-service-tutorial.md)に関するページを参照してください。

これらのクライアント ライブラリでは、参加する通話またはチャットのコンテキストも必要になります。 ユーザー アクセス トークンと同様、このコンテキストも信頼できる独自サービスを介してクライアントに配布する必要があります。 次の一覧は、運用化する必要がある初期化機能とリソース管理機能をまとめたものです。

| Contoso の役割                                 | UI ライブラリの役割                                     |
| -------------------------------------------------------- | --------------------------------------------------------------- |
| Azure からアクセス トークンを提供する                          | 与えられたアクセス トークンをパススルーしてコンポーネントを初期化する        |
| 更新機能を提供する                                 | 開発者から提供された機能を使用してアクセス トークンを更新する          |
| 通話またはチャットの参加情報を取得する、または渡す          | 通話とチャットの情報をパススルーしてコンポーネントを初期化する |
| 任意のカスタム データ モデルのユーザー情報を取得する、または渡す | レンダリングの対象となるコンポーネントにカスタム データ モデルをパススルーする          |

## <a name="platform-support"></a>プラットフォームのサポート

| SDK    | Windows            | macOS                | Ubuntu   | Linux    | Android  | iOS        |
| ------ | ------------------ | -------------------- | -------- | -------- | -------- | ---------- |
| UI SDK | Chrome\*、新しい Edge | Chrome\*、Safari\*\* | Chrome\* | Chrome\* | Chrome\* | Safari\*\* |

\* 前の 2 つのリリースに加えて Chrome の最新バージョンがサポートされていることに注意してください。

\*\* Safari バージョン 13.1 以降がサポートされていることに注意してください。 Safari macOS の発信ビデオはまだサポートされていませんが、iOS ではサポートされています。 発信画面の共有は、デスクトップ iOS でのみサポートされています。

## <a name="accessibility"></a>ユーザー補助

設計によるアクセシビリティは、Microsoft 製品全体の原則です。
UI ライブラリは、すべての UI コンポーネントに完全にアクセスできるようにするために、この原則に従っています。
パブリック プレビュー期間中、UI ライブラリは引き続き改善され、ユーザー補助機能が UI コンポーネントに追加されます。
UI ライブラリの一般提供開始に先立ち、アクセシビリティに関する詳細を追加する予定です。

## <a name="localization"></a>ローカリゼーション

ローカライズは、世界中で、異なる言語を話す人々が使用できる製品を作るための重要な鍵となります。
UI ライブラリでは、一部の言語や RTL などの機能に対して、すぐに使用できるサポートが提供されます。
開発者は、UI ライブラリで使用する独自のローカライズ ファイルを提供することがでます。
これらのローカライズ機能は、一般提供開始に先立って追加されます。

> [!div class="nextstepaction"]
> [UI Library Storybook にアクセス](https://azure.github.io/communication-ui-library)
