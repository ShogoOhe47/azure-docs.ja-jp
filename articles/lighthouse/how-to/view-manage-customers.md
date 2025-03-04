---
title: 顧客と委任されたリソースを Azure portal で表示し、管理する
description: Azure Lighthouse を使用するサービス プロバイダーまたはエンタープライズとして、Azure portal の [マイ カスタマー] にアクセスすることで、自社に委任されたリソースとサブスクリプションをすべて表示できます。
ms.date: 09/17/2021
ms.topic: how-to
ms.openlocfilehash: 4cce38b435ee2613b885dfad959871579579ddce
ms.sourcegitcommit: f6e2ea5571e35b9ed3a79a22485eba4d20ae36cc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2021
ms.locfileid: "128673636"
---
# <a name="view-and-manage-customers-and-delegated-resources-in-the-azure-portal"></a>顧客と委任されたリソースを Azure portal で表示し、管理する

[Azure Lighthouse](../overview.md) を使用するサービス プロバイダーは、[Azure portal](https://portal.azure.com) の **[マイ カスタマー]** ページを使用して、委任された顧客のリソースとサブスクリプションを表示できます。

> [!TIP]
> ここではサービス プロバイダーと顧客に言及しますが、[複数のテナントを管理している企業](../concepts/enterprise.md)では、同じプロセスを使用して自社の管理エクスペリエンスを強化することができます。

Azure portal の **[マイ カスタマー]** ページにアクセスするには、 **[すべてのサービス]** を選択し、 **[マイ カスタマー]** を探して選択します。 Azure portal の上部付近にある検索ボックスに「マイ カスタマー」と入力して見つけることもできます。

**[マイ カスタマー]** ページの先頭の **[顧客]** セクションに表示されるのは、サブスクリプションまたはリソース グループを Azure Active Directory (Azure AD) テナントに、Azure Lighthouse を通じて委任した側の顧客に関する情報だけである点に留意してください。 他の顧客と (たとえば [クラウド ソリューション プロバイダー (CSP) プログラム](/partner-center/csp-overview)を通して) 連携する場合、これらの顧客に関する情報は、[そのリソースを Azure Lighthouse にオンボード](onboard-customer.md)していない限り、 **[顧客]** セクションに表示されません (ただし、特定の CSP 顧客に関する詳細がページの下部の [[クラウド ソリューション プロバイダー (プレビュー)] セクション](#cloud-solution-provider-preview)に表示される場合があります)。

> [!NOTE]
> 顧客は、Azure portal の **[サービス プロバイダー]** に移動して、サービス プロバイダーの情報を表示できます。 詳細については、「[サービス プロバイダーを表示し、管理する](view-manage-service-providers.md)」を参照してください。

## <a name="view-and-manage-customer-details"></a>顧客の詳細を表示して管理する

顧客の詳細を表示するには、 **[マイ カスタマー]** ページの左側にある **[顧客]** を選択します。

> [!IMPORTANT]
> この情報を表示するために、オンボード プロセスでユーザーに[閲覧者](../../role-based-access-control/built-in-roles.md#reader)ロール (または閲覧者アクセス権が含まれる別の組み込みロール) が許可されている必要があります。

顧客ごとに、その顧客名と顧客 ID (テナント ID)、契約に関連付けられている **オファー ID** と **オファーバージョン** が表示されます。 **[委任]** 列には、委任されたサブスクリプションの数または委任されたリソース グループの数が表示されます。

このページの上部にある各オプションで顧客情報を、特定の顧客やオファー、キーワードで並べ替え、フィルター処理、およびグループ化できます。

このページから次の情報を確認できます。

- 顧客に関連付けられているサブスクリプション、オファー、委任をすべて表示するには、その顧客の名前を選択します。
- オファーとその委任の詳細を表示するには、そのオファーの名前を選択します。
- 委任されたサブスクリプションまたはリソース グループについて、ロールの割り当ての詳細を表示するには、該当するエントリを **[委任]** 列で選択します。

> [!NOTE]
> 委任された後に顧客がサブスクリプションの名前を変更すると、更新されたサブスクリプション名が表示されます。 テナントの名前を変更した場合でも、Azure portal の一部の場所に古いテナント名が表示される場合があります。

## <a name="view-and-manage-delegations"></a>委任を表示して管理する

[委任] には、委任されたサブスクリプションまたはリソース グループが、そのアクセス権を持つユーザーおよびアクセス許可と共に表示されます。 この情報を表示するには、 **[マイ カスタマー]** ページの左側にある **[委任]** を選択します。

このページの上部にある各オプションでこの情報を、特定の顧客やオファー、キーワードで並べ替え、フィルター処理、およびグループ化できます。

### <a name="view-role-assignments"></a>ロールの割り当てを表示する

それぞれの委任に関連付けられているユーザーおよびアクセス許可は、 **[ロール割り当て]** 列に表示されます。 各エントリを選択すると、サブスクリプションまたはリソース グループへのアクセス権が与えられたユーザー、グループ、サービス プリンシパルをすべて一覧表示できます。 そこから特定のユーザー、グループ、またはサービス プリンシパルの名前を選択すれば、さらに詳しい情報が表示されます。

### <a name="remove-delegations"></a>委任を削除する

Azure Lighthouse に顧客をオンボードするときに、[マネージド サービスの登録割り当ての削除ロール](../../role-based-access-control/built-in-roles.md#managed-services-registration-assignment-delete-role)をユーザーに付与した場合、そのユーザーは、委任の行に表示されるごみ箱アイコンを選択することで委任を削除できます。 これが行われると、サービス プロバイダーのテナント内のユーザーは、以前に委任されたリソースにアクセスできなくなります。

詳細については、「[委任へのアクセスを削除する](remove-delegation.md)」を参照してください。

## <a name="view-delegation-change-activity"></a>委任の変更アクティビティの表示

**[マイ カスタマー]** ページの **[アクティビティ ログ]** セクションには、顧客のサブスクリプションまたはリソース グループがテナントに委任されるたびに、そして以前に委任されたリソースが削除されるたびに記録されます。 この情報は、[ルート スコープで監視閲覧者ロールが割り当てられている](monitor-delegation-changes.md)ユーザーのみが表示できます。

詳細については、「[Azure portal で委任変更を表示する](monitor-delegation-changes.md#view-delegation-changes-in-the-azure-portal)」を参照してください。

## <a name="work-in-the-context-of-a-delegated-subscription"></a>委任されたサブスクリプションのコンテキストで作業する

Azure portal 内で、サインインしているディレクトリを切り替えることなく、委任されたサブスクリプションのコンテキストで直接作業を行うことができます。 そのためには次を行います。

1. Azure portal の上部付近にある **[ディレクトリ + サブスクリプション]** または **[設定]** アイコンを選択します。
1. [[ディレクトリ + サブスクリプション設定ページ]](../../azure-portal/set-preferences.md#directories--subscriptions) で、 **[高度なフィルター]** トグルが [[無効]](../../azure-portal/set-preferences.md#subscription-filters) になっていることを確認します。
1. **[既定のサブスクリプション フィルター]** セクションで、適切なディレクトリおよびサブスクリプションを選択します。 (サブスクリプション全体ではなく、1 つ以上のリソース グループへのアクセス権が与えられている場合は、そのリソース グループが属しているサブスクリプションを選択します。 その後は、そのサブスクリプションのコンテキストで作業を行うことになりますが、アクセスできるのは指定されたリソース グループのみです。)

:::image type="content" source="../media/subscription-filter-delegated.png" alt-text="1 つの委任されたサブスクリプションが選択された既定のサブスクリプション フィルターのスクリーンショット。":::

その後、[テナント間の管理エクスペリエンス](../concepts/cross-tenant-management-experience.md)をサポートするサービスにアクセスすると、そのサービスは既定でフィルターに含めた委任サブスクリプションのコンテキストになります。

既定のサブスクリプションは、上の手順に従って、別のサブスクリプションを選択するか、複数のサブスクリプションを選択することで、いつでも変更できます。 また、アクセスできるすべてのサブスクリプションをフィルターに含める必要がある場合は、 **[すべてのディレクトリ]** を選択してから、 **[すべて選択]** ボックスをオンにすることもできます。

:::image type="content" source="../media/subscription-filter-all.png" alt-text="すべてのディレクトリとサブスクリプションが選択された既定のサブスクリプション フィルターのスクリーンショット":::

> [!IMPORTANT]
> **[すべて選択]** ボックスをオンにすると、"*現在*" アクセスできるすべてのサブスクリプションが表示されるようフィルターが設定されます。 後で追加のサブスクリプションにアクセスできるようになった場合 (新しい顧客を Azure Lighthouse にオンボードした後など)、それらのサブスクリプションはフィルターに自動では追加されません。 **[ディレクトリ + サブスクリプション]** に戻り、追加のサブスクリプションを選択する (または **[すべて選択]** をオフにして再度オンにする) 必要があります。

テナント間の管理エクスペリエンスをサポートするサービス内から、委任されたサブスクリプションまたはリソース グループに関連した機能にアクセスすることもできます。その場合は、個別のサービス内からサブスクリプションまたはリソース グループを選択してください。

## <a name="cloud-solution-provider-preview"></a>クラウド ソリューション プロバイダー (プレビュー)

**[マイ カスタマー]** ページの別個の **[クラウド ソリューション プロバイダー (プレビュー)]** セクションに、[Microsoft 顧客契約 (MCA) に署名](/partner-center/confirm-customer-agreement)しており [Azure プランに加入している](/partner-center/azure-plan-get-started) CSP 顧客の課金情報とリソースが表示されます。 詳細については、「[Microsoft Partner Agreement の課金アカウントの概要](../../cost-management-billing/understand/mpa-overview.md)」をご覧ください。

そのような CSP 顧客は、Azure Lighthouse にもオンボードしているかどうかにかかわらず、このセクションに表示されます。 同様に、CSP 顧客は、Azure Lighthouse にオンボードするために、 **[マイ カスタマー]** の **[クラウド ソリューション プロバイダー (プレビュー)]** セクションに表示される必要はありません。

## <a name="next-steps"></a>次のステップ

- [テナント間の管理エクスペリエンス](../concepts/cross-tenant-management-experience.md)について学習します。
- 顧客が Azure portal の **[サービス プロバイダー]** に移動することによって、[サービス プロバイダーを表示し、管理](view-manage-service-providers.md)する方法を学習します。
