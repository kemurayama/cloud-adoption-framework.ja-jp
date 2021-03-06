---
title: Netezza に関する Azure Synapse Analytics の移行
description: Azure のクラウド導入フレームワークを使用して、Netezza 用の分析ソリューションと、Azure Synapse Analytics への移行について学習します。
author: v-hanki
ms.author: brblanch
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 792f71c94d9ed16d134d444da8b467983ae9b5a8
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94996334"
---
<!-- docutune:casing Informatica Talend Inmon Attunity Qlik nzLua CBT CBTs NZPLSQL DELIM TABLENAME ORC Parquet nzsql nzunload mpp -->

<!-- cSpell:ignore Informatica Talend Qlik CBTs NZPLSQL CHARINDEX DATEDIFF DELIM STRPOS TABLENAME nzsql nzunload zonemap -->

# <a name="azure-synapse-analytics-solutions-and-migration-for-netezza"></a>Netezza に関する Azure Synapse Analytics ソリューションと移行

IBM による Netezza のサポートが終了するため、現在 Netezza データ ウェアハウス システムを使用している多くの組織では、Azure のようなより新しい環境で革新的なクラウド、サービスとしてのインフラストラクチャ、サービスとしてのプラットフォームを利用することが検討されています。 多くの組織は、インフラストラクチャのメンテナンスやプラットフォームの開発といった、コストのかかるタスクをクラウド プロバイダーに移行するための手順を実行する準備ができています。

Azure Synapse Analytics は、エンタープライズ データ ウェアハウスとビッグ データ分析が統合された制限のない分析サービスです。 サーバーレスのオンデマンド リソースまたはプロビジョニング済みのリソースを使用しながら、各自の条件で自由にデータのクエリを大規模に実行できます。 従来の Netezza システムを Azure Synapse に移行するときに計画する内容について説明します。

Netezza と Azure Synapse は、いずれも大量のデータに対する高いクエリ パフォーマンスを実現するために、超並列処理手法を使用するように設計された SQL データベースであるという点で似ています。 しかし、2 つのプラットフォームは大事な点で違いがあります。

- 従来の Netezza システムはオンプレミスにインストールされ、独自のハードウェアが使用されます。 Azure Synapse はクラウドベースであり、Azure のコンピューティングおよびストレージのリソースが使用されます。
- Netezza 構成のアップグレードは、追加の物理ハードウェアや、長時間かかる可能性のあるデータベースの再構成またはダンプと再読み込みを伴う大きなタスクです。 Azure Synapse では、ストレージ リソースとコンピューティング リソースは分かれています。 Azure の柔軟なスケーラビリティを使用して、個別にスケールアップまたはスケールダウンすることができます。
- サポートする物理システムがないので、必要に応じて Azure Synapse を一時停止したりそのサイズを変更したりして、リソースの使用率とコストを削減することができます。 Azure では、サポート ツールと機能のエコシステムに Azure Synapse が組み込まれている、グローバルに使用できる、高度なセキュリティで保護されたスケーラブルなクラウド環境にアクセスできます。

この記事では、Azure Synapse で移行した Netezza データ ウェアハウスおよびデータ マートについて同等以上のパフォーマンスを得るために、ビューを使用してスキーマを移行する方法について説明します。 既存の Netezza 環境からの移行に特に適用される考慮事項について検討します。

大まかに言えば、移行プロセスには次の表に示す手順が含まれています。

| 準備        | 移行                             | 移行後 |
| :----------------- | :----------------------------- | :---------------- |
| <ul><li> 範囲を定義する: 何を移行するか?</li><li>移行するデータとプロセスのインベントリを作成する。</li><li>データ モデルの変更を定義する。</li><li>使用する最適な Azure およびサードパーティのツールと機能を特定する。</li><li>新しいプラットフォームのスタッフ トレーニングを早期に実施する。</li><li>Azure のターゲット プラットフォームをセットアップする。</li></ul> |  <ul><li> 小規模で簡単なものから始める。</li><li>可能であれば自動化する。</li><li>Azure の組み込みツールと機能を使用して移行作業を減らす。</li><li>テーブルとビューのメタデータを移行する。</li><li>関連する履歴データを移行する。</li><li>ストアド プロシージャとビジネス プロセスを移行またはリファクタリングする。</li><li>ETL または ELT の段階的読み込みプロセスを移行またはリファクタリングする。</li></ul> | <ul><li> 移行プロセスのすべてのステージを監視してドキュメント化する。</li><li>今後の移行のため、得られた経験を利用してテンプレートを作成する。</li><li>必要な場合、新しいプラットフォームのパフォーマンスとスケーラビリティを使用して、データ モデルを再エンジニアリングする。</li><li>アプリケーションとクエリ ツールをテストする。</li><li>クエリ パフォーマンスのベンチマークと最適化を行う。</li></ul> |

従来の Netezza 環境から Azure Synapse に移行するときは、Netezza のドキュメントで説明されている比較的一般的な情報に加えて、いくつかの特定の要因について検討する必要があります。

## <a name="initial-migration-workload"></a>初期移行ワークロード

従来の Netezza 環境は、通常、複数の主題領域と混合ワークロードを含むように、時間の経過と共に進化しています。 最初の移行プロジェクトをどこから始めるか決定するときは、次のような領域を選択することをお勧めします。

- 新しい環境の利点を迅速に提供することで、Azure Synapse への移行の実現可能性が証明される。
- 社内のテクニカル スタッフが、他の領域の移行に使用できるように、新しいプロセスやツールに関する経験を得られる。
- 移行元 Netezza 環境からの追加の移行で使用する、現在のツールとプロセスに基づくテンプレートが作成される。

これらの目標が満たされる Netezza 環境からの初期移行に適した候補は、通常、OLTP ワークロードではなく、Power BI や分析のワークロードが実装されている部分です。 そのようなワークロードでは、スター スキーマやスノーフレーク スキーマなど、最小限の変更で移行できるデータ モデルが使用されている必要があります。

サイズに関しては、最初の演習で移行するデータ量が、短い時間で価値を示すことにより、Azure Synapse 環境の機能と利点を示すのに十分な大きさであることが重要です。 通常、そのような要件を満たすサイズは、1 テラバイト (TB) から 10 TB の範囲です。

リスクと実装時間を最小限に抑える初期移行プロジェクトのアプローチは、データ マートへの移行の範囲を制限することです。 このアプローチは、移行の範囲が明確に制限され、通常は短いタイムスケール内で実現できるため、出発点として適しています。 データ マートの初期移行だけでは、ETL や履歴データの移行方法といった、より広範な問題に対処することはできません。 これらの領域については後のフェーズで対処し、移行したデータ マート レイヤーを、それらを構築するために必要なデータとプロセスでバックフィルする必要があります。

## <a name="lift-and-shift-approach-vs-phased-approach"></a>リフト アンド シフト方式と段階的方式の比較

移行に対して選択した原動力や範囲とは関係なく、次の 2 種類の一般的な移行のどちらかを選択できます。

- **リフトアンドシフト方式:** この方式では、既存のデータ モデル (スター スキーマなど) は、そのまま新しい Azure Synapse プラットフォームに移行されます。 このシナリオで重視されるのは、Azure クラウド環境への移行の利点を実現するために必要な作業を減らすことで、リスクを最小限に抑え、移行にかかる時間を短縮することです。

  この方式は、1 つのデータ マートが移行される既存の Teradata 環境で、データが既に適切に設計されたスター スキーマやスノーフレーク スキーマになっている場合に適しています。 この方式は、より最新のクラウド環境への移行に対して時間とコストの制約がある場合にも適しています。

- **変更を伴う段階的方式:** レガシ ウェアハウスが時間の経過と共に進化してきた場合は、必要なパフォーマンスを維持したり、IoT ストリームなどの新しいデータ ソースをサポートしたりするために、データ ウェアハウスのリエンジニアリングが必要になることがあります。 リエンジニアリング プロセスの一環として、スケーラブルなクラウド環境のよく知られている利点を得るために Azure Synapse に移行することを検討する場合があります。 このプロセスには、基になるデータ モデルの変更 (Inmon モデルから Azure Data Vault への移行など) が含まれる場合があります。

  最初に既存のデータ モデルをそのまま Azure に移行する方式をお勧めします。 その後、Azure サービスのパフォーマンスと柔軟性を利用して、既存の移行元システムに影響を与えずにリエンジニアの変更を適用します。

## <a name="metadata-migration"></a>メタデータの移行

Azure 環境の機能を使用することで、移行プロセスを自動化し、調整することは理にかなっています。 この方式では、既に容量の上限に近い状態で実行されている可能性がある、既存の Netezza 環境への影響も最小限に抑えられます。

Azure Data Factory は、クラウドベースのデータ統合サービスです。 Data Factory を使用すると、クラウドにデータ ドリブン ワークフローを作成して、データ移動とデータ変換を調整および自動化できます。 Data Factory パイプラインでは、さまざまなデータ ストアからデータを取り込んだ後、Apache Hadoop や Apache Spark 用の Azure HDInsight、Azure Data Lake Analytics、Azure Machine Learning などのコンピューティング サービスを使用して、データの処理と変換を行うことができます。 最初に、移行するデータ テーブルとその場所をリストするメタデータを作成してから、Data Factory の機能を使用して移行プロセスを管理します。

## <a name="design-differences-between-netezza-and-azure-synapse"></a>Netezza と Azure Synapse の設計の違い

従来の Netezza 環境から Azure Synapse への移行を計画するときは、2 つのプラットフォームの設計の違いを考慮することが重要です。

### <a name="multiple-databases-vs-a-single-database-and-schemas"></a>複数のデータベースに対して、1 つのデータベースとスキーマ

Netezza 環境では、環境全体の異なる部分に対して複数の異なるデータベースが存在することがあります。 たとえば、データ インジェストおよびステージング テーブルのデータベース、コア ウェアハウス テーブルのデータベース、データ マート ("_セマンティック レイヤー_" とも呼ばれます) のデータベースが個別に存在する場合があります。 Azure Synapse で ETL および ELT パイプラインとして個別のデータベースを処理するには、データベース間結合を実装し、異なるデータベース間でデータを移動する必要があります。

Azure Synapse 環境にあるデータベースは 1 つです。 スキーマは、テーブルを論理的に分かれたグループに分割するために使用されます。 移行先の Azure Synapse で一連のスキーマを使用して、Netezza から移行する個別のデータベースを模倣することをお勧めします。 Netezza 環境でスキーマを使用している場合は、Netezza の既存のテーブルとビューを新しい環境に移動するために、新しい名前付け規則を使用することが必要な場合があります。 たとえば、Netezza の既存のスキーマ名とテーブル名を連結して Azure Synapse の新しいテーブル名にしてから、新しい環境でスキーマ名を使用して、元の個別のデータベース名を維持するような場合があります。

もう 1 つの方法は、基になるテーブルに対して SQL ビューを使用して、論理構造を維持することです。 SQL ビューを使用すると、次のような欠点が生じる可能性があります。

- Azure Synapse のビューは読み取り専用であるため、データに対する更新は、基になるベース テーブルで行う必要があります。
- ビューのレイヤーが既に存在する場合、別のビューのレイヤーを追加すると、パフォーマンスが低下する可能性があります。

### <a name="tables"></a>テーブル

異なるテクノロジ間でテーブルを移行するときは、生データとそれを記述するメタデータだけを、2 つの環境間で物理的に移動します。 インデックスのようなデータベース要素は、新しい環境では必要なかったり、異なる方法で実装されたりする場合があるため、移行元システムからは移行しません。

ただし、インデックスなどのパフォーマンス最適化が移行元環境のどこで使用されていたかを把握しておくことは、新しい環境でパフォーマンスを最適化できる場所を示すのに役立ちます。 たとえば、移行元の Netezza 環境のクエリでゾーン マップが頻繁に使用されている場合は、移行先の Azure Synapse 環境で非クラスター化インデックスを作成すると有益である、またはテーブル レプリケーションのような他のネイティブなパフォーマンス最適化手法を使用する方が、既存のものと同じインデックスを作成するより適している、という結論になる可能性があります。

<!-- docutune:casing "NZ Toolkit" -->

### <a name="unsupported-netezza-database-object-types"></a>サポートされていない Netezza データベース オブジェクトの種類

Netezza では、Azure Synapse で直接サポートされていない、いくつかのデータベース オブジェクトが実装されています。 ただし、Azure Synapse には、次の一覧で説明するように、新しい環境で同じ機能を実現するために使用できる方法が用意されています。

- **ゾーン マップ:** Netezza では、一部の列の型に対して、ゾーン マップが自動的に作成されて維持されます。 ゾーン マップは、スキャンされるデータの量を制限するために、次の列の型に対するクエリ時に使用されます。

  - 長さが 8 バイト以下の `INTEGER` 列
  - `DATE`、`TIME`、`TIMESTAMP` を含むテンポラル列
  - `CHAR` 列 (それらが具体化されたビューの一部であり、`ORDER BY` 句に含まれる場合)

  nz_zonemap ユーティリティを使用して、ゾーン マップがある列を確認できます。 このユーティリティは、NZ ツールキットの一部です。

  Azure Synapse ではゾーン マップは使用されていませんが、ユーザー定義のインデックスの種類またはパーティション分割を使用することで、同様の結果を実現できます。

- **クラスター化されたベース テーブル (CBT):** Netezza で最もよく使用される CBT は、大量のレコードが含まれるファクト テーブルです。 このような大きなテーブルをスキャンするには、関連するレコードを取得するためにフル テーブル スキャンが必要になる可能性があるため、長い処理時間が必要になります。 制限付きの CBT でレコードを整理すると、Netezza で同じエクステントまたは近くにあるエクステントのレコードをグループ化できます。 また、このプロセスでは、スキャンするデータの量を減らすことで、パフォーマンスを向上させるゾーン マップも作成されます。

  Azure Synapse では、パーティション分割または他のインデックスの種類を使用して、同様の結果を得ることができます。

- **具体化されたビュー:** Netezza では、多数の列があり、そのうちの数列だけがクエリでよく使用される大きなテーブルより、1 つ以上の具体化されたビューを作成することが推奨されます。 具体化されたビューは、ベース テーブルのデータが更新されるとシステムで自動的に維持されます。

  現在、Azure Synapse では、Netezza と同じ機能を持つ具体化されたビューのプレビュー サポートが提供されています。

- **データ型のマッピング:** ほとんどの Netezza データ型には、Azure Synapse に直接相当するものがあります。 次の表では、データ型と、データ型をマップする推奨される方法を示します。

  一部のサードパーティ ベンダーからは、データ型のマッピングなどの移行タスクを自動化できるツールとサービスが提供されています。 Informatica や Talend などのサードパーティの ETL ツールが Netezza 環境で既に使用されている場合は、そのツールを使用して、必要なデータ変換を実装できます。

- **SQL データ操作言語 (DML) の構文:** Netezza SQL と Azure Synapse の間で、SQL DML 構文のいくつかの違いに注意する必要があります。

  いくつかの主要な関数とその違いを次に示します。

  - `STRPOS`:Netezza の `STRPOS` 関数からは、文字列内の部分文字列の位置が返されます。 Azure Synapse でそれと同等のものは `CHARINDEX` 関数ですが、引数の順序は逆になります。

    Netezza の場合:

    `SELECT STRPOS('abcdef', 'def') ...`

    Azure Synapse では次のコードに置き換えられます。

    `SELECT CHARINDEX('def', 'abcdef') ...`

  - `AGE`:Netezza では、2 つのテンポラル値 (タイムスタンプ、日付など) の間隔を得るために、`AGE` 演算子がサポートされています。 次に例を示します。

    `SELECT AGE ('23-03-1956', '01-01-2019') FROM ...`

    Azure Synapse では、`DATEDIFF` を使用して同じ結果を実現できます (日付表現の順序に注意してください)。

    `SELECT DATEDIFF(day, '1956-03-23', '2019-01-01') FROM ...`

  - `NOW()`:Azure Synapse での `CURRENT_TIMESTAMP` を表すために、Netezza では `NOW()` が使用されます。

## <a name="functions-stored-procedures-and-sequences"></a>関数、ストアド プロシージャ、シーケンス

Netezza のような成熟したレガシ環境からデータ ウェアハウスを移行するときは、単純なテーブルやビュー以外の要素を新しいターゲット環境に移行することが必要になることがよくあります。 Azure Synapse への移行が必要になる可能性がある Netezza のテーブル以外の要素の例としては、関数、ストアド プロシージャ、シーケンスなどがあります。 移行の準備フェーズでは、移行するオブジェクトのインベントリを作成する必要があります。 プロジェクト計画で、すべてのオブジェクトを処理する方法を定義し、移行のための適切なリソースを割り当てます。

Netezza 環境で関数またはストアド プロシージャとして実装されている機能の代わりになるサービスが、Azure 環境で見つかる場合があります。 通常、Netezza の関数をコーディングし直すのではなく、Azure の組み込み機能を使用する方が効率的です。

また、サードパーティのベンダーから、Netezza からの関数、ストアド プロシージャ、シーケンスの移行を自動化できるツールとサービスが提供されています。 たとえば、Qlik (旧称 Attunity) や WhereScape などです。

関数、ストアド プロシージャ、シーケンスの移行に関する追加情報を次に示します。

- **関数:** ほとんどのデータベース製品と同様に、Netezza では SQL の実装でのシステム関数とユーザー定義関数がサポートされています。 一般的なシステム関数は、Azure Synapse などの別のデータベース プラットフォームに移行されると、一般に新しい環境で使用でき、変更なしに移行できます。 新しい環境でシステム関数の構文が若干異なる場合は、通常、必要な変更を自動化できます。

  新しい環境に同等のものがない任意のユーザー定義関数とシステム関数については、再コーディングが必要になる場合があります。 新しい環境で使用できる言語を使用します。 Netezza のユーザー定義関数は、nzLua または C++ を使用してコーディングされています。 Azure Synapse でユーザー定義関数を実装するには、一般的な Transact-SQL 言語が使用されます。

- **ストアド プロシージャ:** ほとんどの最新のデータベース製品では、データベースにプロシージャを保存できます。 ストアド プロシージャには、通常、SQL ステートメントといくつかの手続き型ロジックが含まれています。 また、データや状態が返される場合もあります。

  Netezza では、ストアド プロシージャ用に、PL/pgSQL に基づく NZPLSQL 言語が用意されています。 Azure Synapse では、T-SQL を使用してストアド プロシージャがサポートされます。 ストアド プロシージャを Azure Synapse に移行する場合は、T-SQL を使用してそれらをコーディングし直す必要があります。

- **シーケンス:** Netezza でのシーケンスは、`CREATE SEQUENCE` ステートメントを使用して作成される名前付きデータベース オブジェクトです。 オブジェクトを使用すると、`NEXT()` メソッドを介して一意の値を提供できます。 値を使用して、主キー値に対する代理キー値となる一意の数値を生成できます。

  Azure Synapse では、`CREATE SEQUENCE` はサポートされていません。 Azure Synapse のシーケンスは、ID 列を使用することで、または SQL コードを使用して系列の次のシーケンス番号を作成することで、処理されます。

## <a name="metadata-and-data-extraction"></a>メタデータとデータの抽出

Netezza 環境からメタデータとデータを抽出する方法を計画する場合は、次の情報を考慮します。

- **データ定義言語 (DDL) の生成:** 前に説明したように、Netezza の既存の `CREATE TABLE` および `CREATE VIEW` スクリプトを編集し、必要に応じてデータ型を変更して、同等の定義を作成することができます。 通常、このタスクでは、`ORGANIZE ON` のように Netezza に固有の句を削除または変更する必要があります。

  Netezza では、現在のテーブルとビューの定義を指定する情報が、システム カタログ テーブルに保持されます。 システム カタログ テーブルは、最新で完全な状態である可能性があるため、情報の最適なソースです。 ユーザーが管理するドキュメントは、現在のテーブル定義と同期されていない可能性があります。

nz_ddl_table のようなユーティリティを使用することで、Netezza のシステム カタログ テーブルにアクセスできます。 テーブルを使用して `CREATE TABLE` DDL ステートメントを生成し、それを Azure Synapse の同等のテーブル用に編集できます。 サードパーティの移行および ETL ツールでも、カタログ情報を使用して同じ結果が得られます。

- **データの抽出:** nzsql や nzsql などの標準的な Netezza ユーティリティと外部テーブルを使用して、既存の Netezza テーブルからフラットな区切りファイルに移行するための生データを抽出できます。 gzip を使用してファイルを圧縮した後、AzCopy または Azure Data Box などの Azure データ転送サービスを使用して、Azure Blob Storage にファイルをアップロードします。

  移行の演習では、できるだけ効率的にデータを抽出することが重要です。 Netezza に対して推奨される方法は、最も高速な方法でもある外部テーブルを使用することです。 複数の抽出を並列に実行し、データ抽出のスループットを最大にできます。

外部テーブルの抽出の簡単な例を次に示します。

  `CREATE EXTERNAL TABLE '/tmp/export_tab1.CSV' USING (DELIM ',') AS SELECT * from <TABLE-NAME>;`

   十分なネットワーク帯域幅が存在する場合は、Data Factory プロセスか、サードパーティのデータ移行または ETL 製品を使用して、オンプレミスの Netezza システムから Azure Synapse テーブルまたは Azure データ ストレージにデータを直接抽出できます。

   抽出されたデータに対して推奨されるデータ形式は、区切りテキスト ファイル ("_コンマ区切り値_" とも呼ばれます)、Optimized Row Columnar、または Parquet ファイルです。

Netezza 環境からデータと ETL を移行するプロセスの詳細については、データ移行 ETL と読み込みに関する Netezza のドキュメントを参照してください。

## <a name="performance-tuning-recommendations"></a>パフォーマンス チューニングに関する推奨事項

Netezza 環境から Azure Synapse に移動する場合、パフォーマンス チューニングの概念の多くは Netezza のものと似ています。

たとえば、次の概念はどちらの環境でも同じです。

- データ分散では、同じ処理ノードにデータが結合されて配置されます。
- 特定の列に対して最小のデータ型を使用すると、ストレージ領域が節約され、クエリ処理が高速化されます。
- 結合される列のデータ型を同一にしておくと、データを一致させるために変換する必要性が減るため、結合処理が最適化されます。
- 統計が最新であることを確認しておくと、オプティマイザーで最適な実行プランを生成するのに役立ちます。

最適化に関しては、プラットフォーム間にいくつかの違いがあります。 パフォーマンス チューニングに関する推奨事項の次の一覧では、Netezza と Azure Synapse での下位レベルの実装の相違点と、移行に対する代替手段が強調して示されています。

- **データ分散オプション:** Netezza と Azure Synapse の両方で、`CREATE TABLE` ステートメントを使用して、分散の定義を指定できます。 Netezza では `DISTRIBUTE ON` を使用し、Azure Synapse では `DISTRIBUTION =` を使用します。

   Azure Synapse は、小さいテーブルと大きいテーブル結合でローカル結合を実現するための追加の方法が提供されています。これは、スター スキーマ モデルで "_ディメンション テーブルとファクト テーブルの結合_" と呼ばれることがよくあります。 この方法では、小さいディメンション テーブルがすべてのノードにレプリケートされることにより、大きいテーブルの結合キーのすべての値に対して、一致するディメンション行をローカル環境で使用できるようになります。 ディメンション テーブルが大きくない場合、テーブルをレプリケートする場合のオーバーヘッドは比較的低くなります。 この場合、前に説明したハッシュ分散アプローチを使用することが推奨されます。

- **データのインデックス作成:** Azure Synapse には、ユーザー定義が可能なさまざまなインデックス作成オプションが用意されていますが、オプションは Netezza のシステム管理ゾーン マップとは操作および使用方法が異なります。 Azure Synapse でのインデックス作成オプションの詳細については、[Azure Synapse SQL プールでのインデックス テーブル](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-index)に関するページを参照してください。

   移行元 Netezza 環境内の既存のシステム管理ゾーン マップでは、データがどのように使用されているかをわかりやすく示すことができ、Azure Synapse 環境内でインデックスを作成するための候補列も示すことができます。

- **データのパーティション分割:** エンタープライズ データ ウェアハウスでは、ファクト テーブルに数 10 億行のデータが含まれる場合があります。 パーティション分割は、これらのテーブルでのメンテナンスとクエリを最適化するための手段です。 テーブルを個別のパーツに分割すると、一度に処理されるデータの量が少なくなります。 テーブルのパーティション分割は、`CREATE TABLE` ステートメントで定義されます。

  パーティション分割に使用できるフィールドは、テーブルごとに 1 つだけです。 多くのクエリが日付または日付範囲によってフィルター処理されるため、頻繁にパーティション分割に使用されるフィールドは日付フィールドです。 テーブルのパーティション分割は、初期読み込みの後で変更できます。 テーブルのパーティション分割を変更するには、`CREATE TABLE AS SELECT` ステートメントを使用する新しい分散でテーブルを再作成します。 Azure Synapse でのパーティション分割の詳細については、[Azure Synapse SQL プールでのテーブルのパーティション分割](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-partition)に関するページを参照してください。

- **データの読み込み用の PolyBase:** PolyBase は、大量のデータをウェアハウスに読み込むために使用する最も効率的な方法です。 PolyBase を使用して、並列ストリームでデータを読み込むことができます。

- **ワークロード管理用のリソース クラス:** Azure Synapse では、リソース クラスを使用してワークロードが管理されます。 一般に、大きなリソース クラスを使用すると、個々のクエリのパフォーマンスが向上します。 リソース クラスを小さくすると、より高いレベルのコンカレンシーが得られます。 動的管理ビューを使用して使用率を監視し、適切なリソースが効率的に使用されるようにすることができます。

## <a name="next-steps"></a>次の手順

Netezza 移行の実装の詳細については、オンプレミスの移行プランについて Microsoft アカウント担当者にお問い合わせください。
