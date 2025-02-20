---
title: Azure Firewall の Web カテゴリ
description: Azure Firewall の Web カテゴリとその説明を示します。
author: vhorne
ms.service: firewall
services: firewall
ms.topic: overview
ms.date: 07/19/2021
ms.author: victorh
ms.openlocfilehash: c8ca827495f9ccfdd2786ee3b2bbf33e939c6a16
ms.sourcegitcommit: 106f5c9fa5c6d3498dd1cfe63181a7ed4125ae6d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2021
ms.locfileid: "131068629"
---
# <a name="azure-firewall-web-categories"></a>Azure Firewall の Web カテゴリ

Web カテゴリでは、管理者は、ギャンブルの Web サイトやソーシャル メディアの Web サイトなどの Web サイト カテゴリへのユーザーのアクセスを許可または拒否できます。 カテゴリは、責任、高帯域幅、ビジネス利用、生産性の低下、一般的なネット サーフィン、未分類の下で重要度に基づいて整理されています。

## <a name="liability"></a>[Liability]


|カテゴリ |説明 |
|---------|---------|
|アルコールとタバコ    |アルコールまたはタバコ関連の製品またはサービスを含むか、奨励するか、または販売しているサイト。|
|児童虐待の画像   |虐待または性的行為を受ける子供を提示または議論するサイト。|
|子供に不適切    |子供に不適切なサイト。R 指定または悪趣味なコンテンツ、冒涜的な言葉、成人向けの素材などが含まれている可能性がある。|
|犯罪行為|違法または犯罪行為を行う方法を奨励または助言するサイト、あるいはそのような行為の検出を回避するサイト。 犯罪行為には、殺人、爆弾の製造、電子デバイスの不正操作、ハッキング、詐欺、ソフトウェアの不正配布などが含まれる。|
|交際と出会い系    |交際と結婚、出会い仲介、オンライン デート、配偶者紹介など、人間関係のネットワーク構築を促進するサイト。|
|ギャンブル    |オンライン ギャンブル、宝くじ、偶然を伴う賭け事の取り次ぎ、カジノなどを提供するか、またはこれらに関連するサイト。|
|ハッキング    |情報の盗用、不正行為の実行、ウイルスの作成、または盗難やデジタル情報に関連するその他の違法行為の実行のために、専用コンピューター システムへの不正アクセスを取得する方法を奨励または助言するサイト。|
|憎悪と不寛容|至上主義者の政治課題を推進し、人種、宗教、性別、年齢、障がい、性的指向、または国籍に基づいて人々または人々のグループを抑圧するように促すサイト。|
|違法薬物    |違法薬物または脱法ドラッグの購入、製造、使用、および治療用薬物などの化合物の乱用に関する情報を含むサイト。|
|不正なソフトウェア    |映画、音楽、解読されたソフトウェア、不正なシリアル番号、不正なライセンス キー ジェネレーターなど、ソフトウェアまたは著作権のある素材を不正に配布するサイト。|
|下着と水着|セミヌードを許容し、挑発的な服装のモデルの画像を提供するサイト。 下着や水着を提供するサイトが含まれる。|
|マリファナ   |マリファナおよび関連する製品またはサービスの情報、ディスカッション、販売を含むサイト。マリファナの合法化と医療目的でのマリファナの使用が含まれる。|
|ヌード    | 意図的に性的露骨であるとは限らないが、完全または部分的なヌードを含むサイト。|
|ポルノグラフィー/性的露骨    |アダルト コンテンツを含むサイト。 成人向け製品 (成人向けのおもちゃ、CD-ROM、ビデオなど)、成人向けサービス (ビデオ会議、エスコート サービス、ストリップ クラブなど)、官能的なストーリー、テキストによる性行為の説明などが含まれる。  |
|学校での不正行為    | テストの解答、執筆済みの論文、研究報告、学期末レポートなどを提供して、不正行為や盗作などの非倫理的行為を助長するサイト。        |
|自傷行為      |自分を傷つけること (自殺、拒食症、過食症など) に関連する行為を助長するサイト。          |
|性教育     |  パートナーの尊重、中絶、避妊薬、性感染症、妊娠などを含む性教育に関連するサイト。       |
|悪趣味     |冒涜的な言葉を含む、不快または悪趣味なコンテンツを含むサイト。          |
|暴力   | 人間、動物、または団体に対する物理的な攻撃を表現または擁護する画像またはテキストを含むサイト。 強い恐怖感を与えるサイト。         |
|武器      |スポーツ用を含む銃器や兵器を表現、販売、論評、または説明するサイト。         |


## <a name="high-bandwidth"></a>高帯域幅

|カテゴリ  |説明  |
|---------|---------|
|画像の共有    |   デジタル写真および画像、オンライン写真集、デジタル写真の交換をホストするサイト。       |
|ピアツーピア    |  中央サーバーに依存せずにユーザー間でファイルを直接交換できるサイト。        |
|ストリーミング メディアとダウンロード    |  インターネット ラジオ、インターネット テレビ、MP3 などのストリーミング コンテンツを配信するサイト、およびライブまたはアーカイブ メディアのダウンロード サイト。 ファン サイトや、音楽家、バンド、レコード レーベルによって運営される公式サイトが含まれる。        |
|ダウンロード サイト      | ダウンロード可能なソフトウェアを含むサイト (シェアウェア、フリーウェア、有料を問わず)。         |
|エンターテイメント     |  テレビ、映画、音楽、ビデオ (ビデオ オン デマンドを含む) のプログラム ガイドを含むサイト、著名人のサイト、エンターテイメント ニュース。        |
|    |         |

## <a name="business-use"></a>ビジネスでの利用

|カテゴリ  |説明  |
|---------|---------|
|Business    |   企業 Web サイトなど、ビジネス関連情報を提供するサイト。 あらゆる規模の企業が日常の商業活動を行うのに役立つ情報、サービス、または製品。       |
|コンピューターとテクノロジ   |コンピューター、ソフトウェア、ハードウェア、周辺機器、コンピューター サービスに関する製品レビュー、ディスカッション、ニュースなどの情報を含むサイト。          |
|Education   |  遠隔教育を含むあらゆる種類の教育機関や学校の後援を受けているサイト。 辞書、百科事典、オンライン コース、補助教材、ディスカッション ガイドなどの一般的な教材や参考資料が含まれる。       |
|Finance    | 銀行取引、金融、支払い、投資に関連するサイト。銀行、証券会社、オンライン株取引、株価情報、資金管理、保険会社、信用組合、クレジット カード会社などが含まれる。         |
|フォーラムとニュースグループ     | ニュースグループ、フォーラム、掲示板の形式で情報を共有するサイト。 個人のブログは含まれない。         |
|政府      |  政府または軍の組織、部署、機関によって運営されるサイト。警察、消防、関税局、救急、民間防衛、テロ対策組織が含まれる。        |
|健康と医療      |   健康、保健医療サービス、フィットネス、福祉に関する情報を含むサイト。医療機器、病院、ドラッグストア、看護、薬物、治療、処方薬などに関する情報が含まれる。       |
|情報セキュリティ     |   新しく検出された脆弱性とそれらをブロックする方法を含む、データ保護に関する正当な情報を提供するサイト。       |
|仕事探し    |  求人情報、キャリア情報、仕事探しの支援 (履歴書の作成、面接のヒントなど)、職業紹介所、人材スカウトなどを含むサイト。        |
|News  |    新聞、ニュース配信サービス、個人向けニュース サービス、放送サイト、雑誌など、ニュースや時事をカバーするサイト。      |
|非営利と NGO     |   クラブ、コミュニティ、組合、非営利組織の専用サイト。 これらのグループの多くは教育や慈善事業を目的としている。       |
|個人サイト     |    個人に関するサイト、または個人によってホストされているサイト。Blogger や AOL などの商用サイトでホストされているものも含まれる。      |
|プライベート IP アドレス      |  RFC 1918 で定義されているプライベート IP アドレスを使用するサイト。つまり、他の企業のホストへのアクセスを必要とせず (またはアクセスを制限する必要があり)、その IP アドレスが企業間では不明確であるが、特定の企業内では明確に定義されるホスト。        |
|職業的なネットワーク構築   | オンライン コミュニティで職業的なネットワークを構築できるサイト。   |
|検索エンジンとポータル   |Web、ニュースグループ、画像、ディレクトリ、その他のオンライン コンテンツを検索できるサイト。 ホワイト ページやイエロー ページなどのポータルおよびディレクトリ サイトが含まれる。    |
|翻訳     |   Web ページまたは語句をある言語から別の言語に翻訳するサイト。 これらのサイトはプロキシ サーバーをバイパスするため、アノニマイザを使用する場合と同様に、許可されていないコンテンツにアクセスされるリスクがある。       |
|ファイルのリポジトリ     |  シェアウェア、フリーウェア、オープン ソース、その他のソフトウェア ダウンロードのコレクションを含む Web ページ。        |
|Web ベースのメール     | ユーザーが Web でアクセスできるメール アカウントを使用してメールを送受信できるサイト。         |
|     |         |


## <a name="productivity-loss"></a>生産性の低下

|カテゴリ   |説明  |
|---------|---------|
|広告とポップアップ    |  Web ページに表示される広告グラフィックスやその他の広告コンテンツ ファイルを提供するサイト。       |
|チャット    |   チャット サービスまたはチャット ルームを介して Web ベースのリアルタイム メッセージ交換を可能にするサイト。       |
|カルト   |   一般に「カルト」と呼ばれる非伝統的な宗教活動に関連するサイト。カルトは、疑似的、非正統的、過激主義的、威圧的であると見なされ、そのメンバーは多くの場合、カリスマ的リーダーの指示の下に生活している。       |
|ゲーム    |    コンピューターやその他のゲーム、ゲーム プロデューサーに関する情報、またはチート コードの入手方法に関連するサイト。 ゲーム関連出版物のサイト。      |
|インスタント メッセージング    | ICQ、AOL Instant Messenger、IRC、MSN、Jabber、Yahoo Messenger などのインスタント メッセージング サービスにログインできるサイト。         |
|ショッピング    |  オンライン ショッピング、カタログ、オンライン注文、会場、オークション、案内広告のサイト。 健康や医薬など、別のカテゴリでカバーされる製品やサービスのショッピングは除外される。       |
|ソーシャル ネットワーキング   |  さまざまなトピックのオンライン コミュニティ、友人関係、交際などのソーシャル ネットワーキングを可能にするサイト。        |
|   |         |

## <a name="general-surfing"></a>一般的なネット サーフィン

|カテゴリ   |説明  |
|---------|---------|
|芸術     | 芸術的コンテンツを含むか、または劇場、美術館、ギャラリー、ダンス カンパニー、写真、デジタル グラフィック リソースなどの芸術機関に関連するサイト。   |
|ファッションと美容    | ファッション、ジュエリー、性的魅力、美容、モデル業、化粧品、または関連する製品やサービスに関するサイト。 製品レビュー、比較、一般的な消費者情報が含まれる。   |
|全般    | 他のカテゴリに明確に分類されないサイト (空白の Web ページなど)。   |
|グリーティング カード    |利用者がグリーティング カードやポストカードを送受信できるサイト。    |
|レジャーとレクリエーション     | レクリエーション活動と趣味に関連するサイト。動物園、公共のレクリエーション センター、プール、遊園地、趣味 (ガーデニング、文芸、手工芸、自宅のリフォーム、インテリア、家族など) が含まれる。 |
|自然と環境保護     | 環境問題、持続可能な生活、エコロジー、自然、環境に関連する情報を含むサイト。        |
|政治     | 政治団体や政治的主張を宣伝するか、または政治団体、利益団体、選挙、法制、ロビー活動に関する情報を提供するサイト。 法律に関する情報や助言を提供するサイトも含まれる。       |
|不動産  |商業用または住宅用不動産サービスに関連するサイト。住宅やオフィスの賃貸、購入、資金調達などが含まれる。    |
|宗教    | 信仰、人間の精神性、宗教的信条を扱うサイト。教会、シナゴーグ、モスク、その他の礼拝所のサイトが含まれる。         |
|レストランと食事  |食品、食事、ケータリング サービスを掲載、論評、奨励、または宣伝するサイト。 レシピ サイト、調理の説明とヒント、食品、ワイン アドバイザーのサイトが含まれる。          |
|スポーツ   | スポーツ チーム、ファン クラブ、スコア、スポーツ ニュースに関連するサイト。 プロかアマチュアかを問わず、すべてのスポーツに関連する。        |
|輸送   | 自動車、バイク、ボート、トラック、RV などの自動車両に関する情報を含むサイト。オンライン購入サイトが含まれる。 製造元のサイト、販売代理店、レビュー サイト、価格、マニアのクラブ、公共交通機関などが含まれる。    |
|トラベル    | 旅行と観光の情報、オンライン予約、旅行サービスを提供するサイト (航空会社、宿泊施設、レンタカーなど)。 地域または都市の情報サイトが含まれる。         |
|未分類     |新しい Web サイトや個人サイトなど、分類されていないサイト。          |
|    |         |

## <a name="next-steps"></a>次のステップ
- [クイックスタート: Azure ファイアウォールとファイアウォール ポリシーを作成する - ARM テンプレート](../firewall-manager/quick-firewall-policy.md)
- [クイック スタート:可用性ゾーンを使用して Azure Firewall をデプロイする - ARM テンプレート](deploy-template.md)
- [チュートリアル:Azure portal を使用して Azure Firewall をデプロイして構成する](tutorial-firewall-deploy-portal.md)

