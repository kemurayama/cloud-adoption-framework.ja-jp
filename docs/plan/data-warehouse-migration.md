---
title: データ ウェアハウス移行の計画
description: データ ウェアハウスの移行、データ ウェアハウス移行プロセスの中心的手順、および各手順でのタスクに関するベスト プラクティスについて説明します。
author: v-hanki
ms.author: janet
ms.date: 06/24/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 4797f40f4353367a99ef68800becf23127c0c203
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94997456"
---
<!-- cSpell:ignore Informatica gzipped Attunity -->

# <a name="plan-a-data-warehouse-migration"></a>データ ウェアハウス移行の計画

データ ウェアハウスの移行は、どの企業にとっても容易なことではありません。 適切に実行し、うれしくない驚きや計画外のコストを回避するには、問題を徹底的に調査し、リスクを軽減し、移行を計画して、可能な限り準備しておく必要があります。 大まかに言えば、計画でデータ ウェアハウス移行プロセスの中心的手順と、その中のタスクがカバーされている必要があります。 プロセスの主要な手順は次のとおりです。

- 移行前の準備
- 移行の戦略と実行
- 移行後

たとえば、準備には、データ ウェアハウス移行チームの、スキルのトレーニングと技術の習熟に関する準備、といったものが含まれます。 また、概念実証ラボのセットアップ、テスト環境と運用環境の管理方法の理解、データと運用システムを企業ファイアウォールの外部に移行するための適切な許可の取得、移行を続けられるようにするためのデータセンターでの移行ソフトウェアのセットアップも含まれます。

データ ウェアハウスの移行を円滑に進めるには、計画で次のことを明確に理解しておく必要があります。

- ビジネス ケース (原動力、ビジネス上の利点、リスクなど)。
- 移行チームの役割と責任。
- 移行を成功させるために必要なスキル セットとトレーニング。
- 完全な移行に対して割り当てられた予算。
- 移行戦略。
- 遅延や修正を避けるために、移行プロジェクトのリスクを回避する方法。
- 既存のデータ ウェアハウス システム、そのアーキテクチャ、スキーマ、データ ボリューム、データ フロー、セキュリティ、運用上の依存関係。
- データ型、SQL 関数、ロジック、その他の考慮事項など、既存のオンプレミス データ ウェアハウスの DBMS と Azure Synapse の相違点。
- 移行が必要なものと優先順位。
- 移行タスク、アプローチ、順序、期限。
- 移行の管理方法。
- 移行の実行中にユーザーが中断されないようにする方法。
- 遅延を避け、移行を可能にするために、オンプレミスで行う必要があること。
- スキーマ、データ、ETL 処理を Azure に安全に移行できるようにするためのツール。
- 移行中および移行後に必要なデータ モデルの設計の変更。
- 移行前または移行後のテクノロジの変更と、修正を最小限にする方法。
- 移行後のテクノロジの廃止。
- 成功を保証するためのテストと品質保証を実装する方法。
- 進行状況を評価し、決定を下せるようにするためのチェックポイント。
- コンティンジェンシー計画と、問題が発生した場合のロールバックのポイント。

このことを理解するためには、移行を始める前に、特定のアクティビティを準備して開始する必要があります。 関係することについてさらに詳しく説明します。

## <a name="pre-migration-preparation"></a>移行前の準備

データ ウェアハウスの移行を始める前に、いくつかの事項に対処しておく必要があります。

### <a name="key-roles-in-a-data-warehouse-migration-team"></a>データ ウェアハウス移行チームでの主要な役割

移行プロジェクトの主な役割は次のとおりです。

- ビジネス所有者
- プロジェクト マネージャー (スクラムなどのアジャイル手法の経験があること)
- プロジェクト コーディネーター
- クラウド エンジニア
- データベース管理者 (既存のデータ ウェアハウスの DBMS と Azure Synapse)
- データ モデラー
- ETL 開発者
- データ仮想化スペシャリスト (データベース管理者でも可)
- テスト エンジニア
- ビジネス アナリスト (BI ツールのクエリ、レポート、分析のテストを支援するため)

さらに、チームにはオンプレミスのインフラストラクチャ チームのサポートが必要です。

### <a name="skills-and-training-to-ready-the-team-for-migration"></a>チームが移行のために準備する必要のあるスキルとトレーニング

スキルに関しては、データ ウェアハウスの移行では専門知識が重要です。 そのため、移行チームの適切なメンバーが、Azure クラウドの基礎、Azure Blob Storage、Azure Data Lake Storage、Azure Data Box、ExpressRoute、Azure の ID 管理、Azure Data Factory、Azure Synapse についてのトレーニングを受けるようにします。 データ モデラーは、多くの場合、既存のデータ ウェアハウスからの移行が行われた後で、Microsoft Azure Synapse のデータ モデルを微調整する必要があります。

### <a name="assessing-your-existing-data-warehouse"></a>既存のデータ ウェアハウスの評価

移行の準備のもう 1 つの部分として、既存のデータ ウェアハウスを完全に評価して、アーキテクチャ、データ ストア、スキーマ、ビジネス ロジック、データ フロー、使用されている DBMS 機能、ウェアハウス操作、依存関係を完全に理解する必要があります。 ここで理解をいっそう深めます。 システムがどのように機能するかについての詳細な知識があると、すべてのベースを伝達して対処するのに役立ちます。

評価の目的は、移行チーム全体で現在のセットアップについて詳しく理解することだけではなく、現在のセットアップの長所と短所を理解することです。 このため、現在のデータ ウェアハウスの評価の結果は、リフト アンド シフトとさらに広い範囲のことの比較に関する移行戦略に影響を与える可能性があります。 たとえば、評価の結果がデータ ウェアハウスの有効期間の終了である場合は、明らかに、戦略はリフト アンド シフト アプローチではなく Azure Synapse で新しく設計されたデータ ウェアハウスへのデータの移行になります。

### <a name="on-premises-preparation-for-data-migration"></a>データ移行のためのオンプレミスの準備

移行先環境向けに移行チームを準備し、現在のセットアップを評価するだけでなく、運用データ ウェアハウスは IT の手順や承認プロセスによって大幅に制御される傾向があるため、オンプレミスでの動きを始めることも同様に重要です。 遅延を回避するには、データセンター インフラストラクチャと運用チームで、データ、スキーマ、ETL ジョブなどを Azure クラウドに移行する準備ができていることを確認します。 データの移行は次の方法で実行できます。

- Azure Blob Storage への AzCopy。
- 圧縮されたデータを Azure に直接転送するための Microsoft Azure ExpressRoute。
- Azure Data Box へのファイルのエクスポート。

これらのオプションの選択に影響を与える主な要因は、データ ボリュームのサイズ (テラバイト) とネットワーク速度 (Mbps) です。 ネットワーク経由でデータを移行するのにかかる時間を決定するには計算が必要です。そのとき、データがデータ ウェアハウスでは圧縮されていて、エクスポート時には圧縮されなくなる可能性があることを考慮します。 このような状況では、データ転送が遅くなることがあります。 上記のいずれかの方法でデータを移動するときに、gzip を使用してデータを再圧縮します。 PolyBase では、gzip で圧縮されたデータを直接処理できます。 データ ボリュームが多く、データの移動に時間がかかりすぎる場合は、Azure Data Box 経由で移行する場合があります。

さらに、Azure からの既存のデータ ウェアハウス データのエクスポートの実行を Azure Data Factory で制御する場合は、セルフホステッド統合ランタイム ソフトウェアをデータセンターにインストールして、移行を続けられるようにする必要があります。 これらの要件があり、これを可能にするために正式な承認が必要な場合は、適切な承認プロセスを早い段階で開始すると、後で遅延が発生するのを防ぐことができます。

### <a name="azure-preparation-for-schema-and-data-migration"></a>スキーマとデータの移行のための Azure の準備

Azure 側での準備に関しては、Microsoft Azure ExpressRoute または Microsoft Azure Data Box のいずれかを使用して、データのインポートを管理する必要があります。 Azure Data Factory パイプラインは、データを Azure Blob Storage に読み込んだ後、そこから PolyBase を使用して Azure Synapse に読み込むための最適な方法です。 そのため、Azure 側での準備としてこのようなパイプラインを開発する必要があります。

別の方法としては、Azure Synapse がサポートされている場合は、Azure で既存の ETL ツールを使用します。これは、Azure Marketplace からツールを入手して Azure にセットアップし、データをインポートして Azure Blob Storage に読み込むようにパイプラインを準備することを意味します。

## <a name="defining-a-migration-strategy"></a>移行戦略の定義

### <a name="migration-goals"></a>移行の目標

どのような戦略でも、成功を示すためには一連の目標を定義する必要があります。 その場合、これらの目標を達成するためのターゲットを設定し、それらの達成に対して担当者に責任を持たせることができます。 クラウド データ ウェアハウス移行プロジェクトでの移行目標と、ターゲットを設定するための対応するメトリックの例を、次の表に示します。

目標の種類とメトリックの例:

#### <a name="improve-overall-performance"></a>全体的なパフォーマンスを向上させる

- データ移行のパフォーマンス
- ELT のパフォーマンス
- データ読み込みのパフォーマンス
- 複雑なクエリのパフォーマンス
- 同時ユーザーの数

#### <a name="run-at-lower-cost"></a>低コストで実行する

- ワークロードごとのコンピューティングのコスト。たとえば、コンピューティング時間数 x 1 時間あたりのコスト:
  - 標準レポート
  - アドホック クエリ
  - バッチ ELT 処理
- ストレージのコスト (ステージング、運用テーブル、インデックス、一時スペース)

#### <a name="operate-with-better-availability-and-service-levels"></a>運用の可用性とサービス レベルを向上させる

- サービスレベル アグリーメント
- 高可用性

#### <a name="improve-productively"></a>生産性を向上させる

- タスクの自動化と、管理作業量の削減

この場合、データ ウェアハウスの移行の成功は、データ ウェアハウスの実行速度が移行元のレガシ システムと同等以上で、コストがより低いことと解釈できます。 これらの目標の所有者を割り当てることで、それらの達成に対するアカウンタビリティが生じます。 また、概念実証ラボでのテストは (このガイドのリスク回避セクションで定義)、目標を達成できる方法が特定された場合に成功と見なされます。

### <a name="migration-approach"></a>移行のアプローチ

既存データ ウェアハウスの Azure Synapse への移行に関しては、いくつかの戦略オプションがあります。

- 既存のデータ ウェアハウスをそのままリフト アンド シフトする。
- 既存のデータ ウェアハウスを簡素化してから移行する。
- Azure Synapse でデータ ウェアハウスを完全に再設計して、データを移行する。

既存のデータ ウェアハウスの評価結果は、戦略に大きく影響します。 評価結果が良ければ、リフト アンド シフト戦略が推奨される場合があります。 機敏性の評価が低いために結果があまり良くない場合は、移行前に簡素化が必要であることを示している可能性があります。 結果が悪い場合は、完全な再設計が必要であることを示している可能性があります。

リフト アンド シフトでは、アーキテクチャをそのままにして、既存システムの移行作業が最小限になるようにします。 既存の ETL ツールで Azure Synapse が既にサポートされている場合は、最小限の労力でターゲットを変更できる可能性があります。 その場合でも、テーブル型、データ型、SQL 関数、ビュー、ストアド プロシージャのビジネス ロジックなどに違いがあります。これらの違いとそれに関する方法については、この移行シリーズの下位レベルのドキュメントで詳しく説明します。

移行前に既存のデータ ウェアハウスを簡素化するとは、複雑さを軽減して移行を容易にすることです。 これには、次のことが含まれます。

- 使用していないテーブルを移行前に削除またはアーカイブして、使用していないデータを移行しないようにする。
- データ仮想化ソフトウェアを使用して物理データ マートを仮想データ マートに変換し、移行する必要のあるデータを削減する。 変換により、機敏性の向上と総保有コストの削減も達成できるので、それは移行時の最新化と見なすことができます。

最初に簡素化してから、残りの部分をリフト アンド シフトすることもできます。

### <a name="migration-scope"></a>移行のスコープ

どのような戦略を選択する場合でも、移行のスコープ、移行の対象、段階的または一括のどちらで移行を行うかを、明確に定義する必要があります。 段階的移行の一例は、最初にデータ マートを移行し、次にデータ ウェアハウスを移行する場合です。 このアプローチを使用すると、優先度の高いビジネス領域に専念することができ、チームは、データ ウェアハウス自体を移行する前に、各マートを個別に移行することにより専門知識を少しずつ蓄積できます。

### <a name="defining-what-has-to-be-migrated"></a>移行が必要なものの定義

移行が必要なすべてのもののインベントリを作成します。 これには、スキーマ、データ、ETL プロセス (パイプライン)、認可特権、ユーザー、BI ツールのセマンティック アクセス レイヤー、および分析アプリケーションが含まれます。 インベントリの移行に関連する項目の詳細については、このシリーズの各下位レベルの移行に関する記事で説明されています。 これらへのリンクは後で示します。

- スキーマの移行、設計、およびパフォーマンスに関する考慮事項。
- データの移行、ETL 処理、読み込み。
- アクセスのセキュリティとデータ ウェアハウスの運用。
- 視覚化とレポートの移行。
- SQL の問題の影響の最小化。
- データ ウェアハウスの移行に役立つサードパーティ製ツール。

最適な方法がわからない場合は、概念実証ラボでテストを実施して、最適な手法を明らかにします。 詳細については、データ ウェアハウス移行プロジェクトのリスク回避に関するセクションを参照してください。

### <a name="migration-control"></a>移行の制御

Azure Synapse へのデータ ウェアハウスの移行には、実行する必要があるタスクが含まれます。

- オンプレミスでは、データのエクスポートなどです。
- ネットワークでは、データの転送などです。
- Azure クラウドでは、データの変換、統合、読み込みなどです。

問題は、すべてのスクリプトとユーティリティを、オンプレミス環境と Azure 環境の両方で個別に開発、テスト、実行する場合、これらのタスクの管理が複雑になる可能性があることです。 バージョン コントロール、テスト管理、移行の実行が調整されていない場合は、特に複雑さが増します。

このような複雑を回避し、ソース管理リポジトリを使用して共通の場所からそれらを制御することで、開発からテストや運用まで変更を管理する必要があります。 移行の実行には、オンプレミス、ネットワーク、Azure で行う必要があるタスクが含まれます。 Azure Synapse はターゲット環境であるため、Azure から移行の実行を制御すると管理が容易になります。 Azure Data Factory を使用して、オンプレミスと Azure の両方で実行を制御するための移行制御パイプラインを作成します。 これにより、自動化が導入され、エラーが最小限になります。 Data Factory は、エンタープライズ データ統合ツールだけでなく、移行オーケストレーション ツールにもなります。

Azure で活動している Microsoft パートナーから利用できるその他の移行制御オプションとしては、移行を自動化するためのデータ ウェアハウス自動化ツールがあります。 たとえば、WhereScape や Attunity などのベンダーです。 これらの自動化ツールのほとんどでは、リフト アンド シフト移行アプローチが対象になっています。 それでも、ストアド プロシージャなど、そのようなツールではサポートされないものがある場合があります。 これらの製品と他のいくつかの詳細については、Azure Synapse への移行を支援するサードパーティ製ツールのみに関する別のガイドを参照してください。

### <a name="migration-testing"></a>移行テスト

テストに必要な最初の作業は、一連のテストと、実行する必要がある各テストを確認して成功と見なすために必要な一連の結果を定義することです。 次のように、すべての側面をテストし、既存システムと移行後のシステムで比較することが重要です。

- スキーマ
- 必要に応じて変換されたデータ型
- Azure Synapse でユーザー定義スキーマを使用して、データ ウェアハウスとデータ マートのテーブルを区別する
- ユーザー
- ロールと、それらのロールに対するユーザーの割り当て
- データ アクセス セキュリティの特権
- データのプライバシーとコンプライアンス
- 管理機能を制御する特権
- データの品質と整合性
- テストなど、データ マートからデータ ウェアハウスとデータ ウェアハウスからデータ マートの両方について Azure Synapse を設定する ETL 処理
- 履歴を含むすべてのテーブルですべての行が正しい
- 緩やかに変化するディメンションの処理
- 変更データ キャプチャ処理
- システム間で異なる可能性のある関数を使用する計算と集計
- すべての既知のクエリ、レポート、ダッシュボードの結果
- パフォーマンスと拡張性
- 分析機能
- 新しい従量課金制環境でのコスト

可能な限りテストを自動化し、各テストを反復可能にして、結果を評価するための一貫した方法を有効にします。 レポートとダッシュボードが矛盾している場合は、元のシステムと移行後のシステムの間でメタデータの系列を比較できるようにすると、違いが強調され、検出が簡単でない場合に発生した場所を特定できるため、移行テスト中に有用です。

これを安全に実行する最善の方法は、ロールを作成し、ロールに特権を割り当てて、ユーザーをロールにアタッチすることです。 新しく移行されたデータ ウェアハウスにアクセスするには、新しいユーザーを作成してロールを割り当てる自動プロセスを設定します。 ロールからユーザーを削除する場合も同じようにします。

変更内容と予期されることを把握できるように、すべてのユーザーにカットオーバーを伝達します。

## <a name="de-risking-your-data-warehouse-migration-project"></a>データ ウェアハウス移行プロジェクトのリスク回避

データ ウェアハウスの移行におけるもう 1 つの重要な要素は、成功の可能性を最大限に高めるためにプロジェクトのリスクを回避することです。 データ ウェアハウスの移行のリスクを回避するためにできることがいくつかあります。 具体的な内容を次に示します。

- 概念実証ラボを設けることにより、チームがさまざまなことを試し、テストを実施し、問題を把握し、移行アプローチの検証、パフォーマンスの向上、コストの削減に役立つ修正や最適化を明らかにしたりできるようにします。 また、タスクを自動化する方法の確立、ベスト プラクティスをキャプチャするための組み込みツールの使用とテンプレートの作成、教訓の追跡にも役立ちます。 これは、リスクを軽減し、成功の可能性を高めるための非常に重要な方法です。 また、移行戦略で定義されている移行の目標とターゲットの達成に対して責任を負う所有者をテストに割り当てることができます。
- BI ツールとデータ ウェアハウスおよびデータ マートの間にデータの仮想化を導入します。 次の図に示すように、データ仮想化を使用してユーザーの透過性を導入することによりデータ ウェアハウスの移行のリスクを軽減し、データ仮想化の BI ツールを使用してユーザーから移行が見えないようにします。

![データ ウェアハウス移行の図](../_images/data-warehouse-migration.png)

この目的は、セルフサービスの BI ツールを使用するビジネス ユーザーと、移行対象の基になるデータ ウェアハウスとデータ マートの物理スキーマの間の依存関係を解消することです。 データの仮想化を導入することにより、Azure Synapse へのデータ ウェアハウスとデータ マートの移行の間に行われた (たとえば、パフォーマンス最適化のための) スキーマの変更を、ビジネス ユーザーから見えないようにできます。ビジネス ユーザーは、データ仮想化レイヤーの仮想テーブルだけにアクセスするためです。 構造的な変更が必要な場合は、ユーザーが引き続きそれらの変更や移行を認識しないように、データ ウェアハウスまたはデータ マートと仮想テーブルの間のマッピングのみを変更する必要があります。

- 使用されていないテーブルを移行してもほとんど意味がないため、データ ウェアハウスを移行する前に、使用されないことがわかった既存のテーブルをアーカイブすることを検討します。 これを行う方法の 1 つとして、使用されていないデータを Azure Blob Storage または Azure Data Lake Storage にアーカイブし、そのデータが引き続きオンラインになるように、Azure Synapse で外部テーブルを作成します。
- Azure に開発バージョン (通常は無料) の仮想マシン (VM) を導入し、この VM 上で既存のレガシ データ ウェアハウスの DBMS を実行する可能性を検討します。 これにより、既存のデータ ウェアハウスのスキーマを VM にすばやく移動した後、Azure クラウドだけで作業している間に Azure Synapse に移動することができます。
- 移行の順序と依存関係を定義します。
- インフラストラクチャ チームと運用チームが、できるだけ早期にデータを移行プロジェクトに移行する準備ができていることを確認します。
- DBMS の機能の違いと、独自のビジネス ロジックが問題になる可能性がある場所を特定します。 たとえば、ELT 処理にストアド プロシージャを使用していると、簡単には移行できず、変換がコードに埋め込まれているため、メタデータ系列が含まれません。
- データ マートを最初に移行し、データ マートに対するソースであるデータ ウェアハウスをその後で移行する戦略を検討します。 このようにすると、段階的な移行が可能になるため、管理が容易になり、ビジネス ニーズに基づいて移行の優先順位を決められるためです。
- データの仮想化を使用して、移行の前に現在のデータ ウェアハウスのアーキテクチャを簡素化する可能性を検討します。たとえば、データ マートを仮想データ マートに置き換えて、移行前に機能を失うことなく、データ マート用の物理的なデータ ストアと ETL ジョブを除去できるようにします。 このようにすると、移行するデータ ストアの数やデータのコピーの数を減らし、総保有コストを削減し、機敏性を向上させることができます。 これには、データ ウェアハウスを移行する前に、データ マートを物理から仮想に切り替える必要があります。 多くの点で、これは移行前のデータ ウェアハウスの最新化手順と考えることができます。

## <a name="next-steps"></a>次のステップ

データ ウェアハウスの移行の詳細については、Informatica から提供されている、[Azure でのクラウド データ ウェアハウスの最新化に関する仮想ワークショップ](https://now.informatica.com/Microsoft_CDW_Workshops.html)に参加してください。
