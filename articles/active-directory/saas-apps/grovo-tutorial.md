---
title: チュートリアル:Azure Active Directory シングル サインオン (SSO) と Grovo の統合 | Microsoft Docs
description: Azure Active Directory と Grovo の間にシングル サインオンを構成する方法について説明します。
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 08/28/2019
ms.author: jeedes
ms.openlocfilehash: 82324eca3d638724f946885fe809f2aba261a692
ms.sourcegitcommit: 1f29603291b885dc2812ef45aed026fbf9dedba0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/29/2021
ms.locfileid: "129229712"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-grovo"></a>チュートリアル:Azure Active Directory シングル サインオン (SSO) と Grovo の統合

このチュートリアルでは、Grovo と Azure Active Directory (Azure AD) を統合する方法について説明します。 Azure AD と Grovo を統合すると、次のことができます。

* Grovo にアクセスできるユーザーを Azure AD で制御できます。
* ユーザーが自分の Azure AD アカウントを使用して Grovo に自動的にサインインできるようにすることができます。
* 1 つの中央サイト (Azure Portal) で自分のアカウントを管理します。

SaaS アプリと Azure AD の統合の詳細については、「[Azure Active Directory でのアプリケーションへのシングル サインオン](../manage-apps/what-is-single-sign-on.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

開始するには、次が必要です。

* Azure AD サブスクリプション。 サブスクリプションがない場合は、[無料アカウント](https://azure.microsoft.com/free/)を取得できます。
* Grovo でのシングル サインオン (SSO) が有効なサブスクリプション。

## <a name="scenario-description"></a>シナリオの説明

このチュートリアルでは、テスト環境で Azure AD の SSO を構成してテストします。

* Grovo では、**SP Initiated SSO と IDP Initiated SSO** がサポートされます
* Grovo では、**Just-In-Time** ユーザー プロビジョニングがサポートされます

## <a name="adding-grovo-from-the-gallery"></a>ギャラリーからの Grovo の追加

Azure AD への Grovo の統合を構成するには、ギャラリーから管理対象 SaaS アプリの一覧に Grovo を追加する必要があります。

1. 職場または学校アカウントか、個人の Microsoft アカウントを使用して、[Azure portal](https://portal.azure.com) にサインインします。
1. 左のナビゲーション ウィンドウで **[Azure Active Directory]** サービスを選択します。
1. **[エンタープライズ アプリケーション]** に移動し、 **[すべてのアプリケーション]** を選択します。
1. 新しいアプリケーションを追加するには、 **[新しいアプリケーション]** を選択します。
1. **[ギャラリーから追加する]** セクションで、検索ボックスに「**Grovo**」と入力します。
1. 結果のパネルから **[Grovo]** を選択し、アプリを追加します。 お使いのテナントにアプリが追加されるのを数秒待機します。

## <a name="configure-and-test-azure-ad-single-sign-on-for-grovo"></a>Grovo の Azure AD シングル サインオンの構成とテスト

**B.Simon** というテスト ユーザーを使用して、Grovo に対する Azure AD SSO を構成してテストします。 SSO を機能させるには、Azure AD ユーザーと Grovo の関連ユーザーとの間にリンク関係を確立する必要があります。

Grovo に対する Azure AD SSO を構成してテストするには、次の構成要素を完了します。

1. **[Azure AD SSO の構成](#configure-azure-ad-sso)** - ユーザーがこの機能を使用できるようにします。
    1. **[Azure AD のテスト ユーザーの作成](#create-an-azure-ad-test-user)** - B.Simon で Azure AD のシングル サインオンをテストします。
    1. **[Azure AD テスト ユーザーの割り当て](#assign-the-azure-ad-test-user)** - B.Simon が Azure AD シングル サインオンを使用できるようにします。
1. **[Grovo SSO の構成](#configure-grovo-sso)** - アプリケーション側でシングル サインオン設定を構成します。
    1. **[Grovo テスト ユーザーの作成](#create-grovo-test-user)** - Azure AD の B.Simon にリンクさせるために、対応するユーザーを Grovo で作成します。
1. **[SSO のテスト](#test-sso)** - 構成が機能するかどうかを確認します。

## <a name="configure-azure-ad-sso"></a>Azure AD SSO の構成

これらの手順に従って、Azure portal で Azure AD SSO を有効にします。

1. [Azure portal](https://portal.azure.com/) の **Grovo** アプリケーション統合ページで、 **[管理]** セクションを探して、 **[シングル サインオン]** を選択します。
1. **[シングル サインオン方式の選択]** ページで、 **[SAML]** を選択します。
1. **[SAML でシングル サインオンをセットアップします]** ページで、 **[基本的な SAML 構成]** の編集 (ペン) アイコンをクリックして設定を編集します。

   ![基本的な SAML 構成を編集する](common/edit-urls.png)

1. **[基本的な SAML 構成]** セクションで、アプリケーションを **IDP** 開始モードで構成する場合は、次のフィールドの値を入力します。

    a. **[識別子]** ボックスに、`https://<subdomain>.grovo.com/sso/saml2/metadata` の形式で URL を入力します。

    b. **[応答 URL]** ボックスに、`https://<subdomain>.grovo.com/sso/saml2/saml-assertion` のパターンを使用して URL を入力します

    c. **[追加の URL を設定します]** をクリックします。

    d. **[リレー状態]** ボックスに、`https://<subdomain>.grovo.com` のパターンで URL を入力します。

1. アプリケーションを **SP** 開始モードで構成する場合は、 **[追加の URL を設定します]** をクリックして次の手順を実行します。

    **[サインオン URL]** ボックスに、`https://<subdomain>.grovo.com/sso/saml2/saml-assertion` という形式で URL を入力します。

    > [!NOTE]
    > これらは実際の値ではありません。 実際の識別子、応答 URL、サインオン URL、リレー状態でこれらの値を更新します。 この値を取得するには、[Grovo クライアント サポート チーム](https://www.grovo.com/contact-us)にお問い合わせください。 Azure portal の **[基本的な SAML 構成]** セクションに示されているパターンを参照することもできます。

1. **[SAML でシングル サインオンをセットアップします]** ページの **[SAML 署名証明書]** セクションで、 **[証明書 (Base64)]** を見つけて、 **[ダウンロード]** を選択し、証明書をダウンロードして、お使いのコンピューターに保存します。

    ![証明書のダウンロードのリンク](common/certificatebase64.png)

1. **[Grovo のセットアップ]** セクションで、要件に基づいて適切な URL をコピーします。

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

このセクションでは、B.Simon に Grovo へのアクセスを許可することで、このユーザーが Azure シングル サインオンを使用できるようにします。

1. Azure portal で **[エンタープライズ アプリケーション]** を選択し、 **[すべてのアプリケーション]** を選択します。
1. アプリケーションの一覧で **[Grovo]** を選択します。
1. アプリの概要ページで、 **[管理]** セクションを見つけて、 **[ユーザーとグループ]** を選択します。

   ![[ユーザーとグループ] リンク](common/users-groups-blade.png)

1. **[ユーザーの追加]** を選択し、 **[割り当ての追加]** ダイアログで **[ユーザーとグループ]** を選択します。

    ![[ユーザーの追加] リンク](common/add-assign-user.png)

1. **[ユーザーとグループ]** ダイアログの [ユーザー] の一覧から **[B.Simon]** を選択し、画面の下部にある **[選択]** ボタンをクリックします。
1. SAML アサーション内に任意のロール値が必要な場合、 **[ロールの選択]** ダイアログでユーザーに適したロールを一覧から選択し、画面の下部にある **[選択]** をクリックします。
1. **[割り当ての追加]** ダイアログで、 **[割り当て]** をクリックします。

## <a name="configure-grovo-sso"></a>Grovo SSO の構成

1. 別の Web ブラウザー ウィンドウで、Grovo に管理者としてサインインします。

2. **[管理者]**  >  **[統合]** に移動します。
 
    ![[Integrations]\(統合\) が選択されている [Admin]\(管理者\) メニューを示すスクリーンショット。](./media/grovo-tutorial/tutorial_grovo_admin.png) 

3. **[SP Initiated SAML 2.0]\(SP によって開始された SAML 2.0\)** セクションで **[設定]** をクリックします。

    ![[Set up]\(設定\) ボタンが選択されている [SP Initiated SAML 2.0]\(SP によって開始された SAML 2.0\) セクションを示すスクリーンショット。](./media/grovo-tutorial/tutorial_grovo_setup.png)

4. **[SP Initiated SAML 2.0]\(SP によって開始された SAML 2.0\)** ポップアップ ウィンドウで、次の手順を実行します。

    ![Grovo 構成](./media/grovo-tutorial/tutorial_grovo_saml.png)

    a. **[Entity ID]\(エンティティ ID\)** ボックスに、Azure portal からコピーした **Azure AD ID** の値を貼り付けます。

    b. **[Single sign-on service endpoint]\(シングル サインオン サービス エンドポイント\)** ボックスに、Azure portal からコピーした **ログイン URL** の値を貼り付けます。

    c. **[Single sign-on service endpoint binding]\(シングル サインオン サービス エンドポイント バインディング\)** として `urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect` を選択します。
    
    d. Azure Portal からダウンロードした **Base64 でエンコードされた証明書** をメモ帳で開き、 **[公開キー]** ボックスに貼り付けます。

    e. **[次へ]** をクリックします。

### <a name="create-grovo-test-user"></a>Grovo テスト ユーザーの作成

このセクションでは、B. Simon というユーザーを Grovo に作成します。 Grovo では、Just-In-Time ユーザー プロビジョニングがサポートされており、既定で有効になっています。 このセクションでは、ユーザー側で必要な操作はありません。 Grovo にユーザーがまだ存在していない場合は、認証後に新しく作成されます。

> [!Note]
> ユーザーを手動で作成する必要がある場合は、[Grovoサポート チーム](https://www.grovo.com/contact-us)にお問い合わせください。

## <a name="test-sso"></a>SSO のテスト 

このセクションでは、アクセス パネルを使用して Azure AD のシングル サインオン構成をテストします。

アクセス パネル上で [Grovo] タイルをクリックすると、SSO を設定した Grovo に自動的にサインインします。 アクセス パネルの詳細については、[アクセス パネルの概要](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510)に関する記事を参照してください。

## <a name="additional-resources"></a>その他のリソース

- [SaaS アプリと Azure Active Directory を統合する方法に関するチュートリアルの一覧](./tutorial-list.md)

- [Azure Active Directory でのアプリケーション アクセスとシングル サインオンとは](../manage-apps/what-is-single-sign-on.md)

- [Azure Active Directory の条件付きアクセスとは](../conditional-access/overview.md)

- [Azure AD で Grovo を試す](https://aad.portal.azure.com/)