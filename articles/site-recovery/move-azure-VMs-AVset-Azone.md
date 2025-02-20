---
title: Azure Site Recovery を使用して可用性ゾーンがある Azure リージョンに VM を移動する
description: Site Recovery を使用して VM を別のリージョンの可用性ゾーンに移動する方法について説明します
services: site-recovery
author: sideeksh
ms.service: site-recovery
ms.topic: tutorial
ms.date: 01/28/2019
ms.author: sideeksh
ms.custom: MVC
ms.openlocfilehash: 52b467401cfffeef4908750caea9c6d3ee88eb1b
ms.sourcegitcommit: 106f5c9fa5c6d3498dd1cfe63181a7ed4125ae6d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2021
ms.locfileid: "131075032"
---
# <a name="move-azure-vms-into-availability-zones"></a>Azure VM を Availability Zones に移動する

この記事では、Azure VM を別のリージョンの可用性ゾーンに移動する方法について説明します。 同じリージョン内の別のゾーンに移動する場合は、[こちらの記事をご確認ください](./azure-to-azure-how-to-enable-zone-to-zone-disaster-recovery.md)。


Azure の Availability Zones は、アプリケーションとデータをデータセンターの障害から保護するのに役立ちます。 それぞれの可用性ゾーンは、独立した電源、冷却手段、ネットワークを備えた 1 つまたは複数のデータセンターで構成されています。 回復性を確保するため、有効になっているリージョンにはいずれも最低 3 つのゾーンが別個に存在しています。 Availability Zones はリージョン内で物理的に分離されているため、データセンターで障害が発生してもアプリケーションとデータは保護されます。 Availability Zones により、Azure では仮想マシン (VM) の 99.99% のアップタイムというサービス レベル アグリーメント (SLA) が提供されます。 [Availability Zones がサポートされるリージョン](../availability-zones/az-region.md)に関するページで説明されているように、Availability Zones は一部のリージョンでサポートされています。

VM を "*単一インスタンス*" として特定のリージョンにデプロイしてあり、それらの VM を可用性ゾーンに移動することで可用性を強化したい場合、その手段として Azure Site Recovery を使用することができます。 この操作は、さらに次のように分類できます。

- 単一インスタンスの VM をターゲット リージョン内の Availability Zones に移動する
- 可用性セット内の VM をターゲット リージョン内の Availability Zones に移動する

> [!IMPORTANT]
> Azure VM を別のリージョンの可用性ゾーンに移動する場合、[Azure Resource Mover](../resource-mover/move-region-availability-zone.md) を使用することをお勧めします。 Resource Mover は、現在、パブリック プレビュー段階にあり、以下を実現します。
> - 単一のハブを使用してリージョン間でリソースを移動できます。
> - 移動時間と複雑さを軽減できます。 必要なものをすべて 1 か所にまとめることができます。
> - シンプルかつ一貫性のあるエクスペリエンスによって、さまざまな種類の Azure リソースを移動できます。
> - 移動するリソース間の依存関係を簡単に識別できます。 これにより、関連リソースをまとめて移動することができるため、移動後にすべてのリソースがターゲット リージョンで期待どおりに動作します。
> - 移動後にソース リージョンのリソースを削除する場合は、自動的にクリーンアップされます。
> - テスト。 移動を試してみて、完全に移動することは望まない場合は破棄することができます。



## <a name="check-prerequisites"></a>前提条件を確認する

- ターゲット リージョンで [Availability Zones がサポートされている](../availability-zones/az-region.md)ことを確認します。 選択した[ソース リージョン/ターゲット リージョンの組み合わせがサポートされている](./azure-to-azure-support-matrix.md#region-support)ことを確認します。 ターゲット リージョンの情報に基づいて判断します。
- [シナリオのアーキテクチャとコンポーネント](azure-to-azure-architecture.md)を理解している。
- [サポートの制限と要件](azure-to-azure-support-matrix.md)を確認する。
- アカウントのアクセス許可を確認します。 無料の Azure アカウントを作成したばかりであれば、自分のサブスクリプションの管理者になっています。 サブスクリプションの管理者でなければ、管理者に協力をあおぎ、必要なアクセス許可を割り当てます。 VM のレプリケーションを有効にし、最終的に Azure Site Recovery を使用してデータをターゲットにコピーするには、次の要件を満たす必要があります。

    1. VM を Azure リソースに作成するアクセス許可。 "*仮想マシン共同作成者*" 組み込みロールには次のアクセス許可が与えられています。
        - 選択したリソース グループ内に VM を作成するためのアクセス許可
        - 選択した仮想ネットワーク内に VM を作成するためのアクセス許可
        - 選択したストレージ アカウントに書き込むためのアクセス許可

    2. Azure Site Recovery のタスクを管理するためのアクセス許可。 "*Site Recovery 共同作成者*" ロールには、Recovery Services コンテナーでの Site Recovery の操作の管理に必要なすべてのアクセス許可があります。

## <a name="prepare-the-source-vms"></a>ソース VM を準備する

1. Site Recovery を使用して可用性ゾーンに VM を移動する場合、その VM でマネージド ディスクが使用されている必要があります。 アンマネージド ディスクを使用する既存の Windows VM を、マネージド ディスクを使用するように変換できます。 「[Windows 仮想マシンを非管理対象ディスクからマネージド ディスクに変換する](../virtual-machines/windows/convert-unmanaged-to-managed-disks.md)」の手順に従ってください。 可用性セットは必ず "*マネージド*" として構成してください。
2. 移動する Azure VM に、最新のルート証明書がすべて存在することを確認します。 最新のルート証明書が存在しない場合、セキュリティ上の制約により、ターゲット リージョンへのデータ コピーを有効にすることができません。

3. Windows VM については、最新のすべての Windows 更新プログラムを VM にインストールして、すべての信頼されたルート証明書をマシンに用意します。 接続されていない環境の場合は、組織の標準の Windows Update プロセスおよび証明書更新プロセスに従ってください。

4. Linux VM の場合は、Linux ディストリビューターから提供されるガイダンスに従って、VM で最新の信頼されたルート証明書と証明書失効リストを取得します。
5. 移動しようとする VM のネットワーク接続を制御するために認証プロキシを使用していないことを確認します。

6. [VM の発信接続要件](azure-to-azure-tutorial-enable-replication.md#set-up-vm-connectivity)を確認します。

7. ソース ネットワーク レイアウトと確認のために現在使用しているリソースを特定します (ロード バランサー、NSG、パブリック IP など)。

## <a name="prepare-the-target-region"></a>ターゲット リージョンを準備する

1. Azure サブスクリプションによって、ディザスター リカバリーに使用されるターゲット リージョンに VM を作成できることを確認します。 必要に応じて、サポートに連絡し、必要なクォータを有効にしてください。

2. サブスクリプションに、ソース VM と一致するサイズの VM をサポートするための十分なリソースがあることを確認します。 Site Recovery を使用してターゲットにデータをコピーする場合、ターゲット VM には、同じサイズ (または可能な限り近いサイズ) が選択されます。

3. ソース ネットワーク レイアウトから特定されたすべてのコンポーネントについてターゲット リソースを作成します。 この操作により、ターゲット リージョンへの切り替え後、ソースにあったすべての機能を VM に確保します。

    > [!NOTE]
    > ソース VM のレプリケーションを有効にすると、Azure Site Recovery によって仮想ネットワークとストレージ アカウントが自動的に検出されて作成されます。 レプリケーションを有効にする手順の一環として、このようなリソースを事前に作成して VM に割り当てることもできます。 ただし後述のように、その他のリソースについては、ターゲット リージョンに手動で作成する必要があります。

     最も一般的に使用されるネットワーク リソースについては、次のドキュメントを参照して、実際の環境に適したものをソース VM の構成に基づいて作成してください。

    - [ネットワーク セキュリティ グループ](../virtual-network/manage-network-security-group.md)
    - [ロード バランサー](../load-balancer/index.yml)
    - [パブリック IP](../virtual-network/ip-services/virtual-network-public-ip-address.md)
    
   その他のネットワーク コンポーネントについては、ネットワークに関する[ドキュメント](../index.yml?pivot=products&panel=network)を参照してください。

    > [!IMPORTANT]
    > ターゲットでは、ゾーン冗長ロード バランサーを使用する必要があります。 詳しくは、「[Standard Load Balancer と可用性ゾーン](../load-balancer/load-balancer-standard-availability-zones.md)」をご覧ください。

4. ターゲット リージョンに切り替える前に構成をテストしたい場合は、ターゲット リージョンに手動で[非運用ネットワークを作成](../virtual-network/quick-create-portal.md)します。 運用環境への影響が最小限で済むため、このアプローチをお勧めします。

## <a name="enable-replication"></a>レプリケーションを有効にする
以下の手順では、最終的にデータを Availability Zones に移動する前に、Azure Site Recovery を使用して、ターゲット リージョンへのデータのレプリケーションを有効にする方法を説明しています。

> [!NOTE]
> これらの手順は単一の VM 用です。 同じ手順を複数の VM に拡張できます。 Recovery Services コンテナーに移動して、 **[+ レプリケート]** を選択し、一緒に関連する VM を選択します。

1. Azure portal で **[仮想マシン]** を選択して、Availability Zones に移動する VM を選択します。
2. **[操作]** で、 **[ディザスター リカバリー]** を選択します。
3. **[ディザスター リカバリーの構成]**  >  **[ターゲット リージョン]** で、レプリケート先のターゲット リージョンを選択します。 このリージョンで Availability Zones が[サポートされている](../availability-zones/az-region.md)ことを確認します。
4. **詳細設定** を選択します。
5. ターゲット サブスクリプション、ターゲット VM リソース グループ、仮想ネットワークに適切な値を選択します。
6. **[可用性]** セクションで、VM の移動先となる可用性ゾーンを選択します。 
   > [!NOTE]
   > 可用性セットまたは可用性ゾーンのオプションが表示されない場合は、[前提条件](#prepare-the-source-vms)が満たされていること、またソース VM の[準備](#prepare-the-source-vms)が完了していることを確認します。
  

7. **[レプリケーションを有効にする]** を選択します。 これにより VM レプリケーションを有効にするジョブが開始されます。

## <a name="check-settings"></a>設定を確認する

レプリケーション ジョブの完了後、レプリケーションの状態を確認し、レプリケーションの設定を変更して、デプロイをテストできます。

1. VM のメニューで、 **[ディザスター リカバリー]** を選択します。
2. レプリケーションの正常性、作成された復旧ポイント、およびマップ上のソース リージョンとターゲット リージョンを確認できます。


## <a name="test-the-configuration"></a>構成をテストする

1. 仮想マシンのメニューで **[ディザスター リカバリー]** を選択します。
2. **[テスト フェールオーバー]** アイコンを選択します。
3. **[テスト フェールオーバー]** で、フェールオーバーに使用する復旧ポイントを選択します。

   - **最後に処理があった時点**:Site Recovery サービスによって処理された最新の復旧ポイントに VM をフェールオーバーします。 タイム スタンプが表示されます。 このオプションを使用すると、データの処理に時間がかからないため、目標復旧時間 (RTO) が低くなります。
   - **最新のアプリ整合性**:このオプションでは、すべての VM が最新のアプリ整合性の復旧ポイントにフェールオーバーされます。 タイム スタンプが表示されます。
   - **Custom**:任意の復旧ポイントを選択します。

3. Azure VM の移動先となるテスト用のターゲット Azure 仮想ネットワークを選択し、構成をテストします。 

    > [!IMPORTANT]
    > テスト フェールオーバーには、VM の移動先となるターゲット リージョンの運用環境のネットワークではなく、別個の Azure VM ネットワークを使用することをお勧めします。

4. 移動テストを開始するには、 **[OK]** を選択します。 進行状況を追跡するには、VM を選択して、そのプロパティを開きます。 または、コンテナー名の **[設定]**  >  **[ジョブ]**  >  **[Site Recovery ジョブ]** で、**テスト フェールオーバー** ジョブを選択することもできます。
5. フェールオーバーの完了後、レプリカの Azure VM は、Azure Portal の **[仮想マシン]** に表示されます。 VM が実行中で、適切なサイズであること、また、適切なネットワークに接続されていることを確認してください。
6. 移動テストの過程で作成した VM を削除する場合は、[レプリケートされたアイテム] の **[テスト フェールオーバーのクリーンアップ]** を選択します。 **[メモ]** を使用して、テストに関連する観察結果をすべて記録し、保存します。

## <a name="move-to-the-target-region-and-confirm"></a>ターゲット リージョンに移動して確認する

1.  仮想マシンのメニューで **[ディザスター リカバリー]** を選択します。
2. **[フェールオーバー]** アイコンを選択します。
3. **[フェールオーバー]** で **[最新]** を選択します。 
4. **[フェールオーバーを開始する前にマシンをシャットダウンします]** を選択します。 Site Recovery は、フェールオーバーを開始する前にソース VM をシャットダウンしようとします。 仮にシャットダウンが失敗したとしても、フェールオーバーは続行されます。 フェールオーバーの進行状況は **[ジョブ]** ページで確認できます。 
5. ジョブが完了したら、ターゲット Azure リージョンに VM が正しく表示されることを確認します。
6. **[レプリケートされたアイテム]** で [VM] > **[コミット]** を右クリックします。 これでターゲット リージョンへの移動プロセスは完了です。 コミット ジョブが完了するまで待ちます。

## <a name="discard-the-resource-in-the-source-region"></a>ソース リージョンのリソースを破棄する

VM に移動します。 **[レプリケーションの無効化]** を選択します。 これで VM のデータをコピーするプロセスが停止します。  

> [!IMPORTANT]
> 移動後に Site Recovery レプリケーションの請求を避けるため、前記の手順を行います。 ソース レプリケーションの設定は自動的にクリーンアップされます。 レプリケーションの一部としてインストールされた Site Recovery 拡張機能は削除されないため、手動で削除する必要がある点に注意してください。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、Azure VM を可用性セットまたは可用性ゾーンに移動することによってその可用性を強化しました。 次には、移動した VM のディザスター リカバリーを設定できます。

> [!div class="nextstepaction"]
> [移行後のディザスター リカバリーのセットアップ](azure-to-azure-quickstart.md)