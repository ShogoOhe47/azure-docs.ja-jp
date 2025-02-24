---
title: 空の Lake データベースを作成する
description: 簡単に追加できる空の Lake データベースを Azure Synapse Analytics で作成する方法について学習します。
author: aamerril
ms.author: aamerril
ms.service: synapse-analytics
ms.subservice: database-editor
ms.topic: how-to
ms.date: 11/02/2021
ms.custom: template-how-to, ignite-fall-2021
ms.openlocfilehash: 2cff956fa8507ec1dcbf8e3ab3576d19ecebf526
ms.sourcegitcommit: 61f87d27e05547f3c22044c6aa42be8f23673256
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2021
ms.locfileid: "132060814"
---
# <a name="how-to-create-an-empty-lake-database"></a>方法: 空の Lake データベースを作成する

この記事では、データベース デザイナーを使用して、簡単に追加できる空の [Lake データベース](./concepts-lake-database.md)を Azure Synapse Analytics で作成する方法について学習します。 データベース デザイナーを使用すると、コードを記述することなく、データベースを簡単に作成してデプロイできます。 

## <a name="prerequisites"></a>前提条件

- ギャラリーから Lake データベース テンプレートを探索するには、少なくとも Synapse ユーザー ロールのアクセス許可が必要です。
- Synapse ワークスペースで Lake データベースを作成するには、Synapse 管理者、Synapse 共同作成者、または Synapse 成果物パブリッシャーのアクセス許可が必要です。
- データ レイクでは、ストレージ BLOB データ共同作成者のアクセス許可が必要です。

## <a name="create-lake-database-from-database-template"></a>データベース テンプレートから Lake データベースを作成する
1. Azure Synapse Analytics ワークスペースの **[ホーム]** タブから、左側の **[データ]** タブを選択します。 **[データ]** タブが開き、ワークスペースに既に存在するデータベースの一覧が表示されます。
2. **+** ボタンにマウス ポインターを移動し、 **[Lake データベース (プレビュー)]** を選択します。
![空の Lake データベースの作成を示すスクリーンショット](./media/create-empty-lake-database/create-empty-lakedb.png)
3. [データベース デザイナー] タブが開き、空のデータベースが表示されます。
4. データベース デザイナーの右側には、構成する必要がある **[プロパティ]** が表示されます。
    - **名前** - データベース名を指定します。 データベースのパブリッシュ後に名前を編集することはできないため、選択した名前が正しいか確認してください。
    - **説明** - データベースの説明は省略可能ですが、説明を入力すれば、ユーザーがデータベースの目的を理解しやすくなります。
    - **データベースのストレージの設定** - このセクションには、データベースのテーブルの既定のストレージ情報が表示されます。 この既定値は、テーブル自体でオーバーライドされない限り、データベースの各テーブルに適用されます。
    - **リンクされたサービス** - Azure Data Lake Storage にデータを格納するために使用されるリンクされた既定のサービスです。  Synapse ワークスペースに関連付けられているリンクされた既定のサービスが表示されますが、**リンクされたサービス** を任意の ADLS ストレージ アカウントに変更できます。 
    - **入力フォルダー** - ファイル ブラウザーを使用して、リンクされたサービス内の既定のコンテナーとフォルダー パスを設定するために使用されます。
    - **データ形式** - Azure Synapse データの Lake データベースでは、データのストレージ形式として Parquet および区切りテキストをサポートしています。

> [!NOTE]
> テーブルの既定のストレージ設定はテーブル単位でいつでもオーバーライドできます。既定の設定はいつでもカスタマイズできます。 何を選択する必要があるかわからない場合は、後で再確認できます。
 
5. データベースにテーブルを追加するには、 **[+ テーブル]** ボタンを選択します。 
    - **[カスタム]** を選択すると、キャンバスに新しいテーブルが追加されます。
    - **[テンプレートから]** を選択すると、ギャラリーが開き、新しいテーブルを追加するときに使用するデータベース テンプレートを選択できます。 詳細については、[データベース テンプレートからの Lake データベースの作成](./create-lake-database-from-lake-database-templates.md)に関するページを参照してください。
    - **[データ レイクから]** を選択すると、レイクに既に存在するデータを使用してテーブル スキーマをインポートできます。
6. **[カスタム]** を選択します。 "Table_1" という名前の新しいテーブルがキャンバスに表示されます。
7. 次に、テーブル名、説明、ストレージ設定、列、リレーションシップなど、Table_1 をカスタマイズできます。 詳細については、[Lake データベースの変更](./modify-lake-database.md)に関するページを参照してください。
8. **[+ テーブル]** 、 **[データ レイクから]** の順に選択して、データ レイクから新しいテーブルを追加します。
9. **[Data Lake から外部テーブルを作成する]** ペインが表示されます。 ペインに以下の詳細を入力し、 **[続行]** を 選択します。
    - **外部テーブル** - 作成するテーブルに付ける名前を指定します。
    - **リンクされたサービス** - Azure Data Lake Storage の場所が含まれ、データ ファイルが存在するリンクされたサービス。
    - **入力ファイルまたはフォルダーは** - ファイル ブラウザーを使用して、使用するテーブルを作成するレイク上のファイルに移動して選択します。
![[データ レイク] ペインからの外部テーブルの作成に関するオプションを示すスクリーンショット](./media/create-empty-lake-database/create-from-lake.png)
    - 次の画面では、Azure Synapse でファイルをプレビューし、スキーマを検出します。
    - **[新しい外部テーブル]** ページに移動します。ここでは、データ形式に関連する設定を更新し、**データのプレビュー** を実行して、Synapse がファイルを正しく識別しているかどうかを確認します。
    - 設定に問題がなければ、 **[作成]** を選択します。
    - 選択した名前の新しいテーブルがキャンバスに追加され、 **[テーブルのストレージ設定]** セクションに、指定したファイルが表示されます。
    
10. データベースがカスタマイズされたので、次にパブリッシュします。 Synapse ワークスペースとの Git 統合を使用している場合は、変更をコミットし、コラボレーション ブランチに統合する必要があります。 [Azure Synapse でのソース管理の詳細](././cicd/../../cicd/source-control.md)。 Synapse Live モードを使用している場合は、[パブリッシュ] を選択できます。
    - データベースをパブリッシュする前に、エラーが検証されます。 エラーが見つかると、[通知] タブに表示されます。このタブには、エラーを解決する方法が表示されます。
    
       ![データベースの検証エラーを示す [検証] ペインのスクリーンショット](./media/create-empty-lake-database/validation-error.png)
    - パブリッシュすると、データベース スキーマが Azure Synapse メタストアに作成されます。 パブリッシュ後、データベースおよびテーブル オブジェクトが他の Azure サービスに表示され、データベースのメタデータを Power BI や Purview などのアプリにフローできます。

11. これで、空の Lake データベースが Azure Synapse に作成され、 **[カスタム]** オプションと **[データ レイクから]** オプションを使用してテーブルが追加されました。

## <a name="next-steps"></a>次のステップ

次のリンクを使用して、データベース デザイナーの機能の詳細を引き続き確認します。 
- [lake データベースを変更する](./modify-lake-database.md)
- [Lake データベースの詳細](./concepts-lake-database.md)
- [データベース テンプレートから Lake データベースを作成する](./create-lake-database-from-lake-database-templates.md)
