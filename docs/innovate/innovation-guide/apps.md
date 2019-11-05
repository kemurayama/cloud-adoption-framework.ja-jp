---
title: Azure イノベーション ガイド:アプリによる連携
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Azure を利用したアプリによる連携でイノベーションを行う方法について説明します。
author: billyclaymyersmsft
ms.author: wimyers
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: df91d44d9b1efc2196b8b322c247dd39ef3d0d1e
ms.sourcegitcommit: 910efd3e686bd6b9bf93951d84253b43d4cc82b5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72769359"
---
::: zone target="docs"

# <a name="azure-innovation-guide-engage-through-apps"></a>Azure イノベーション ガイド:アプリによる連携

::: zone-end

::: zone target="chromeless"

# <a name="engage-through-apps"></a>アプリによる連携

::: zone-end

アプリによるイノベーションには、オンプレミスでホストされている既存のアプリの最新化と、コンテナー技術またはサーバーレス技術を利用し、クラウドネイティブのアプリをビルドすることの両方が含まれます。 アプリの最新化に関しては、.NET、.NET Core、Java、Node.js、Ruby、Python、PHP で記述された既存の Web アプリや API アプリを簡単に最新化して Azure でデプロイするための PaaS サービス (Azure App Service など) が Azure から提供されます。 オープン標準のコンテナー モデルを使用することで、Azure Kubernetes Services、Azure Container Instances、Web App for Containers などのマネージド サービスによるマイクロサービスの構築、既存のアプリケーションのコンテナー化、Azure でのそれらのデプロイが簡単になります。 Azure Functions や Azure Logic Apps などのサーバーレス技術を使用すると、インフラストラクチャのデプロイと管理ではなく、従量課金モデル (使用したものに支払う) によるアプリケーションのビルドに集中できます。

<!-- markdownlint-disable MD025 -->

# <a name="deliver-value-fastertabdelivervaluefaster"></a>[より短期間で価値を届ける](#tab/DeliverValueFaster)

クラウドベース ソリューションの利点には、フィードバックを短期間で収集し、エンド ユーザーに価値を届けられるということが挙げられます。 そのエンド ユーザーが外部の顧客であっても、自分の会社のユーザーであっても、アプリケーションに関するフィードバックは早く届くに越したことはありません。

## <a name="azure-app-service"></a>Azure App Service

Azure App Service からはアプリケーションのホスティング環境が提供され、それによってインフラストラクチャ管理と OS パッチ適用の負担が取り除かれます。 これはユーザーの需要に合わせて自動的にスケーリングし、同時に、定義した上限で制約し、コストを抑えます。

Azure App Service では、ASP.NET、ASP.NET Core、Java、Ruby、Node.js、PHP、Python などの言語が最高レベルでサポートされています。 別のランタイム スタックをホストする必要がある場合、Web App for Containers を使用すると、Azure App Service 環境内で Docker コンテナーを短時間で簡単にホストし、サーバーの管理が要らない環境でカスタム コード スタックをホストできます。

### <a name="action"></a>Action

Azure App Service のデプロイを構成または監視するには:

1. **[App Service]** に移動します。
2. 新しいサービスを構成する: **[追加 +]** リンクをクリックし、画面の指示に従います。
3. 既存のサービスを管理する:ホストされているアプリケーションの一覧から目的のアプリを選択します。

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites]" submitText="Go to App Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-cognitive-services"></a>Azure Cognitive Services

Azure Cognitive Services では、Microsoft がサポートする AI と Machine Learning のアルゴリズムを活用できる一連の API を介して、高度なインテリジェンスをアプリケーションに直接、取り込むことができます。

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Action

Azure Cognitive Service デプロイを構成または監視するには:

1. **[Cognitive Services]** に移動します。
2. 新しいサービスを構成する: **[追加 +]** リンクをクリックし、画面の指示に従います。
3. 既存のサービスを管理する:ホステッド サービスの一覧から目的のサービスを選択します。

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-bot-services"></a>Azure Bot Services

Azure Bot Services では、AI と Machine Learning を利用して顧客との新しい対話を作成するナチュラル ボット インターフェイスを追加する目的で標準のアプリケーションを拡張できます。

### <a name="action"></a>Action

Azure Bot Services デプロイを構成または監視するには:

1. **[Bot Services]** に移動します。
2. 新しいサービスを構成する: **[追加 +]** リンクをクリックし、画面の指示に従います。
3. 既存のサービスを管理する:ホステッド サービスの一覧から目的のボットを選択します。

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.BotService%2FbotServices]" submitText="Go to Bot Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-devops"></a>Azure DevOps

イノベーションの過程では、最終的に DevOps に向かって進むことになります。 Microsoft には長い間、Team Foundation Server (TFS) と呼ばれるオンプレミス製品がありました。 Microsoft はそのイノベーションの過程で、さまざまな言語とリリース目的を支援するビルド ツールとリリース ツールを提供するクラウドベース サービスとなる Azure DevOps を開発しました。 [Azure DevOps](https://docs.microsoft.com/azure/devops)

## <a name="visual-studio-app-center"></a>Visual Studio App Center

モバイル アプリの人気が上がり続ける中、さまざまな構成を持つ実際のデバイスでテストを自動化できるプラットフォームに対するニーズが増えています。 Visual Studio App Center は、iOS、Android、Windows、macOS をまたいでアプリケーションをテストできる場所だけでなく、Azure Application Insights を活用し、利用統計情報に基づいて短時間で簡単に判断するための機能を持った監視プラットフォームとなります。 詳細については、[Visual Studio App Center の概要](https://docs.microsoft.com/appcenter)ページをご覧ください。

Visual Studio App Center からは通知サービスも提供されます。1 回の呼び出しでプラットフォームに関係なく通知を送信できます。通知サービス別に連絡する必要がありません。 詳細については、「[Visual Studio App Center Push (ACP)](https://docs.microsoft.com/appcenter/push)」を参照してください。

### <a name="read-more"></a>詳細情報

- [App Service の概要](https://docs.microsoft.com/azure/app-service/overview)
- [Web Apps for Containers:カスタム コンテナーの実行](https://docs.microsoft.com/azure/app-service/containers/quickstart-docker)
- [Azure Functions の概要](https://docs.microsoft.com/azure/azure-functions/functions-overview)
- [.NET および .NET Core 開発者向けの Azure](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet)
- [Azure SDK for Python のドキュメント](https://docs.microsoft.com/azure/python)
- [Java クラウド開発者向けの Azure](https://docs.microsoft.com/azure/java/?view=azure-java-stable)
- [Azure に PHP Web アプリを作成する](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-php)
- [Azure SDK for JavaScript のドキュメント](https://docs.microsoft.com/azure/javascript)
- [Azure SDK for Go のドキュメント](https://docs.microsoft.com/azure/go)
- [DevOps ソリューション](https://azure.microsoft.com/solutions/devops)

# <a name="cloud-native-appstabcloudnative"></a>[クラウド ネイティブ アプリ](#tab/CloudNative)

<!-- markdownlint-disable MD026 -->

## <a name="what-are-cloud-native-applications"></a>クラウドネイティブ アプリケーションとは

クラウドネイティブ アプリケーションは一から構築され、クラウドの規模やパフォーマンスに合わせて最適化されます。 マイクロサービスのアーキテクチャに基づいて疎結合されており、マネージド サービスを使用し、観察可能です。また、継続的デリバリーを利用して高い信頼性を実現し、市場投入までの時間を短縮します。 一般的に移植可能であり、パブリック クラウド、プライベート クラウド、ハイブリッド クラウドなど、動的な環境で実行できます。 通常、クラウドネイティブ アプリケーションは、次の 1 つ以上の方法を利用して構築されます。

- マイクロサービス
- サーバーレス
- コンテナー

## <a name="microservices"></a>マイクロサービス

独立した小さなモジュールで構成されるアプリケーションが適切に定義された API コントラクトを使用して相互にやり取りするスタイルのソフトウェア アーキテクチャをマイクロサービスといいます。 サービスのモジュールは単一の機能を実装した小さなブロックであり、それぞれが高度に切り離されています。 マイクロサービスは次のことを支援します。

- サービスを個別に構築する。
- サービスを個別にスケーリングする。
- デプロイとプログラミング言語に関して、最適な方法を使用する。
- 障害点を分離する。
- 短期間で価値を届ける。

### <a name="azure-kubernetes-service-aks"></a>Azure Kubernetes Service (AKS)

フル マネージドの Kubernetes サービスにより、クラスター リソースをオンデマンドでプロビジョニング、アップグレード、スケーリングできます。 AKS を利用すると、コンテナー化されたアプリケーションを簡単にデプロイし、管理できます。 サーバーレスの Kubernetes、統合された継続的インテグレーションと継続的デリバリー (CI/CD) エクスペリエンス、エンタープライズ レベルのセキュリティとガバナンスが提供されます。 開発チームと運用チームを単一のプラットフォーム上で統合し、迅速かつ確実にアプリケーションをビルド、デリバリー、スケーリングします。

#### <a name="action"></a>Action

Azure Kubernetes Service を構成または監視するには:

1. **[Kubernetes サービス]** に移動します。
2. 新しいサービスを構成する: **[追加 +]** リンクをクリックし、画面の指示に従います。
3. 既存のサービスを管理する:一覧から目的の Kubernetes サービスを選択します。

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.ContainerService%2FmanagedClusters]" submitText="Go to Kubernetes Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="event-based-solutions"></a>イベントベースのソリューション

### <a name="azure-functions"></a>Azure Functions

Azure Functions からは、小規模なコード ("関数") をクラウド内で実行するためのプラットフォームが提供されます。 コードをマイクロサービス アーキテクチャにリファクタリングするとき、Functions から始めることができます。

Azure Functions ランタイムでは、C#、Java、JavaScript、Python など、さまざまな言語がサポートされています。 完全な一覧は、「[Azure Functions でサポートされている言語](https://docs.microsoft.com/azure/azure-functions/supported-languages)」を参照してください。

関数のもう 1 つの長所は、HTTPTriggers、TimerTriggers、他の Azure サービス (Blob Storage、EventGrid、ServiceBus) からのトリガーなど、さまざまなアクションやイベントでトリガーできることです。 トリガーとバインドの詳細については、「[Azure Functions でのトリガーとバインドの概念](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings)」をご覧ください。

#### <a name="action"></a>Action

Azure Functions デプロイを構成または監視するには:

1. **[Function App]** に移動します。
2. 新しいアプリを構成する: **[追加 +]** リンクをクリックし、画面の指示に従います。
3. 既存のアプリを管理する:Function Apps の一覧から目的のアプリを選択します。

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites/kind/functionapp]" submitText="Go to Azure Functions" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="serverless-solutions"></a>サーバーレス ソリューション

スケーリング、可用性、パフォーマンスが自動的に処理されるフル マネージド プラットフォームを使用すると、インフラストラクチャのプロビジョニングや管理を行うことなく、クラウドネイティブ アプリを構築できます。 Azure サーバーレス ソリューションの利点:

- 開発者ベロシティを高める
- チームのパフォーマンスを向上させる
- 組織的影響を改善する

### <a name="azure-logic-apps"></a>Azure Logic Apps

異なるシステム間で必要になる複雑な統合コードを記述せずに、データとアプリを統合します。 Azure Logic Apps によりサーバーレス ワークフローを視覚的に作成し、独自の API やサーバーレス関数のほか、Salesforce、Microsoft Office 365、Dropbox など、すぐに使えるサービスとしてのソフトウェア (SaaS) コネクタを使用できます。

#### <a name="action"></a>Action

Azure Logic Apps を構成または監視するには:

1. **[Logic Apps]** に移動します。
2. 新しいアプリを構成する: **[追加 +]** リンクをクリックし、画面の指示に従います。
3. 既存のアプリを管理する:一覧で目的の Logic App を選択します。

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Logic%2Fworkflows]" submitText="Go to Azure Logic Apps" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="serverless-api-management"></a>サーバーレス API 管理

サーバーレス アプリケーションに自然に適合するように設計および実装された使用モデルを提供するフル マネージド サービス、Azure API Management を使用しては、API を発行、セキュリティ保護、変換、メンテナンス、監視します。

#### <a name="action"></a>Action

API Management サービスを構成または監視するには:

1. **[API Management サービス]** に移動します。
2. 新しいサービスを構成する: **[追加 +]** リンクをクリックし、画面の指示に従います。
3. 既存のサービスを管理する:一覧から目的のサービスを選択します。

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice]" submitText="Go to API Management Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="containers"></a>Containers

アプリケーション ポートフォリオを最新化するとき、Azure からは、既存のアプリケーションをコンテナーにリフトアンドシフトするための、また、短期間でユーザーに価値を届けるクラウドネイティブ マイクロサービス アプリケーションをビルドするためのさまざまなコンテナー サービスが提供されます。 エンドツーエンドの開発者向けツールと CI/CD ツールを利用し、コンテナー化されたアプリケーションを開発、更新、デプロイします。 Azure Active Directory と統合されるフル マネージド Kubernetes コンテナー オーケストレーション サービスを利用し、大規模にコンテナーを管理します。 アプリを最新化する過程のどの段階にあっても、セキュリティ要件を満たしながら、コンテナー化アプリケーションの開発を加速します。

### <a name="azure-container-instances"></a>Azure Container Instances

サーバーレスなマネージド Azure 環境内で Docker コンテナーをオンデマンドで実行します。 Azure Container Instances (ACI) は、オーケストレーションすることなく分離コンテナー内で運用できる、あらゆるシナリオ向けのソリューションです。 ACI でワークロードを実行することで、アプリケーションの設計と開発に集中できます。アプリケーションを実行するインフラストラクチャの管理を心配する必要はありません。

### <a name="action"></a>Action

コンテナー インスタンスを構成または監視するには:

1. **[Container Instances]** に移動します。
2. 新しいコンテナー インスタンスを構成する: **[追加 +]** リンクをクリックし、画面の指示に従います。
3. 既存のコンテナー インスタンスを管理する:一覧から目的のコンテナー インスタンスを選択します。

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ContainerInstance%2FcontainerGroups]" submitText="Go to Container instances" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="azure-red-hat-openshift"></a>Azure Red Hat OpenShift

Azure Red Hat OpenShift では、フル マネージドの OpenShift クラスターをセルフサービスで柔軟にデプロイすることが可能です。 マスター ノード、インフラストラクチャ ノード、アプリケーション ノードのパッチ適用、更新、監視が Microsoft と Red Hat の両社によって行われるので、規制準拠を維持し、アプリケーション開発に専念できます。 独自のレジストリ、ネットワーク、ストレージ、CI/CD のソリューションを選択するか、自動化されたソース コード管理、コンテナーとアプリケーションのビルド、デプロイ、スケーリング、正常性の管理などが含まれる組み込みソリューションをすぐにでも開始します。

**[[Azure Red Hat OpenShift]](https://docs.microsoft.com/azure/openshift/intro-openshift) に移動します。**

# <a name="isolate-points-of-failuretabisolatepointsoffailure"></a>[障害点を分離する](#tab/IsolatePointsOfFailure)

最初のテスト段階からの移行を始めるとき、障害点を分離し、除去するための方法を評価します。 Azure クラウドには分散性があり、障害を最小限に抑え、同時にパフォーマンスを改善するようにアプリケーションを設計できます。

## <a name="azure-front-door"></a>Azure Front Door

Azure Front Door からは、世界中にアプリケーションを届けるための安全かつスケーラブルなエントリ ポイントが提供されます。 Azure Front Door では、トラフィックの最適化を組み合わせることで最良のパフォーマンスと瞬間的なグローバル フェールオーバーが得られます。 トランスポート層セキュリティ (TLS) プロトコル終了 (SSL オフロード) または HTTP/HTTPS 要求あたりのアプリケーション層処理が必要な場合、Azure Front Door を Traffic Manager にフェールオーバーしてください。

### <a name="action"></a>Action

フロント ドアを構成または監視するには:

1. **[フロント ドア]** に移動します。
2. 新しいフロント ドアを構成する: **[追加 +]** リンクをクリックし、画面の指示に従います。
3. 既存のフロント ドアを管理する:一覧から目的のフロント ドアを選択します。

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Network%2Ffrontdoors]" submitText="Go to Front Doors" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="traffic-manager"></a>Traffic Manager

Traffic Manager からは、さまざまなルールに基づいて経路を指定できる DNS ベースの負荷分散が提供されます。 デプロイしたサービスに障害が発生した場合の回復力になります。 また、Traffic Manager をスタックすることで障害ベースのルーティングとパフォーマンスベースのルーティングの両方を使用できます。場所に基づいて最良の体験が与えられます。

### <a name="action"></a>Action

Traffic Manager プロファイルを構成または監視するには:

1. **[Traffic Manager プロファイル]** に移動します。
2. 新しいプロファイルを構成する: **[追加 +]** リンクをクリックし、画面の指示に従います。
3. 既存のプロファイルを管理する:一覧から目的のプロファイルを選択します。

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Network%2Ftrafficmanagerprofiles]" submitText="Go to Traffic Manager profiles" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-content-delivery-network"></a>Azure Content Delivery Network

Azure からは、エンド ユーザーの近くでキャッシュすることでアセットをタイムリーに配信することを可能にする分散コンテンツ配信ネットワーク (CDN) が提供されます。 このキャッシュにより顧客体験が改善され、コンテンツをダウンロードするとき、CDN エンドポイントとアプリケーションをホストしているデータセンターの間のネットワーク問題によりダウンロードに失敗する問題が防止されます。 この CDN は Azure でホストされていないアプリケーションで利用することもできます。

### <a name="action"></a>Action

CDN プロファイルを構成または監視するには:

1. **[CDN プロファイル]** に移動します。
2. 新しいプロファイルを構成する: **[追加 +]** リンクをクリックし、画面の指示に従います。
3. 既存のプロファイルを管理する:一覧から目的のプロファイルを選択します。

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.cdn%2Fprofiles]" submitText="Go to CDN profiles" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="read-more"></a>詳細情報

- [Azure Front Door](https://docs.microsoft.com/azure/frontdoor/front-door-overview)
- [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager)
- [Content Delivery Network](https://docs.microsoft.com/azure/cdn)