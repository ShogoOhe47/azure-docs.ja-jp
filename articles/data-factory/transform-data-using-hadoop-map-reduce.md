---
title: Hadoop MapReduce アクティビティを使用してデータを変換する
description: Azure Data Factory または Synapse Analytics を使用して Azure HDInsight クラスター上の Hadoop MapReduce プログラムを実行してデータを処理する方法について説明します。
titleSuffix: Azure Data Factory & Azure Synapse
ms.service: data-factory
ms.subservice: tutorials
ms.topic: conceptual
author: nabhishek
ms.author: abnarain
ms.custom: synapse
ms.date: 09/09/2021
ms.openlocfilehash: 42e2b188f0fbc1c16b33f2cc44b7fe637dd6a8f9
ms.sourcegitcommit: 106f5c9fa5c6d3498dd1cfe63181a7ed4125ae6d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2021
ms.locfileid: "131005706"
---
# <a name="transform-data-using-hadoop-mapreduce-activity-in-azure-data-factory-or-synapse-analytics"></a>Azure Data Factory または Synapse Analytics で Hadoop MapReduce アクティビティを使用してデータを変換する

> [!div class="op_single_selector" title1="使用している Data Factory サービスのバージョンを選択してください:"]
> * [Version 1](v1/data-factory-map-reduce.md)
> * [現在のバージョン](transform-data-using-hadoop-map-reduce.md)

[!INCLUDE[appliesto-adf-asa-md](includes/appliesto-adf-asa-md.md)]

Azure Data Factory または Synapse Analytics [パイプライン](concepts-pipelines-activities.md)の HDInsight MapReduce アクティビティは、[独自の](compute-linked-services.md#azure-hdinsight-linked-service)または[オンデマンドの](compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight クラスターで MapReduce プログラムを起動します。 この記事は、データ変換とサポートされる変換アクティビティの概要を説明する、 [データ変換アクティビティ](transform-data.md) に関する記事に基づいています。

詳細については、この記事を読む前に、[Azure Data Factory](introduction.md) と [Synapse Analytics](../synapse-analytics/overview-what-is.md) の概要に関する記事を参照し、[データ変換のチュートリアル](tutorial-transform-data-spark-powershell.md)を実行してください。

HDInsight Pig と Hive アクティビティを使用してパイプラインから HDInsight クラスター上の Pig/Hive スクリプトを実行する方法の詳細については、[Pig](transform-data-using-hadoop-pig.md) と [Hive](transform-data-using-hadoop-hive.md) に関する記事をご覧ください。

## <a name="syntax"></a>構文

```json
{
    "name": "Map Reduce Activity",
    "description": "Description",
    "type": "HDInsightMapReduce",
    "linkedServiceName": {
        "referenceName": "MyHDInsightLinkedService",
        "type": "LinkedServiceReference"
    },
    "typeProperties": {
        "className": "org.myorg.SampleClass",
        "jarLinkedService": {
            "referenceName": "MyAzureStorageLinkedService",
            "type": "LinkedServiceReference"
        },
        "jarFilePath": "MyAzureStorage/jars/sample.jar",
        "getDebugInfo": "Failure",
        "arguments": [
            "-SampleHadoopJobArgument1"
        ],
        "defines": {
            "param1": "param1Value"
        }
    }
}
```

## <a name="syntax-details"></a>構文の詳細

| プロパティ          | 説明                              | 必須 |
| ----------------- | ---------------------------------------- | -------- |
| name              | アクティビティの名前                     | はい      |
| description       | アクティビティの用途を説明するテキストです。 | いいえ       |
| type              | MapReduce アクティビティの場合、アクティビティの種類は HDinsightMapReduce です | はい      |
| linkedServiceName | リンクされたサービスとして登録されている HDInsight クラスターへの参照。 このリンクされたサービスの詳細については、[計算のリンクされたサービス](compute-linked-services.md)に関する記事をご覧ください。 | はい      |
| className         | 実行するクラスの名前         | はい      |
| jarLinkedService  | Jar ファイルの格納に使用される Azure Storage のリンクされたサービスへの参照。 ここでは **[Azure Blob Storage](./connector-azure-blob-storage.md)** および **[ADLS Gen2](./connector-azure-data-lake-storage.md)** にリンクされたサービスのみがサポートされています。 このリンクされたサービスを指定していない場合は、HDInsight のリンクされたサービスで定義されている Azure Storage のリンクされたサービスが使用されます。 | いいえ       |
| jarFilePath       | jarLinkedServiceで参照される Azure Storage に格納されている Jar ファイルへのパスを指定します。 ファイル名は大文字と小文字が区別されます。 | はい      |
| jarlibs           | jarLinkedServiceで定義される Azure Storage に格納されているジョブで参照される Jar ライブラリ ファイルへのパスの文字列配列。 ファイル名は大文字と小文字が区別されます。 | いいえ       |
| getDebugInfo      | HDInsight クラスターで使用されている Azure Storage または jarLinkedService で指定された Azure Storage にログ ファイルがコピーされるタイミングを指定します。 使用できる値は以下の通りです。None、Always、または Failure。 既定値:[なし] : | いいえ       |
| 引数         | Hadoop ジョブの引数の配列を指定します。 引数はコマンド ライン引数として各タスクに渡されます。 | いいえ       |
| defines           | Hive スクリプト内で参照するキーと値のペアとしてパラメーターを指定します。 | いいえ       |



## <a name="example"></a>例
HDInsight MapReduce アクティビティを使用して、HDInsight クラスター上で MapReduce jar ファイルを実行できます。 次のサンプルのパイプラインの JSON 定義では、Mahout JAR ファイルを実行するために HDInsight アクティビティが構成されます。

```json
{
    "name": "MapReduce Activity for Mahout",
    "description": "Custom MapReduce to generate Mahout result",
    "type": "HDInsightMapReduce",
    "linkedServiceName": {
        "referenceName": "MyHDInsightLinkedService",
        "type&quot;: &quot;LinkedServiceReference"
    },
    "typeProperties": {
        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
        "jarLinkedService": {
            "referenceName": "MyStorageLinkedService",
            "type&quot;: &quot;LinkedServiceReference"
        },
        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
        "arguments": [
            "-s",
            "SIMILARITY_LOGLIKELIHOOD",
            "--input",
            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input",
            "--output",
            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/",
            "--maxSimilaritiesPerItem",
            "500",
            "--tempDir",
            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"
        ]
    }
}
```
**arguments** セクションで MapReduce プログラムに任意の引数を指定できます。 実行時に、MapReduce フレームワークのいくつかの引数 (mapreduce.job.tags など) が表示されます。 MapReduce の引数と区別するために、次の例のように、オプションと値の両方を引数として使用することを検討してください (-s、--input、--output などがオプションであり、直後に値が続きます)。

## <a name="next-steps"></a>次のステップ
別の手段でデータを変換する方法を説明している次の記事を参照してください。

* [U-SQL アクティビティ](transform-data-using-data-lake-analytics.md)
* [Hive アクティビティ](transform-data-using-hadoop-hive.md)
* [Pig アクティビティ](transform-data-using-hadoop-pig.md)
* [Hadoop Streaming アクティビティ](transform-data-using-hadoop-streaming.md)
* [Spark アクティビティ](transform-data-using-spark.md)
* [.NET カスタム アクティビティ](transform-data-using-dotnet-custom-activity.md)
* [ストアド プロシージャ アクティビティ](transform-data-using-stored-procedure.md)
