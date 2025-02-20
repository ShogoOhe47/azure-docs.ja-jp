---
title: 高速フォレスト分位点回帰: モジュール リファレンス
titleSuffix: Azure Machine Learning
description: 高速フォレスト分位点回帰コンポーネントを使用して、指定した数の分位点の値を予測する回帰モデルを作成する方法について説明します。
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: reference
author: likebupt
ms.author: keli19
ms.date: 07/13/2020
ms.openlocfilehash: b6478b1c666f6aee593473f8cdf2a6acd3e1e8c9
ms.sourcegitcommit: e41827d894a4aa12cbff62c51393dfc236297e10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2021
ms.locfileid: "131565608"
---
# <a name="fast-forest-quantile-regression"></a>高速フォレスト分位点回帰

この記事では Azure Machine Learning デザイナーのモジュールについて説明します。

このコンポーネントは、パイプラインで高速フォレスト分位点回帰モデルを作成するために使用します。 高速フォレスト分位点回帰は、1 つの平均予測値を取得するのではなく、予測された値の分布をより詳細に把握する場合に便利です。 この手法には、次のような多くの用途があります。  
  
- 価格の予測  
  
- 学生の成績の予測または子供の発達を評価するための成長グラフの適用  
  
- 変数間に弱い関係だけが存在する場合の予測的関係の発見  
  
この回帰アルゴリズムは、**教師あり** 学習手法であるため、ラベル列を含むタグ付けされたデータセットが必要となります。 回帰アルゴリズムであるため、ラベル列には数値のみを含める必要があります。

## <a name="more-about-quantile-regression"></a>分位点回帰の詳細

回帰にはさまざまな種類があります。 簡単に言えば、回帰は数値ベクトルで表された対象にモデルを合わせることを指します。 しかし、より高度な回帰の手法の開発が統計学者によって進められています。

*分位点* の最も簡単な定義は、一連のデータを同じサイズのグループに分割する値であるため、分位点値はグループ間の境界をマークします。 統計的に述べると、分位点は、ランダム変数の累積分布関数 (CDF) の逆数から一定の間隔で取得した値です。

線形回帰モデルでは、1 つの推量を使用して数値変数の値 (*平均*) を予測しようとしますが、ターゲット変数の範囲分布または全体分布を予測することが必要になる場合があります。 そのために、ベイズ回帰や分位点回帰などの手法が開発されました。

分位点回帰は、予測値の分布を理解するのに役立ちます。 このコンポーネントで使用されているものを含む、ツリーベースの分位点回帰モデルは、さらにノンパラメトリック分布の予測に使用できるという利点があります。

  
## <a name="how-to-configure-fast-forest-quantile-regression"></a>高速フォレスト分位点回帰を構成する方法

1. デザイナーでパイプラインに **高速フォレスト分位点回帰** コンポーネントを追加します。 このコンポーネントは、 **[Machine Learning アルゴリズム]** の **[回帰]** カテゴリにあります。

2. **高速フォレスト分位点回帰** コンポーネントの右ペインで、 **[トレーナー モードの作成]** オプションを設定してモデルをトレーニングする方法を指定します。  
  
    - **Single Parameter (単一パラメーター)** : モデルの構成方法を決めている場合は、特定の値のセットを引数として渡します。 モデルをトレーニングする場合は、[トレーニング モデル](train-model.md)を使用します。
  
    - **[Parameter Range]\(パラメーター範囲\)** : 最適なパラメーターがわからない場合は、[[モデルのハイパーパラメーターの調整]](tune-model-hyperparameters.md) コンポーネントを使用してパラメーターのスイープを行います。 トレーナーは、指定された複数の値で繰り返し最適な構成を見つけます。

3. **[ツリー数]** には、アンサンブルに作成できるデシジョン ツリーの最大数を入力します。 より多くのツリーを作成すると、一般的に精度は向上しますが、トレーニング時間が長くなります。  

4. **[リーフ数]** には、ツリーに作成できるリーフ (終端ノード) の最大数を指定します。  

5. **[リーフを形成するために必要なトレーニング インスタンスの最小数]** には、ツリーの終端ノード (リーフ) を作成するうえで必要な最小サンプル数を指定します。  
  
     この値を増やすと、新しいルールを作成するためのしきい値が大きくなります。 たとえば、既定値の 1 では、ケースが 1 つであっても新しいルールを作成できます。 この値を 5 に増やした場合、同じ条件を満たすケースがトレーニング データに少なくとも 5 つ含まれている必要があります。

6. **[バギングの割合]** には、分位点の各グループを構築するときに使用するサンプルの割合を表す 0 ~ 1 の数値を指定します。 サンプルは、復元ありでランダムに選択されます。

7. **[分割の割合]** には、ツリーの各分割で使用する特徴の割合を表す 0 ~ 1 の数値を入力します。 使用される特徴は、常にランダムに選択されます。

8. **[推定される分位点]** には、トレーニングや予測の作成の対象となる分位点のセミコロン区切りの一覧を指定します。
  
     たとえば、分位点を推定するモデルを構築する場合は、「`0.25; 0.5; 0.75`」と入力します。  

9. 必要に応じて、 **[乱数シード]** には、モデルによって使用される乱数ジェネレーターにシードを設定する値を入力できます。  既定値は 0、つまりランダム シードが選択されます。
  
     同じデータで連続して実行された結果を再現する必要がある場合に、値を指定する必要があります。  

10. トレーニング データセットとトレーニングされていないモデルをトレーニング コンポーネントのいずれかに接続します。 

    - **[Create trainer mode]\(トレーナー モードの作成\)** を **[Single Parameter]\(単一パラメーター\)** に設定した場合は、[モデルのトレーニング](train-model.md) コンポーネントを使用します。

    - **[トレーナー モードの作成]** を **[Parameter Range]\(パラメーター範囲\)** に設定した場合は、[モデルのハイパーパラメーターの調整](tune-model-hyperparameters.md)コンポーネントを使用します。

    > [!WARNING]
    > 
    > - パラメーター範囲を [[モデルのトレーニング]](train-model.md) に渡すと、パラメーター範囲リストの 1 番目の値のみが使用されます。
    > 
    > - [モデルのハイパーパラメーターの調整](tune-model-hyperparameters.md)コンポーネントで各パラメーターにさまざまな設定が必要なときに、1 つのパラメーター値のセットを渡すと、それらの値は無視され、学習器の既定値が使用されます。
    > 
    > - **[Parameter Range]\(パラメーター範囲\)** オプションを選択し、任意のパラメーターに単一の値を入力した場合、指定した単一の値はスイープ全体で使用されます。これは、他のパラメーターが値の範囲の中で変化する場合でも同様です。

11. パイプラインを送信します。

## <a name="results"></a>結果

トレーニングの完了後:

+ トレーニング済みモデルのスナップショットを保存するには、トレーニング コンポーネントを選択し、右側のパネルの **[出力とログ]** タブに切り替えます。 **[データセットの登録]** アイコンをクリックします。  保存されたモデルは、コンポーネント ツリーにコンポーネントとして示されます。

## <a name="next-steps"></a>次の手順

Azure Machine Learning で[使用できる一連のコンポーネント](component-reference.md)を参照してください。
