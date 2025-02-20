---
title: Azure Active Directory アプリケーションのプロビジョニングの検疫状態
description: 自動ユーザー プロビジョニング用にアプリケーションを構成したら、検疫のプロビジョニング状態とクリアする方法について説明します。
services: active-directory
author: kenwith
manager: karenh444
ms.service: active-directory
ms.subservice: app-provisioning
ms.workload: identity
ms.topic: troubleshooting
ms.date: 05/11/2021
ms.author: kenwith
ms.reviewer: arvinh
ms.openlocfilehash: 93b00212bda4f02b6a31c151856639b1f461cac1
ms.sourcegitcommit: 106f5c9fa5c6d3498dd1cfe63181a7ed4125ae6d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2021
ms.locfileid: "131050833"
---
# <a name="application-provisioning-in-quarantine-status"></a>検疫状態のアプリケーションのプロビジョニング

Azure AD プロビジョニング サービスは、構成の正常性を監視します。 また、異常なアプリを "検疫" 状態にします。 ターゲット システムに対する呼び出しのほとんどまたはすべてが常に失敗する場合、プロビジョニング ジョブは検疫状態になります。 失敗の例としては、無効な管理者資格情報が原因で受け取るエラーがあります。

検疫中は、次のようになります。
- 増分サイクルの頻度は徐々に減少し、最終的には 1 日 1 回になります。
- すべてのエラーが修正されると、プロビジョニング ジョブは検疫から削除され、次の同期サイクルが開始します。 
- プロビジョニング ジョブが検疫にとどまっている期間が 4 週間を超えると、そのプロビジョニング ジョブは無効 (実行が停止) になります。

## <a name="how-do-i-know-if-my-application-is-in-quarantine"></a>アプリケーションが検疫されているかどうかを確認するにはどうすればよいですか。

アプリケーションが検疫中かどうかを確認するには、次の 3 つの方法があります。

- Azure portal で、 **[Azure Active Directory]**  >  **[エンタープライズ アプリケーション]**  > &lt;*アプリケーション名*&gt; >  **[プロビジョニング]** の順に移動し、検疫メッセージの進行状況バーを確認します。   

  ![検疫状態を示すプロビジョニング ステータス バー](./media/application-provisioning-quarantine-status/progress-bar-quarantined.png)

- Azure portal で **[Azure Active Directory]**  >  **[監査ログ]** の順に移動し、 **[アクティビティ: 検疫]** フィルターをオンにして、検疫履歴を確認します。 前に説明した進行状況バーのビューは、プロビジョニングが現在検疫中かどうかを示しています。 監査ログには、アプリケーションの検疫履歴が表示されます。 

- Microsoft Graph 要求の [Get synchronizationJob](/graph/api/synchronization-synchronizationjob-get?tabs=http&view=graph-rest-beta&preserve-view=true) を使用して、プロビジョニング ジョブの状態をプログラムで取得します。

```microsoft-graph
        GET https://graph.microsoft.com/beta/servicePrincipals/{id}/synchronization/jobs/{jobId}/
```

- メールを確認します。 アプリケーションが検疫されると、1 回限りの通知メールが送信されます。 検疫の理由が変化した場合、新しい検疫理由を示す更新されたメールが送信されます。 メールが送信されない場合は、次を確認します。

  - アプリケーションのプロビジョニング構成で有効な **通知メール** を指定していることを確認します。
  - 通知メールの受信トレイにスパム フィルターが適用されていないことを確認します。
  - メールの登録を解除していないことを確認します。
  - `azure-noreply@microsoft.com` からの電子メールを確認します。

## <a name="why-is-my-application-in-quarantine"></a>アプリケーションが検疫されているのはなぜですか。

|説明|推奨される操作|
|---|---|
|**SCIM へのコンプライアンスの問題:** 予期される HTTP/200 OK 応答ではなく、HTTP/404 Not Found 応答が返されました。 この場合、Azure AD プロビジョニング サービスによってターゲット アプリケーションへの要求が行われ、予期しない応答を受け取りました。|管理者資格情報のセクションを確認します。 アプリケーションでテナントの URL を指定する必要があるかどうか、および URL が正しいことを確認します。 問題が見つからない場合は、アプリケーションの開発者に連絡し、サービスが SCIM に準拠していることを確認してください。 https://tools.ietf.org/html/rfc7644#section-3.4.2 |
|**無効な資格情報:** ターゲット アプリケーションへのアクセスの承認を試みたとき、指定された資格情報が無効であることを示す応答をターゲット アプリケーションから受け取りました。|プロビジョニング構成 UI の管理者資格情報セクションに移動し、有効な資格情報で再度アクセスを承認してください。 アプリケーションがギャラリーにある場合は、アプリケーション構成のチュートリアルで追加の手順を確認してください。|
|**重複したロール:** Salesforce や Zendesk などの特定のアプリケーションからインポートされるロールは、一意である必要があります。 |Azure portal でアプリケーションの[マニフェスト](../develop/reference-app-manifest.md)に移動し、重複するロールを削除します。|

 プロビジョニング ジョブの状態を取得するための Microsoft Graph 要求では、次の検疫理由が示されます。
- `EncounteredQuarantineException` は、無効な資格情報が指定されたことを示します。 プロビジョニング サービスは、ソース システムとターゲット システム間の接続を確立できません。
- `EncounteredEscrowProportionThreshold` は、プロビジョニングがエスクローのしきい値を超えたことを示します。 この状態は、40% 以上のプロビジョニング イベントが失敗すると発生します。 詳細については、エスクローのしきい値の詳細を以下で確認してください。
- `QuarantineOnDemand` は、アプリケーションの問題を検出し、検疫するよう手動で設定したことを意味します。

**エスクローのしきい値**

エスクローの相応なしきい値に達した場合、プロビジョニング ジョブは検疫に入ります。 このロジックは変更される可能性がありますが、ほぼ次のように動作します。 

ジョブは、管理者の資格情報や SCIM コンプライアンスなどのイシューの失敗数に関係なく、検疫に入ることがあります。 ただし、一般に、失敗が多いことが原因での検疫を行うかどうかの評価を開始するには、最低でも 5,000 の失敗が必要です。 たとえば、4,000 の失敗が発生したジョブは検疫に入りません。 しかし、5,000 の失敗が発生したジョブでは、評価がトリガーされます。 評価では、次の条件が使用されます。  
- プロビジョニング イベントの 40% が失敗した場合、または 40,000 個を超える失敗が発生した場合、プロビジョニング ジョブは検疫に入ります。 参照の失敗は、40% のしきい値または 40,000 のしきい値の一部としてカウントされません。 たとえば、マネージャーまたはグループ メンバーの更新の失敗は、参照の失敗です。
- 45,000 人のユーザーが正常にプロビジョニングされなかったジョブは、40,000 のしきい値を超えているため、検疫に入ります。
- 30,000 人のユーザーがプロビジョニングに失敗し、5,000 人は正常に完了したジョブは、40% のしきい値と 5,000 の最小値を超えているため、検疫に入ります。
- 20,000 の失敗が発生し、100,000 が成功したジョブは、40% の失敗のしきい値または 40,000 の失敗の最大値を超えていないため、検疫に入りません。  
- 参照と非参照の両方の失敗から成る、60,000 の失敗の絶対しきい値があります。 たとえば、40,000 人のユーザーのプロビジョニングに失敗し、21,000 人のマネージャーの更新が失敗したとします。 失敗の合計は 61,000 であり、60,000 の制限を超えています。


## <a name="how-do-i-get-my-application-out-of-quarantine"></a>アプリケーションを検疫しないよう設定するにはどうすればよいですか。

まず、アプリケーションが検疫される原因となった問題を解決します。

- アプリケーションのプロビジョニング設定を調べ、[有効な管理者の資格情報](../app-provisioning/configure-automatic-user-provisioning-portal.md#configuring-automatic-user-account-provisioning)が入力されていることを確認してください。 Azure AD は、ターゲット アプリケーションとの信頼関係を確立する必要があります。 有効な資格情報を入力し、アカウントに必要なアクセス許可があることを確認します。

- [プロビジョニング ログ](../reports-monitoring/concept-provisioning-logs.md)を確認して、検疫の原因となっているエラーを詳しく調査し、解決します。 **[Azure Active Directory]** &gt; **[エンタープライズ アプリ]** &gt; **[プロビジョニング ログ (プレビュー)]** ( **[アクティビティ]** セクション内) を順に選択します。

問題を解決したら、プロビジョニング ジョブを再開します。 属性マッピングやスコープフィルターなど、アプリケーションのプロビジョニング設定に特定の変更を加えると、自動的にプロビジョニングが再開されます。 アプリケーションの **[プロビジョニング]** ページの進行状況バーは、プロビジョニングが最後に開始された日時を示します。 プロビジョニング ジョブを手動で再起動する必要がある場合は、次のいずれかの方法を使用します。  

- Azure portal を使用して、プロビジョニング ジョブを再起動します。 アプリケーションの **プロビジョニング** ページで、**プロビジョニングを再開する** を選択します。 この操作により、プロビジョニング サービスが完全に再起動されます (しばらく時間がかかることがあります)。 すべての初回サイクルが再度実行されます。これにより、エスクローがクリアされ、アプリが検疫から削除され、透かしがクリアされます。 このサービスでは、ソース システム内のすべてのユーザーを再度評価し、プロビジョニングの対象になっているかどうかを判断します。 これは、この記事で説明されているように、アプリケーションが現在検査中である場合や、属性マッピングを変更する必要がある場合に便利です。 初期サイクルは、評価が必要なオブジェクトの数が多いため、通常の増分サイクルよりも完了までに時間がかかることに注意してください。 初期サイクルと増分サイクルのパフォーマンスの詳細については、[こちら](application-provisioning-when-will-provisioning-finish-specific-user.md)を参照してください。

- Microsoft Graph を使用して、[プロビジョニング ジョブを再起動します](/graph/api/synchronization-synchronizationjob-restart?tabs=http&view=graph-rest-beta&preserve-view=true)。 再起動する対象は完全に制御できます。 エスクローをクリアするか (検疫状態と判定されるためのエスクロー カウンターを再起動するため)、検疫をオフにするか (検疫からアプリケーションを削除するため)、または透かしをクリアするかを選択できます。 次の要求を使用します。

```microsoft-graph
        POST /servicePrincipals/{id}/synchronization/jobs/{jobId}/restart
```

"{Id}" をアプリケーション ID の値に置き換え、"{jobId}" を[同期ジョブの ID](/graph/api/resources/synchronization-configure-with-directory-extension-attributes?tabs=http&view=graph-rest-beta&preserve-view=true#list-synchronization-jobs-in-the-context-of-the-service-principal) に置き換えます。
