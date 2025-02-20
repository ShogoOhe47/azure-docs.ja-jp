---
title: 条件付きアクセスのレポート専用モードとは - Azure Active Directory
description: 条件付きアクセス ポリシーのデプロイでのレポート専用モードの利点
services: active-directory
ms.service: active-directory
ms.subservice: conditional-access
ms.topic: conceptual
ms.date: 05/01/2020
ms.author: joflore
author: MicrosoftGuyJFlo
manager: karenhoran
ms.reviewer: dawoo
ms.collection: M365-identity-device-management
ms.openlocfilehash: c558c61f2ea35045cc3e3e66408340664e00ecf9
ms.sourcegitcommit: f6e2ea5571e35b9ed3a79a22485eba4d20ae36cc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2021
ms.locfileid: "128637971"
---
# <a name="what-is-conditional-access-report-only-mode"></a>条件付きアクセスのレポート専用モードとは

条件付きアクセスは、適切な状況下で適切なアクセス制御を適用することによってセキュリティを維持する目的で、お客様に広く使用されています。 条件付きアクセスポリシーを組織にデプロイする際の課題の 1 つに、エンド ユーザーに対する影響を見定めることが挙げられます。 レガシ認証のブロック、多数のユーザーに対する多要素認証の要求、サインイン リスク ポリシーの実装など、よくあるデプロイ イニシアティブによって影響を受けるユーザーの数と名前は、予測が難しいことがあります。 

レポート専用モードは、条件付きアクセス ポリシーの新しい状態です。このモードを使うと、管理者が環境で条件付きアクセス ポリシーを有効にする前に、その影響を評価することができます。  レポート専用モードのリリースによる変更点は次のとおりです。

- 条件付きアクセス ポリシーは、レポート専用モードで有効にできます。これは、"ユーザー アクション" スコープには適用されません。
- サインイン中に、レポート専用モードになっているポリシーが評価されますが、強制はされません。
- 結果は、サインイン ログの詳細にある **[条件付きアクセス]** および **[レポート専用]** タブに記録されます。
- Azure Monitor サブスクリプションをお持ちのお客様は、条件付きアクセスに関する分析情報のブックを使用して、条件付きアクセス ポリシーの影響を監視できます。

> [!VIDEO https://www.youtube.com/embed/NZbPYfhb5Kc]

> [!WARNING]
> レポート専用モードになっているポリシーで準拠しているデバイスが要求されている場合には、デバイスの準拠が強制されていなくても、ポリシーの評価中に Mac、iOS、および Android のユーザーに対してデバイス証明書の選択が求められる場合があります。 これらのプロンプトの表示は、デバイスが準拠状態になるまで繰り返される場合があります。 サインイン時にエンド ユーザーにプロンプトが表示されないようにするには、デバイス プラットフォームである Mac、iOS、および Android を、デバイスの準拠状態を確認するレポート専用ポリシーから除外します。 レポート専用モードは、"ユーザー アクション" スコープの条件付きアクセス ポリシーには適用されないことに注意してください。

![Azure AD の [サインイン] のレポート専用タブ](./media/concept-conditional-access-report-only/report-only-detail-in-sign-in-log.png)

## <a name="policy-results"></a>ポリシーの結果

特定のサインインについてレポート専用モードになっているポリシーが評価された場合、結果として返される可能性があるのは新たに用意された次の 4 つの値のいずれかです。

| 結果 | 説明 |
| --- | --- |
| レポートのみ: Success | 構成されているポリシー条件、必要な非対話型の許可コントロール、セッション コントロールをすべて充足しています。 たとえば、トークンに既に存在する MFA 要求によって多要素認証の要件が満たされている場合や、準拠しているデバイスでデバイス チェックを実行することにより、準拠しているデバイス ポリシーを充足している場合が挙げられます。 |
| レポートのみ: 障害 | 構成されているポリシー条件はすべて充足していますが、必要な非対話型の許可コントロールまたはセッション コントロールの一部またはすべてが充足できていません。 たとえば、ブロック コントロールが構成されているのにユーザーにポリシーが適用されている場合や、いずれかのデバイスが準拠しているデバイス ポリシーに準拠していない場合が挙げられます。 |
| レポートのみ: ユーザーによる操作が必要です | 構成されているポリシー条件はすべて充足していますが、必要な許可コントロールまたはセッション コントロールを充足するためにユーザーによる操作が必要です。 レポート専用モードでは、必要なコントロールの充足を求めるプロンプトがユーザーに表示されることはありません。 たとえば、多要素認証チャレンジや利用規約に関するプロンプトがユーザーに表示されることはありません。   |
| レポートのみ: 適用されていません | 構成されているポリシー条件の一部またはすべてを充足できていません。 たとえば、ユーザーがポリシーから除外されているか、またはポリシーが特定の信頼されたネームド ロケーションにしか適用されていません。 |

## <a name="conditional-access-insights-workbook"></a>条件付きアクセスに関する分析情報のブック

管理者は、レポート専用モードのポリシーを複数作成できます。そのため、各ポリシーが及ぼす個別の影響と、複数のポリシーが一緒に評価されたことによる複合的な影響の両方を把握する必要があります。 新しい "条件付きアクセスに関する分析情報のブック" を使用すると、管理者が条件付きアクセス クエリを視覚化して、特定の期間、一連のアプリケーション、ユーザーに対するポリシーの影響を監視できます。 
 
## <a name="next-steps"></a>次のステップ

[条件付きアクセス ポリシーに対するレポート専用モードの構成](howto-conditional-access-insights-reporting.md)
