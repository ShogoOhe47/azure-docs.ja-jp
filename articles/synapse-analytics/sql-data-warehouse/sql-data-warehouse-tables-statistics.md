---
title: テーブルの列の統計を作成および更新する
description: 専用 SQL プール内のテーブルに関するクエリ用に最適化された統計の作成と更新のレコメンデーションと例。
services: synapse-analytics
author: XiaoyuMSFT
manager: craigg
ms.service: synapse-analytics
ms.topic: conceptual
ms.subservice: sql-dw
ms.date: 05/09/2018
ms.author: xiaoyul
ms.reviewer: igorstan
ms.custom: seo-lt-2019, azure-synapse
ms.openlocfilehash: fe1003e78aac6085d415378d0069f2f6181b354f
ms.sourcegitcommit: 91fdedcb190c0753180be8dc7db4b1d6da9854a1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112298351"
---
# <a name="table-statistics-for-dedicated-sql-pool-in-azure-synapse-analytics"></a>Azure Synapse Analytics の専用 SQL プールのテーブルの統計

この記事では、専用 SQL プール内のテーブルに関するクエリ用に最適化された統計の作成と更新のレコメンデーションと例を示します。

## <a name="why-use-statistics"></a>統計を使用する理由

専用 SQL プールがデータに関する情報を多く持っているほど、それに対するクエリを高速に実行できます。 専用 SQL プールにデータを読み込んだ後、データに関する統計を収集することは、クエリの最適化のために実行できる最も重要なことの 1 つです。

専用 SQL プール クエリ オプティマイザーは、コストベースのオプティマイザーです。 オプティマイザーでは、さまざまなクエリ プランのコストが比較されて、最も低コストのプランが選択されます。 多くの場合、それは最も高速に実行されるプランが選択されます。

たとえば、クエリでフィルター処理されている日付に対して返されるのは 1 行であるとオプティマイザーで推定されると、1 つのプランが選択されます。 選択された日付で返されるのが 100 万行であると推定された場合は、別のプランが返されます。

## <a name="automatic-creation-of-statistic"></a>統計の自動作成

データベースの AUTO_CREATE_STATISTICS オプションがオンの場合、専用 SQL プールでは足りない統計に対して受信ユーザー クエリが分析されます。

統計が足りない場合、クエリ オプティマイザーでは、クエリ述語または結合条件内の個々の列で統計を作成することで、クエリ プランに対するカーディナリティ評価が改善されます。

> [!NOTE]
> 既定では､統計の自動作成は有効です｡

専用 SQL プールで AUTO_CREATE_STATISTICS が構成されているかどうかは、次のコマンドを実行することで確認できます。

```sql
SELECT name, is_auto_create_stats_on
FROM sys.databases
```

専用 SQL プールで AUTO_CREATE_STATISTICS が構成されていない場合は、次のコマンドを実行してこのプロパティを有効にすることをお勧めします。

```sql
ALTER DATABASE <yourdatawarehousename>
SET AUTO_CREATE_STATISTICS ON
```

結合が含まれること、または述語が存在することが検出されると、次のステートメントによって統計の自動作成がトリガーされます。

- SELECT
- INSERT-SELECT
- CTAS
- UPDATE
- DELETE
- EXPLAIN

> [!NOTE]
> 一時テーブルや外部テーブルに対して自動作成の統計が作成にされることはありません｡

統計の自動作成は同期的に行われるため、列に統計がない場合、クエリのパフォーマンスが多少低下することがあります。 1 つの列の統計を作成する時間は、テーブルのサイズに依存します。

明らかなパフォーマンスの低下を回避するには、システムをプロファイルする前にベンチマーク用ワークロードを実行することによって、統計を先に作成しておく必要があります。

> [!NOTE]
> 統計の作成は、各ユーザー コンテキスト内の [sys.dm_pdw_exec_requests](/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) にログ記録されます。

自動統計が作成されると､_WA_Sys_<16 進 8 桁の列 ID>_<16 進 8 桁のテーブル ID> の形式でログ記録されます。 作成済みの統計は、[DBCC SHOW_STATISTICS](/sql/t-sql/database-console-commands/dbcc-show-statistics-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) コマンドを実行して表示できます。

```sql
DBCC SHOW_STATISTICS (<table_name>, <target>)
```

table_name は、表示する統計が格納されているテーブルの名前です。 このテーブルに外部テーブルを指定することはできません。 target は、統計情報を表示するターゲットのインデックス、統計、または列の名前です。

## <a name="update-statistics"></a>統計を更新します。

ベスト プラクティスの 1 つが、新しい日付が追加されるたびに日付列の統計を更新することです。 新しい行が専用 SQL プールに読み込まれるたびに、新しい読み込みの日付またはトランザクションの日付が追加されます。 これらの追加によってデータの分布が変わり、統計が古くなります。

顧客テーブルの国または地域の列の統計は更新する必要がないと考えられます。一般的に値の分布は変わらないためです。 顧客間で分布が一定であると仮定すると、テーブル バリエーションに新しい行を追加しても、データの分布が変わることはありません。

ただし、専用 SQL プールに 1 つの国または地域しか含まれておらず、新しい国または地域のデータを取り込んで複数の国または地域のデータが格納されるようになった場合は、国または地域の列の統計を更新する必要があります。

統計更新のレコメンデーションは次の通りです｡

| 統計属性 | 推奨|
|-|-|
| **統計の更新の頻度**  | 控えめ: 毎日 </br> データを読み込むか変換した後 |
| **サンプリング** |  行数が 10 億未満の場合は、既定のサンプリング (20%) が使用されます。 </br> 10 億行を超えると、2% のサンプリングが使用されます。 |

クエリのトラブルシューティングを行うときに最初に尋ねる質問の 1 つが、「**統計は最新の状態ですか**」というものです。

この質問は、データの経過時間で答えられるものではありません。 基になるデータに重要な変更がない場合は、最新の統計オブジェクトが古い可能性があります。 行数が大幅に変わった場合や、列の値の分布で重大な変更があった場合は、"*その後で*" 統計を更新する必要があります。 

前回の統計が更新されてからテーブル内のデータが変更されたかどうかを判断するための動的管理ビューはありません。  次の 2 つのクエリは、統計が古くなっているかどうかを判断するのに役立ちます。

**クエリ 1:** 統計による行数 (**stats_row_count**) と実際の行数 (**actual_row_count**) の違いを確認します。 

```sql
select 
objIdsWithStats.[object_id], 
actualRowCounts.[schema], 
actualRowCounts.logical_table_name, 
statsRowCounts.stats_row_count, 
actualRowCounts.actual_row_count,
row_count_difference = CASE
    WHEN actualRowCounts.actual_row_count >= statsRowCounts.stats_row_count THEN actualRowCounts.actual_row_count - statsRowCounts.stats_row_count
    ELSE statsRowCounts.stats_row_count - actualRowCounts.actual_row_count
END,
percent_deviation_from_actual = CASE
    WHEN actualRowCounts.actual_row_count = 0 THEN statsRowCounts.stats_row_count
    WHEN statsRowCounts.stats_row_count = 0 THEN actualRowCounts.actual_row_count
    WHEN actualRowCounts.actual_row_count >= statsRowCounts.stats_row_count THEN CONVERT(NUMERIC(18, 0), CONVERT(NUMERIC(18, 2), (actualRowCounts.actual_row_count - statsRowCounts.stats_row_count)) / CONVERT(NUMERIC(18, 2), actualRowCounts.actual_row_count) * 100)
    ELSE CONVERT(NUMERIC(18, 0), CONVERT(NUMERIC(18, 2), (statsRowCounts.stats_row_count - actualRowCounts.actual_row_count)) / CONVERT(NUMERIC(18, 2), actualRowCounts.actual_row_count) * 100)
END
from
(
    select distinct object_id from sys.stats where stats_id > 1
) objIdsWithStats
left join
(
    select object_id, sum(rows) as stats_row_count from sys.partitions group by object_id
) statsRowCounts
on objIdsWithStats.object_id = statsRowCounts.object_id 
left join
(
    SELECT sm.name [schema] ,
        tb.name logical_table_name ,
        tb.object_id object_id ,
        SUM(rg.row_count) actual_row_count
    FROM sys.schemas sm
         INNER JOIN sys.tables tb ON sm.schema_id = tb.schema_id
         INNER JOIN sys.pdw_table_mappings mp ON tb.object_id = mp.object_id
         INNER JOIN sys.pdw_nodes_tables nt ON nt.name = mp.physical_name
         INNER JOIN sys.dm_pdw_nodes_db_partition_stats rg  ON rg.object_id = nt.object_id
            AND rg.pdw_node_id = nt.pdw_node_id
            AND rg.distribution_id = nt.distribution_id
    WHERE rg.index_id = 1
    GROUP BY sm.name, tb.name, tb.object_id
) actualRowCounts
on objIdsWithStats.object_id = actualRowCounts.object_id

```

**クエリ 2:** 各テーブルで統計が最後に更新された日時を調べて、統計の経過期間を確認します。 

> [!NOTE]
> 列の値の分布に重要な変更がある場合は、最後に更新された時刻に関係なく統計を更新する必要があります。

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

たとえば、専用 SQL プールの **日付列** では、通常、統計を頻繁に更新する必要があります。 新しい行が専用 SQL プールに読み込まれるたびに、新しい読み込みの日付またはトランザクションの日付が追加されます。 これらの追加によってデータの分布が変わり、統計が古くなります。

一方、顧客テーブルの性別列の統計は更新する必要がないと考えられます。 顧客間で分布が一定であると仮定すると、テーブル バリエーションに新しい行を追加しても、データの分布が変わることはありません。

専用 SQL プールに 1 つの性別しか含まれておらず、新しい要件によって複数の性別が含まれるようになった場合は、性別列の統計を更新する必要があります。

詳しくは、「[統計](/sql/relational-databases/statistics/statistics?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true)」をご覧ください。

## <a name="implementing-statistics-management"></a>統計管理の実装

多くの場合、読み込みの終わりに統計が確実に更新されるように、データ読み込みプロセスを拡張し、同時実行クエリ間のブロックやリソースの競合を回避または最小化することが推奨されます。  

テーブルのサイズや値の分布が変わる頻度が最も高いのがデータの読み込み時です。 データ読み込みは、何らかの管理プロセスを実装する論理的な場所となります。

統計を更新する際の基本原則は、次のとおりです。

- 読み込まれた各テーブルに更新された統計オブジェクトが少なくとも 1 つは含まれていることを確認します。 これにより、統計の更新の一環として、テーブル サイズ (行数とページ数) 情報が更新されます。
- JOIN、GROUP BY、ORDER BY、DISTINCT の各句に関与している列を重視します。
- トランザクションの日付などの "昇順キー" 列の値は、統計ヒストグラムに含まれないため、これらの列の更新頻度を増やすことを検討します。
- 静的な分布列の更新頻度を減らすことを検討します。
- 各統計オブジェクトは順序どおりに更新されることに注意してください。 特に、多数の統計オブジェクトが含まれた幅の広いテーブルでは、 `UPDATE STATISTICS <TABLE_NAME>` を実装するだけでは十分とはいえない場合があります。

詳細については、「[カーディナリティ推定](/sql/relational-databases/performance/cardinality-estimation-sql-server?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true)」を参照してください。

## <a name="examples-create-statistics"></a>例 :統計を作成する

以下の例では、さまざまなオプションを使用して統計を作成する方法を示します。 各列に使用するオプションは、データの特性とクエリでの列の使用方法によって異なります。

### <a name="create-single-column-statistics-with-default-options"></a>既定のオプションを使用した単一列統計の作成

列の統計を作成するには、統計オブジェクトの名前と列の名前を指定します。

次の構文では、既定のオプションをすべて使用しています。 既定では、統計を作成するときに、テーブルの **20%** がサンプリングされます。

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

次に例を示します。

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="create-single-column-statistics-by-examining-every-row"></a>すべての列の検査による単一列統計の作成

ほとんどの場合、20% という既定のサンプリング レートで十分です。 ただし、サンプリング レートを調整することもできます。

テーブル全体をサンプリングするには、次の構文を使用します。

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

次に例を示します。

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="create-single-column-statistics-by-specifying-the-sample-size"></a>サンプル サイズを指定した単一列統計の作成

サンプル サイズをパーセントで指定することもできます。

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="create-single-column-statistics-on-only-some-of-the-rows"></a>一部の行のみの単一列統計の作成

テーブルの一部の行の統計を作成することもできます。 これは、フィルター選択された統計と呼ばれます。

たとえば、大規模なパーティション テーブルの特定のパーティションのクエリを計画するときに、フィルター選択された統計を使用できます。 パーティション値のみで統計を作成すると、統計の精度が向上するので、クエリのパフォーマンスが向上します。

次の例では、値の範囲の統計を作成します。 パーティションの値の範囲に一致する値を簡単に定義できます。

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> クエリ オプティマイザーが分散クエリ プランを選択するときに、フィルター選択された統計の使用も考慮されるようにするには、クエリが統計オブジェクトの定義の範囲内である必要があります。 前の例では、クエリの WHERE 句で col1 の値として 2000101 ～ 20001231 の値を指定する必要があります。

### <a name="create-single-column-statistics-with-all-the-options"></a>すべてのオプションを使用した単一列統計の作成

オプションは組み合わせることができます。 次の例では、カスタム サンプル サイズを指定してフィルター選択された統計オブジェクトを作成します。

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

詳細については、「[CREATE STATISTICS](/sql/t-sql/statements/create-statistics-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true)」をご覧ください。

### <a name="create-multi-column-statistics"></a>複数列統計の作成

複数列統計オブジェクトを作成するには、これまでの例を使用しますが、複数の列を指定します。

> [!NOTE]
> クエリ結果の行数の推定に使用されるヒストグラムは、統計オブジェクト定義に示されている最初の列にのみ使用できます。

次の例では、ヒストグラムは *product\_category* で使用されます。 列間の統計は、*product\_category* と *product\_sub_category* で計算されます。

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

*product\_category* と *product\_sub\_category* の間には相関関係があるため、これらの列に同時にアクセスする場合は複数列統計オブジェクトが役立ちます。

### <a name="create-statistics-on-all-columns-in-a-table"></a>テーブルのすべての列の統計の作成

統計を作成する方法の 1 つとして、テーブルの作成後に CREATE STATISTICS コマンドを発行します。

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="use-a-stored-procedure-to-create-statistics-on-all-columns-in-a-sql-pool"></a>ストアド プロシージャを使用した、SQL プール内のすべての列の統計の作成

専用 SQL プールには、SQL Server の sp_create_stats に相当するシステム ストアド プロシージャはありません。 このストアド プロシージャは、まだ統計がない SQL プールのすべての列の単一列統計オブジェクトを作成します。

次の例は、SQL プールの設計を開始する際に役立ちます。 ニーズに合わせて、このオブジェクトを自由に変更できます。

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type IS NULL
BEGIN
    SET @create_type = 1;
END;

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+CONVERT(varchar(4),@sample_pct)+' PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

既定値を使用してテーブルのすべての列の統計を作成するには、ストアド プロシージャを実行します。

```sql
EXEC [dbo].[prc_sqldw_create_stats] 1, NULL;
```

フルスキャンを使用してテーブルのすべての列の統計を作成するには、次のプロシージャを呼び出します。

```sql
EXEC [dbo].[prc_sqldw_create_stats] 2, NULL;
```

テーブルのすべての列にサンプルの統計を作成するには、「3」およびサンプル率を入力します。 このプロシージャでは、20% のサンプル レートを使用します。

```sql
EXEC [dbo].[prc_sqldw_create_stats] 3, 20;
```

## <a name="examples-update-statistics"></a>例 :統計を更新します。

統計を更新するには、次の操作を行います。

- 統計オブジェクトを 1 つ更新します。 更新する統計オブジェクトの名前を指定します。
- テーブルのすべての統計オブジェクトを更新します。 特定の統計オブジェクトではなく、テーブルの名前を指定します。

### <a name="update-one-specific-statistics-object"></a>1 つの特定の統計オブジェクトの更新

特定の統計オブジェクトを更新するには、次の構文を使用します。

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

次に例を示します。

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

特定の統計オブジェクトを更新することで、統計を管理するために必要な時間とリソースを最小限に抑えることができます。 そうするには、更新する最適な統計オブジェクトの選択について少し検討する必要があります。

### <a name="update-all-statistics-on-a-table"></a>テーブルのすべての統計を更新する

テーブルのすべての統計オブジェクトを更新する簡単な方法を次に示します。

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

次に例を示します。

```sql
UPDATE STATISTICS dbo.table1;
```

UPDATE STATISTICS ステートメントは簡単に使用できます。 このステートメントはテーブルの *すべて* の統計を更新するので、必要以上の処理が実行される可能性があります。 パフォーマンスが問題でない場合は、これが、統計が最新の状態であることを保証する最も簡単で最も包括的な方法です。

> [!NOTE]
> テーブルのすべての統計を更新する場合、専用 SQL プールでは、統計オブジェクトごとにテーブルのスキャンを実行してサンプリングします。 テーブルが大きく、多数の列と統計が含まれている場合は、ニーズに基づいて個々の統計を更新する方が効率的です。

`UPDATE STATISTICS` プロシージャの実装については、[一時テーブル](sql-data-warehouse-tables-temporary.md)に関する記事をご覧ください。 実装方法は前述の `CREATE STATISTICS` プロシージャと若干異なりますが、結果は同じです。

完全な構文については、「[UPDATE STATISTICS ](/sql/t-sql/statements/update-statistics-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true)」を参照してください。

## <a name="statistics-metadata"></a>統計のメタデータ

統計に関する情報を確認する際に使用できるシステム ビューとシステム関数がいくつかあります。 たとえば、stats-date 関数を使用して、統計が最後に作成または更新されたのがいつであるかを確認することで、統計オブジェクトが古くなっているかどうかがわかります。

### <a name="catalog-views-for-statistics"></a>統計のカタログ ビュー

次のシステム ビューは、統計に関する情報を提供します。

| カタログ ビュー | 説明 |
|:--- |:--- |
| [sys.columns](/sql/relational-databases/system-catalog-views/sys-columns-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) |列ごとに 1 行。 |
| [sys.objects](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) |データベース内のオブジェクトごとに 1 行。 |
| [sys.schemas](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) |データベースのスキーマごとに 1 行。 |
| [sys.stats](/sql/relational-databases/system-catalog-views/sys-stats-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) |統計オブジェクトごとに 1 行。 |
| [sys.stats_columns](/sql/relational-databases/system-catalog-views/sys-stats-columns-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) |統計オブジェクトの列ごとに 1 行。 sys.columns にリンク。 |
| [sys.tables](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) |テーブル (外部テーブルを含む) ごとに 1 行。 |
| [sys.table_types](/sql/relational-databases/system-catalog-views/sys-table-types-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) |データ型ごとに 1 行。 |

### <a name="system-functions-for-statistics"></a>統計のシステム関数

次のシステム関数は統計の操作に役立ちます。

| システム関数 | 説明 |
|:--- |:--- |
| [STATS_DATE](/sql/t-sql/functions/stats-date-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) |統計オブジェクトの最終更新日。 |
| [DBCC SHOW_STATISTICS](/sql/t-sql/database-console-commands/dbcc-show-statistics-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) |統計オブジェクトで認識される値の分布に関する概要レベルの情報と詳細情報。 |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a>1 つのビューへの統計列と関数の統合

このビューには、統計に関連する列と、STATS_DATE() 関数の結果が一緒に表示されます。

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_definition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-show_statistics-examples"></a>DBCC SHOW_STATISTICS() の例

DBCC SHOW_STATISTICS() は、統計オブジェクト内に保持されているデータを表示します。 このデータは 3 つの部分で提供されます。

- ヘッダー
- 密度ベクトル
- ヒストグラム

ヘッダーには、統計に関するメタデータが含まれます。 ヒストグラムには、統計オブジェクトの最初のキー列の値の分布が表示されます。 密度ベクトルは、列間の相関関係を測定します。

> [!NOTE]
> 専用 SQL プールでは、統計オブジェクト内のデータを使用してカーディナリティ推定値を計算します。

### <a name="show-header-density-and-histogram"></a>ヘッダー、密度、ヒストグラムの表示

次の簡単な例は、統計オブジェクトの 3 つの部分をすべて表示します。

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

次に例を示します。

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-show_statistics"></a>DBCC SHOW_STATISTICS() の 1 つ以上の部分の表示

特定の部分だけを表示する場合は、`WITH` 句を使用して表示する部分を指定します。

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

次に例を示します。

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-show_statistics-differences"></a>DBCC SHOW_STATISTICS() の相違点

SQL Server に比べ、専用 SQL プールでは、DBCC SHOW_STATISTICS() がより厳密に実装されています。

- ドキュメントに記載されていない機能はサポートされていません。
- Stats_stream は使用できません。
- 統計データの特定のサブセットの結果を結合することはできません たとえば、STAT_HEADER JOIN DENSITY_VECTOR。
- メッセージを抑制するために、NO_INFOMSGS を設定することはできません。
- 統計名を囲む角かっこは使用できません。
- 列名を使用して、統計オブジェクトを識別することはできません。
- カスタム エラー 2767 はサポートされていません。

## <a name="next-steps"></a>次のステップ

クエリのパフォーマンスをさらに向上させるには、[ワークロードの監視](sql-data-warehouse-manage-monitor.md)に関する記事を参照してください
