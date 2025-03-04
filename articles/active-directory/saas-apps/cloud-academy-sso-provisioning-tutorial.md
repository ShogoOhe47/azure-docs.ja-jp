---
title: 'チュートリアル: Azure Active Directory を使用した自動ユーザー プロビジョニングに対応するように Cloud Academy - SSO を構成する | Microsoft Docs'
description: Azure AD から Cloud Academy - SSO へのユーザー アカウントのプロビジョニングとプロビジョニング解除を自動的に実行する方法について説明します。
services: active-directory
documentationcenter: ''
author: twimmers
writer: twimmers
manager: beatrizd
ms.assetid: 224777cb-fc03-4e4a-8c8d-5befe1174233
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 06/02/2021
ms.author: thwimmer
ms.openlocfilehash: 1158bbb0e7f2bfd7e0503d2de3e4fb44b8e3a4f3
ms.sourcegitcommit: 5f659d2a9abb92f178103146b38257c864bc8c31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2021
ms.locfileid: "122321823"
---
# <a name="tutorial-configure-cloud-academy---sso-for-automatic-user-provisioning"></a>チュートリアル: 自動ユーザー プロビジョニングに対応するように Cloud Academy - SSO を構成する

このチュートリアルでは、自動ユーザー プロビジョニングを構成するために Cloud Academy - SSO と Azure Active Directory (Azure AD) の両方で実行する必要がある手順について説明します。 構成すると、Azure AD で Azure AD プロビジョニング サービスを使用して、[Cloud Academy - SSO](https://cloudacademy.com) へのユーザーとグループのプロビジョニングとプロビジョニング解除が自動的に実行されます。 このサービスが実行する内容、しくみ、よく寄せられる質問の重要な詳細については、「[Azure Active Directory による SaaS アプリへのユーザー プロビジョニングとプロビジョニング解除の自動化](../app-provisioning/user-provisioning.md)」を参照してください。 


## <a name="capabilities-supported"></a>サポートされる機能
> [!div class="checklist"]
> * Cloud Academy - SSO でユーザーを作成する
> * アクセスが不要になった場合に Cloud Academy - SSO のユーザーを削除する
> * Azure AD と Cloud Academy - SSO の間でのユーザー属性の同期を維持する
> * Cloud Academy - SSO への[シングル サインオン](./cloud-academy-sso-tutorial.md) (推奨)

## <a name="prerequisites"></a>前提条件

このチュートリアルで説明するシナリオでは、次の前提条件目があることを前提としています。

* [Azure AD テナント](../develop/quickstart-create-new-tenant.md) 
* プロビジョニングを構成するための[アクセス許可](../roles/permissions-reference.md)を持つ Azure AD のユーザー アカウント (アプリケーション管理者、クラウド アプリケーション管理者、アプリケーション所有者、グローバル管理者など)。 
* AD 統合をアクティブ化して API キーを生成するために、会社で管理者ロールを持つ Cloud Academy のユーザー アカウント。

## <a name="step-1-plan-your-provisioning-deployment"></a>手順 1. プロビジョニングのデプロイを計画する
1. [プロビジョニング サービスのしくみ](../app-provisioning/user-provisioning.md)を確認します。
2. [プロビジョニングの対象](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md)となるユーザーを決定します。
3. [Azure AD と Cloud Academy - SSO の間でマップする](../app-provisioning/customize-application-attributes.md)データを決定します。 

## <a name="step-2-configure-cloud-academy---sso-to-support-provisioning-with-azure-ad"></a>手順 2. Azure AD を使用したプロビジョニングをサポートするように Cloud Academy - SSO を構成する

1. [Sigma Computing](https://cloudacademy.com/) 管理ポータルにログインします。

2. ホームページのプロファイル アイコンの横にある **[Dashboard]\(ダッシュボード\)** をクリックします。

    ![ホーム](media/cloud-academy-sso-provisioning-tutorial/dashboard.png)

3. **自分のプロファイル** >  **[Settings & Integrations]\(設定および統合\)** に移動します。

    ![統合](media/cloud-academy-sso-provisioning-tutorial/settings.png)

4. Azure AD で、 **[統合]** タブをクリックし、 **[統合の表示]** をクリックします。

    ![ディレクトリ](media/cloud-academy-sso-provisioning-tutorial/active.png)

5. **[Generate a new API Key]\(新しい API キーの生成\)** を選択します。

    ![Generate](media/cloud-academy-sso-provisioning-tutorial/key.png)

6. 完全な API キーをコピーします。 この値を、Azure portal で Cloud Academy - SSO アプリケーションの [プロビジョニング] タブ内の **[シークレット トークン]** フィールドに入力します。

   >[!Note]
   >必要に応じて、新しい API キーを生成できます。 古い API キーは、AD ポータルで構成を更新するために必要な時間を確保するために、その後 **8 時間以内** に期限切れとしてマークされます。

7. テナント URL は、会社が登録されている場所に基づいて、`https://cloudacademy.com/webhooks/ad/v1/scim` または `https://app.qa.com/webhooks/ad/v1/scim` です。 この値を、Azure portal で Cloud Academy - SSO アプリケーションの [プロビジョニング] タブ内の **[テナント URL]** フィールドに入力します。

## <a name="step-3-add-cloud-academy---sso-from-the-azure-ad-application-gallery"></a>手順 3. Azure AD アプリケーション ギャラリーから Cloud Academy - SSO を追加する

Azure AD アプリケーションギャラリーから Cloud Academy-SSO を追加し、Cloud Academy-SSO へのプロビジョニングの管理を開始します。 SSO のために Cloud Academy - SSO を以前に設定している場合は、その同じアプリケーションを使用できます。 ただし、統合を初めてテストするときは、別のアプリを作成することをお勧めします。 ギャラリーからアプリケーションを追加する方法の詳細については、[こちら](../manage-apps/add-application-portal.md)を参照してください。 

## <a name="step-4-define-who-will-be-in-scope-for-provisioning"></a>手順 4. プロビジョニングの対象となるユーザーを定義する 

Azure AD プロビジョニング サービスを使用すると、アプリケーションへの割り当て、ユーザーまたはグループの属性に基づいてプロビジョニングされるユーザーのスコープを設定できます。 割り当てに基づいてアプリにプロビジョニングされるユーザーのスコープを設定する場合、以下の[手順](../manage-apps/assign-user-or-group-access-portal.md)を使用して、ユーザーとグループをアプリケーションに割り当てることができます。 ユーザーまたはグループの属性のみに基づいてプロビジョニングされるユーザーのスコープを設定する場合、[こちら](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md)で説明されているスコープ フィルターを使用できます。 

* Cloud Academy - SSO にユーザーとグループを割り当てるときは、**既定のアクセス** 以外のロールを選択する必要があります。 既定のアクセス ロールを持つユーザーは、プロビジョニングから除外され、プロビジョニング ログで実質的に資格がないとマークされます。 アプリケーションで使用できる唯一のロールが既定のアクセス ロールである場合は、[アプリケーション マニフェストを更新](../develop/howto-add-app-roles-in-azure-ad-apps.md)してロールを追加することができます。 

* 小さいところから始めましょう。 全員にロールアウトする前に、少数のユーザーとグループでテストします。 プロビジョニングのスコープが割り当て済みユーザーとグループに設定される場合、これを制御するには、1 つまたは 2 つのユーザーまたはグループをアプリに割り当てます。 スコープがすべてのユーザーとグループに設定されている場合は、[属性ベースのスコープ フィルター](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md)を指定できます。 


## <a name="step-5-configure-automatic-user-provisioning-to-cloud-academy---sso"></a>手順 5. Cloud Academy - SSO への自動ユーザー プロビジョニングを構成する 

このセクションでは、Azure AD でのユーザー、グループ、またはその両方の割り当てに基づいて、TestApp でユーザー、グループ、またはその両方が作成、更新、および無効化されるように Azure AD プロビジョニング サービスを構成する手順について説明します。

### <a name="to-configure-automatic-user-provisioning-for-cloud-academy---sso-in-azure-ad"></a>Azure AD で Cloud Academy - SSO の自動ユーザー プロビジョニングを構成するには:

1. [Azure portal](https://portal.azure.com) にサインインします。 **[エンタープライズ アプリケーション]** を選択し、 **[すべてのアプリケーション]** を選択します。

    ![[エンタープライズ アプリケーション] ブレード](common/enterprise-applications.png)

2. アプリケーションの一覧で **[Cloud Academy - SSO]** を選択します。

    ![アプリケーションの一覧の Cloud Academy - SSO リンク](common/all-applications.png)

3. **[プロビジョニング]** タブを選択します。

    ![[プロビジョニング] タブ](common/provisioning.png)

4. **[プロビジョニング モード]** を **[自動]** に設定します。

    ![[プロビジョニング] タブの [自動]](common/provisioning-automatic.png)

5. **[管理者資格情報]** セクションで、Cloud Academy - SSO のテナント URL とシークレット トークンを入力します。 **[テスト接続]** をクリックして、Azure AD から Cloud Academy - SSO に接続できることを確認します。 接続できない場合は、使用中の Cloud Academy - SSO アカウントに管理者アクセス許可があることを確認してからもう一度試します。

    ![トークン](common/provisioning-testconnection-tenanturltoken.png)

6. **[通知用メール]** フィールドに、プロビジョニングのエラー通知を受け取るユーザーまたはグループの電子メール アドレスを入力して、 **[エラーが発生したときにメール通知を送信します]** チェック ボックスをオンにします。

    ![通知用メール](common/provisioning-notification-email.png)

7. **[保存]** を選択します。

8. **[マッピング]** セクションの **[Synchronize Azure Active Directory Users to Cloud Academy - SSO]\(Azure Active Directory ユーザーを Cloud Academy - SSO に同期する\)** を選択します。

9. **[属性マッピング]** セクションで、Azure AD から Cloud Academy - SSO に同期されるユーザー属性を確認します。 **[Matching]\(照合\)** プロパティとして選択されている属性は、更新処理で Cloud Academy - SSO のユーザー アカウントとの照合に使用されます。 [照合する対象の属性](../app-provisioning/customize-application-attributes.md)を変更する場合は、その属性に基づいたユーザーのフィルター処理が Cloud Academy - SSO API でサポートされていることを確認する必要があります。 **[保存]** ボタンをクリックして変更をコミットします。

   |属性|Type|フィルター処理のサポート|
   |---|---|---|
   |userName|String|&check;|
   |externalId|String|
   |active|Boolean|
   |name.givenName|String|
   |name.familyName|String|

10. スコープ フィルターを構成するには、[スコープ フィルターのチュートリアル](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md)の次の手順を参照してください。

11. Cloud Academy - SSO に対して Azure AD プロビジョニング サービスを有効にするには、 **[設定]** セクションで **[プロビジョニング状態]** を **[オン]** に変更します。

    ![プロビジョニングの状態を [オン] に切り替える](common/provisioning-toggle-on.png)

12. **[設定]** セクションの **[スコープ]** で目的の値を選択して、Cloud Academy - SSO にプロビジョニングするユーザーやグループを定義します。

    ![プロビジョニングのスコープ](common/provisioning-scope.png)

13. プロビジョニングの準備ができたら、 **[保存]** をクリックします。

    ![プロビジョニング構成の保存](common/provisioning-configuration-save.png)

この操作により、 **[設定]** セクションの **[スコープ]** で定義したすべてのユーザーとグループの初期同期サイクルが開始されます。 初期サイクルは後続の同期よりも実行に時間がかかります。後続のサイクルは、Azure AD のプロビジョニング サービスが実行されている限り約 40 分ごとに実行されます。 

## <a name="step-6-monitor-your-deployment"></a>手順 6. デプロイを監視する
プロビジョニングを構成したら、次のリソースを使用してデプロイを監視します。

1. [プロビジョニング ログ](../reports-monitoring/concept-provisioning-logs.md)を使用して、正常にプロビジョニングされたユーザーと失敗したユーザーを特定します。
2. [進行状況バー](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user.md)を確認して、プロビジョニング サイクルの状態と完了までの時間を確認します。
3. プロビジョニング構成が異常な状態になったと考えられる場合、アプリケーションは検疫されます。 検疫状態の詳細については、[こちら](../app-provisioning/application-provisioning-quarantine-status.md)を参照してください。

## <a name="additional-resources"></a>その他のリソース

* [エンタープライズ アプリのユーザー アカウント プロビジョニングの管理](../app-provisioning/configure-automatic-user-provisioning-portal.md)
* [Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](../manage-apps/what-is-single-sign-on.md)

## <a name="next-steps"></a>次のステップ

* [プロビジョニング アクティビティのログの確認方法およびレポートの取得方法](../app-provisioning/check-status-user-account-provisioning.md)