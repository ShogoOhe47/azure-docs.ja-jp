---
title: 'チュートリアル: Azure Active Directory シングル サインオン (SSO) と Nintex Promapp の統合 | Microsoft Docs'
description: Azure Active Directory と Nintex Promapp の間でシングル サインオンを構成する方法について説明します。
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 08/31/2021
ms.author: jeedes
ms.openlocfilehash: 02eecf37fa94570e26bb795cd3882f2bec9b0aa1
ms.sourcegitcommit: 677e8acc9a2e8b842e4aef4472599f9264e989e7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2021
ms.locfileid: "132306759"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-nintex-promapp"></a>チュートリアル: Azure Active Directory シングル サインオン (SSO) と Nintex Promapp の統合

このチュートリアルでは、Nintex Promapp と Azure Active Directory (Azure AD) を統合する方法について説明します。 Azure AD と Nintex Promapp を統合すると、次のことができます。

* Nintex Promapp にアクセスできるユーザーを Azure AD で制御できます。
* ユーザーが自分の Azure AD アカウントを使用して Nintex Promapp に自動的にサインインできるように設定できます。
* 1 つの中央サイト (Azure Portal) で自分のアカウントを管理します。

## <a name="prerequisites"></a>前提条件

開始するには、次が必要です。

* Azure AD サブスクリプション。 サブスクリプションがない場合は、[無料アカウント](https://azure.microsoft.com/free/)を取得できます。
* Nintex Promapp でのシングル サインオン (SSO) が有効なサブスクリプション。

## <a name="scenario-description"></a>シナリオの説明

このチュートリアルでは、テスト環境で Azure AD の SSO を構成してテストします。

* Nintex Promapp では、**SP Initiated SSO と IDP Initiated SSO** がサポートされます。
* Nintex Promapp では、**Just In Time** ユーザー プロビジョニングがサポートされます。

* Nintex Promapp では、[自動化されたユーザー プロビジョニング](promapp-provisioning-tutorial.md)がサポートされます。

> [!NOTE]
> このアプリケーションの識別子は固定文字列値であるため、1 つのテナントで構成できるインスタンスは 1 つだけです。

## <a name="add-nintex-promapp-from-the-gallery"></a>ギャラリーからの Nintex Promapp の追加

Azure AD への Nintex Promapp の統合を構成するには、ギャラリーからマネージド SaaS アプリの一覧に Nintex Promapp を追加する必要があります。

1. 職場または学校アカウントか、個人の Microsoft アカウントを使用して、Azure portal にサインインします。
1. 左のナビゲーション ウィンドウで **[Azure Active Directory]** サービスを選択します。
1. **[エンタープライズ アプリケーション]** に移動し、 **[すべてのアプリケーション]** を選択します。
1. 新しいアプリケーションを追加するには、 **[新しいアプリケーション]** を選択します。
1. **[ギャラリーから追加する]** セクションで、検索ボックスに「**Nintex Promapp**」と入力します。
1. 結果のパネルから **[Nintex Promapp]** を選択し、アプリを追加します。 お使いのテナントにアプリが追加されるのを数秒待機します。

## <a name="configure-and-test-azure-ad-sso-for-nintex-promapp"></a>Nintex Promapp の Azure AD SSO の構成とテスト

**B.Simon** というテスト ユーザーを使用して、Nintex Promapp に対する Azure AD SSO を構成してテストします。 SSO が機能するためには、Azure AD ユーザーと Nintex Promapp の関連ユーザーとの間にリンク関係を確立する必要があります。

Nintex Promapp に対して Azure AD SSO を構成してテストするには、次の手順を実行します。

1. **[Azure AD SSO の構成](#configure-azure-ad-sso)** - ユーザーがこの機能を使用できるようにします。
    1. **[Azure AD のテスト ユーザーの作成](#create-an-azure-ad-test-user)** - B.Simon で Azure AD のシングル サインオンをテストします。
    1. **[Azure AD テスト ユーザーの割り当て](#assign-the-azure-ad-test-user)** - B.Simon が Azure AD シングル サインオンを使用できるようにします。
1. **[Nintex Promapp の SSO の構成](#configure-nintex-promapp-sso)** - アプリケーション側でシングル サインオン設定を構成します。
    1. **[Nintex Promapp のテスト ユーザーの作成](#create-nintex-promapp-test-user)** - Nintex Promapp で B.Simon に対応するユーザーを作成し、Azure AD の B.Simon にリンクさせます。
1. **[SSO のテスト](#test-sso)** - 構成が機能するかどうかを確認します。

## <a name="configure-azure-ad-sso"></a>Azure AD SSO の構成

これらの手順に従って、Azure portal で Azure AD SSO を有効にします。

1. Azure portal の **Nintex Promapp** アプリケーション統合ページで、 **[管理]** セクションを見つけて、 **[シングル サインオン]** を選択します。
1. **[シングル サインオン方式の選択]** ページで、 **[SAML]** を選択します。
1. **[SAML によるシングル サインオンのセットアップ]** ページで、 **[基本的な SAML 構成]** の鉛筆アイコンをクリックして設定を編集します。

   ![基本的な SAML 構成を編集する](common/edit-urls.png)

1. **[基本的な SAML 構成]** セクションで、アプリケーションを **IDP** 開始モードで構成する場合は、次の手順を実行します。

    1. **[識別子]** ボックスに、次のいずれかの URL を入力します。
        
        | 識別子 |
        |-----|
        |`https://go.promapp.com/TENANTNAME/`|
        |`https://au.promapp.com/TENANTNAME/`|
        |`https://us.promapp.com/TENANTNAME/`|
        |`https://eu.promapp.com/TENANTNAME/`|
        |`https://ca.promapp.com/TENANTNAME/`|

       > [!NOTE]
       > Nintex Promapp と Azure AD の統合は、現在、サービスによって開始される認証向けにのみ構成されています  (つまり、Nintex Promapp URL に移動することで、認証プロセスが開始されます)。ただし、 **[応答 URL]** フィールドは必須です。

    1. **[応答 URL]** ボックスに、`https://<DOMAIN_NAME>.promapp.com/TENANTNAME/saml/authenticate.aspx` の形式で URL を入力します。

1. アプリケーションを **SP** 開始モードで構成する場合は、 **[追加の URL を設定します]** をクリックして次の手順を実行します。

    **[サインオン URL]** ボックスに、`https://<DOMAIN_NAME>.promapp.com/TENANTNAME/saml/authenticate` という形式で URL を入力します。

    > [!NOTE]
    > これらの値はプレースホルダーです。 実際の識別子、応答 URL、サインオン URL を使用する必要があります。 この値を取得するには、[Nintex Promapp サポート チーム](https://www.promapp.com/about-us/contact-us/)に問い合わせてください。 また、Azure portal の **[基本的な SAML 構成]** ダイアログ ボックスに示されているパターンを参照することもできます。

1. **[SAML でシングル サインオンをセットアップします]** ページの **[SAML 署名証明書]** セクションで、 **[証明書 (Base64)]** を見つけて、 **[ダウンロード]** を選択し、証明書をダウンロードして、お使いのコンピューターに保存します。

    ![証明書のダウンロードのリンク](common/certificatebase64.png)

1. **[Nintex Promapp のセットアップ]** セクションで、要件に基づいて適切な URL をコピーします。

    ![構成 URL のコピー](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Azure AD のテスト ユーザーの作成

このセクションでは、Azure portal 内で B.Simon というテスト ユーザーを作成します。

1. Azure portal の左側のウィンドウから、 **[Azure Active Directory]** 、 **[ユーザー]** 、 **[すべてのユーザー]** の順に選択します。
1. 画面の上部にある **[新しいユーザー]** を選択します。
1. **[ユーザー]** プロパティで、以下の手順を実行します。
   1. **[名前]** フィールドに「`B.Simon`」と入力します。  
   1. **[ユーザー名]** フィールドに「username@companydomain.extension」と入力します。 たとえば、「 `B.Simon@contoso.com` 」のように入力します。
   1. **[パスワードを表示]** チェック ボックスをオンにし、 **[パスワード]** ボックスに表示された値を書き留めます。
   1. **Create** をクリックしてください。

### <a name="assign-the-azure-ad-test-user"></a>Azure AD テスト ユーザーの割り当て

このセクションでは、B.Simon に Nintex Promapp へのアクセスを許可することで、このユーザーが Azure シングル サインオンを使用できるようにします。

1. Azure portal で **[エンタープライズ アプリケーション]** を選択し、 **[すべてのアプリケーション]** を選択します。
1. アプリケーションの一覧で **[Nintex Promapp]** を選択します。
1. アプリの概要ページで、 **[管理]** セクションを見つけて、 **[ユーザーとグループ]** を選択します。
1. **[ユーザーの追加]** を選択し、 **[割り当ての追加]** ダイアログで **[ユーザーとグループ]** を選択します。
1. **[ユーザーとグループ]** ダイアログの [ユーザー] の一覧から **[B.Simon]** を選択し、画面の下部にある **[選択]** ボタンをクリックします。
1. ユーザーにロールが割り当てられることが想定される場合は、 **[ロールの選択]** ドロップダウンからそれを選択できます。 このアプリに対してロールが設定されていない場合は、[既定のアクセス] ロールが選択されていることを確認します。
1. **[割り当ての追加]** ダイアログで、 **[割り当て]** をクリックします。

## <a name="configure-nintex-promapp-sso"></a>Nintex Promapp の SSO の構成

1. Nintex Promapp 企業サイトに管理者としてサインインします。

2. ウィンドウ上部のメニューで **[Admin]\(管理者\)** を選択します。

    ![[Admin]\(管理者\) の選択](./media/promapp-tutorial/admin.png)

3. **[Configure]\(構成\)** を選択します。

    ![[Configure]\(構成\) の選択](./media/promapp-tutorial/configuration.png)

4. **[Security]\(セキュリティ\)** ダイアログ ボックスで、次の手順を実行します。

    ![[Security]\(セキュリティ\) ダイアログ ボックス](./media/promapp-tutorial/certificate.png)

    1. **[SSO Login URL]\(SSO ログイン URL\)** ボックスに、Azure portal からコピーした **[ログイン URL]** を貼り付けます。

    1. **[SSO - Single Sign-on Mode]\(SSO - シングル サインオン モード\)** の一覧で **[Optional]\(省略可能\)** を選択します。 **[保存]** を選択します。

       > [!NOTE]
       > [Optional]\(省略可能\) モードはテスト目的専用です。 構成が完了したら、**[SSO - Single Sign-on Mode]\(SSO - シングル サインオン モード\)** の一覧で **[Required]\(必須\)** を選択して、すべてのユーザーに強制的に Azure AD による認証が実施されるようにします。

    1. メモ帳で、前のセクションでダウンロードした証明書を開きます。 証明書の内容の、最初の行 (**-----BEGIN CERTIFICATE-----**) と最後の行 (**-----END CERTIFICATE-----**) 以外の部分をコピーします。 証明書の内容を **[SSO-x.509 Certificate]\(SSO-x.509 証明書\)** ボックスに貼り付けてから、**[Save]\(保存\)** を選択します。

### <a name="create-nintex-promapp-test-user"></a>Nintex Promapp のテスト ユーザーの作成

このセクションでは、B.Simon というユーザーを Nintex Promapp に作成します。 Nintex Promapp では、Just-In-Time ユーザー プロビジョニングがサポートされており、既定で有効になっています。 このセクションでは、ユーザー側で必要な操作はありません。 Nintex Promapp にユーザーがまだ存在していない場合は、認証後に新しく作成されます。

Nintex Promapp では、自動ユーザー プロビジョニングもサポートされます。自動ユーザー プロビジョニングの構成方法について詳しくは、[こちら](./promapp-provisioning-tutorial.md)をご覧ください。

## <a name="test-sso"></a>SSO のテスト

このセクションでは、次のオプションを使用して Azure AD のシングル サインオン構成をテストします。 

#### <a name="sp-initiated"></a>SP Initiated:

* Azure portal で **[このアプリケーションをテストします]** をクリックします。 これにより、ログイン フローを開始できる Nintex Promapp のサインオン URL にリダイレクトされます。  

* Nintex Promapp のサインオン URL に直接移動し、そこからログイン フローを開始します。

#### <a name="idp-initiated"></a>IDP Initiated:

* Azure portal で **[このアプリケーションをテストします]** をクリックすると、SSO を設定した Nintex Promapp に自動的にサインインされます。 

また、Microsoft マイ アプリを使用して、任意のモードでアプリケーションをテストすることもできます。 マイ アプリで [Nintex Promapp] タイルをクリックすると、SP モードで構成されている場合は、ログイン フローを開始するためのアプリケーション サインオン ページにリダイレクトされます。IDP モードで構成されている場合は、SSO を設定した Nintex Promapp に自動的にサインインされます。 マイ アプリの詳細については、[マイ アプリの概要](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

Nintex Promapp を構成したら、組織の機密データを流出と侵入からリアルタイムで保護するセッション制御を適用できます。 セッション制御は、条件付きアクセスを拡張したものです。 [Microsoft Defender for Cloud Apps でセッション制御を適用する方法をご覧ください](/cloud-app-security/proxy-deployment-aad)。
