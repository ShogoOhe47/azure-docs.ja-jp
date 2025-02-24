---
title: 'チュートリアル: Azure AD SSO と IBM Kenexa Survey Enterprise の統合'
description: Azure Active Directory と IBM Kenexa Survey Enterprise の間でシングル サインオンを構成する方法について説明します。
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 10/13/2021
ms.author: jeedes
ms.openlocfilehash: 49975523978cbf19e6900cd84ea5730a161c7c34
ms.sourcegitcommit: 677e8acc9a2e8b842e4aef4472599f9264e989e7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2021
ms.locfileid: "132294810"
---
# <a name="tutorial-azure-ad-sso-integration-with-ibm-kenexa-survey-enterprise"></a>チュートリアル: Azure AD SSO と IBM Kenexa Survey Enterprise の統合

このチュートリアルでは、IBM Kenexa Survey Enterprise と Azure Active Directory (Azure AD) を統合する方法について説明します。 IBM Kenexa Survey Enterprise と Azure AD を統合すると、次のことができます。

* IBM Kenexa Survey Enterprise にアクセスする Azure AD ユーザーを制御できます。
* ユーザーが自分の Azure AD アカウントを使用して IBM Kenexa Survey Enterprise に自動的にサインインできるように設定できます。
* 1 つの中央サイト (Azure Portal) で自分のアカウントを管理します。

## <a name="prerequisites"></a>前提条件

開始するには、次が必要です。

* Azure AD サブスクリプション。 サブスクリプションがない場合は、[無料アカウント](https://azure.microsoft.com/free/)を取得できます。
* IBM Kenexa Survey Enterprise のシングル サインオン (SSO) が有効なサブスクリプション。

## <a name="scenario-description"></a>シナリオの説明

このチュートリアルでは、テスト環境で Azure AD のシングル サインオンを構成してテストします。

* IBM Kenexa Survey Enterprise では、**IDP** によって開始される SSO がサポートされます。

## <a name="add-ibm-kenexa-survey-enterprise-from-the-gallery"></a>ギャラリーからの IBM Kenexa Survey Enterprise の追加

Azure AD への IBM Kenexa Survey Enterprise の統合を構成するには、ギャラリーから管理対象 SaaS アプリの一覧に IBM Kenexa Survey Enterprise を追加する必要があります。

1. 職場または学校アカウントか、個人の Microsoft アカウントを使用して、Azure portal にサインインします。
1. 左のナビゲーション ウィンドウで **[Azure Active Directory]** サービスを選択します。
1. **[エンタープライズ アプリケーション]** に移動し、 **[すべてのアプリケーション]** を選択します。
1. 新しいアプリケーションを追加するには、 **[新しいアプリケーション]** を選択します。
1. **[ギャラリーから追加する]** セクションで、検索ボックスに「**IBM Kenexa Survey Enterprise**」と入力します。
1. 結果のパネルから **[IBM Kenexa Survey Enterprise]** を選択し、アプリを追加します。 お使いのテナントにアプリが追加されるのを数秒待機します。

## <a name="configure-and-test-azure-ad-sso-for-ibm-kenexa-survey-enterprise"></a>IBM Kenexa Survey Enterprise の Azure AD SSO の構成とテスト

**B.Simon** というテスト ユーザーを使用して、IBM Kenexa Survey Enterprise に対する Azure AD SSO を構成してテストします。 SSO を機能させるために、Azure AD ユーザーと IBM Kenexa Survey Enterprise の関連ユーザーとの間にリンク関係を確立する必要があります。

IBM Kenexa Survey Enterprise に対して Azure AD SSO を構成してテストするには、次の手順を実行します。

1. **[Azure AD SSO の構成](#configure-azure-ad-sso)** - ユーザーがこの機能を使用できるようにします。
    1. **[Azure AD のテスト ユーザーの作成](#create-an-azure-ad-test-user)** - B.Simon で Azure AD のシングル サインオンをテストします。
    1. **[Azure AD テスト ユーザーの割り当て](#assign-the-azure-ad-test-user)** - B.Simon が Azure AD シングル サインオンを使用できるようにします。
1. **[IBM Kenexa Survey Enterprise の SSO の構成](#configure-ibm-kenexa-survey-enterprise-sso)** - アプリケーション側でシングル サインオン設定を構成します。
    1. **[IBM Kenexa Survey Enterprise のテスト ユーザーの作成](#create-ibm-kenexa-survey-enterprise-test-user)** - IBM Kenexa Survey Enterprise で B.Simon に対応するユーザーを作成し、Azure AD のこのユーザーにリンクさせます。
1. **[SSO のテスト](#test-sso)** - 構成が機能するかどうかを確認します。

## <a name="configure-azure-ad-sso"></a>Azure AD SSO の構成

これらの手順に従って、Azure portal で Azure AD SSO を有効にします。

1. Azure portal の **IBM Kenexa Survey Enterprise** アプリケーション統合ページで、 **[管理]** セクションを見つけて、 **[シングル サインオン]** を選択します。
1. **[シングル サインオン方式の選択]** ページで、 **[SAML]** を選択します。
1. **[SAML によるシングル サインオンのセットアップ]** ページで、 **[基本的な SAML 構成]** の鉛筆アイコンをクリックして設定を編集します。

   ![基本的な SAML 構成を編集する](common/edit-urls.png)

4. **[SAML でシングル サインオンをセットアップします]** ページで、次の手順を実行します。

    a. **[識別子]** ボックスに、`https://surveys.kenexa.com/<companycode>` の形式で URL を入力します。

    b. **[応答 URL]** ボックスに、`https://surveys.kenexa.com/<companycode>/tools/sso.asp` のパターンを使用して URL を入力します

    > [!NOTE]
    > これらは実際の値ではありません。 実際の識別子と応答 URL でこれらの値を更新します。 これらの値を入手するには、[IBM Kenexa Survey Enterprise クライアント サポート チーム](https://www.ibm.com/support/home/?lnk=fcw)にお問い合わせください。 Azure portal の **[基本的な SAML 構成]** セクションに示されているパターンを参照することもできます。

5. IBM Kenexa Survey Enterprise アプリケーションでは、特定の形式の Security Assertions Markup Language (SAML) アサーションを使用するため、カスタム属性マッピングを SAML トークン属性の構成に追加する必要があります。 応答内のユーザー識別子要求の値は、Kenexa システムで構成された SSO ID に一致する必要があります。 組織内の適切なユーザー ID を SSO Internet Datagram Protocol (IDP) としてマッピングするには、[IBM Kenexa Survey Enterprise サポート チーム](https://www.ibm.com/support/home/?lnk=fcw)と連携してください。

    既定では、Azure AD はユーザーの識別子を、ユーザー プリンシパル名 (UPN) の値として設定します。 この値は、以下のスクリーン ショットに示すように **[ユーザー属性]** タブから変更できます。 マッピングを正しく完了した後にのみ統合は機能します。

    ![image](common/edit-attribute.png)

6. **[SAML でシングル サインオンをセットアップします]** ページの **[SAML 署名証明書]** セクションで、 **[ダウンロード]** をクリックして要件のとおりに指定したオプションからの **証明書 (Base64)** をダウンロードして、お使いのコンピューターに保存します。

    ![証明書のダウンロードのリンク](common/certificatebase64.png)

7. **[IBM Kenexa Survey Enterprise のセットアップ]** セクションで、要件に従って適切な URL をコピーします。

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

このセクションでは、B.Simon に IBM Kenexa Survey Enterprise へのアクセスを許可することで、このユーザーが Azure シングル サインオンを使用できるようにします。

1. Azure portal で **[エンタープライズ アプリケーション]** を選択し、 **[すべてのアプリケーション]** を選択します。
1. アプリケーションの一覧で、 **[IBM Kenexa Survey Enterprise]** を選択します。
1. アプリの概要ページで、 **[管理]** セクションを見つけて、 **[ユーザーとグループ]** を選択します。
1. **[ユーザーの追加]** を選択し、 **[割り当ての追加]** ダイアログで **[ユーザーとグループ]** を選択します。
1. **[ユーザーとグループ]** ダイアログの [ユーザー] の一覧から **[B.Simon]** を選択し、画面の下部にある **[選択]** ボタンをクリックします。
1. ユーザーにロールが割り当てられることが想定される場合は、 **[ロールの選択]** ドロップダウンからそれを選択できます。 このアプリに対してロールが設定されていない場合は、[既定のアクセス] ロールが選択されていることを確認します。
1. **[割り当ての追加]** ダイアログで、 **[割り当て]** をクリックします。

## <a name="configure-ibm-kenexa-survey-enterprise-sso"></a>IBM Kenexa Survey Enterprise SSO の構成

**IBM Kenexa Survey Enterprise** 側でシングル サインオンを構成するには、ダウンロードした **証明書 (Base64)** と Azure portal からコピーした適切な URL を [IBM Kenexa Survey Enterprise サポート チーム](https://www.ibm.com/support/home/?lnk=fcw)に送信する必要があります。 サポート チームはこれを設定して、SAML SSO 接続が両方の側で正しく設定されるようにします。

### <a name="create-ibm-kenexa-survey-enterprise-test-user"></a>IBM Kenexa Survey Enterprise のテスト ユーザーの作成

このセクションでは、IBM Kenexa Survey Enterprise で Britta Simon というユーザーを作成します。

IBM Kenexa Survey Enterprise システムでユーザーを作成し、それに SSO ID をマッピングするには、[IBM Kenexa Survey Enterprise サポート チーム](https://www.ibm.com/support/home/?lnk=fcw)と連携してください。 また、この SSO ID 値を Azure AD のユーザー ID の値にマップする必要があります。 **[属性]** タブでこの既定の設定を変更できます。

## <a name="test-sso"></a>SSO のテスト

このセクションでは、次のオプションを使用して Azure AD のシングル サインオン構成をテストします。

* Azure portal で [このアプリケーションをテストします] をクリックすると、SSO を設定した IBM Kenexa Survey Enterprise に自動的にサインインされます。

* Microsoft マイ アプリを使用することができます。 マイ アプリで [IBM Kenexa Survey Enterprise] タイルをクリックすると、SSO を設定した IBM Kenexa Survey Enterprise に自動的にサインインされます。 マイ アプリの詳細については、[マイ アプリの概要](../user-help/my-apps-portal-end-user-access.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

IBM Kenexa Survey Enterprise を構成したら、組織の機密データを流出と侵入からリアルタイムで保護するセッション制御を適用できます。 セッション制御は、条件付きアクセスを拡張したものです。 [Microsoft Defender for Cloud Apps でセッション制御を適用する方法をご覧ください](/cloud-app-security/proxy-deployment-aad)。
