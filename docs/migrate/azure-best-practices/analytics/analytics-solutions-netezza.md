---
title: Netezza の分析ソリューション
description: Azure のクラウド導入フレームワークを使用して、Teradata を使用した分析ソリューションについて学習します。Azure のクラウド導入フレームワークを使用して、Netezza を使用する分析ソリューションについて学習します。
author: v-hanki
ms.author: brblanch
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4de63bd39c9b5e22d5848532aef956374fa32414
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452658"
---
<!-- cSpell:ignore Netezza Informatica Talend InMon zonemap CBTs Attunity Wherescape nzlua CBT NZPLSQL DELIM TABLENAME ORC Parquet nzsql nzunload mpp -->

# <a name="analytics-solutions-for-netezza"></a>Netezza の分析ソリューション

IBM からのサポートが終了したため、Netezza データ ウェアハウス システムの既存ユーザーの多くが、新しい環境 (クラウド、IaaS、PaaS など) によって提供されるイノベーションを活用し、インフラストラクチャのメンテナンスやプラットフォーム開発などのタスクをクラウド プロバイダーに委任することを検討しています。

Netezza と Azure Synapse Analytics には類似点があり、両者とも非常に大規模なデータ量に対して高いクエリ パフォーマンスを実現するために、超並列処理 (MPP) 手法を使用するように設計された SQL データベースですが、アプローチには基本的な違いがいくつかあります。

- レガシ Netezza システムは、独自のハードウェアを使用してオンプレミスにインストールされます。一方、Azure Synapse Analytics は Azure Storage とコンピューティング リソースを使用したクラウドベースです。
- Netezza 構成のアップグレードは、物理ハードウェアの追加や、長時間かかる可能性のあるデータベースの再構成またはダンプと再読み込みを伴う大きなタスクです。 ストレージとコンピューティング リソースは Azure 環境では分離されているため、エラスティック スケーラビリティ機能を使用して容易に個別でスケール (アップおよびダウン) することができます。
- 必要に応じて、Azure Synapse Analytics を一時停止またはサイズ変更して、リソース使用率とコストを削減することができます。 Microsoft Azure は、グローバルに使用できる、高度なセキュリティで保護されたスケーラブルなクラウド環境であり、サポート ツールと機能のエコシステム内に Azure Synapse が組み込まれています。

以下では、Azure Synapse で移行した Netezza データ ウェアハウスおよびデータ マートについて同等以上のパフォーマンスを得るために、ビューを使用してスキーマを移行する方法について説明します。 このホワイトペーパーに記載されているトピックは、既存の Netezza 環境からの移行に特化して適用されます。

## <a name="design-considerations"></a>設計上の考慮事項

### <a name="migration-scope"></a>移行のスコープ

### <a name="preparation-for-migration"></a>移行の準備

Netezza 環境から移行する場合は、ドキュメントのセクション 1: デザインとパフォーマンスに関する記事で説明されている一般的な情報に加えて、いくつかの特定のトピックについて考慮する必要があります。

### <a name="choosing-the-workload-for-the-initial-migration"></a>初期移行のワークロードの選択

レガシ Netezza 環境は、通常、複数の主題領域と混合ワークロードを含むように、時間の経過と共に進化しています。 最初の移行プロジェクトの開始位置を決定するときは、次のことが可能な領域を選択することをお勧めします。

- 新しい環境の利点を迅速に提供することで、Azure Synapse への移行の可能性を証明する。
- 社内のテクニカル スタッフが、他の領域の移行に使用できるプロセスおよびツールの重要な体験を得られるようにする。
- 移行の演習をさらに行うために、ソース Netezza 環境と既に配置済みの現在のツールおよびプロセスに固有のテンプレートを作成する。

上記の事項を可能にする Netezza 環境からの初期移行に適した候補は、通常、OLTP ワークロードではなく BI/分析ワークロードを実装するもので、最小限の変更で移行できるデータ モデル (通常は開始スキーマまたはスノーフレーク スキーマ) を使用するものです。

サイズに関しては、最初の演習で移行するデータ量が、Azure Synapse 環境の機能と利点を示すのに十分な大きさであることが重要であるとともに、価値を示す時間を短く抑える (通常は 1 から 10 TB の範囲) 必要があります。

初期移行プロジェクトでリスクを最小化し、初期プロジェクトの実装時間を短縮する方法の 1 つとして、移行のスコープをデータ マートのみに限定することが挙げられます。 このアプローチでは、定義上、移行のスコープが制限され、通常は短いタイムスケール内で実現できるため、出発点として適している可能性があります。 ただし、初期移行プロジェクトの一環としての ETL の移行や履歴データの移行など、より広範なトピックには対応していません。 これらのトピックには、プロジェクトの後の段階で、移行されたデータ マート レイヤーがそれらを構築するために必要なデータとプロセスでバック フィルされたときに、対処する必要があります。

### <a name="lift-and-shift-as-is-versus-a-phased-approach-incorporating-changes"></a>そのままでのリフト アンド シフトと、変更を伴う段階的なアプローチ

目的の移行のドライバーやスコープにかかわらず、通常は次の 2 種類の移行があります。

- **リフト アンド シフト:** この場合、既存のデータ モデル (スター スキーマなど) は、そのまま新しい Azure Synapse プラットフォームに移行されます。 ここで重視される点は、Azure クラウド環境への移行の利点を実現するために必要な作業を減らすことで、リスクを最小限に抑え、移行にかかる時間を短縮することです。

  このアプローチは、1 つのデータ マートが移行される既存の Netezza 環境に適しています。または、適切に設計されたスター スキーマまたはスノーフレーク スキーマにデータが既に含まれている場合や、最新のクラウド環境に移行するための時間とコストのプレッシャーがある場合に適しています。

- **変更を伴う段階的なアプローチ:** レガシ ウェアハウスが時間の経過と共に進化してきた場合は、必要なパフォーマンスを維持したり、IoT ストリームなどの新しいデータ ソースをサポートしたりするために、リエンジニアリングが必要になることがあります。 リエンジニアリング プロセスの一環として、スケーラブルなクラウド環境のよく知られている利点を得るために Azure Synapse に移行することを検討する場合があります。 このプロセスには、基になるデータ モデルの変更 (Inmon モデルから Azure Data Vault への移行など) が含まれる場合があります。

  最初に既存のデータ モデルをそのまま Azure に移行してから、Azure のパフォーマンスと柔軟性を生かして、リエンジニアリングの変更を適用することをお勧めします。そのとき、必要に応じて Azure の機能を使用して、既存のソース システムに影響を与えずに変更を加えます。

### <a name="use-azure-data-factory-to-implement-a-metadata-driven-migration"></a>Azure Data Factory を使用してメタデータに基づく移行を実装する

Azure 環境で機能を利用することで、移行プロセスを自動化し、調整することは理にかなっています。 このアプローチにより、既存の Netezza 環境への影響も最小限に抑えられます (既に全容量に近い状態で実行されている可能性があります)。

Azure Data Factory は、データドリブン型のワークフローをクラウドに作成することでデータの移動と変換を制御し、自動化することができるクラウドベースのデータ統合サービスです。 Azure Data Factory を使えば、各種のデータ ストアからデータを取り込むことができるデータ主導型のワークフロー (パイプライン) を作成し、スケジューリングできます。 そのデータは、Azure HDInsight Hadoop、Spark、Azure Data Lake Analytics、Azure Machine Learning などのコンピューティング サービスを使って処理し、変換することができます。

移行するデータ テーブルとその場所をリストするメタデータを作成することにより、Azure Data Factory の機能を使用して移行プロセスを管理できます。

### <a name="design-differences-between-netezza-and-azure-synapse"></a>Netezza と Azure Synapse の設計の違い

**複数のデータベースと 1 つのデータベースおよびスキーマ:**

Netezza 環境では、環境全体の個々の部分に対して複数の異なるデータベースが存在することがあります。 たとえば、データ インジェストおよびステージング テーブルのデータベース、コア ウェアハウス テーブルのデータベース、データ マート (セマンティック レイヤーとも呼ばれる) のデータベースが個別に存在する場合があります。 ETL/ELT パイプラインなどの処理では、複数データベースにまたがる結合が実装され、これらの個別のデータベース間でデータが移動されます。

Azure Synapse 環境には 1 つのデータベースがあり、スキーマを使用して、テーブルが論理的に分離されたグループに分割されます。 したがって、Netezza 環境から移行される個別のデータベースを模倣するために、ターゲットの Azure Synapse 内で一連のスキーマを使用することをお勧めします。 Netezza 環境内でスキーマが使用されている場合は、新しい名前付け規則を使用して、既存の Netezza テーブルおよびビューを新しい環境に移動する必要があります (既存の Netezza スキーマおよびテーブル名を新しい Azure Synapse テーブル名に連結する、新しい環境でスキーマ名を使用して元の個別のデータベース名を維持するなど)。 もう 1 つの方法は、基になるテーブルに SQL ビューを使用して論理構造を維持することですが、この方法には潜在的な欠点がいくつかあります。

- Azure Synapse のビューは読み取り専用であるため、データの更新は、基になるベース テーブルで行われる必要があります。
- 既にビューの 1 つ以上のレイヤーが存在しており、追加のビュー レイヤーを追加すると、パフォーマンスが低下する可能性があります。

**テーブルに関する考慮事項:**

異なるテクノロジ間でテーブルを移行する場合、通常は、2 つの環境間で物理的に移動される生データ (およびそれを記述するメタデータ) のみが移行されます。 インデックスなど、ソース システムのその他のデータベース要素は移行されません。これは、これらの要素が必要ないか、新しいターゲット環境内で異なる方法で実装される可能性があるためです。

ただし、インデックスなどのパフォーマンスの最適化がソース環境で使用されている場所を理解することが重要です。これは、新しいターゲット環境でパフォーマンスの最適化が追加される可能性のある場所を示す有益な情報となるためです。 たとえば、ソース Netezza 環境内でクエリによってゾーン マップが頻繁に使用される場合、移行された Azure Synapse 内で非クラスター化インデックスを作成する必要があることを示している可能性がありますが、同一条件下での直接的なインデックスの作成よりも、テーブル レプリケーションなどのその他のネイティブなパフォーマンス最適化手法の方が適していることがあります。

<!-- docsTest:ignore "NZ Toolkit" -->

**サポートされていない Netezza データベース オブジェクトの種類:**

Netezza では、Azure Synapse で直接サポートされていないいくつかのデータベース オブジェクトが実装されますが、通常は新しい環境内で同じ機能を実現する方法があります。

- **ゾーン マップ:** Netezza では、一部の列の種類に対してゾーン マップが自動的に作成され、維持されます。また、これらはクエリ時に、スキャンされるデータの量を制限するために使用されます。 これらは、次の列の種類に対して作成されます。

  - `INTEGER` 長さが 8 バイト以下の列。
  - テンポラル列 (`DATE`、`TIME`、`TIMESTAMP` など)。
  - `CHAR` 列 (これらが具体化されたビューの一部であり、`ORDER BY` 句で示されている場合)。 nz_zonemap ユーティリティ (NZ ツールキットの一部) を使用して、どの列にゾーン マップがあるかを確認できます。

  Azure Synapse にはゾーン マップは含まれませんが、他の (ユーザー定義の) インデックスの種類またはパーティション分割を使用して同様の結果を得ることができます。

- **クラスター化されたベース テーブル (CBT):** Netezza では、大量のレコードを含むファクト テーブルに対しては、CBT が最もよく使用されます。 このような大きなテーブルをスキャンするには、関連するレコードを取得するためにフル テーブル スキャンが必要になる可能性があるため、多くの処理時間が必要になります。 制限付きの CBT でレコードを整理すると、Netezza では同じまたは近くにあるエクステントのレコードをグループ化できます。また、このプロセスでは、スキャンするデータの量を減らすことでパフォーマンスを向上させるゾーン マップも作成されます。

  Azure Synapse では、他のインデックスをパーティション分割または使用することで、同様の効果を実現できます。

- **具体化されたビュー:** Netezza では、具体化されたビューがサポートされています。多数の列が含まれており、そのうち数列のみがクエリで定期的に使用される大規模なテーブルに対して、こうしたビューを 1 つ以上作成することをお勧めします。 具体化されたビューは、ベース テーブルのデータが更新されるとシステムで自動的に維持されます。 2019 年 5 月の時点で、Microsoft は、Netezza と同じ機能を持つ具体化されたビューが Azure Synapse でサポートされることを発表しました。 現在、この機能はプレビューでご利用いただけます。

- **Netezza データ型マッピング:** ほとんどの Netezza データ型には、Azure Synapse に直接相当するものがあります。 次の表は、これらのデータ型を、これらのマッピングに推奨される方法と共に示しています。

  前述のように、データ型のマッピングなど、移行を自動化するためのツールとサービスを提供するサードパーティ ベンダーが存在します。 また、Informatica や Talend などのサードパーティの ETL ツールが既に Netezza 環境で使用されている場合は、必要なデータ変換を実装できます。

- **SQL DML 構文の相違点:** 移行時の注意点として、Netezza SQL と Azure Synapse の SQL データ操作言語 (DML) 構文には、いくつかの相違点があります。

  <!-- TODO: This query should probably be a code snippet that the user can copy and use. -->

  ![SQL クエリ (SQL query)](../../../_images/analytics/sql-query-netezza.png)

### <a name="functions-stored-procedures-and-sequences"></a>関数、ストアド プロシージャ、シーケンス

Netezza などの成熟したレガシ データ ウェアハウス環境から移行する場合、新しいターゲット環境に移行する必要がある、単純なテーブルとビュー以外の要素が存在することがよくあります。 Netezza でのこのような例としては、関数、ストアド プロシージャ、シーケンスがあります。 準備フェーズの一環として、プロジェクト計画で割り当てられているリソースの適切な配分を使用して、移行対象のこれらのオブジェクトのインベントリを作成し、それらのオブジェクトの処理方法を定義する必要があります。

Netezza 環境で関数またはストアド プロシージャとして実装されている機能を置き換えるファシリティが、Azure 環境に存在する場合があります。 この場合、通常は、Netezza 関数をコーディングし直すよりも、組み込みの Azure ファシリティを使用する方が効率的です。

サードパーティ ベンダーによって、これらの移行を自動化できるツールとサービスが提供されています (例については、Attunity または Wherescape の移行製品を参照してください)。

- **関数:** ほとんどのデータベース製品と同様に、Netezza ではシステム関数と SQL 実装内のユーザー定義関数がサポートされています。 Azure Synapse などの別のデータベース プラットフォームに移行する場合、通常は共通のシステム関数を使用でき、変更なしに移行することができます。 システム関数によっては構文が若干異なることがありますが、この場合は必要な変更を自動化できます。

  同等のものがないシステム関数や、任意のユーザー定義関数の場合は、ターゲット環境で使用可能な言語を使用してコーディングし直す必要が生じることがあります。 Netezza のユーザー定義関数は、nzlua または C++ 言語でコーディングされています。一方、Azure Synapse では、ユーザー定義関数の実装に一般的な Transact-SQL 言語が使用されます。

- **ストアド プロシージャ:** 最新のデータベース製品では、データベース内にプロシージャを格納することができます。 Netezza では、この目的で NZPLSQL 言語が提供されています。 NZPLSQL は、PostgreSQL PL/pgSQL に基づいています。 ストアド プロシージャには、通常、SQL ステートメントといくつかの手続き型のロジックが含まれており、データや状態を返すことができます。

  Azure SQL Data Warehouse では T-SQL を使用したストアド プロシージャもサポートされているので、ストアド プロシージャを移行する場合は、それに応じてコーディングし直す必要があります。

- **シーケンス:** Netezza では、シーケンスは create sequence を使用して作成された名前付きデータベース オブジェクトで、メソッドの次の値を使用して一意の値を指定できます。 これらは、主キー値の代理キー値として使用できる一意の数値を生成するために使用できます。

  Azure Synapse では `CREATE SEQUENCE` が存在しないため、シーケンスは ID 列を使用して処理されるか、SQL コードを使用して系列の次のシーケンス番号が作成されます。

### <a name="extracting-metadata-and-data-from-a-netezza-environment"></a>Netezza 環境からのメタデータとデータの抽出

- **DDL の生成:** Netezza の既存の create table および create view スクリプトを編集して、同等の定義を作成することができます (前述のように、必要に応じて、変更されたデータ型を使用します)。 この場合、通常は、不要な Netezza 固有の句 (`ORGANIZE ON` など) をすべて削除または変更する必要があります。

  ただし、既存の Netezza 環境内のテーブルおよびビューの現在の定義を指定するすべての情報は、システム カタログ テーブル内で保持されます。 この情報は、最新の状態かつ完全になるようにバインドされているため、この情報源として最適です。 ユーザーが管理するドキュメントは、現在のテーブル定義と同期されていない可能性があります。

  この情報には、nz_ddl_table などのユーティリティを使用してアクセスできます。また、この情報は、Azure Synapse の同等のテーブルに対して編集できる create table DDL ステートメントを生成するために使用できます。

  サードパーティの移行および ETL ツールでも、カタログ情報を使用して同じ結果が得られます。

- **Netezza からのデータの抽出:** 既存の Netezza テーブルから移行する生データは、nzsql や nzunload などの標準の Netezza ユーティリティを使用し、外部テーブルを使用して、区切られたフラット ファイルに抽出できます。 これらのファイルは gzip を使用して圧縮し、AzCopy を使用するか、Azure Data Box などの Azure データ転送ファシリティを使用して、Azure Blob storage にアップロードできます。

  移行の演習では、できるだけ効率的にデータを抽出することが重要です。 Netezza の推奨される方法としては、最も高速な方法である外部テーブルのアプローチを使用します。 データ抽出のスループットを最大化するために、複数の抽出を並列に実行できます。 外部テーブルの抽出の簡単な例を次に示します。

  `CREATE EXTERNAL TABLE '/tmp/export_tab1.CSV' USING (DELIM ',') AS SELECT * from <TABLENAME>;`

十分なネットワーク帯域幅が存在する場合は、Azure Data Factory プロセスか、サードパーティのデータ移行または ETL 製品を使用して、オンプレミスの Netezza システムから Azure Synapse テーブルまたは Azure データ ストレージにデータを直接抽出できます。

抽出されたデータに対して推奨されるデータ形式は、区切りテキスト ファイル (コンマ区切り値などとも呼ばれる) か、Optimized Row Columnar (ORC) または Parquet ファイルです。

Netezza 環境からデータと ETL を移行するプロセスの詳細については、Netezza の関連ドキュメントのセクション 2.1: データ移行 ETL と読み込みに関する記事を参照してください。

### <a name="performance-recommendations-for-netezza-migrations"></a>Netezza 移行のパフォーマンスに関する推奨事項

- **パフォーマンス チューニング アプローチの概念の類似点:** Netezza 環境から移行する場合、Azure SQL Data Warehouse のパフォーマンス チューニングの概念の多くは Netezza のものと似ています。 次に例を示します。

  - データ分布を使用して、同じ処理ノードに結合するデータを同一場所に配置します。
  - 特定の列に対して最小のデータ型を使用すると、ストレージ領域が節約され、クエリ処理が高速化されます。
  - 結合する列のデータ型が同一であることを確認しておくと、データを一致させるために変換する必要性が低減するため、結合処理が最適化されます。
  - 統計が最新であることを確認しておくと、オプティマイザーで最適な実行プランを生成するのに役立ちます。

- **パフォーマンス チューニング アプローチの相違点:** このセクションでは、パフォーマンス チューニングに関する Netezza と Azure Synapse の下位レベルの実装の違いについて説明します。

- **データ分散オプション:** `CREATE TABLE` Netezza と Azure Synapse のステートメントを使用すると、Netezza では `DISTRIBUTE ON`、Azure Synapse では `DISTRIBUTION =` を介して、両者とも分散定義を指定できます。

  Netezza と比較すると、Azure Synapse では、小さいテーブルと大きいテーブルの結合 (通常は、開始スキーマ モデルでディメンション テーブルからファクト テーブルへ) のためのローカル結合を実現する、追加の方法が提供されています。これにより、より小さいディメンション テーブルがすべてのノードにわたってレプリケートされるため、より大きいテーブルの結合キーのどの値にも、対応するディメンション行がローカルに存在するようになります。 ディメンション テーブルが大きくない場合、テーブルをレプリケートする場合のオーバーヘッドは比較的低くなります。 この場合、前述のハッシュ分散アプローチが適しています。

- **データのインデックス作成:** Azure Synapse には、ユーザー定義が可能なインデックス作成オプションがいくつか用意されていますが、これらは、Netezza のシステム管理ゾーン マップとは操作および使用方法が異なります。 説明されているさまざまなインデックス作成オプションを理解しておきましょう。 <!-- TODO verify link: https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-datawarehouse-tables-index -->

  一方、ソース Netezza 環境内の既存のシステム管理ゾーン マップでは、データが現在どのように使用されているかをわかりやすく示すことができ、Azure Synapse 環境内でインデックスを作成するための候補列も示すことができます。

- **データのパーティション分割:** エンタープライズ データ ウェアハウスでは、ファクト テーブルに多数の行を含めることができます。パーティション分割を使用すると、これらのテーブルを別々の部分に分割して、処理されるデータの量を減らすことで、これらのテーブルのメンテナンスとクエリを最適化することができます。 テーブルのパーティション分割指定は、create table ステートメントで定義されます。

  パーティション分割に使用できるフィールドは、各テーブルに 1 つだけです。多くのクエリは日付や日付範囲によってフィルター処理されるため、パーティション分割には日付フィールドが頻繁に使用されます。 必要に応じて、`CREATE TABLE AS SELECT` ステートメントを使用し、新しい分散を指定してテーブルを再作成することにより、初期読み込み後にテーブルのパーティション分割を変更することができます。 解決方法については、 <!-- TODO verify link https://docs.microsoft.com/en-us/azure/sql-datawarehouse/sql-data-warehouse-tables-partition --> Azure Synapse でのパーティション分割の詳細をご覧ください。

- **データの読み込み用の PolyBase:** PolyBase は、並列読み込みストリームを使用できるため、ウェアハウスに大量のデータを読み込むための最も効率的な方法です。

- **ワークロード管理用のリソース クラスの使用:** Azure Synapse では、リソース クラスを使用してワークロードが管理されます。 一般に、リソース クラスが大きいほど、クエリのパフォーマンスが向上します。一方、リソース クラスが小さいほど、より高いレベルの同時実行が可能になります。 使用率を動的管理ビューで監視して、適切なリソースが効率的に使用されていることを確保することができます。

## <a name="next-steps"></a>次のステップ

Netezza 移行の実装の詳細については、オンプレミスの移行プランについて Microsoft アカウント担当者にお問い合わせください。