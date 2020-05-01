---
title: Azure リソースの料金計算とサイズ設定
description: Azure 向けのクラウド導入フレームワークを使用して、Azure リソースの料金計算とサイズ設定のベスト プラクティスについて学習します。
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 1e175ee448467d9796b1483f66568389fc5d24b0
ms.sourcegitcommit: 825f9ae5b6cdd2fa6cb18c14a9733ba9106194f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81646877"
---
# <a name="best-practices-for-costing-and-sizing-resources-hosted-in-azure"></a>Azure でホストされるリソースの料金計算とサイズ設定のベスト プラクティス

ガバナンスの規範を提供する一方で、コスト管理は企業レベルで繰り返し発生するテーマです。 コストを最適化して管理することで、Azure 環境の長期的な成功を保証できます。 すべてのチーム (財務チーム、管理チーム、アプリケーション開発チーム) が関連するコストを理解しておき、定期的に確認することが重要です。

> [!IMPORTANT]
> この記事で説明するベスト プラクティスと見解は、記事の執筆時点で利用できる Azure のプラットフォームとサービスの機能に基づいています。 特徴や機能は時間の経過と共に変化します。 すべての推奨事項がお客様のデプロイに当てはまるとは限らないため、お客様の状況に適したものを選択してください。

## <a name="best-practices-by-team-and-accountability"></a>ベスト プラクティス (チーム別) とアカウンタビリティ

企業全体のコスト管理は、クラウド ガバナンスおよびクラウド運用機能です。 ただし、すべてのコスト管理を決定することで、ワークロードをサポートする資産が変更されます。 これらの変更がワークロードのアーキテクチャに影響を与える場合は、エンドユーザーとビジネス機能への影響を最小限に抑えるために、追加の考慮事項が必要になります。 そのワークロードを構成または開発したクラウド導入チームが、これらの種類の変更を完了するためのアカウンタビリティを保持している可能性があります。

この記事では、ベスト プラクティスを 2 つのカテゴリに分類します:運用上のベスト プラクティスとワークロードのベスト プラクティス。 ガバナンス、運用、および導入チームを、コストの最適化のすべての変更に合わせて調整する必要がある一方で、これらの2つのセクションに分離することは、職務の分離が明確であることを示すのに役立ちます。

## <a name="operational-cost-management-best-practices"></a>運用コスト管理のベスト プラクティス

次のベスト プラクティスは、通常、修正プログラムやその他のスケジュールされたメンテナンス プロセスに従って、クラウド ガバナンスまたはクラウド運用チームのメンバーによって実行されます。 これらの各ベスト プラクティスは、この記事の後半で、実行可能なガイダンスにマップされます。

- **タグ付けはすべてのガバナンスにとって重要:** すべてのワークロードとリソースが **[適切な名前付けおよびタグ付け規則](../../ready/azure-best-practices/naming-and-tagging.md)** に従っていることを確認し、[Azure ポリシーを使用してタグ付け規則を適用します](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags)。
- **適切なサイズの機会の特定:** 環境全体の現在のリソース使用率とパフォーマンスの要件を確認して、一定期間 (通常は 90 日以上) にわたって使用されているリソースを特定します。
- **適切なサイズにプロビジョニングされた SKU :** :使用率が低いリソースを、各リソースのパフォーマンス要件をサポートできる最小のインスタンスまたは SKU を使用するように変更します。
- **VM の自動シャットダウン:** VM が継続的に使用されていない場合は、シャットダウンの自動化を検討してください。 VM は削除も使用停止もされませんが、再び有効になるまでコンピューティングとメモリのコストの消費を停止します。
- **すべての非運用資産を自動的にシャットダウンする:** :VM が非運用環境の一部である場合、特に開発環境では、未使用のコストを削減するための自動シャットダウン ポリシーを確立します。 可能な場合は、セルフサービス オプションの開発/テスト ラボを利用して、開発者がコストに関する責任を負うことができるようにします。
- **使用されていないリソースをシャットダウンして使用停止する:** はい、これは 2 回言いました。 リソースが 90 日以上使用されておらず、アップタイムの要件が明確でない場合は、無効にします。 さらに重要なこととして、マシンが停止またはシャットダウンされてから 90 日以上経過した場合は、そのリソースのプロビジョニングを解除して削除します。 * バックアップやその他のメカニズムを使用して、データ保持ポリシーが満たされていることを検証します。
- **孤立したディスクのクリーンアップ:** 未使用のストレージ (特に VM に接続されていない VM ストレージ) を削除します。
- **適切なサイズの冗長性:** リソースに高度な冗長性が必要ない場合は、geo 冗長ストレージを削除します。
- **自動スケール パラメーターの調整:** 運用の監視は、さまざまな資産の使用パターンを明らかにする可能性があります。 これらの使用パターンが自動スケール動作を実行するために使用されるパラメーターにマップされると、運用チームは通常、季節需要や、予算割り当てに対する変更を満たすように自動スケール パラメーターを調整します。 * 重要な事前の注意事項については、「ワークロード コスト管理のベスト プラクティス」を参照してください。

## <a name="workload-cost-management-best-practices"></a>ワークロード コスト管理のベスト プラクティス

アーキテクチャを変更する前に、ワークロードの技術リーダーに問い合わせてください。 [Azure アーキテクチャ レビュー](/assessments/?id=azure-architecture-review) と [Azure アーキテクチャ](/azure/architecture/framework/) フレームワークを使用したワークロードの確認を容易にし、次の種類のアーキテクチャ変更に関する決定について説明します。

- **Azure App Services。** Premium App Service プランの運用上の要件を確認します。 ワークロードのビジネス要件と、基になる資産の構成を理解していないと、Premium App Service プランが必要かどうかを判断するのが困難になります。
- **垂直を上回る水平スケーリング。** 複数の小さいインスタンスを使用すると、1 つの大きなインスタンスを簡単にスケーリングできます。 これによりスケーリングの自動化が可能になり、コストの最適化が実現します。 ただし、ワークロードを水平方向にスケーリングできるようにするには、アプリケーションがべき等であることを技術チームが確認する必要があります。 水平方向のスケールを実現するには、まず、アプリケーションのさまざまなレイヤーのコードと構成を変更する必要があります。
- **自動スケール。** すべての App Service で自動スケールを有効にして、バースト可能な数のより小さな VM を許可します。 自動スケーリングの有効化には、同じべき等要件があるため、ワークロード アーキテクチャに関する知識が必要です。 運用上の変更を行う前に、ワークロードとサポート資産が、水平スケーリングと自動スケーリングについて導入チームによって承認されている必要があります。
- **サーバーレス テクノロジの実装:** VM ワークロードは、多くの場合、ダウンタイムを回避するために "現状のまま" で移行されます。 VM は、断続的で実行期間が短いタスクや、その逆に長時間かかるタスクをホストしている場合もよくあります。 たとえば、Windows タスク スケジューラや PowerShell スクリプトでなどの、スケジュールされたタスクを実行する VM です。 これらのタスクが実行中でないときには、それにもかかわらず VM とディスク ストレージのコストが費やされています。 移行後に、ワークロードのレイヤーを Azure Functions や Azure Batch ジョブなどのサーバーレス テクノロジに再構築することを検討してください。

## <a name="actionable-best-practices"></a>実施可能なベスト プラクティス

この記事の残りの部分では、クラウド ガバナンスまたはクラウド運用チームが企業全体のコストを最適化するために従うことができる運用上のベスト プラクティスについて、戦術的な例を提供します。

## <a name="before-adoption"></a>導入前

ワークロードをクラウドに移動する前に、それらを Azure で実行する毎月のコストを見積もります。 クラウドのコストを先を見越して管理すれば、運営費の予算に準拠する助けになります。 このセクションのベスト プラクティスは、コストの見積もりと、ワークロードをクラウドにデプロイする前に VM およびストレージのサイズの適正化を実行するのに役立ちます。

## <a name="best-practice-estimate-monthly-workload-costs"></a>ベスト プラクティス:毎月のワークロード コストを見積る

Azure リソースの月額料金を予測するために、利用できるツールがいくつかあります。

- **Azure 料金計算ツール:** VM やストレージなど、見積りをする製品を選択します。 料金計算ツールにコストを入力し、見積りを作成します。

 ![Azure 料金計算ツール](../../migrate/azure-best-practices/media/migrate-best-practices-costs/pricing.png) *Azure 料金計算ツール*

- **Azure Migrate:** コストを見積もるには、Azure でワークロードを実行するために必要なすべてのリソースを確認し、それらを計上します。 このデータを取得するには、サーバー、VM、データベース、ストレージを含む資産のインベントリを作成します。 この情報は、Azure Migrate を使用して収集できます。

  - Azure Migrate は、オンプレミス環境で検出と評価を行ってインベントリを提供します。
  - Azure Migrate では、全体像を把握できるように、VM 間の依存関係をマップして表示できます。
  - Azure Migrate の評価には、推定コストが含まれています。
    - **コンピューティング コスト:** Azure Migrate は、評価の作成時には推奨される Azure VM のサイズを採用し、Billing API を使用して VM の推定月間コストを計算します。 この見積りでは、オペレーティング システム、ソフトウェア アシュアランス、予約インスタンス、VM のアップタイム、場所、および通貨の設定が考慮されます。 評価に含まれるすべての VM にわたるコストが集計され、月間コンピューティング コストの合計が計算されます。
    - **ストレージ コスト:** Azure Migrate は、評価に含まれるすべての VM のストレージ コストを集計して、月間ストレージ コストの合計を計算します。 特定のマシンの月間ストレージ コストは、そのマシンに接続されているすべてのディスクの月間コストを集計することで計算できます。

    ![Azure Migrate](../../migrate/azure-best-practices/media/migrate-best-practices-costs/assess.png)
    "*Azure Migrate の評価*"

**詳細情報:**

- [Azure 料金計算ツール](https://azure.microsoft.com/pricing/calculator)を使用します。
- [Azure Migrate の概要](https://docs.microsoft.com/azure/migrate/migrate-overview)を確認します。
- [Azure Migrate の評価](https://docs.microsoft.com/azure/migrate/concepts-assessment-calculation)についてのページを読みます。
- [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) の詳細について確認します。

## <a name="best-practice-right-size-vms"></a>ベスト プラクティス:適切なサイズの VM

ワークロードをサポートする Azure VM をデプロイするときは、さまざまなオプションを選択できます。 各種類の VM には特定の機能があり、さまざまな組み合わせの CPU、メモリ、およびディスクが用意されています。 VM は以下のようにグループ化されます。

**Type** | **詳細** | **用途**
--- | --- | ---
**汎用** | CPU とメモリのバランスがとれています。 | テストと開発、中小規模のデータベース、トラフィック量が中小程度の Web サーバーに適しています。
**コンピューティング最適化** | メモリに対する CPU の比が大きくなっています。 | トラフィック量が中程度の Web サーバー、ネットワーク アプライアンス、バッチ処理、アプリ サーバーに適しています。
**メモリ最適化** | 高いメモリ対 CPU。 | リレーショナル データベース、中から大規模のキャッシュ、インメモリ分析に適しています。
**ストレージの最適化** | 高いディスク スループットと IO。 | ビッグ データ、SQL、および NoSQL のデータベースに適しています。
**GPU の最適化** | 特殊な VM。 1 つまたは複数の GPU。 | 大量のグラフィックスおよびビデオの編集。
**高性能** | 最も高速で最も強力な CPU。 オプションの、高スループットのネットワーク インターフェイス (RDMA) を備えた VM | クリティカルな高性能アプリ。

- これらの VM 間の価格の違いと、長期的な予算への影響を理解しておくことが重要です。
- 種類ごとに、内部にいくつかの VM シリーズがあります。
- さらに、あるシリーズ内の VM を選択すると、そのシリーズ内の VM のみをスケールアップまたはスケールダウンできます。 たとえば、DSv2\_2 は DSv2\_4 にスケールアップできますが、Fsv2\_2 などの異なるシリーズには変更できません。

**詳細情報:**

- [VM の種類とサイズ設定](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)、およびサイズの種類へのマップに関する詳細を確認します。
- [VM のサイズ変更](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs)を計画します。
- [架空の Contoso 社の評価サンプル](../../plan/contoso-migration-assessment.md)を確認します。

## <a name="best-practice-select-the-right-storage"></a>ベスト プラクティス:適切なストレージを選択する

オンプレミス ストレージ (SAN または NAS) とそれらをサポートするネットワークのチューニングと維持管理は、コストが高く時間がかかる場合があります。 ファイル (ストレージ) のデータは、一般に、運用と管理の負担を軽減するため、クラウドに移行されます。 Microsoft では、Azure にデータを移動するためのオプションをいくつか提供しており、それらのオプションについて決定する必要があります。 データにとって適切なストレージの種類を選択すれば、組織は毎月数千ドルを節約できます。 いくつかの考慮事項があります。

- あまりアクセスされないデータやビジネス クリティカルでないデータは、最も高価なストレージに配置する必要がありません。
- 逆に、重要なビジネス クリティカル データは、より高いレベルのストレージ オプションに配置する必要があります。
- 導入計画時には、最適なストレージにマップするために、データのインベントリを作成し、重要度で分類します。 予算とコストに加えて、パフォーマンスを考慮に入れます。 コストは、必ずしも主な意思決定要因ではないでしょう。 最小コストのオプションを選択すると、ワークロードがパフォーマンスと可用性のリスクにさらされる可能性があります。

### <a name="storage-data-types"></a>ストレージのデータの種類

Azure では、ストレージ データのさまざまな種類が提供されています。

<!--markdownlint-disable MD033 -->

**データの種類** | **詳細** | **使用方法**
--- | --- |  ---
**BLOB** | テキスト データやバイナリ データなどの大量の非構造化オブジェクトを格納するために最適化されています<br/><br/> | HTTP/HTTPS 経由でどこからでもデータにアクセスします。 | ストリーミングやランダム アクセスのシナリオに使用します。 たとえば、イメージやドキュメントをブラウザーに直接提供する、ビデオやオーディオをストリーム配信する、バックアップやディザスター リカバリーのデータを格納するなどです。
**[ファイル]** | マネージド ファイル共有は SMB 3.0 経由でアクセスされます | オンプレミスのファイル共有を移行する場合に、ファイル データへの複数アクセス/接続を提供するために使用します。
**ディスク** | ページ BLOB に基づきます。<br/><br/> ディスクの種類 (速度):Standard (HDD または SSD) または Premium (SSD)。<br/><br/>ディスクの管理:アンマネージド (ユーザーがディスクの設定とストレージを管理する) またはマネージド (ユーザーがディスクの種類を選択し、Azure 側でディスクを管理する)。 | VM には Premium ディスクを使用します。 簡単な管理とスケーリングのためにはマネージド ディスクを使用します。
**キュー** | 認証された呼び出し (HTTP または HTTPS) を介してアクセスされる大量のメッセージを格納および取得します | 非同期メッセージ キューを使用してアプリのコンポーネントを接続します。
**テーブル** | テーブルを格納します。 | 現在では Azure Cosmos DB Table API の一部です。

<!--markdownlint-enable MD033 -->

### <a name="access-tiers"></a>アクセス層

Azure のストレージには、ブロック BLOB データにアクセスするためのさまざまなオプションが用意されています。 レベルに合った適切なアクセス層を選択することで、最も費用対効果の高い方法でブロック BLOB データが格納されるようにする助けとなります。

<!--markdownlint-disable MD033 -->

**Type** | **詳細** | **使用方法**
--- | --- | ---
**ホット** | ストレージ コストはクールより高いです。 アクセス料金はクールよりも低いです。<br/><br/>これが既定のレベルです。 | 頻繁にアクセスされる、アクティブに使用中のデータに使用します。
**クール** | ストレージ コストはホットより低いです。 アクセス料金はホットよりも高いです。<br/><br/> 少なくとも 30 日間格納します。 | 短期に格納し、データは使用できますが、アクセス頻度は低いものです。
**Archive** | 個々 のブロック BLOB に使用されます。<br/><br/> 最も費用対効果の高いストレージ オプション。 データ アクセスは、ホットとコールドよりも高価です。 | 取得の待ち時間としてのサーバー時間を許容でき、少なくとも 180 日間同じレベルに留まるデータに使用します。

<!--markdownlint-enable MD033 -->

### <a name="storage-account-types"></a>ストレージ アカウントの種類

Azure では、さまざまな種類のストレージ アカウントとパフォーマンス レベルが提供されています。

<!--markdownlint-disable MD033 -->

**アカウントの種類** | **詳細** | **使用方法**
--- | --- | ---
**General Purpose v2 Standard** | BLOB (ブロック、ページ、追加)、ファイル、ディスク、キュー、およびテーブルをサポートしています。<br/><br/> ホット、クール、およびアーカイブのアクセス層をサポートしています。 ゾーン冗長ストレージ (ZRS) がサポートされています。 | ほとんどのシナリオの、ほとんどの種類のデータに使用します。 Standard ストレージ アカウントは、HDD または SSD ベースとして指定できます。
**General Purpose v2 Premium** | BLOB ストレージ データ (ページ BLOB) をサポートしています。 ホット、クール、およびアーカイブのアクセス層をサポートしています。 ZRS がサポートされています。<br/><br/> SSD に格納されます。 | すべての VM のために使用することをお勧めします。
**General Purpose v1** | アクセスの階層化はサポートされません。 ZRS をサポートしていません | アプリに Azure クラシック デプロイ モデルが必要な場合に使用します。
**BLOB** | 非構造化オブジェクトを格納するための特殊なストレージ アカウント。 ブロック BLOB と 追加 BLOB のみを提供します (ファイル、キュー、テーブル、ディスクのストレージ サービスはありません)。 同じ持続性、可用性、スケーラビリティ、および General Purpose v2 と同じパフォーマンスを提供します。 | これらのアカウントにページ BLOB を格納することはできないため、VHD ファイルは格納できません。 アクセス層はホットまたはクールに設定できます。

<!--markdownlint-enable MD033 -->

### <a name="storage-redundancy-options"></a>ストレージ冗長オプション

ストレージ アカウントでは、回復力と高可用性のためにさまざまな種類の冗長性を使用できます。

**Type** | **詳細** | **使用方法**
--- | --- | ---
**ローカル冗長ストレージ (LRS)** | 1 つのストレージ単位内で、別個の障害ドメインと更新ドメインにレプリケートすることで、ローカルの障害から保護します。 1 つのデータ センター内に複数のデータコピーを保管します。 オブジェクトに年間 99.999999999% (9 が 11 個) 以上の持続性を提供します。 | アプリが格納するデータは簡単に再構築できるものかどうかを考慮に入れます。
**ゾーン冗長ストレージ (ZRS)** | 1 つのリージョン内の 3 つのストレージ クラスター間でレプリケートすることで、データ センター停止の保護に冗長性を持たせます。 各ストレージ クラスターは、物理的に分離されており、独自の可用性ゾーン内に置かれています。 複数のデータセンターまたはリージョンにわたってデータのコピーを複数保持することで、年間 99.9999999999% (9 が 12 個) 以上のオブジェクトの持続性を提供します。 | 一貫性、持続性、および高可用性が必要かどうかを考慮します。 複数のゾーンが永続的に影響を受けるリージョンの災害からは保護されないことがあります。
**geo 冗長ストレージ (GRS)** | プライマリから数百マイル離れたセカンダリ リージョンにデータをレプリケートすることで、リージョン全体の障害から保護します。 オブジェクトに年間 99.99999999999999% (9 が 16 個) 以上の持続性を提供します。 | Microsoft がセカンダリ リージョンへのフェールオーバーを開始しない限り、レプリカは使用できません。 フェールオーバーが発生した場合、読み取りと書き込みのアクセスは可能です。
**読み取りアクセス geo 冗長ストレージ (RA-GRS)** | GRS に似ています。 オブジェクトに年間 99.99999999999999% (9 が 16 個) 以上の持続性を提供します | GRS で使用される 2 番目のリージョンからの読み取りアクセスを許可することで、99.99% の読み取り可用性を提供します。

**詳細情報:**

- Azure Storage の料金を[確認します](https://azure.microsoft.com/pricing/details/storage)。
- 大量のデータの Azure BLOB とファイルへの導入に関して、Azure Import/Export の[詳細を確認します](https://docs.microsoft.com/azure/storage/common/storage-import-export-service)。
- ストレージ データの種類の、BLOB、ファイル、およびディスクを[比較します](https://docs.microsoft.com/azure/storage/common/storage-introduction?toc=/azure/storage/blobs/toc.json)。
- アクセス レベルの[詳細を確認します](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers)。
- さまざまな種類のストレージ アカウントを[確認します](https://docs.microsoft.com/azure/storage/common/storage-account-overview?toc=/azure/storage/blobs/toc.json)。
- LRS、ZRS、GRS、読み取りアクセス GRS など、[Azure Storage の冗長性](https://docs.microsoft.com/azure/storage/common/storage-redundancy)について説明します。
- [Azure Files](https://docs.microsoft.com/azure/storage/files/storage-files-introduction) の詳細を確認します。

## <a name="after-adoption"></a>導入後

導入前のコスト予測は、ワークロード所有者とクラウド導入チームによって行われた決定に依存しています。 ガバナンス チームはこれらの決定に影響を与えることができますが、ガバナンス チームが取るべきアクションはほとんどありません。

リソースが運用環境に配置されると、データを集計したり、環境レベルで傾向を分析したりできます。 このデータは、実際の使用パターンと現在の状態のアーキテクチャに基づいて、ガバナンス チームがサイズと使用の決定を個別に行うのに役立ちます。

- データを分析して、Azure のリソース グループとリソースについての予算ベースラインを生成します。
- さらにコストを削減するために、リソースのサイズを減らしたり停止/一時停止したりできる使用パターンを特定します。

このセクションのベスト プラクティスには、Azure ハイブリッド特典と予約 VM の使用、複数のサブスクリプションにわたるクラウドの支出の削減、コストの予算管理と分析での Azure Cost Management の使用、リソースの監視とリソース グループ予算の実施、および監視、ストレージ、VM の最適化が含まれます。

## <a name="best-practice-take-advantage-of-azure-hybrid-benefits"></a>ベスト プラクティス:Azure ハイブリッド特典を活用する

Windows Server や SQL Server などのシステムへのソフトウェア投資により、Microsoft は、クラウドで顧客価値を提供する特別な立場にあり、他のクラウド プロバイダーが提供できるとは限らない大幅な割引を実現しています。

Microsoft の統合されたオンプレミス/Azure 製品ポートフォリオによって、競争上とコスト上の長所が生み出されています。 オペレーティング システム、またはソフトウェア アシュアランス (SA) を通したその他のソフトウェア ライセンスを現在所有している場合は、Azure ハイブリッド特典によって、クラウドへの移行時にそれらのライセンスをクラウドに移動できます。

**詳細情報:**

- ハイブリッド特典の節約額計算ツールを[見てみます](https://azure.microsoft.com/pricing/hybrid-benefit)。
- Windows Server 向けのハイブリッド特典の[詳細を確認します](https://azure.microsoft.com/pricing/hybrid-benefit)。
- SQL Server Azure VM の料金ガイダンスを[確認します](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance)。

## <a name="best-practice-use-reserved-vm-instances"></a>ベスト プラクティス:予約 VM インスタンスを使用する

ほとんどのクラウド プラットフォームは、従量課金制で提供されています。 動的なワークロードがどのようになるか分かっているとは限らないため、このモデルには不利な点があります。 ワークロードの明確な意図を指定すれば、インフラストラクチャの計画に貢献することになります。

Azure 予約 VM インスタンスを使用して、1 年または 3 年の期間の VM インスタンスに対して前払いします。

- 前払いにより、使用するリソースに関して割引が提供されます。
- VM、SQL データベースのコンピューティング、Azure Cosmos DB、またはその他のリソース コストを、従量課金制の料金の最大 72% まで大幅に削減できます。
- 予約は課金割引を提供するもので、リソースの実行時の状態には影響しません。
- 予約インスタンスはキャンセルできます。

![予約インスタンス](../../migrate/azure-best-practices/media/migrate-best-practices-costs/reserve.png)
*Azure 予約 VM*

**詳細情報:**

- Azure の予約の[詳細を確認します](https://docs.microsoft.com/azure/billing/billing-save-compute-costs-reservations)。
- 予約インスタンスの FAQ を[読みます](https://azure.microsoft.com/pricing/reserved-vm-instances/#faq)。
- SQL Server Azure VM の[料金ガイダンスを表示します](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance)。

## <a name="best-practice-aggregate-cloud-spend-across-subscriptions"></a>ベスト プラクティス:サブスクリプション間のクラウド支出を集約する

最終的に複数の Azure サブスクリプションを利用することになるのは避けられません。 たとえば、開発と運用の境界を分けるために追加のサブスクリプションが必要な場合があります。また、クライアントごとに別個のサブスクリプションを必要とするプラットフォームがある場合もあります。 すべてのサブスクリプションにわたってデータのレポート作成を 1 つのプラットフォームに集約する機能があるのは、有用な特徴です。

これを行うために、Azure Cost Management API を使用できます。 その後、Azure SQL などの 1 つのソースにデータを集約したら、Power BI などのツールを使用して、集約されたデータを明示できます。 集約されたサブスクリプション レポートや、きめ細かなレポートを作成できます。 たとえば、コスト管理に関する事前対応のための分析情報が必要なユーザーのために、部門、リソース グループ、またはその他の情報に基づいて、コストに関する特定のビューを作成できます。 彼らに Azure の課金データへのフル アクセスを提供する必要はありません。

**詳細情報:**

- Azure Consumption API の[概要を確認します](https://docs.microsoft.com/azure/billing/billing-consumption-api-overview)。
- Power BI Desktop で Azure Consumption Insights に接続すること[について学びます](https://docs.microsoft.com/power-bi/desktop-connect-azure-consumption-insights)。
- ロール ベースのアクセス制御 (RBAC) を使用して、Azure の課金情報へのアクセスを管理する[方法について学びます](https://docs.microsoft.com/azure/billing/billing-manage-access)。

## <a name="best-practice-monitor-resource-utilization"></a>ベスト プラクティス:リソースの使用率を監視する

Azure では、リソースが消費されたときに使用した分だけ支払いを行います。そうでないときに支払いはしません。 VM の場合、VM が割り当てられているときに課金が発生し、VM の割り当てが解除された後は課金されません。 これを念頭に置いて使用中の VM を監視し、VM のサイズ設定を確認します。

- ベースラインを特定するために、継続的に VM のワークロードを評価します。
- たとえば、月曜日から金曜日の午前 8 時から午後 6 時まではワークロードの用頻度が高く、それ以外の時間帯はほとんど使用されない場合は、ピーク時間帯以外はVM をダウングレードできます。 これは、VM のサイズを変更すること、または仮想マシン スケール セットを使用して VM の上下の自動スケーリングを行うことを意味する場合もあります。
- 一部の企業は、いつ使用可能な必要があり、いつ必要でないかを指定するカレンダーに VM を置くことで、VM を "眠らせ" ます。
- VM の監視に加えて、利用不足や使いすぎが起きていないか、ExpressRoute や仮想ネットワーク ゲートウェイなどの他のネットワーク リソースを監視する必要があります。
- Azure Cost Management、Azure Monitor、Azure Advisor などの Microsoft ツールを使用して VM の使用状況を監視できます。 サードパーティ製のツールも使用できます。

**詳細情報:**

- [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) と [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) の概要を表示しますします。
- Advisor のコストに関する推奨事項を[表示します](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations)。
- [推奨事項に従ってコストを最適化](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=/azure/billing/toc.json)し、[予期しない料金を防ぐ](https://docs.microsoft.com/azure/billing/billing-getting-started)方法を学びます。
- [Azure Resource Optimization (ARO) ツールキット](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit)について学びます。

## <a name="best-practice-reduce-non-production-costs"></a>ベスト プラクティス:非運用コストの削減

開発サイクル中は、開発、テスト、品質保証 (QA) の環境が必要です。 残念ながら、それらの環境は、役に立たなかった後もプロビジョニングされたままになることがよくあります。 使用されていない非運用環境を定期的に確認すると、コストにすぐに影響が及ぶ可能性があります。

また、非運用環境では、一般コストを削減することを検討してください。

- 低コストの B シリーズ VM と標準ストレージを使用するために、非運用環境のリソースを削減します。
- Azure ポリシーを適用して、非運用リソースのリソース レベルのコスト削減を要求します。

**詳細情報:**

- [タグを使用](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources)して、サイズ変更や終了のための開発、テスト、または QA のターゲットを特定します。
- [VM の自動シャットダウン](https://docs.microsoft.com/azure/cost-management-billing/manage/getting-started#consider-cost-cutting-features-like-auto-shutdown-for-vms)により、VM の終了時間を夜間に設定します。 この機能を使用すると、非運用 VM が毎晩停止されるため、開発を再開する準備ができたら、開発者はこれらの VM を再起動する必要があります。
- 開発チームは、[Azure DevTest Labs](https://docs.microsoft.com/azure/lab-services/devtest-lab-overview) を使用して独自のコスト管理アプローチを確立し、前のステップの標準の自動シャットダウンのタイミングの影響を回避することをお勧めします。

## <a name="best-practice-use-azure-cost-management"></a>ベスト プラクティス:Azure Cost Management を使用する

Microsoft では、支出を追跡する助けとなる Azure Cost Management を提供しています。

- Azure の支出の監視と管理を行い、リソースの使用を最適化する助けになります。
- サブスクリプション全体と、そのすべてのリソースが見直されて、推奨事項が示されます。
- 外部ツールやレポート用の財務システムと統合するための完全な API を提供します。
- リソースの使用状況を追跡し、1 つの統一されたビューでクラウドのコストを管理します。
- 情報に基づいた決定を下しやすいように、運用と財務に関する豊富な分析情報が提供されます。

Cost Management では以下のことが可能です。

- **予算を作成する:** 財務上の説明責任のために予算を作成します。
  - 特定の期間 (月単位、四半期単位、年単位) と範囲 (サブスクリプション/リソース グループ) について、使用またはサブスクライブしているサービスを計算に入れることができます。 たとえば、月、四半期、または年の期間の Azure サブスクリプション予算を作成できます。
    - 作成した予算は、コストの分析に表示されます。 現在の支出に対する予算を表示することは、コストや支出を分析するときに必要な最初の手順の 1 つです。
  - 予算がしきい値に達したときに電子メールの通知を送信できます。
  - コスト管理データは、分析のために Azure のストレージにエクスポートできます。

    ![Cost Management の予算](../../migrate/azure-best-practices/media/migrate-best-practices-costs/budget.png)
    "*Azure Cost Management の予算*"

- **コスト分析を行う:** コスト分析を取得し、組織のコストを探って分析すれば、コストがどのように生じるかを理解し、支出の傾向を識別する助けになります。
  - EA ユーザーがコスト分析を使用できます。
  - 部門、アカウント、サブスクリプション、リソース グループを含む多様な範囲別に、コスト分析データを表示できます。
  - 現在の月の総コストと、毎日の累積コストを表示するコスト分析を取得できます。

    ![Cost Management での分析](../../migrate/azure-best-practices/media/migrate-best-practices-costs/analysis.png)
    "*Azure Cost Management での分析*"

- **推奨事項を取得する:** 最適化と効率向上が可能な方法を示す Advisor の推奨事項を取得します。

**詳細情報:**

- Azure Cost Management の[概要を表示します](https://docs.microsoft.com/azure/cost-management/overview)。
- Azure Cost Management を使用してクラウドへの投資を最適化する[方法を学びます](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices)。
- Azure Cost Management のレポートを使用する[方法を学びます](https://docs.microsoft.com/azure/cost-management/use-reports)。
- 推奨事項に従ってコストを最適化することに関する[チュートリアルを表示します](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=/azure/billing/toc.json)。
- Azure Consumption API について[確認します](https://docs.microsoft.com/rest/api/consumption/budgets)。

## <a name="best-practice-implement-resource-group-budgets"></a>ベスト プラクティス:リソース グループの予算を実施する

多くの場合、リソース グループはコストの境界を表すために使用されます。 この使用パターンと共に、Azure チームは、リソース グループとリソースでの予算を作成する機能など、さまざまなレベルでリソースの支出を追跡して分析する、新しい強化された方法を引き続き開発しています。

- リソース グループの予算は、リソース グループに関連するコストを追跡するのに役立ちます。
- 予算に達したか予算を超えたときにアラートをトリガーし、さまざまなプレイブックを実行できます。

**詳細情報:**

- Azure Budgets でコストを管理する[方法を学びます](https://docs.microsoft.com/azure/billing/billing-cost-management-budget-scenario)。
- [チュートリアルに従って](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/billing/toc.json)、Azure の予算を作成して管理します。

## <a name="best-practice-review-azure-advisor-recommendations"></a>ベスト プラクティス:Azure Advisor の推奨事項を確認する

Azure Advisor のコストに関する推奨事項によって、コストを削減する機会が特定されます。 予算が高いように見えたり使用率が低いように見えたりする場合は、このレポートを使用して、コストをすばやく調整するための迅速な機会を見つけることができます。

**詳細情報:**

- アクションを即座に実行するため、[Azure Advisor のコストに関する推奨事項を確認します](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations)。

## <a name="best-practice-optimize-azure-monitor-retention"></a>ベスト プラクティス:Azure Monitor の保持期間を最適化する

Azure にリソースを移動し、それらの診断ログを有効にすると、大量のログ データが生成されます。 通常、このログ データは、Log Analytics ワークスペースにマップされているストレージ アカウントに送信されます。

- ログ データの保持期間が長いほど、より多くのデータを持つことになります。
- すべてのログ データが一様なわけではなく、一部のリソースは他よりも多くのログ データを生成します。
- 規制とコンプライアンスのため、おそらく一部のリソースのログ データは、他のデータよりも長く保持する必要があります。
- ログのストレージ コストを最適化することと、必要なログ データを保管することのバランスを取ります。
- 移行の完了直後にログ記録を評価して設定を行うことをお勧めします。そうすることで、重要でないログの保持にコストがかからなくなります。

**詳細情報:**

- 使用量と推定コストの監視[について学びます](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-usage-and-estimated-costs)。

## <a name="best-practice-optimize-storage"></a>ベスト プラクティス:ストレージを最適化する

導入の前にベスト プラクティスに従ってストレージを選択した場合は、おそらくいくつかの利点を得ることになります。 ただし十中八九は、まだ最適化できるその他のストレージ コストがあります。 BLOB やファイルは時間の経過と共に古くなります。 データがもはや使用されない可能性もありますが、規制の要件のため、データを一定期間保管する必要がある可能性があります。 そのため、元の導入に使用したパフォーマンスが高いストレージにデータを格納する必要がない場合があります。

古いデータを識別して、より低コストのストレージ領域に移動することが、月単位のストレージ予算とコスト削減に大きな影響を及ぼすことがあります。 Azure では、こうした古いデータを識別して格納する場合に役立つ方法を多数提供しています。

- 重要度の低いデータをホット アクセス層からクールやアーカイブのアクセス層に移動することで、汎用 v2 ストレージのアクセス層を活用します。
- カスタマイズしたポリシーに基づいて古いデータを移動しやすくなるように、StorSimple を使用します。

**詳細情報:**

- アクセス レベルの[詳細を確認します](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers)。
- StorSimple と、[StorSimple の価格](https://azure.microsoft.com/pricing/details/storsimple)の[概要を確認します](https://docs.microsoft.com/azure/azure-monitor/overview)。

## <a name="best-practice-automate-vm-optimization"></a>ベスト プラクティス:VM の最適化を自動化する

クラウドで VM を実行する場合の最終目標は、VM が使用する CPU、メモリ、およびディスクを最大利用することです。 最適化されていない VM を検出した場合や、VM が使用されていない期間が頻繁にある場合は、それらの VM を、シャット ダウンするか、仮想マシン スケール セットを使用してスケールダウンすることが理にかなっています。

VM は、Azure Automation、仮想マシン スケール セット、自動シャット ダウン、スクリプト型のソリューション、サード パーティ製のソリューションを使用して最適化できます。

**詳細情報:**

- 垂直方向の自動スケーリングを使用[する方法を学びます](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-vertical-scale-reprovision)。
- VM の自動開始を[スケジュールします](https://azure.microsoft.com/updates/azure-devtest-labs-schedule-vm-auto-start)。
- Azure Automation で業務時間外の VM を開始または停止する[方法を学びます](https://docs.microsoft.com/azure/automation/automation-solution-vm-management)。
- [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) と [Azure Resource Optimization (ARO) ツールキット](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit)に関する[詳細情報を表示します]。

## <a name="best-practices-use-logic-apps-and-runbooks-with-budgets-api"></a>ベスト プラクティス:Budgets API によって Logic Apps と Runbook を使用する

Azure では、テナント課金情報にアクセスできる REST API が提供されています。

- Budgets API を使用して、外部システムとワークフローを統合できます。これらは、作成したメトリックによって API データからトリガーされます。
- 使用状況やリソースに関するデータを、お使いのデータ分析ツールで取得できます。
- Azure Resource Usage API と Azure Resource RateCard API は、コストを正確に予測して管理するうえで役立ちます。
- これらの API はリソース プロバイダーとして実装されていて、Azure Resource Manager が公開している API に含まれています。
- Budgets API は、Azure Logic Apps や Runbook と統合できます。

**詳細情報:**

- Budgets API の[詳細について学びます](https://docs.microsoft.com/rest/api/consumption/budgets)。
- Billing API を使用して Azure の使用状況の[分析情報を取得します](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview)。


## <a name="next-steps"></a>次のステップ

ベスト プラクティスを理解したうえで、[Cost Management ツールチェーン](./toolchain.md)を調べて、これらのベスト プラクティスを実行するのに役立つ Azure のツールと機能を特定します。

> [!div class="nextstepaction"]
> [Azure 向けコスト管理ツールチェーン](./toolchain.md)