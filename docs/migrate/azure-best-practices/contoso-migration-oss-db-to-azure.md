---
title: オープンソース データベースを Azure に移行する
description: Contoso によって、オンプレミスのオープンソース データベースが Azure にどのように移行されたかについて学習します。
author: deltadan
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 1dcff70eaf185d59592682bdb61d777bf7dd0795
ms.sourcegitcommit: c1d6c1c777475f92a3f8be6def84f1779648a55c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/21/2020
ms.locfileid: "92334614"
---
# <a name="migrate-open-source-databases-to-azure"></a>オープンソース データベースを Azure に移行する

この記事では、架空の会社である Contoso が、さまざまなオンプレミス オープンソース データベースの Azure への移行をどのように評価、計画し、実行したかについて説明します。

Azure への移行を検討する際、Contoso では技術的および財務的な評価を実行して、オンプレミスのワークロードがクラウドへの移行に適しているかどうかを確認する必要があります。 Contoso 社のチームは特に、移行対象のマシンおよびデータベースの互換性を評価する必要があります。 また、Azure で Contoso のリソースを実行するための容量とコストを見積もる必要があります。

## <a name="business-drivers"></a>ビジネス ドライバー

Contoso では、自社のネットワーク上に存在する多種多様なバージョンのオープン ソース データベース ワークロードを維持するために、さまざまな問題が発生しています。 最近の投資家との会合の後、CFO と CTO は、これらすべてのワークロードを Azure に移行することを決定しました。 これにより、構造化された資本費用モデルから流動的な運用費用モデルに移行します。

IT リーダーシップ チームは、ビジネス パートナーと密接に連絡を取り合い、ビジネス面および技術面での要件を次のように理解しました。 目的は次のとおりです。

- **セキュリティを強化する。** Contoso では、すべてのデータ リソースを、よりタイムリーかつ効率的な方法で監視および保護できる必要があります。 また、この会社は、データベース アクセス パターンに対して、より集中管理されたレポート システムをセットアップしたいとも考えています。
- **コンピューティング リソースを最適化する。** Contoso では、大規模なオンプレミスのサーバー インフラストラクチャをデプロイしてきました。 会社の SQL Server インスタンスの中には、割り当てられた基になる CPU、メモリ、ディスクを消費してはいるものの、実際には効率的に使用していないものがいくつかあります。
- **効率化。** Contoso では、不要な手順を取り除き、開発者とユーザーのプロセスを効率化する必要があります。 ビジネス部門は、顧客の要求により迅速に対応するために、IT 部門に対して、時間やコストを無駄にせず、迅速に作業を行うことを求めています。 移行後のデータベース管理は、削減するか、最小限に抑える必要があります。
- **機敏性の向上。** Contoso IT は、ビジネス部門の要求に対して、対応力を向上させる必要があります。 また、グローバル経済で成功を収めるために、市場の変化よりも迅速に対応する必要があります。 ビジネスの妨げや、障害にならないようにする必要があります。
- **スケール。** ビジネスが順調に成長している中で、Contoso IT 部門は、同じペースで拡張するシステムを提供する必要があります。
- **コストを把握する。** ビジネスおよびアプリケーションの所有者は、オンプレミスでアプリケーションを実行する場合と比較して、クラウドのコストが高くなって行き詰まることを避けたいと考えています。

## <a name="migration-goals"></a>移行の目標

Contoso のクラウド チームは、さまざまな移行の目標を設定しました。 これらの目標は最良の移行方法を決定するために使用されました。

| 必要条件 | 詳細 |
| --- | --- |
| **パフォーマンス** | 移行後も、Azure 内のアプリケーションには、Contoso のオンプレミス環境で現在提供されているのと同じパフォーマンス能力が必要です。 クラウドに移行するのは、そのアプリケーションのパフォーマンスがそれほど重要でないからではありません。 |
| **互換性** | Contoso では、自社のアプリケーションおよびデータベースと Azure との互換性を理解する必要があります。 また、Contoso では Azure ホスティングのオプションについても理解する必要があります。 |
| **[データ ソース]** | すべてのデータベースは例外なく、Azure に移動されます。 使用中の SQL 機能のデータベースおよびアプリケーション分析に基づいて、サービスとしてのプラットフォーム (PaaS) またはサービスとしてのインフラストラクチャ (IaaS) に移動します。 すべてのデータベースを移動する必要があります。 |
| **Application** | アプリケーションは、可能な限りクラウドに移動する必要があります。 移動できない場合、移行されたデータベースには Azure ネットワーク経由でプライベート接続を使用してのみ接続します。 |
| **コスト** | Contoso は移行オプションだけでなく、インフラストラクチャをクラウドに移動した後のインフラストラクチャに関連するコストも理解する必要があります。 |
| **管理** | 移行されるすべてのデータベースを管理するためにリソース グループと共に、さまざまな部門に対してリソース管理グループを作成する必要があります。 すべてのリソースには、チャージバック要件のために部門の情報をタグ付けする必要があります。 |
| **制限事項** | 最初は、アプリケーションを実行するすべての支店に Azure への直接 ExpressRoute リンクがあるわけではありません。 これらの支店からは、仮想ネットワーク ゲートウェイ経由で接続する必要があります。 |

## <a name="solution-design"></a>ソリューション設計

Contoso では、[Azure Migrate](/azure/migrate/migrate-services-overview) を使用して、自社のデジタル資産の[移行評価](../..//plan/contoso-migration-assessment.md)を既に実行しました。

![移行プロセスを示す図。](./media/contoso-migration-oss-db-to-azure/migration-process.png)
_図 1: 移行プロセス。_

### <a name="solution-review"></a>ソリューションのレビュー

Contoso は、長所と短所の一覧をまとめて、提案されたデザインを評価します。

| 考慮事項 | 詳細 |
| --- | --- |
| **長所** | Azure では、データベース ワークロードを一元的に確認できます。 <br><br> コストは Azure Cost Management + Billing によって監視されます。 <br><br> ビジネスのチャージバック課金は、Azure Billing API シリーズを使用して簡単に実行できます。 <br><br> サーバーとソフトウェアのメンテナンスは、IaaS ベースの環境のみに限定されます。 |
| **短所** | IaaS ベースの VM の要件により、これらのコンピューター上では引き続きソフトウェアを管理する必要があります。 |

### <a name="budget-and-management"></a>予算と管理

移行を実行する前に、ソリューションの管理と課金の側面をサポートするために、必要な Azure 構造を整える必要があります。

管理要件については、組織の構造をサポートするために、いくつかの[管理グループ](/azure/governance/management-groups/overview)が作成されました。

課金要件については、各 Azure リソースに、該当する課金タグが[タグ付け](/azure/azure-resource-manager/management/tag-resources)されます。

### <a name="migration-process"></a>移行プロセス

データの移行は、標準的で反復可能なパターンに従います。 このプロセスには、[Microsoft のベスト プラクティス](https://datamigration.microsoft.com/)に基づく次の手順が含まれます。

- 移行前:
  - **検出:** インベントリ データベース資産とアプリケーション スタック。
  - **評価:** ワークロードを評価し、推奨事項を修正します。
  - **変換:** ターゲットで動作するようにソース スキーマを変換します。
- 移行:
  - **移行:** ソース スキーマ、ソース データ、オブジェクトをターゲットに移行します。
  - **データの同期:** データを同期します (ダウンタイムを最小限に抑えるため)。
  - **カットオーバー:** ソースからターゲットにカット オーバーします。
- 移行後:
  - **アプリケーションの修復:** アプリケーションに対して、必要な変更を繰り返し実行します。
  - **テストの実行:** 機能とパフォーマンスのテストを繰り返し実行します。
  - **最適化:** テストに基づいて、パフォーマンスの問題に対処し、パフォーマンスの向上を確認するために再テストします。
  - **資産の廃止:** 古い VM とホスティング環境がバックアップされ、廃止されます。

#### <a name="step-1-discovery"></a>手順 1:探索

Contoso では、Azure Migrate を使用して、Contoso 環境全体の依存関係を明らかにしました。 Azure Migrate によって、Windows および Linux システム上のアプリケーション コンポーネントが自動的に検出され、サービス間の通信がマップされました。 Contoso サーバー間の接続、プロセス、インバウンド接続とアウトバウンド接続の待ち時間、TCP 接続アーキテクチャ全体のポートも Azure Migrate によって明らかになりました。 Contoso で必要な作業は、[Microsoft Monitoring Agent](/azure/azure-monitor/platform/agent-windows) および [Microsoft Dependency Agent](/azure/azure-monitor/insights/vminsights-enable-hybrid#install-the-dependency-agent-on-windows) をインストールすることだけでした。

Contoso によって、移行する必要がある 300 個を超えるデータベース インスタンスが特定されました。 これらのインスタンスのうち約 40% は、PaaS ベースのサービスに移行できます。 残りの 60% は、各データベース ソフトウェアを実行する VM を使用して、IaaS ベースのアプローチに移行する必要があります。

#### <a name="step-2-application-assessment"></a>手順 2:アプリケーション評価

評価の結果は、主に Java、PHP、および Node.js アプリケーションを使用していることを Contoso に示しています。 会社では次のアプリケーションが特定されました。

- 100 個の Java アプリケーション
- 約 50 個の Node.js アプリケーション
- 約 25 個の PHP アプリケーション

#### <a name="step-3-database-assessment"></a>手順 3:データベースの評価

データベースがインベントリされたときに、Azure への移行方法を決定するために各種類のデータベースが確認されました。 次のガイドラインに従って、データベースを移行しました。

| データベースの種類 | 詳細 | 移行先 | 移行ガイド |
| --- | --- | --- | --- |
| **MySQL** | サポートされているすべてのバージョンは、移行前にサポートされるバージョンにアップグレードされます | Azure Database for MySQL (PaaS) | [ガイド](/azure/dms/tutorial-mysql-azure-mysql-online)
| **PostgreSQL** | サポートされているすべてのバージョンは、移行前にサポートされるバージョンにアップグレードされます | Azure Database for PostgreSQL (PaaS) | [ガイド](/azure/dms/tutorial-postgresql-azure-postgresql-online) |
| **MariaDB** | サポートされているすべてのバージョンは、移行前にサポートされるバージョンにアップグレードされます | Azure Database for MariaDB (PaaS) | [ガイド](https://datamigration.microsoft.com/scenario/mariadb-to-azuremariadb?step=1) |

#### <a name="step-4-migration-planning"></a>手順 4:移行の計画

データベースの数が多いため、Contoso では、すべてのデータベース移行インスタンスを追跡するようにプロジェクト管理オフィスを設定しました。 各ビジネスおよびアプリケーション チームには、[説明責任と責任](../..//migrate/migration-considerations/assess/index.md)が割り当てられました。

Contoso では、[ワークロードの準備状況のレビュー](../..//migrate/migration-considerations/assess/evaluate.md)も実行しました。 このレビューでは、インフラストラクチャ、データベース、ネットワークのコンポーネントについて調査しました。

#### <a name="step-5-test-migrations"></a>手順 5:テスト移行

移行準備の最初の部分には、設定前の環境への各データベースのテスト移行が含まれていました。 時間を節約するために、Contoso では移行のすべての操作をスクリプト化し、それぞれの時間を記録しました。 移行を高速化するために、会社は同時に実行できる移行操作を特定しました。

予期しないエラーが発生した場合のために、データベースの各ワークロードについてロールバック手順を特定しました。

IaaS ベースのワークロードについては、必要なすべてのサードパーティ製ソフトウェアを事前に設定しました。

テスト移行の後、Contoso ではさまざまな Azure [コスト見積もりツール](../..//migrate/migration-considerations/assess/estimate.md)を使用して、移行の将来の運用コストをより正確に把握しました。

#### <a name="step-6-migration"></a>手順 6:移行

運用環境への移行について、Contoso では、すべてのデータベースの移行の時間枠と、週末の時間枠 (金曜日の午前 0 時から日曜日の午前 0 時まで) 内で十分に実行できる作業内容を特定し、ビジネスのダウンタイムを最小限に抑えました。

### <a name="clean-up-after-migration"></a>移行後にクリーンアップする

Contoso では、すべてのデータベース ワークロードのアーカイブ時間枠を特定しました。 時間枠の期限が切れると、オンプレミスのインフラストラクチャからリソースの割り当てが解除されます。 このプロセスには、オンプレミス サーバーからの運用データの削除と、最後のワークロード時間枠の期限が切れた時点でのホスティング サーバーの廃止が含まれます。

### <a name="review-the-deployment"></a>デプロイを再調査する

リソースを Azure に移行したら、新しいインフラストラクチャを完全に操作可能にして、セキュリティで保護する必要があります。

#### <a name="security"></a>セキュリティ

Contoso は次のことを行う必要があります。

- 新しい Azure データベース ワークロードがセキュリティで保護されていることを確認します。 詳細については、[Azure SQL Database と SQL Managed Instance のセキュリティ機能](/azure/azure-sql/database/security-overview)に関するページを参照してください。
- ファイアウォールと仮想ネットワークの構成を確認します。
- Azure Private Link を設定して、すべてのデータベース トラフィックが Azure とオンプレミス ネットワーク内に保持されるようにします。
- Azure Advanced Threat Protection を有効にします。

#### <a name="backups"></a>バックアップ

Azure データベースが geo リストアを使用してバックアップされていることを確認します。 これにより、リージョン規模の障害が発生した場合は、ペアのリージョンにあるバックアップを使用できます。

> [!IMPORTANT]
> Azure リソースが削除されないようにするため、[リソース ロック](/azure/azure-resource-manager/management/lock-resources)が保持されていることを確認します。 削除されたサーバーを復元することはできません。

#### <a name="licensing-and-cost-optimization"></a>ライセンスとコストの最適化

- 多くの Azure データベース ワークロードは、スケールアップまたはスケールダウンすることができます。 サーバーとデータベースのパフォーマンスを監視することは、ニーズを確実に満たし、コストを最小限に抑えるために重要なことです。
- CPU とストレージの両方がコストに関連します。 選択できる価格レベルはいくつかあります。 データ ワークロードに適した価格プランが選択されていることを確認してください。
- 各読み取りレプリカは、選択されたコンピューティングとストレージに基づいて課金されます。
- 予約容量を使用してコストを削減します。

## <a name="conclusion"></a>まとめ

この記事では、Contoso によって、オープンソース データベースの Azure PaaS および IaaS ソリューションへの移行が評価、計画、実行されました。
