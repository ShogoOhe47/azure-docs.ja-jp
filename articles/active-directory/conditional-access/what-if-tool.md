---
title: 条件付きアクセスの What If ツール - Azure Active Directory
description: お使いの環境での条件付きアクセス ポリシーの影響を把握する方法について説明します。
services: active-directory
ms.service: active-directory
ms.subservice: conditional-access
ms.topic: conceptual
ms.date: 06/22/2020
ms.author: joflore
author: MicrosoftGuyJFlo
manager: karenhoran
ms.reviewer: nigu
ms.collection: M365-identity-device-management
ms.openlocfilehash: 47215f936ebc43b7aa720bc68f2caba294f03d46
ms.sourcegitcommit: f6e2ea5571e35b9ed3a79a22485eba4d20ae36cc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2021
ms.locfileid: "128595353"
---
# <a name="troubleshoot-using-the-what-if-tool-in-conditional-access"></a>What If ツールを使用した条件付きアクセスのトラブルシューティング

[条件付きアクセス](./overview.md)は、承認されたユーザーによるクラウド アプリへのアクセスを制御できるようにする、Azure Active Directory (Azure AD) の機能です。 環境内で条件付きアクセス ポリシーから予期される事柄を知るにはどうすればよいでしょうか。 この質問に答えるために、**条件付きアクセスの What If ツール** を使用できます。

この記事では、このツールを使用して、条件付きアクセス ポリシーをテストする方法について説明します。

> [!VIDEO https://www.youtube.com/embed/M_iQVM-3C3E]

## <a name="what-it-is"></a>説明

**条件付きアクセスの What If ポリシー ツール** によって、条件付きアクセス ポリシーが環境に与える影響を理解することができます。 複数のサインインを手動で実行することでポリシーの適用をテストする代わりに、このツールを使用して、ユーザーのシミュレートされたサインインを評価できます。 シミュレーションでは、サインインがポリシーに与える影響を推定し、シミュレーション レポートが生成されます。 レポートには、適用された条件付きアクセス ポリシーだけではなく、[クラシック ポリシー](policy-migration.md#classic-policies)が存在する場合はそれらも一覧表示されます。    

**What If** ツールは、特定のユーザーに適用されるポリシーをすばやく判断する方法も提供します。 この情報は、たとえば問題をトラブルシューティングする必要がある場合に使用できます。    

## <a name="how-it-works"></a>しくみ

**条件付きアクセスの What If ツール** では、シミュレートするサインイン シナリオの設定を最初に構成する必要があります。 これらの設定には、以下が含まれます。

- テストするユーザー 
- ユーザーがアクセスを試みるクラウド アプリ
- 構成されたクラウド アプリへのアクセスが実行される条件
     
次の手順として、設定を評価するシミュレーションの実行を開始できます。 有効になっているポリシーのみが、評価実行の一部になります。

評価が完了すると、ツールは、影響を受けたポリシーのレポートを生成します。 条件付きアクセス ポリシーに関する詳細情報を収集するには、レポート専用モードのポリシーと現在有効なポリシーの詳細について「[条件付きアクセスに関する分析情報とレポート」ワークブック](howto-conditional-access-insights-reporting.md)を参照してください。

## <a name="running-the-tool"></a>ツールの実行

**What If** ツールは、Azure portal の **[[条件付きアクセス - ポリシー]](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies)** ページで見つけることができます。

ツールを起動するには、ポリシーの一覧の上部にあるツール バーで、 **[What If]** をクリックします。

:::image type="content" source="./media/what-if-tool/01.png" alt-text="Azure portal の [条件付きアクセス - ポリシー] ページのスクリーンショット。ツールバーで、[What If] 項目が強調表示されていることを確認します。" border="false":::

評価を実行する前に、設定を構成する必要があります。

## <a name="settings"></a>設定

このセクションでは、シミュレーションの実行の設定について説明します。

:::image type="content" source="./media/what-if-tool/02.png" alt-text="Azure portal の [What If] ページに、ユーザー、クラウド アプリ、IP アドレス、デバイス プラットフォーム、クライアント アプリ、サインイン リスクのフィールドがあるスクリーンショット。" border="false":::

### <a name="user"></a>User

ユーザーは １ 人だけ選択できます。 これは唯一の必須フィールドです。

### <a name="cloud-apps"></a>クラウド アプリ

この設定の既定値は **[すべてのクラウド アプリ]** です。 既定の設定では、環境内で使用可能なすべてのポリシーの評価が実行されます。 特定のクラウド アプリに影響する範囲のポリシーに絞り込むことができます。

> [!NOTE]
> What If ツールを使用する場合、[条件付きアクセスのサービスの依存関係](service-dependencies.md)はテストされません。 たとえば、What If を使用して Microsoft Teams の条件付きアクセス ポリシーをテストする場合、Office 365 Exchange Online に適用されるポリシー (Microsoft Teams の条件付きアクセス サービスの依存関係) は、結果に考慮されません。

### <a name="ip-address"></a>IP アドレス

IP アドレスは、[場所の条件](location-condition.md)を模倣するための 1 つの IPv4 アドレスです。 このアドレスは、ユーザーがサインインするために使用するデバイスのインターネット アドレスを表します。 デバイスの IP アドレスは、たとえば [What is my IP address](https://whatismyipaddress.com) に移動することで確認できます。    

### <a name="device-platforms"></a>デバイス プラットフォーム

この設定は、[デバイス プラットフォームの条件](concept-conditional-access-conditions.md#device-platforms)を模倣し、 **[すべてのプラットフォーム (サポート対象外を含む)]** に相当します。 

### <a name="client-apps"></a>クライアント アプリ

この設定は、[クライアント アプリの条件](concept-conditional-access-conditions.md#client-apps)を模倣します。
既定では、この設定は、 **[ブラウザー]** または **[モバイル アプリとデスクトップ クライアント]** のどちらかが選択されているか両方が選択されているすべてのポリシーを評価します。 **[Exchange ActiveSync (EAS)]** を適用するポリシーも検出されます。 以下を選択することで、この設定を絞り込むことができます。

- 少なくとも  **[ブラウザー]** が選択されているすべてのポリシーのみを評価するには **[ブラウザー]** を選択。 
- 少なくとも **[モバイルアプリとデスクトップ クライアント]** が選択されているすべてのポリシーのみを評価するには **[モバイル アプリとデスクトップ クライアント]** を選択。 

### <a name="sign-in-risk"></a>サインイン リスク

この設定は、[サインイン リスクの条件](concept-conditional-access-conditions.md#sign-in-risk)を模倣します。   

## <a name="evaluation"></a>評価 

**[What If]** をクリックして評価を開始します。 以下で構成されるレポートによって評価結果が示されます。 

:::image type="content" source="./media/what-if-tool/03.png" alt-text="評価レポートのスクリーンショット。テキストは、少なくとも 1 つのクラシック ポリシーが構成されていることを示します。タブは、ポリシーを表示するために使用できます。" border="false":::

- 環境内にクラシック ポリシーが存在するかどうかを示すインジケーター
- ユーザーに適用されるポリシー
- ユーザーに適用されないポリシー

選択したクラウド アプリに適用される[クラシック ポリシー](policy-migration.md#classic-policies)が存在する場合は、インジケーターが表示されます。 インジケーターをクリックすると、クラシック ポリシー ページにリダイレクトされます。 クラシック ポリシー ページで、クラシック ポリシーを移行したり、単に無効にしたりできます。 このページを閉じることで、評価結果に戻ることができます。

選択したユーザーに適用されるポリシーの一覧で、ユーザーが満たす必要がある[許可コントロール](concept-conditional-access-grant.md)と[セッション](concept-conditional-access-session.md) コントロールの一覧も確認できます。

ユーザーに適用されないポリシーの一覧では、これらのポリシーが適用されない理由も確認できます。 表示されている各ポリシーの理由は、満たされていない最初の条件を表します。 ポリシーは、これ以上評価されないために無効なポリシーであるという理由で、適用されない場合があります。   

## <a name="next-steps"></a>次のステップ

- 条件付きアクセス ポリシー アプリケーションの詳細については、「[条件付きアクセスに関する分析情報とレポート](howto-conditional-access-insights-reporting.md)」のポリシーのレポート専用モードを参照してください。
- 環境に条件付きアクセス ポリシーを構成する準備ができたら、[一般的な条件付きアクセス ポリシー](concept-conditional-access-policy-common.md)に関するページを参照してください。
