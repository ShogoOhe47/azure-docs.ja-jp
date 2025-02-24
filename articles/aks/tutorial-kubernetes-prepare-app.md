---
title: Kubernetes on Azure のチュートリアル - アプリケーションの準備
description: この Azure Kubernetes Service (AKS) チュートリアルでは、Docker Compose を使用して複数コンテナー アプリを準備およびビルドする方法を説明します。その後、AKS にデプロイすることができます。
services: container-service
ms.topic: tutorial
ms.date: 01/12/2021
ms.custom: mvc
ms.openlocfilehash: 349bf90ea0b344d5232c885358814f39fba4c19f
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/29/2021
ms.locfileid: "98251958"
---
# <a name="tutorial-prepare-an-application-for-azure-kubernetes-service-aks"></a>チュートリアル: Azure Kubernetes Service (AKS) 用のアプリケーションの準備

7 つのパートのうちの 1 番目であるこのチュートリアルでは、複数コンテナー アプリケーションを Kubernetes で使用する準備をします。 Docker Compose などの既存の開発ツールは、アプリケーションをローカルでビルドしてテストするために使用されます。 学習内容は次のとおりです。

> [!div class="checklist"]
> * GitHub からサンプル アプリケーション ソースをクローンする
> * サンプル アプリケーション ソースからコンテナー イメージを作成する
> * ローカル Docker 環境で複数コンテナー アプリケーションをテストする

完了後、次のアプリケーションがローカル開発環境で実行されます。

:::image type="content" source="./media/container-service-kubernetes-tutorials/azure-vote-local.png" alt-text="ローカル Web ブラウザーで開かれた、ローカルで実行されている Azure 投票アプリのコンテナー イメージを示すスクリーンショット" lightbox="./media/container-service-kubernetes-tutorials/azure-vote-local.png":::

後続のチュートリアルでは、このコンテナー イメージが Azure Container Registry にアップロードされ、AKS クラスターにデプロイされます。

## <a name="before-you-begin"></a>開始する前に

このチュートリアルの前提として、コンテナー、コンテナー イメージ、`docker` コマンドなど、Docker のコア概念を基本的に理解している必要があります。 [Docker の入門][docker-get-started]に関するドキュメントでコンテナーの基礎についての入門情報を参照してください。

このチュートリアルを完了するには、Linux コンテナーを実行するローカルの Docker 開発環境が必要です。 Docker では、[Mac][docker-for-mac]、[Windows][docker-for-windows]、または [Linux][docker-for-linux] システム上に Docker を構成するパッケージが提供されています。

> [!NOTE]
> Azure Cloud Shell には、これらのチュートリアルのすべてのステップを完了するために必要な Docker コンポーネントが含まれているわけではありません。 そのため、完全な Docker 開発環境の使用をお勧めします。

## <a name="get-application-code"></a>アプリケーションのコードを入手する

このチュートリアルで使用する[サンプル アプリケーション][sample-application]は、フロントエンド Web コンポーネントとバックエンド Redis インスタンスで構成される基本的な投票アプリです。 Web コンポーネントは、カスタム コンテナー イメージにパッケージ化されています。 Redis インスタンスでは、Docker Hub から変更されていないイメージを使用します。

サンプル アプリケーションを開発環境にクローンするには、[git][] を使用します。

```console
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

クローンされたディレクトリに移動します。

```console
cd azure-voting-app-redis
```

ディレクトリ内には、アプリケーションのソース コード、事前作成された Docker Compose ファイル、および Kubernetes マニフェスト ファイルがあります。 これらのファイルは、チュートリアル セット全体で使用されます。 ディレクトリの内容と構造は次のとおりです。

```output
azure-voting-app-redis
│   azure-vote-all-in-one-redis.yaml
│   docker-compose.yaml
│   LICENSE
│   README.md
│
├───azure-vote
│   │   app_init.supervisord.conf
│   │   Dockerfile
│   │   Dockerfile-for-app-service
│   │   sshd_config
│   │
│   └───azure-vote
│       │   config_file.cfg
│       │   main.py
│       │
│       ├───static
│       │       default.css
│       │
│       └───templates
│               index.html
│
└───jenkins-tutorial
        config-jenkins.sh
        deploy-jenkins-vm.sh
```

## <a name="create-container-images"></a>コンテナー イメージを作成する

[Docker Compose][docker-compose] は、コンテナー イメージのビルドと複数コンテナー アプリケーションのデプロイとを自動化するために使用することができます。

コンテナー イメージの作成、Redis イメージのダウンロード、およびアプリケーションの起動を行うために、`docker-compose.yaml` サンプル ファイルを実行します。

```console
docker-compose up -d
```

完了したら、[docker images][docker-images] コマンドを使って、作成されたイメージを確認します。 3 つのイメージがダウンロードまたは作成されていることを確認してください。 *azure-vote-front* イメージにはフロントエンド アプリケーションが含まれており、ベースとして *nginx-flask* イメージが使用されます。 *redis* イメージは、Redis インスタンスを起動するために使用されます。

```
$ docker images

REPOSITORY                                     TAG                 IMAGE ID            CREATED             SIZE
mcr.microsoft.com/azuredocs/azure-vote-front   v1                  84b41c268ad9        9 seconds ago       944MB
mcr.microsoft.com/oss/bitnami/redis            6.0.8               3a54a920bb6c        2 days ago          103MB
tiangolo/uwsgi-nginx-flask                     python3.6           a16ce562e863        6 weeks ago         944MB
```

[docker ps][docker-ps] コマンドを実行して、実行中のコンテナーを確認します。

```
$ docker ps

CONTAINER ID        IMAGE                                             COMMAND                  CREATED             STATUS              PORTS                           NAMES
d10e5244f237        mcr.microsoft.com/azuredocs/azure-vote-front:v1   "/entrypoint.sh /sta…"   3 minutes ago       Up 3 minutes        443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
21574cb38c1f        mcr.microsoft.com/oss/bitnami/redis:6.0.8         "/opt/bitnami/script…"   3 minutes ago       Up 3 minutes        0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a>ローカルでアプリケーションをテストする

実行中のアプリケーションを表示するには、ローカルの Web ブラウザーで「 `http://localhost:8080`」と入力します。 次の例で示すように、サンプル アプリケーションが読み込まれます。

:::image type="content" source="./media/container-service-kubernetes-tutorials/azure-vote-local.png" alt-text="ローカル Web ブラウザーで開かれた、ローカルで実行されている Azure 投票アプリのコンテナー イメージを示すスクリーンショット" lightbox="./media/container-service-kubernetes-tutorials/azure-vote-local.png":::

## <a name="clean-up-resources"></a>リソースをクリーンアップする

アプリケーションの機能を検証したので、実行中のコンテナーを停止して削除できます。 ***コンテナー イメージを削除しないでください** _。次のチュートリアルで、_azure-vote-front* イメージは Azure Container Registry インスタンスにアップロードされます。

[docker-compose down][docker-compose-down] コマンドを使用して、コンテナー インスタンスとリソースを停止して削除します。

```console
docker-compose down
```

ローカル アプリケーションが削除されると、Azure Vote アプリケーション *azure-vote-front* を含む Docker イメージが作成され、次のチュートリアルで使用できます。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、アプリケーションをテストし、アプリケーション用のコンテナー イメージを作成しました。 以下の方法を学習しました。

> [!div class="checklist"]
> * GitHub からサンプル アプリケーション ソースをクローンする
> * サンプル アプリケーション ソースからコンテナー イメージを作成する
> * ローカル Docker 環境で複数コンテナー アプリケーションをテストする

次のチュートリアルでは、Azure Container Registry にコンテナー イメージを格納する方法について学習します。

> [!div class="nextstepaction"]
> [Azure Container Registry にイメージをプッシュする][aks-tutorial-prepare-acr]

<!-- LINKS - external -->
[docker-compose]: https://docs.docker.com/compose/
[docker-for-linux]: https://docs.docker.com/engine/installation/#supported-platforms
[docker-for-mac]: https://docs.docker.com/docker-for-mac/
[docker-for-windows]: https://docs.docker.com/docker-for-windows/
[docker-get-started]: https://docs.docker.com/get-started/
[docker-images]: https://docs.docker.com/engine/reference/commandline/images/
[docker-ps]: https://docs.docker.com/engine/reference/commandline/ps/
[docker-compose-down]: https://docs.docker.com/compose/reference/down
[git]: https://git-scm.com/downloads
[sample-application]: https://github.com/Azure-Samples/azure-voting-app-redis

<!-- LINKS - internal -->
[aks-tutorial-prepare-acr]: ./tutorial-kubernetes-prepare-acr.md
