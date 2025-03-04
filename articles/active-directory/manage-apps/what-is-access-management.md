---
title: アプリへのアクセスを管理する
titleSuffix: Azure AD
description: Azure Active Directory により、組織が各ユーザーがアクセスするアプリをどのように指定できるかついて説明します。
services: active-directory
author: davidmu1
manager: CelesteDG
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.topic: conceptual
ms.date: 09/23/2021
ms.author: davidmu
ms.reviewer: alamaral
ms.openlocfilehash: 0f162e7c14fc2f4c9d123c5beca6a76dc9e6a072
ms.sourcegitcommit: 05c8e50a5df87707b6c687c6d4a2133dc1af6583
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2021
ms.locfileid: "132553102"
---
# <a name="manage-access-to-an-application"></a>アプリケーションへのアクセスの管理

継続的なアクセスの管理、使用状況の評価、レポート作成は、アプリが組織の ID システムに統合された後でも簡単な作業ではありません。 アプリへのアクセスの管理では、多くの場合、IT 管理者またはヘルプ デスクが進行中のアクティブな役割を担う必要があります。 場合によっては、割り当ては一般的なまたは部門の IT チームによって実行されます。 割り当ての決定はビジネスの意思決定者に委ねられ、IT が割り当てを行う前に彼らの承認が求められることが一般的です。  

他の組織は、既存の自動 ID との統合に投資し、ロール ベースの Access Control (RBAC)、属性ベースの Access Control (ABAC) などの管理システムにアクセスします。 統合とルールの開発はいずれも専門知識や高いコストが求められる傾向にあります。 いずれの管理方法での監視またはレポートも、個々にコストがかかる複雑な投資になります。

## <a name="how-does-azure-active-directory-help"></a>Azure Active Directory の機能

Azure AD では、構成済みのアプリケーション用に広範なアクセスの管理がサポートされているため、組織は、属性に基づく自動的な割り当て (ABAC または RBAC シナリオ) から、委任、また管理者の管理までにわたり、適切なアクセス ポリシーを簡単に達成できます。 Azure AD を使用すると、1 つのアプリケーションに対して複数の管理モデルを組み合わせて複雑なポリシーを簡単に達成できるだけでなく、同じ対象ユーザーに対して、アプリケーション全体で管理ルールを再利用することもできます。

Azure AD では、使用量と割り当てのレポートが完全に統合されるため、管理者は割り当ての状態、割り当てに関するエラーのほか、使用量に関して簡単にレポート作成できます。

### <a name="assigning-users-and-groups-to-an-app"></a>ユーザーとグループをアプリに割り当てる

Azure AD のアプリケーション割り当ては、次の 2 つの主要な割り当てモードが中心となります。

* **個別の割り当て** ディレクトリへのグローバル管理者のアクセス許可を持つ IT 管理者は個々のユーザー アカウントを選択してアプリケーションへのアクセス権を付与できます。

* **グループ ベースの割り当て (Azure AD Premium P1 または P2 に必要)** ディレクトリへのグローバル管理者のアクセス許可を持つ IT 管理者はアプリケーションにグループを割り当てることができます。 ユーザーのアクセス権は、そのユーザーがアプリケーションにアクセスしようとしたときに、ユーザーがグループのメンバーであるかどうかによって決まります。 言い換えると、管理者は "割り当てられたグループの現在のメンバーがアプリケーションへのアクセス権を持つ" ことを示す割り当てルールを効率的に作成できます。 この割り当てオプションを使用することで、管理者は Azure AD グループ管理オプションのメリットが得られます。グループには、[属性ベースの動的なグループ](../fundamentals/active-directory-groups-create-azure-portal.md)、外部システム グループ (オンプレミスの Active Directory や Workday など)、管理者によって管理されたグループ、セルフサービスで管理されたグループなどがあります。 1 つのグループを複数のアプリに簡単に割り当てて、割り当てアフィニティを持つアプリケーションで割り当てルールを共有し、全体的な管理の複雑さを軽減できます。

>[!NOTE]
>現時点では、アプリケーションに対するグループベースの割り当てでは、グループ メンバーシップはサポートされていません。

これら 2 つの割り当てモードを使用して、管理者は理想的な割り当て管理アプローチを実現できます。

### <a name="requiring-user-assignment-for-an-app"></a>アプリのユーザー割り当ての要求

特定の種類のアプリケーションでは、アプリケーションにユーザーを割り当てることを要求できます。 そうすることで、明示的に割り当てたユーザー以外の人がアプリケーションにサインインすることを禁止します。 次の種類のアプリケーションでこのオプションがサポートされています。

* SAML ベースの認証を使用したフェデレーション シングル サインオン (SSO) 用に構成されたアプリケーション
* Azure Active Directory 事前認証を使用するアプリケーション プロキシのアプリケーション
* ユーザーまたは管理者がそのアプリケーションに同意した後に OAuth 2.0/OpenID Connect 認証を使用する Azure AD アプリケーション プラットフォームに構築されたアプリケーション。 エンタープライズ アプリケーションには、サインインを許可されるユーザーをより詳細に制御できるものがあります。

ユーザー割り当てが要求される場合は、アプリケーションに (直接のユーザー割り当てを使用して、またはグループ メンバーシップに基づいて) 割り当てたユーザーのみがサインインできます。 アプリには、各自の [マイ アプリ] ポータルで、または直接リンクを使用してアクセスできます。

ユーザー割り当てが要求されない場合、割り当てられていないユーザーはマイ アプリにアプリが表示されませんが、引き続きアプリケーション自体にサインインする (SP によって開始されるサインオンともいう) か、またはアプリケーションの **[プロパティ]** ページで **[ユーザー アクセス URL]** を使用する (IDP によって開始されるサイン オンともいう) ことができます。 ユーザー割り当て構成の要求の詳細については、「[アプリケーションの構成](add-application-portal-configure.md)」を参照してください。

この設定は、アプリケーションが [マイ アプリ] に表示されるかどうかには影響しません。 アプリケーションにユーザーまたはグループを割り当てると、アプリケーションはユーザーの [マイ アプリ] アクセス パネルに表示されます。

> [!NOTE]
> アプリケーションが割り当てを要求する場合、そのアプリケーションに対するユーザーの同意は許可されません。 これは、そのアプリに対するユーザーの同意がそれ以外の場合に許可されている場合でも当てはまります。 割り当てを必要とするアプリに対して、[テナント全体の管理者の同意を付与](../manage-apps/grant-admin-consent.md)してください。

一部のアプリケーションでは、アプリケーションのプロパティにユーザー割り当てを要求するオプションがありません。 そのような場合、PowerShell を利用し、サービス プリンシパルで appRoleAssignmentRequired プロパティを設定できます。

### <a name="determining-the-user-experience-for-accessing-apps"></a>アプリにアクセスするときのユーザー エクスペリエンスを決定する

Azure AD には、組織内のエンド ユーザーに[アプリケーションをデプロイするためのカスタマイズ可能な方法が複数](end-user-experiences.md)用意されています。

* Azure AD のマイ アプリ
* Microsoft 365 アプリケーション起動プログラム
* フェデレーション アプリへの直接サインオン (service-pr)
* フェデレーション アプリ、パスワードベースのアプリ、または既存のアプリへのディープ リンク

企業アプリに割り当てられているユーザーがマイ アプリや Microsoft 365 アプリケーション起動プログラムでそれを表示できるかどうかを決定できます。

## <a name="example-complex-application-assignment-with-azure-ad"></a>例:Azure AD を使用した複雑なアプリケーション割り当て

Salesforce のようなアプリケーションについて考えます。 多くの企業では、Salesforce は主にマーケティング チームや販売チームが使用します。 通常、マーケティング チームのメンバーは Salesforce に対する高い特権アクセスを持つ一方、販売チームのメンバーのアクセス権は制限されます。 多くの場合、インフォメーション ワーカーの占める割合が多いと、アプリケーションへのアクセスも制限されます。 これらのルールに対する例外が、問題を複雑にします。 通常、マーケティングまたは販売の指揮部隊には、これらの一般的なルールとは無関係に、ユーザーにアクセス権を付与したり、そのロールを変更したりする特権があります。

Azure AD では、Salesforce のようなアプリケーションをシングル サインオン (SSO) やプロビジョニングの自動化向けに事前構成できます。 アプリケーションが構成されたら、管理者は 1 回限りの操作を実行して、適切なグループを作成、割り当てることができます。 この例では、管理者は次のような割り当てを実行できます。

* [動的なグループ](../fundamentals/active-directory-groups-create-azure-portal.md) を定義できます。
  
  * マーケティング グループのすべてのメンバーは、Salesforce で "marketing" ロールに割り当てられます。
  * 販売チームのすべてのメンバーは、Salesforce で "sales" ロールに割り当てられます。 さらに調整するために、さまざまな Salesforce ロールに割り当てられた地域の販売チームを表す複数のグループを使用することもできます。

* 例外のメカニズムを有効にするには、各ロールについてセルフ サービス グループを作成できます。 たとえば、"salesforce marketing 例外" グループを、セルフ サービス グループとして作成します。 このグループを Salesforce marketing ロールに割り当て、マーケティングの指揮部隊を所有者にすることができます。 マーケティングの指揮部隊のメンバーはユーザーを追加または削除、参加ポリシーを設定できるほか、各ユーザーの参加要求を承認または拒否することもできます。 このメカニズムは、インフォメーション ワーカーに該当するエクスペリエンス全体でサポートされ、所有者またはメンバーになるための特別なトレーニングを必要としません。

この場合、割り当てられたすべてのユーザーは、Salesforce に自動的にプロビジョニングされます。 別のグループに追加されるときに、ロール割り当ては Salesforce で更新されます。 ユーザーは、マイ アプリ、Office Web クライアントを通じて、また組織の Salesforce サインイン ページに移動して、Salesforce を探してアクセスできます。 管理者は Azure AD レポート機能を使用して、使用量や割り当ての状態を簡単に確認できます。

管理者は、 [Azure AD 条件付きアクセス](../conditional-access/concept-conditional-access-users-groups.md) を使用して、特定のロールのアクセス ポリシーを設定できます。 これらのポリシーには、企業環境の外部でアクセスが許可されるかどうかや、場合によっては、さまざまな状況でアクセスを実現するための多要素認証やデバイス要件も含めることができます。

## <a name="access-to-microsoft-applications"></a>Microsoft アプリケーションへのアクセス

Microsoft アプリケーション (Exchange、SharePoint、Yammer など) の割り当てと管理は、サード パーティの SaaS アプリケーションや、シングル サインオンで Azure AD と統合する他のアプリケーションとは少し異なる方法で行います。

Microsoft が公開したアプリケーションにユーザーがアクセスする方法は、主に 3 つあります。

* Microsoft 365 またはその他の有料のスイートのアプリケーションでは、**ライセンスの割り当て** によってユーザーにアクセス権が付与されます。ライセンスの割り当ては、ユーザー アカウントに直接、またはグループ ベースのライセンス割り当て機能を使用してグループを通じて行われます。
* Microsoft またはサード パーティが誰でも使用できるように無料で公開するアプリケーションでは、[ユーザーの同意](configure-user-consent.md)によってユーザーにアクセス権が付与されます。 つまり、ユーザーは自分の Azure AD 職場または学校アカウントでアプリケーションにサインインし、そのアカウントの限定されたデータ セットにアクセスすることが許可されます。

* Microsoft またはサード パーティがだれでも使用できるよう無料で公開するアプリケーションでは、[管理者の同意](manage-consent-requests.md)によってユーザーにアクセス権を付与することもできます。 つまり、管理者は組織の全員がそのアプリケーションを使用する可能性があると判断しているため、グローバル管理者アカウントを使用してアプリケーションにサインインし、組織の全員にアクセス権を付与します。

一部のアプリケーションでは、これらのメソッドを組み合わせています。 たとえば、一部の Microsoft アプリケーションは Microsoft 365 サブスクリプションに含まれていますが、同意する必要が依然としてあります。

ユーザーは Office 365 ポータルから Microsoft 365 アプリケーションにアクセスできます。 また、ディレクトリの **[ユーザー設定]** にある [Office 365 表示切り替え機能](hide-application-from-user-portal.md)を利用し、マイ アプリで Microsoft 365 アプリケーションの表示と非表示を切り替えることができます。

企業アプリケーションと同様に、Azure portal から特定の Microsoft アプリケーションに[ユーザーを割り当てる](assign-user-or-group-access-portal.md)ことができます。あるいは、ポータルを利用できない場合、PowerShell を利用してユーザーを割り当てることができます。

## <a name="next-steps"></a>次のステップ

* [条件付きアクセスを使用したアプリケーションの保護](../conditional-access/concept-conditional-access-cloud-apps.md)
* [セルフサービス グループの管理/SSAA](../enterprise-users/groups-self-service-management.md)
