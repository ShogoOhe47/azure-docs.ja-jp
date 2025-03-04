---
title: Azure File Sync エージェントのリリース ノート | Microsoft Docs
description: Azure File Sync エージェントのリリース ノートを読み、Azure Files で組織のファイル共有を集中管理できるようにします。
services: storage
author: wmgries
ms.service: storage
ms.topic: conceptual
ms.date: 11/9/2021
ms.author: wgries
ms.subservice: files
ms.openlocfilehash: 27a5e1e1341b93a8172a179db1dc8596c103a184
ms.sourcegitcommit: 0415f4d064530e0d7799fe295f1d8dc003f17202
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2021
ms.locfileid: "132716032"
---
# <a name="release-notes-for-the-azure-file-sync-agent"></a>Azure File Sync エージェントのリリース ノート
Azure File Sync を使用すると、オンプレミスのファイル サーバーの柔軟性、パフォーマンス、互換性を損なわずに Azure Files で組織のファイル共有を一元化できます。 お使いの Windows Server のインストール済み環境が、Azure ファイル共有の高速キャッシュに生まれ変わります。 SMB、NFS、FTPS など、Windows Server 上で利用できるあらゆるプロトコルを使用して、データにローカルにアクセスできます。 キャッシュは、世界中にいくつでも必要に応じて設置することができます。

この記事では、サポートされているバージョンの Azure File Sync エージェントのリリース ノートについて取り上げます。

## <a name="supported-versions"></a>サポートされているバージョン
サポートされる Azure File Sync エージェント バージョンは次のとおりです。

| マイルストーン | エージェントのバージョン番号 | リリース日 | Status |
|----|----------------------|--------------|------------------|
| V14 リリース - [KB5001872](https://support.microsoft.com/topic/92290aa1-75de-400f-9442-499c44c92a81)| 14.0.0.0 | 2021 年 10 月 29 日 | サポート対象 - フライティング |
| V13 リリース - [KB4588753](https://support.microsoft.com/topic/632fb833-42ed-4e4d-8abd-746bd01c1064)| 13.0.0.0 | 2021 年 7 月 12 日 | サポートされています |
| V12.1 リリース - [KB4588751](https://support.microsoft.com/topic/497dc33c-d38b-42ca-8015-01c906b96132)| 12.1.0.0 | 2021 年 5 月 20 日 | サポートされている |
| V12 リリース- [KB4568585](https://support.microsoft.com/topic/b9605f04-b4af-4ad8-86b0-2c490c535cfd)| 12.0.0.0 | 2021 年 3 月 26 日 | サポートされている |
| V11.3 リリース - [KB4539953](https://support.microsoft.com/topic/f68974f6-bfdd-44f4-9659-bf2d8a696c26)| 11.3.0.0 | 2021 年 4 月 7 日 | サポートされています |
| V11.2 リリース - [KB4539952](https://support.microsoft.com/topic/azure-file-sync-agent-v11-2-release-february-2021-c956eaf0-cd8e-4511-98c0-e5a1f2c84048)| 11.2.0.0 | 2021 年 2 月 2 日 | サポートされています |
| V11.1 リリース - [KB4539951](https://support.microsoft.com/help/4539951)| 11.1.0.0 | 2020 年 11 月 4 日 | サポートされています |

## <a name="unsupported-versions"></a>サポートされていないバージョン
次の Azure File Sync エージェント バージョンは、有効期限が切れており、サポートされなくなりました。

| マイルストーン | エージェントのバージョン番号 | リリース日 | Status |
|----|----------------------|--------------|------------------|
| V10 リリース | 10.0.0.0 - 10.1.0.0 | 該当なし | サポートされていません - エージェント バージョンは 2021 年 6 月 28 日に有効期限が切れました |
| V9 リリース | 9.0.0.0 - 9.1.0.0 | 該当なし | サポートされていません - エージェント バージョンは 2021 年 2 月 16 日に有効期限が切れました |
| V8 リリース | 8.0.0.0 | N/A | サポートされていません - エージェント バージョンは 2021 年 1 月 12 日に有効期限が切れました |
| V7 リリース | 7.0.0.0 ～ 7.2.0.0 | 該当なし | サポートされていません - エージェント バージョンは 2020 年 9 月 1 日に有効期限が切れました |
| V6 リリース | 6.0.0.0 ～ 6.3.0.0 | 該当なし | サポートされていません - エージェント バージョンは 2020 年 4 月 21 日に有効期限が切れました |
| V5 リリース | 5.0.2.0 - 5.2.0.0 | 該当なし | サポートされていません - エージェント バージョンは 2020 年 3 月 18 日に有効期限が切れました |
| V4 リリース | 4.0.1.0 ～ 4.3.0.0 | 該当なし | サポートされていません - エージェント バージョンは 2019 年 11 月 6 日に有効期限が切れました |
| V3 リリース | 3.1.0.0 - 3.4.0.0 | 該当なし | サポートされていません - エージェント バージョンは 2019 年 8 月 19 日に有効期限が切れました |
| GA 前のエージェント | 1.1.0.0 - 3.0.13.0 | 該当なし | サポートされていません - エージェント バージョンは 2018 年 10 月 1 日に有効期限が切れました |

### <a name="azure-file-sync-agent-update-policy"></a>Azure File Sync Agent の更新ポリシー
[!INCLUDE [storage-sync-files-agent-update-policy](../../../includes/storage-sync-files-agent-update-policy.md)]

## <a name="agent-version-14000"></a>エージェント バージョン 14.0.0.0
次のリリース ノートは、Azure File Sync エージェントのバージョン 14.0.0.0 (2021 年 10 月 29 日にリリース) を対象としています。

### <a name="improvements-and-issues-that-are-fixed"></a>機能強化と修正された問題
- クラウド変更列挙ジョブの実行時のトランザクションの削減 
    - Azure File Sync には、24 時間ごとに実行されるクラウド変更列挙ジョブがあり、Azure ファイル共有で直接行われた変更を検出し、それらの変更を同期グループ内のサーバーに同期します。 このジョブの実行時のトランザクション数を減らすために改善が行われました。

- ポータルでのサーバー エンドポイントのプロビジョニング解除を支援するガイダンスの改善
    - ポータルを用いてサーバー エンドポイントを削除するとき、削除の理由に応じたステップ バイ ステップのガイダンスが表示されるようになりました。これによってデータの損失を防ぐと共に、あるべき場所 (サーバーまたは Azure ファイル共有) にデータを保持することができます。 また、この機能には新しい PowerShell コマンドレット (Get-StorageSyncStatus および New-StorageSyncUploadSession) が用意されており、それらをローカル サーバーで使用しながらプロビジョニング解除プロセスを効率よく進めることができます。

- Invoke-AzStorageSyncChangeDetection コマンドレットの改善
    - v14 未満のリリースでは、Azure ファイル共有に直接変更を加えた場合、Invoke-AzStorageSyncChangeDetection コマンドレットを使用して変更を検出し、同期グループ内のサーバーと同期させることができました。 ただしこのコマンドレットは、指定されたパスに含まれる項目の数が 10,000 を超えると実行に失敗します。 この Invoke-AzStorageSyncChangeDetection コマンドレットが改良されています。共有全体をスキャンする際に 10,000 項目の制限は適用されません。 詳細については、[Invoke-AzStorageSyncChangeDetection](/powershell/module/az.storagesync/invoke-azstoragesyncchangedetection) のドキュメントを参照してください。

- その他の機能強化
    - Azure File Sync が米国西部 3 リージョンでサポートされるようになりました。
    - FileSyncErrorsReport.ps1 スクリプトが項目ごとのエラーの一覧を提供しない原因となったバグが修正されました。
    - 項目単位の同期エラーが原因でファイルのアップロードが常態的に失敗する場合、トランザクション数が減らされます。
    - クラウドを使った階層化と同期に関して信頼性とテレメトリが改善されています。 

### <a name="evaluation-tool"></a>評価ツール
Azure File Sync をデプロイする前に、Azure File Sync 評価ツールを使用して、お使いのシステムと互換性があるかどうかを評価する必要があります。 このツールは Azure PowerShell コマンドレットであり、サポートされていない文字やサポートされていない OS バージョンなど、ファイル システムとデータセットに関する潜在的な問題をチェックします。 インストールおよび使用手順については、計画ガイドの「[評価ツール](file-sync-planning.md#evaluation-cmdlet)」セクションを参照してください。 

### <a name="agent-installation-and-server-configuration"></a>エージェントのインストールとサーバー構成
Windows Server で Azure File Sync エージェントをインストールして構成する方法の詳細については、「[Planning for an Azure File Sync deployment (Azure File Sync のデプロイの計画)](file-sync-planning.md)」および [Azure File Sync をデプロイする方法](file-sync-deployment-guide.md)に関するページを参照してください。

- エージェントのバージョンが 12.0 より前の場合は、Azure File Sync エージェントが既にインストールされているサーバーでは再起動が必要です。
- エージェント インストール パッケージは、引き上げられた (管理者) 特権でインストールする必要があります。
- Nano Server のデプロイ オプションでは、このエージェントはサポートされません。
- このエージェントは、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2022 でのみサポートされます。
- エージェントには、少なくとも 2 GiB のメモリが必要です。 動的メモリを有効にした仮想マシンでサーバーが実行されている場合は、2048 MiB 以上のメモリで VM を構成する必要があります。 詳細については、「[推奨されるシステム リソース](file-sync-planning.md#recommended-system-resources)」を参照してください。
- Storage Sync Agent (FileSyncSvc) サービスは、システム ボリューム情報 (SVI) ディレクトリが圧縮されているボリュームに配置されたサーバーのエンドポイントをサポートしません。 この構成は、予期しない結果になります。

### <a name="interoperability"></a>相互運用性
- 階層化されたファイルにアクセスするウイルス対策やバックアップなどのアプリケーションは、オフライン属性を考慮してそれらのファイルのコンテンツの読み取りをスキップする場合を除き、望ましくない再呼び出しを行う可能性があります。 詳細については、「[Troubleshoot Azure File Sync (Azure File Sync のトラブルシューティング)](file-sync-troubleshoot.md)」を参照してください。
- ファイル スクリーンによってファイルがブロックされた場合、File Server Resource Manager (FSRM) ファイル スクリーンが頻繁に同期エラーを引き起こす可能性があります。
- Azure File Sync エージェントがインストールされているサーバー上での sysprep の実行はサポートされていません。予期しない結果になる可能性があります。 Azure File Sync エージェントは、サーバー イメージの展開と sysprep ミニ セットアップの完了後にインストールされます。

### <a name="sync-limitations"></a>同期の制限事項
次の項目は同期されませんが、システムの残りの部分は引き続き正常に動作します。
- サポートされていない文字を含むファイル。 サポートされていない文字の一覧については、[トラブルシューティング ガイド](file-sync-troubleshoot.md#handling-unsupported-characters)のページを参照してください。
- 末尾がピリオドのファイルまたはディレクトリ。
- 2,048 文字を超えるパス。
- 監査に使用されるセキュリティ記述子のシステム アクセス制御リスト (SACL) 部分。
- 拡張属性。
- 代替データ ストリーム。
- 再解析ポイント。
- ハード リンク。
- 圧縮がサーバー ファイルに設定されている場合、変更が他のエンドポイントからそのファイルに同期されるときに、圧縮は保持されません。
- サービスがデータを読み取ることを妨げる、EFS (またはその他のユーザー モードの暗号化) で暗号化されたファイル。

    > [!Note]  
    > 転送中のデータは、Azure File Sync によって常に暗号化されます。 データは常に暗号化されて Azure に保存されます。
 
### <a name="server-endpoint"></a>サーバー エンドポイント
- サーバー エンドポイントは、NTFS ボリューム上にのみ作成できます。 ReFS、FAT、FAT32 などのファイル システムは、現在 Azure File Sync でサポートされていません。
- システム ボリュームでは、クラウドの階層化はサポートされていません。 システム ボリュームにサーバー エンドポイントを作成するには、サーバー エンドポイントを作成するときにクラウドの階層化を無効にします。
- フェールオーバー クラスタリングは、クラスター化ディスクでのみサポートされ、クラスターの共有ボリューム (CSV) ではサポートされません。
- サーバー エンドポイントを入れ子にすることはできません。 同じボリューム上に、別のエンドポイントと並列に共存させることはできます。
- サーバー エンドポイントの場所内に OS またはアプリケーションのページング ファイルを格納しないでください。

### <a name="cloud-endpoint"></a>クラウド エンドポイント
- Azure File Sync は、Azure ファイル共有に対する直接的な変更をサポートします。 ただし、Azure ファイル共有に対して行われた変更は、まず Azure File Sync の変更検出ジョブによって認識される必要があります。 クラウド エンドポイントに対する変更検出ジョブは、24 時間に 1 回起動されます。 Azure ファイル共有で変更されたファイルを直ちに同期したければ、[Invoke-AzStorageSyncChangeDetection](/powershell/module/az.storagesync/invoke-azstoragesyncchangedetection) PowerShell コマンドレットを使用すると、Azure ファイル共有における変更の検出を手動で開始できます。 さらに、REST プロトコルで Azure ファイル共有に対して行われた変更は、SMB の最終更新時刻を更新するものではなく、同期による変更とは見なされません。
- ストレージ同期サービスやストレージ アカウントは、別のリソース グループ、サブスクリプション、または Azure AD テナントに移動できます。 ストレージ同期サービスまたはストレージ アカウントを移動した後、Microsoft.StorageSync アプリケーションにストレージ アカウントへのアクセス権を付与する必要があります (「[Azure File Sync がストレージ アカウントへのアクセス権を持っていることを確認します](file-sync-troubleshoot.md?tabs=portal1%252cportal#troubleshoot-rbac)」を参照してください)。

    > [!Note]  
    > クラウド エンドポイントを作成するときは、ストレージ同期サービスとストレージ アカウントが同じ Azure AD テナントに存在する必要があります。 クラウド エンドポイントが作成された後、ストレージ同期サービスとストレージ アカウントを別の Azure AD テナントに移動できます。

### <a name="cloud-tiering"></a>クラウドの階層化
- 階層化されたファイルが Robocopy を使用して別の場所にコピーされた場合、その結果のファイルは階層化されません。 誤ってオフライン属性が Robocopy によるコピー操作の対象となり、オフライン属性が設定される場合があります。
- robocopy を使用してファイルをコピーする場合は、/MIR オプションを使用してファイルのタイムスタンプを保存します。 これにより、必ず最近アクセスされたファイルより先に、古いファイルが階層化されます。

## <a name="agent-version-13000"></a>エージェント バージョン 13.0.0.0
次のリリース ノートは、2021 年 7 月 12 日にリリースされた Azure File Sync エージェントのバージョン 13.0.0.0 を対象としています。

### <a name="improvements-and-issues-that-are-fixed"></a>機能強化と修正された問題
- 権限のあるアップロード  
    - 権限のあるアップロードは、同期グループで最初のサーバー エンドポイントを作成するときに使用できる新しいモードです。 クラウド (Azure ファイル共有) にデータの一部または大部分が含まれているものの、古くなって、新しいサーバー エンドポイントで最新のデータを検出する必要がある場合に便利です。 たとえば、DataBox のようなオフライン移行シナリオの場合です。 DataBox がいっぱいになり、Azure に送信されると、ローカル サーバーのユーザーはローカル サーバー上のファイルの変更、追加、削除を続けます。 これにより、データが DataBox に作成され、Azure ファイル共有が少し古いものになります。 権限のあるアップロードを使用すると、サーバーとクラウドを指定できるようになります。この問題を解決する方法と、サーバー上の最新の変更に合わせてクラウドをシームレスに更新する方法について説明します。 

        データがどのようにクラウドにあるかに関係なく、このモードでは、データがサーバー上の一致する場所からのものである場合、Azure ファイル共有を更新できます。 クラウドへの最初のコピーから権威のあるアップロードに追いつくまでの間に、大規模なディレクトリの再構築を行わないように注意してください。 これにより、更新プログラムのみが転送されるようになります。 ディレクトリ名を変更すると、これらの名前が変更されたディレクトリ内のすべてのファイルが再度アップロードされます。 この機能は、ソースに存在しなくなったターゲット上のファイルの削除など、RoboCopy/MIR = mirror source から target へのセマンティクスに匹敵します。 
        
        権限のあるアップロードは、ステージング共有を介して Azure File Sync との統合に使用される "オフラインデータ転送" 機能に代わるものです。 DataBox を使用するために、ステージング共有は不要になりました。 新しいオフライン データ転送ジョブは、AFS V13 エージェントで開始できなくなりました。 サーバー上の既存のジョブは、エージェント バージョン 13 にアップグレードした場合でも続行されます。

- クラウドの変更の列挙と同期の進行状況を表示するためのポータルの機能強化  
    - 新しい同期グループが作成されると、クラウドの変更の列挙が完了したときに、接続されているすべてのサーバー エンドポイントが同期を開始できます。  この同期グループのクラウド エンドポイント (Azure ファイル共有) にファイルが既に存在する場合、クラウド内のコンテンツの列挙を変更すると時間がかかることがあります。 名前空間に含まれる項目 (ファイルとフォルダー) が多いほど、このプロセスにかかる時間が長くなります。 管理者は、Azure portal でクラウド変更の列挙の進行状況を取得して、サーバーでの完了/同期のための eta を見積もることができるようになりました。

- サーバー名の変更のサポート  
    - 登録済みサーバーの名前を変更すると、Azure File Syn ではポータルに新しいサーバー名が表示されるようになります。 V13 リリースより前にサーバーの名前を変更した場合、ポータルのサーバー名が更新され、正しいサーバー名が表示されるようになります。

- Windows Server 2022 のサポート  
    - Azure File Sync エージェントは、Windows Server 2022 でサポートされるようになりました。

    > [!Note]  
    > Windows サーバー 2022 では、Azure File Sync で現在サポートされていない TLS 1.3 のサポートが追加されています。[TLS 設定](/windows-server/security/tls/tls-ssl-schannel-ssp-overview)がグループ ポリシーによって管理されている場合は、TLS 1.2 をサポートするようにサーバーを構成する必要があります。 

- その他の機能強化
    - 同期、クラウドの階層化、およびクラウドの変更の列挙の信頼性の向上。
    - サーバーで多数のファイルが変更された場合、同期アップロードは VSS スナップショットから実行されるようになりました。これにより、項目ごとのエラーと同期セッション エラーが減少します。 
    - Invoke-StorageSyncFileRecall コマンドレットは、ファイルがサーバー エンドポイントの場所の外に移動した場合でも、サーバー エンドポイントに関連付けられているすべての階層化されたファイルを再呼び出しします。 
    - Explorer.exe は、クラウド階層の最終アクセス時間の追跡から除外されるようになりました。
    - クラウドの階層化が有効になっているサーバー エンドポイントを削除した後に、孤立した階層化されたファイルのクリーンアップの進行状況を監視するための新しいテレメトリ (イベント ID 6664)。


### <a name="evaluation-tool"></a>評価ツール
Azure File Sync をデプロイする前に、Azure File Sync 評価ツールを使用して、お使いのシステムと互換性があるかどうかを評価する必要があります。 このツールは Azure PowerShell コマンドレットであり、サポートされていない文字やサポートされていない OS バージョンなど、ファイル システムとデータセットに関する潜在的な問題をチェックします。 インストールおよび使用手順については、計画ガイドの「[評価ツール](file-sync-planning.md#evaluation-cmdlet)」セクションを参照してください。 

### <a name="agent-installation-and-server-configuration"></a>エージェントのインストールとサーバー構成
Windows Server で Azure File Sync エージェントをインストールして構成する方法の詳細については、「[Planning for an Azure File Sync deployment (Azure File Sync のデプロイの計画)](file-sync-planning.md)」および [Azure File Sync をデプロイする方法](file-sync-deployment-guide.md)に関するページを参照してください。

- エージェントのバージョンが 12.0 より前の場合は、Azure File Sync エージェントが既にインストールされているサーバーでは再起動が必要です。
- エージェント インストール パッケージは、引き上げられた (管理者) 特権でインストールする必要があります。
- Nano Server のデプロイ オプションでは、このエージェントはサポートされません。
- このエージェントは、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2022 でのみサポートされます。
- エージェントには、少なくとも 2 GiB のメモリが必要です。 動的メモリを有効にした仮想マシンでサーバーが実行されている場合は、2048 MiB 以上のメモリで VM を構成する必要があります。 詳細については、「[推奨されるシステム リソース](file-sync-planning.md#recommended-system-resources)」を参照してください。
- Storage Sync Agent (FileSyncSvc) サービスは、システム ボリューム情報 (SVI) ディレクトリが圧縮されているボリュームに配置されたサーバーのエンドポイントをサポートしません。 この構成は、予期しない結果になります。

### <a name="interoperability"></a>相互運用性
- 階層化されたファイルにアクセスするウイルス対策やバックアップなどのアプリケーションは、オフライン属性を考慮してそれらのファイルのコンテンツの読み取りをスキップする場合を除き、望ましくない再呼び出しを行う可能性があります。 詳細については、「[Troubleshoot Azure File Sync (Azure File Sync のトラブルシューティング)](file-sync-troubleshoot.md)」を参照してください。
- ファイル スクリーンによってファイルがブロックされた場合、File Server Resource Manager (FSRM) ファイル スクリーンが頻繁に同期エラーを引き起こす可能性があります。
- Azure File Sync エージェントがインストールされているサーバー上での sysprep の実行はサポートされていません。予期しない結果になる可能性があります。 Azure File Sync エージェントは、サーバー イメージの展開と sysprep ミニ セットアップの完了後にインストールされます。

### <a name="sync-limitations"></a>同期の制限事項
次の項目は同期されませんが、システムの残りの部分は引き続き正常に動作します。
- サポートされていない文字を含むファイル。 サポートされていない文字の一覧については、[トラブルシューティング ガイド](file-sync-troubleshoot.md#handling-unsupported-characters)のページを参照してください。
- 末尾がピリオドのファイルまたはディレクトリ。
- 2,048 文字を超えるパス。
- 監査に使用されるセキュリティ記述子のシステム アクセス制御リスト (SACL) 部分。
- 拡張属性。
- 代替データ ストリーム。
- 再解析ポイント。
- ハード リンク。
- 圧縮がサーバー ファイルに設定されている場合、変更が他のエンドポイントからそのファイルに同期されるときに、圧縮は保持されません。
- サービスがデータを読み取ることを妨げる、EFS (またはその他のユーザー モードの暗号化) で暗号化されたファイル。

    > [!Note]  
    > 転送中のデータは、Azure File Sync によって常に暗号化されます。 データは常に暗号化されて Azure に保存されます。
 
### <a name="server-endpoint"></a>サーバー エンドポイント
- サーバー エンドポイントは、NTFS ボリューム上にのみ作成できます。 ReFS、FAT、FAT32 などのファイル システムは、現在 Azure File Sync でサポートされていません。
- システム ボリュームでは、クラウドの階層化はサポートされていません。 システム ボリュームにサーバー エンドポイントを作成するには、サーバー エンドポイントを作成するときにクラウドの階層化を無効にします。
- フェールオーバー クラスタリングは、クラスター化ディスクでのみサポートされ、クラスターの共有ボリューム (CSV) ではサポートされません。
- サーバー エンドポイントを入れ子にすることはできません。 同じボリューム上に、別のエンドポイントと並列に共存させることはできます。
- サーバー エンドポイントの場所内に OS またはアプリケーションのページング ファイルを格納しないでください。

### <a name="cloud-endpoint"></a>クラウド エンドポイント
- Azure File Sync は、Azure ファイル共有に対する直接的な変更をサポートします。 ただし、Azure ファイル共有に対して行われた変更は、まず Azure File Sync の変更検出ジョブによって認識される必要があります。 クラウド エンドポイントに対する変更検出ジョブは、24 時間に 1 回起動されます。 Azure ファイル共有で変更されたファイルを直ちに同期したければ、[Invoke-AzStorageSyncChangeDetection](/powershell/module/az.storagesync/invoke-azstoragesyncchangedetection) PowerShell コマンドレットを使用すると、Azure ファイル共有における変更の検出を手動で開始できます。 さらに、REST プロトコルで Azure ファイル共有に対して行われた変更は、SMB の最終更新時刻を更新するものではなく、同期による変更とは見なされません。
- ストレージ同期サービスやストレージ アカウントは、別のリソース グループ、サブスクリプション、または Azure AD テナントに移動できます。 ストレージ同期サービスまたはストレージ アカウントを移動した後、Microsoft.StorageSync アプリケーションにストレージ アカウントへのアクセス権を付与する必要があります (「[Azure File Sync がストレージ アカウントへのアクセス権を持っていることを確認します](file-sync-troubleshoot.md?tabs=portal1%252cportal#troubleshoot-rbac)」を参照してください)。

    > [!Note]  
    > クラウド エンドポイントを作成するときは、ストレージ同期サービスとストレージ アカウントが同じ Azure AD テナントに存在する必要があります。 クラウド エンドポイントが作成された後、ストレージ同期サービスとストレージ アカウントを別の Azure AD テナントに移動できます。

### <a name="cloud-tiering"></a>クラウドの階層化
- 階層化されたファイルが Robocopy を使用して別の場所にコピーされた場合、その結果のファイルは階層化されません。 誤ってオフライン属性が Robocopy によるコピー操作の対象となり、オフライン属性が設定される場合があります。
- robocopy を使用してファイルをコピーする場合は、/MIR オプションを使用してファイルのタイムスタンプを保存します。 これにより、必ず最近アクセスされたファイルより先に、古いファイルが階層化されます。

## <a name="agent-version-12100"></a>エージェント バージョン 12.1.0.0
次のリリース ノートは、2021 年 5 月 20 日にリリースされた Azure File Sync エージェントのバージョン 12.1.0.0 を対象としています。 これらは、バージョン 12.0.0.0 に関して記載されているリリース ノートへの追記です。

### <a name="improvements-and-issues-that-are-fixed"></a>機能強化と修正された問題 
v12.0 エージェント リリースに含まれていた次の 2 つのバグが、このリリースで修正されました。
- エージェントの自動更新で、エージェントを新しいバージョンに更新できない。
- FileSyncErrorsReport.ps1 スクリプトで、項目ごとのエラーの一覧が提供されない。

## <a name="agent-version-12000"></a>エージェント バージョン 12.0.0.0
次のリリース ノートは、(2021 年 3 月 26 日にリリースされた) Azure File Sync エージェントのバージョン 12.0.0.0 を対象としています。

### <a name="improvements-and-issues-that-are-fixed"></a>機能強化と修正された問題
- ネットワーク アクセス ポリシーとプライベート エンドポイント接続を構成するための新しいポータル エクスペリエンス
    - ポータルを使用して、ストレージ同期サービスのパブリック エンドポイントへのアクセスを無効にしたり、プライベート エンドポイント接続を承認、拒否、および削除したりできるようになりました。 ネットワーク アクセス ポリシーとプライベート エンドポイント接続を構成するには、ストレージ同期サービス ポータルを開き、[設定] セクションにアクセスして、[ネットワーク] をクリックします。
 
- 64 KiB を超えるボリューム クラスター サイズのクラウド階層化のサポート
    - クラウドの階層化では、Server 2019 で最大 2 MiB のボリューム クラスター サイズがサポートされるようになりました。 詳細については、「[階層化するファイルの最小ファイル サイズはどのくらいですか。](./file-sync-choose-cloud-tiering-policies.md#minimum-file-size-for-a-file-to-tier)」を参照してください。
 
- Azure File Sync サービスとストレージ アカウントの帯域幅と待機時間を測定する
    - Test-StorageSyncNetworkConnectivity コマンドレットを使用して、Azure File Sync サービスとストレージ アカウントの待機時間と帯域幅を測定できるようになりました。 このコマンドレットを実行すると、既定では、Azure File Sync サービスとストレージ アカウントの待機時間が測定されます。  "-MeasureBandwidth" パラメーターを使用すると、ストレージ アカウントへのアップロードとダウンロードの帯域幅が測定されます。
 
        たとえば、Azure File Sync サービスとストレージ アカウントの帯域幅と待機時間を測定するには、次の PowerShell コマンドを実行します。
 
        ```powershell
        Import-Module "C:\Program Files\Azure\StorageSyncAgent\StorageSync.Management.ServerCmdlets.dll"
        Test-StorageSyncNetworkConnectivity -MeasureBandwidth 
        ``` 
 
- サーバー エンドポイントの作成に失敗した場合にポータルに表示されるエラー メッセージの改善
    - お客様からのフィードバックを基に、サーバー エンドポイントの作成に失敗したときのエラー メッセージとガイダンスを改善しました。
 
- さまざまなパフォーマンスと信頼性の向上
    - Azure ファイル共有で変更されたファイルを検出するための変更検出のパフォーマンスが向上しました。
    - 調整同期セッションのパフォーマンスが向上しました。 
    - 同期の機能強化により、ECS_E_SYNC_METADATA_KNOWLEDGE_SOFT_LIMIT_REACHED と ECS_E_SYNC_METADATA_KNOWLEDGE_LIMIT_REACHED のエラーが減少しました。
    - クラウドを使った階層化が有効になっているときに、/B パラメーターを指定した Robocopy を使用して階層化ファイルをコピーすると、データが破損するバグを修正しました。
    - ボリュームでデータ重複除去が有効になっている場合に Server 2019 でファイルが階層化されない原因となるバグを修正しました。
    - ファイルが 2 GiB より大きい場合に AFSDiag でファイルの圧縮に失敗する原因となるバグを修正しました。

### <a name="evaluation-tool"></a>評価ツール
Azure File Sync をデプロイする前に、Azure File Sync 評価ツールを使用して、お使いのシステムと互換性があるかどうかを評価する必要があります。 このツールは Azure PowerShell コマンドレットであり、サポートされていない文字やサポートされていない OS バージョンなど、ファイル システムとデータセットに関する潜在的な問題をチェックします。 インストールおよび使用手順については、計画ガイドの「[評価ツール](file-sync-planning.md#evaluation-cmdlet)」セクションを参照してください。 

### <a name="agent-installation-and-server-configuration"></a>エージェントのインストールとサーバー構成
Windows Server で Azure File Sync エージェントをインストールして構成する方法の詳細については、「[Planning for an Azure File Sync deployment (Azure File Sync のデプロイの計画)](file-sync-planning.md)」および [Azure File Sync をデプロイする方法](file-sync-deployment-guide.md)に関するページを参照してください。

- 既存の Azure File Sync エージェントがインストールされているサーバーでは、再起動が必要です。
- エージェント インストール パッケージは、引き上げられた (管理者) 特権でインストールする必要があります。
- Nano Server のデプロイ オプションでは、このエージェントはサポートされません。
- このエージェントがサポートされるのは、Windows Server 2019、Windows Server 2016 および Windows Server 2012 R2 のみです。
- エージェントには、少なくとも 2 GiB のメモリが必要です。 動的メモリを有効にした仮想マシンでサーバーが実行されている場合は、2048 MiB 以上のメモリで VM を構成する必要があります。 詳細については、「[推奨されるシステム リソース](file-sync-planning.md#recommended-system-resources)」を参照してください。
- Storage Sync Agent (FileSyncSvc) サービスは、システム ボリューム情報 (SVI) ディレクトリが圧縮されているボリュームに配置されたサーバーのエンドポイントをサポートしません。 この構成は、予期しない結果になります。

### <a name="interoperability"></a>相互運用性
- 階層化されたファイルにアクセスするウイルス対策やバックアップなどのアプリケーションは、オフライン属性を考慮してそれらのファイルのコンテンツの読み取りをスキップする場合を除き、望ましくない再呼び出しを行う可能性があります。 詳細については、「[Troubleshoot Azure File Sync (Azure File Sync のトラブルシューティング)](file-sync-troubleshoot.md)」を参照してください。
- ファイル スクリーンによってファイルがブロックされた場合、File Server Resource Manager (FSRM) ファイル スクリーンが頻繁に同期エラーを引き起こす可能性があります。
- Azure File Sync エージェントがインストールされているサーバー上での sysprep の実行はサポートされていません。予期しない結果になる可能性があります。 Azure File Sync エージェントは、サーバー イメージの展開と sysprep ミニ セットアップの完了後にインストールされます。

### <a name="sync-limitations"></a>同期の制限事項
次の項目は同期されませんが、システムの残りの部分は引き続き正常に動作します。
- サポートされていない文字を含むファイル。 サポートされていない文字の一覧については、[トラブルシューティング ガイド](file-sync-troubleshoot.md#handling-unsupported-characters)のページを参照してください。
- 末尾がピリオドのファイルまたはディレクトリ。
- 2,048 文字を超えるパス。
- 監査に使用されるセキュリティ記述子のシステム アクセス制御リスト (SACL) 部分。
- 拡張属性。
- 代替データ ストリーム。
- 再解析ポイント。
- ハード リンク。
- 圧縮がサーバー ファイルに設定されている場合、変更が他のエンドポイントからそのファイルに同期されるときに、圧縮は保持されません。
- サービスがデータを読み取ることを妨げる、EFS (またはその他のユーザー モードの暗号化) で暗号化されたファイル。

    > [!Note]  
    > 転送中のデータは、Azure File Sync によって常に暗号化されます。 データは常に暗号化されて Azure に保存されます。
 
### <a name="server-endpoint"></a>サーバー エンドポイント
- サーバー エンドポイントは、NTFS ボリューム上にのみ作成できます。 ReFS、FAT、FAT32 などのファイル システムは、現在 Azure File Sync でサポートされていません。
- システム ボリュームでは、クラウドの階層化はサポートされていません。 システム ボリュームにサーバー エンドポイントを作成するには、サーバー エンドポイントを作成するときにクラウドの階層化を無効にします。
- フェールオーバー クラスタリングは、クラスター化ディスクでのみサポートされ、クラスターの共有ボリューム (CSV) ではサポートされません。
- サーバー エンドポイントを入れ子にすることはできません。 同じボリューム上に、別のエンドポイントと並列に共存させることはできます。
- サーバー エンドポイントの場所内に OS またはアプリケーションのページング ファイルを格納しないでください。
- サーバーの名前を変更した場合、ポータル内のサーバー名は更新されません。

### <a name="cloud-endpoint"></a>クラウド エンドポイント
- Azure File Sync は、Azure ファイル共有に対する直接的な変更をサポートします。 ただし、Azure ファイル共有に対して行われた変更は、まず Azure File Sync の変更検出ジョブによって認識される必要があります。 クラウド エンドポイントに対する変更検出ジョブは、24 時間に 1 回起動されます。 Azure ファイル共有で変更されたファイルを直ちに同期したければ、[Invoke-AzStorageSyncChangeDetection](/powershell/module/az.storagesync/invoke-azstoragesyncchangedetection) PowerShell コマンドレットを使用すると、Azure ファイル共有における変更の検出を手動で開始できます。 さらに、REST プロトコルで Azure ファイル共有に対して行われた変更は、SMB の最終更新時刻を更新するものではなく、同期による変更とは見なされません。
- ストレージ同期サービスやストレージ アカウントは、別のリソース グループ、サブスクリプション、または Azure AD テナントに移動できます。 ストレージ同期サービスまたはストレージ アカウントを移動した後、Microsoft.StorageSync アプリケーションにストレージ アカウントへのアクセス権を付与する必要があります (「[Azure File Sync がストレージ アカウントへのアクセス権を持っていることを確認します](file-sync-troubleshoot.md?tabs=portal1%252cportal#troubleshoot-rbac)」を参照してください)。

    > [!Note]  
    > クラウド エンドポイントを作成するときは、ストレージ同期サービスとストレージ アカウントが同じ Azure AD テナントに存在する必要があります。 クラウド エンドポイントが作成された後、ストレージ同期サービスとストレージ アカウントを別の Azure AD テナントに移動できます。

### <a name="cloud-tiering"></a>クラウドの階層化
- 階層化されたファイルが Robocopy を使用して別の場所にコピーされた場合、その結果のファイルは階層化されません。 誤ってオフライン属性が Robocopy によるコピー操作の対象となり、オフライン属性が設定される場合があります。
- robocopy を使用してファイルをコピーする場合は、/MIR オプションを使用してファイルのタイムスタンプを保存します。 これにより、必ず最近アクセスされたファイルより先に、古いファイルが階層化されます。

## <a name="agent-version-11300"></a>エージェント バージョン 11.3.0.0
次のリリース ノートは、2021 年 4 月 7 日にリリースされた Azure File Sync エージェントのバージョン 11.3.0.0 を対象としています。 これらは、バージョン 11.1.0.0 に関して記載されているリリース ノートへの追記です。

### <a name="improvements-and-issues-that-are-fixed"></a>機能強化と修正された問題 
クラウドを使った階層化が有効になっているときに、/B パラメーターを指定した Robocopy を使用して階層化ファイルをコピーすると、データが破損するバグを修正しました。

## <a name="agent-version-11200"></a>エージェント バージョン 11.2.0.0
次のリリース ノートは、2021 年 2 月 2 日にリリースされた Azure File Sync エージェントのバージョン 11.2.0.0 を対象としています。 これらは、バージョン 11.1.0.0 に関して記載されているリリース ノートへの追記です。

### <a name="improvements-and-issues-that-are-fixed"></a>機能強化と修正された問題 
- 項目ごとのエラーの数が多いために同期セッションがキャンセルされると、項目ごとのエラーを修正するためにカスタム同期セッションが必要であると Azure File Sync サービスによって判断された場合、新しいセッションが開始されたときに同期が調整されることがあります。
- Register-AzStorageSyncServer コマンドレットを使用したサーバーの登録が、"ハンドルされない例外" エラーで失敗することがあります。
- サーバー上で許可されるサーバー エンドポイント パスを構成するするための新しい PowerShell コマンドレット (Add-StorageSyncAllowedServerEndpointPath)。 このコマンドレットは、Azure File Sync のデプロイがクラウド ソリューション プロバイダー (CSP) またはサービス プロバイダーによって管理され、顧客がサーバー上で許可されているサーバー エンドポイント パスを構成する必要があるシナリオに役立ちます。 サーバー エンドポイントを作成するとき、指定されたパスが許可リストに含まれていない場合、サーバー エンドポイントの作成は失敗します。 これはオプションの機能であり、サポートされているすべてのパスは、サーバー エンドポイントを作成するときに既定で許可されることに注意してください。  

    
    - 許可されるサーバー エンドポイント パスを追加するには、サーバーで次の PowerShell コマンドを実行します。

    ```powershell
    Import-Module 'C:\Program Files\Azure\StorageSyncAgent\StorageSync.Management.ServerCmdlets.dll' -verbose
    Add-StorageSyncAllowedServerEndpointPath -Path <path>
    ```  

    - サポートされているパスの一覧を取得するには、次の PowerShell コマンドを実行します。
    
    ```powershell
    Get-StorageSyncAllowedServerEndpointPath
    ```     
    - パスを削除するには、次の PowerShell コマンドを実行します。
    
    ```powershell
    Remove-StorageSyncAllowedServerEndpointPath -Path <path>
    ```  
## <a name="agent-version-11100"></a>エージェント バージョン 11.1.0.0
次のリリース ノートは、2020 年 11 月 4 日にリリースされた Azure File Sync エージェントのバージョン 11.1.0.0 を対象としています。

### <a name="improvements-and-issues-that-are-fixed"></a>機能強化と修正された問題
- 初回ダウンロードと事前呼び戻しを制御する新しいクラウドを使った階層化のモード
    - 初回ダウンロード モード: 新しいサーバー エンドポイントへの初回ファイル ダウンロードの方法を選択できるようになりました。 すべてのファイルを階層化したり、最後に変更されたタイムスタンプに応じてサーバーにできる限り多くのファイルをダウンロードすることなどが できるようになります。 クラウドの階層化が使用できない場合も問題ありません。 システム上で階層化されたファイルを使用しないように選択できるようになりました。 詳細については、Azure File Sync のデプロイに関するドキュメントの「[サーバー エンドポイントを作成する](../file-sync/file-sync-deployment-guide.md?tabs=azure-portal%252cproactive-portal#create-a-server-endpoint)」セクションを参照してください。
    - 事前呼び戻しモード: ファイルが作成または変更されるたびに、同じ同期グループ内で指定したサーバーにファイルを事前に呼び戻すことができます。 これにより、指定した各サーバーでファイルをすぐに使用できるようになります。 世界中のチームが同じデータを使用していますか? 事前呼び戻しを有効にすると、チームが翌朝到着したときに、異なるタイム ゾーンのチームが更新したすべてのファイルがダウンロードされ、すぐに使用できるようになります。 詳細については、Azure File Sync のデプロイのドキュメントにある「[新規および変更されたファイルを Azure ファイル共有から事前に呼び戻す](../file-sync/file-sync-deployment-guide.md?tabs=azure-portal%252cproactive-portal#proactively-recall-new-and-changed-files-from-an-azure-file-share)」セクションを参照してください。

- クラウドを使った階層化の最終アクセス時間の追跡からアプリケーションを除外する。最後のアクセス時間の追跡からアプリケーションを除外できるようになりました。 アプリケーションからファイルへアクセスが行われると、ファイルの最終アクセス時刻がクラウドを使った階層化データベースで更新されます。 ファイル システムをスキャンするウイルス対策アプリケーションなどを使用すると、すべてのファイルの最終アクセス時刻が同じになるため、ファイルが階層化された時間に影響を及ぼします。

    最後のアクセス時刻の追跡からアプリケーションを除外するには、プロセス名を HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure\StorageSync の下にある HeatTrackingProcessNameExclusionList レジストリ設定に追加します。

    例: reg ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure\StorageSync" /v HeatTrackingProcessNameExclusionList /t REG_MULTI_SZ /d "SampleApp.exe\0AnotherApp.exe" /f

    > [!Note]  
    > データ重複除去と File Server Resource Manager (FSRM) のプロセスは既定で除外され (ハード コーディングされています)、プロセスの除外リストは 5 分ごとに更新されます。

- さまざまなパフォーマンスと信頼性の向上
    - Azure ファイル共有で変更されたファイルを検出するための変更検出のパフォーマンスが向上しました。
    - 同期アップロードのパフォーマンスが向上しました。
    - 初回アップロードが VSS スナップショットから実行されるようになりました。これにより、項目ごとのエラーと同期セッション エラーが減少します。
    - 特定の I/O パターンの同期信頼性が向上しました。
    - フェールオーバーが発生したときに、フェールオーバー クラスターで同期データベースが巻き戻るバグを修正しました。
    - 階層化されたファイルにアクセスするときの呼び戻しのパフォーマンスが向上しました。

### <a name="evaluation-tool"></a>評価ツール
Azure File Sync をデプロイする前に、Azure File Sync 評価ツールを使用して、お使いのシステムと互換性があるかどうかを評価する必要があります。 このツールは Azure PowerShell コマンドレットであり、サポートされていない文字やサポートされていない OS バージョンなど、ファイル システムとデータセットに関する潜在的な問題をチェックします。 インストールおよび使用手順については、計画ガイドの「[評価ツール](../file-sync/file-sync-planning.md#evaluation-cmdlet)」セクションを参照してください。 

### <a name="agent-installation-and-server-configuration"></a>エージェントのインストールとサーバー構成
Windows Server で Azure File Sync エージェントをインストールして構成する方法の詳細については、「[Planning for an Azure File Sync deployment (Azure File Sync のデプロイの計画)](../file-sync/file-sync-planning.md)」および [Azure File Sync をデプロイする方法](../file-sync/file-sync-deployment-guide.md)に関するページを参照してください。

- エージェント インストール パッケージは、引き上げられた (管理者) 特権でインストールする必要があります。
- Nano Server のデプロイ オプションでは、このエージェントはサポートされません。
- このエージェントがサポートされるのは、Windows Server 2019、Windows Server 2016 および Windows Server 2012 R2 のみです。
- エージェントには、少なくとも 2 GiB のメモリが必要です。 動的メモリを有効にした仮想マシンでサーバーが実行されている場合は、2048 MiB 以上のメモリで VM を構成する必要があります。 詳細については、「[推奨されるシステム リソース](../file-sync/file-sync-planning.md#recommended-system-resources)」を参照してください。
- Storage Sync Agent (FileSyncSvc) サービスは、システム ボリューム情報 (SVI) ディレクトリが圧縮されているボリュームに配置されたサーバーのエンドポイントをサポートしません。 この構成は、予期しない結果になります。

### <a name="interoperability"></a>相互運用性
- 階層化されたファイルにアクセスするウイルス対策やバックアップなどのアプリケーションは、オフライン属性を考慮してそれらのファイルのコンテンツの読み取りをスキップする場合を除き、望ましくない再呼び出しを行う可能性があります。 詳細については、「[Troubleshoot Azure File Sync (Azure File Sync のトラブルシューティング)](../file-sync/file-sync-troubleshoot.md)」を参照してください。
- ファイル スクリーンによってファイルがブロックされた場合、File Server Resource Manager (FSRM) ファイル スクリーンが頻繁に同期エラーを引き起こす可能性があります。
- Azure File Sync エージェントがインストールされているサーバー上での sysprep の実行はサポートされていません。予期しない結果になる可能性があります。 Azure File Sync エージェントは、サーバー イメージの展開と sysprep ミニ セットアップの完了後にインストールされます。

### <a name="sync-limitations"></a>同期の制限事項
次の項目は同期されませんが、システムの残りの部分は引き続き正常に動作します。
- サポートされていない文字を含むファイル。 サポートされていない文字の一覧については、[トラブルシューティング ガイド](../file-sync/file-sync-troubleshoot.md#handling-unsupported-characters)のページを参照してください。
- 末尾がピリオドのファイルまたはディレクトリ。
- 2,048 文字を超えるパス。
- 監査に使用されるセキュリティ記述子のシステム アクセス制御リスト (SACL) 部分。
- 拡張属性。
- 代替データ ストリーム。
- 再解析ポイント。
- ハード リンク。
- 圧縮がサーバー ファイルに設定されている場合、変更が他のエンドポイントからそのファイルに同期されるときに、圧縮は保持されません。
- サービスがデータを読み取ることを妨げる、EFS (またはその他のユーザー モードの暗号化) で暗号化されたファイル。

    > [!Note]  
    > 転送中のデータは、Azure File Sync によって常に暗号化されます。 データは常に暗号化されて Azure に保存されます。
 
### <a name="server-endpoint"></a>サーバー エンドポイント
- サーバー エンドポイントは、NTFS ボリューム上にのみ作成できます。 ReFS、FAT、FAT32 などのファイル システムは、現在 Azure File Sync でサポートされていません。
- システム ボリュームでは、クラウドの階層化はサポートされていません。 システム ボリュームにサーバー エンドポイントを作成するには、サーバー エンドポイントを作成するときにクラウドの階層化を無効にします。
- フェールオーバー クラスタリングは、クラスター化ディスクでのみサポートされ、クラスターの共有ボリューム (CSV) ではサポートされません。
- サーバー エンドポイントを入れ子にすることはできません。 同じボリューム上に、別のエンドポイントと並列に共存させることはできます。
- サーバー エンドポイントの場所内に OS またはアプリケーションのページング ファイルを格納しないでください。
- サーバーの名前を変更した場合、ポータル内のサーバー名は更新されません。

### <a name="cloud-endpoint"></a>クラウド エンドポイント
- Azure File Sync は、Azure ファイル共有に対する直接的な変更をサポートします。 ただし、Azure ファイル共有に対して行われた変更は、まず Azure File Sync の変更検出ジョブによって認識される必要があります。 クラウド エンドポイントに対する変更検出ジョブは、24 時間に 1 回起動されます。 Azure ファイル共有で変更されたファイルを直ちに同期したければ、[Invoke-AzStorageSyncChangeDetection](/powershell/module/az.storagesync/invoke-azstoragesyncchangedetection) PowerShell コマンドレットを使用すると、Azure ファイル共有における変更の検出を手動で開始できます。 さらに、REST プロトコルで Azure ファイル共有に対して行われた変更は、SMB の最終更新時刻を更新するものではなく、同期による変更とは見なされません。
- ストレージ同期サービスやストレージ アカウントは、別のリソース グループ、サブスクリプション、または Azure AD テナントに移動できます。 ストレージ同期サービスまたはストレージ アカウントを移動した後、Microsoft.StorageSync アプリケーションにストレージ アカウントへのアクセス権を付与する必要があります (「[Azure File Sync がストレージ アカウントへのアクセス権を持っていることを確認します](../file-sync/file-sync-troubleshoot.md?tabs=portal1%252cportal#troubleshoot-rbac)」を参照してください)。

    > [!Note]  
    > クラウド エンドポイントを作成するときは、ストレージ同期サービスとストレージ アカウントが同じ Azure AD テナントに存在する必要があります。 クラウド エンドポイントが作成された後、ストレージ同期サービスとストレージ アカウントを別の Azure AD テナントに移動できます。

### <a name="cloud-tiering"></a>クラウドの階層化
- 階層化されたファイルが Robocopy を使用して別の場所にコピーされた場合、その結果のファイルは階層化されません。 誤ってオフライン属性が Robocopy によるコピー操作の対象となり、オフライン属性が設定される場合があります。
- robocopy を使用してファイルをコピーする場合は、/MIR オプションを使用してファイルのタイムスタンプを保存します。 これにより、必ず最近アクセスされたファイルより先に、古いファイルが階層化されます。
    > [!Warning]  
    > Robocopy /B スイッチは Azure File Sync ではサポートされていません。転送元として Azure File Sync サーバー エンドポイントで Robocopy /B スイッチを使用すると、ファイルが破損する可能性があります。