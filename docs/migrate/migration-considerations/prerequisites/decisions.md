---
title: 移行に影響を与える意思決定
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 移行プロセスに関連して行われる重要な意思決定
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4bc84ad8bd2d0a0521399c1762585db6f9a5a6ab
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025411"
---
# <a name="decisions-that-affect-migrations"></a>移行に影響を与える意思決定

移行中に、意思決定や実行アクティビティに影響を与えるいくつかの要因が存在します。 この記事では、これらの意思決定の中心的なテーマについて説明した後、クラウド導入フレームワーク ガイダンスのこのセクションでの移行原則の説明を貫くいくつかの疑問について調べます。

## <a name="business-outcomes"></a>ビジネス成果

何らかの導入作業の目的または目標が、実行への推奨されるアプローチに大きな影響を与える場合があります。

- **移行。** 運用の成果の例には、差し迫ったビジネス上の動機、導入の速度、またはコスト削減があります。 これらの成果は、IT または運用モデルでの推移的な変更からビジネス価値を向上させようとする努力の中心に存在します。 クラウド導入フレームワークの「移行」のセクションは、移行に焦点を絞ったビジネス成果に大きな重点を置いています。
- **アプリケーションのイノベーション。** カスタマー エクスペリエンスの改善や増加する市場シェアは、増分型の成果の例です。 これらの成果は、現在の顧客のニーズや要望に焦点を絞った増分型の変更のコレクションから得られます。
- **データ主導のイノベーション。** 新しい製品またはサービス (特に、データの力から来るもの) は、破壊的な成果の例です。 これらの成果は、データを使用して市場の現状を混乱させる実験や予測の結果です。

これらの成果の 1 つだけを追求するビジネスは存在しません。 運用がなければ、顧客は存在せず、その逆も同じです。 クラウド導入もまったく同様です。 企業は一般に、これらの各成果を実現するために作業しますが、それらのすべてに同時に重点を置こうとすると、作業を非常に薄く分散させ、ビジネス ニーズが最も大きな利点を得る可能性のある作業の進捗を遅らせる場合があります。

この前提条件は、ユーザーにこれらの 3 つの目標のうちの 1 つを選択させるためではなく、代わりに、クラウド戦略チームとクラウド導入チームが、今後 3 か月間から 6 か月間の実行につながる一連の運用上の優先順位を確定するのに役立てるためのものです。 これらの優先順位は、このチームが次の 1 ～ 2 四半期に実行できる作業に関連しているため、項目別の 3 つの各オプションを*最も重要なもの*から*最も重要度の低いもの*にランク付けすることによって設定されます。

### <a name="acting-on-migration-outcomes"></a>移行の成果に基づいて行動する

運用の成果のランクが一覧内で最も高い場合、クラウド導入フレームワークのこのセクションはチームにとって適切に機能します。 このセクションでは、主な主要業績評価指標 (KPI) として速度とコスト削減を優先する必要があることを前提にしています。この場合、導入までの移行モデルは成果と適切に整合します。 移行に重点を置いたモデルは、データセンターを十分に使用したり、コスト削減を生成したりするために、サービスとしてのインフラストラクチャ (IaaS) 資産の "リフト アンド シフト" 移行に大きく依存しています。 このようなモデルでは、最新化は実行される可能性がありますが、主要な移行の目的が実現されるまでは二次的な焦点です。

### <a name="acting-on-application-innovations"></a>アプリケーションのイノベーションに基づいて行動する

市場シェアとカスタマー エクスペリエンスが主要な動機である場合、これは、チームの作業を導くためのクラウド導入フレームワークの最適なセクションではない可能性があります。 アプリケーションのイノベーションには、基になるインフラストラクチャには関係なく、ワークロードの最新化と切り替えに重点を置いた計画が必要です。 このような場合、このセクションのガイダンスは参考になることがありますが、中核の意思決定を導くための最適なアプローチではない可能性があります。

### <a name="acting-on-data-innovations"></a>データのイノベーションに基づいて行動する

データ、実験、研究開発 (R&D)、または新しい製品が今後 6 か月間ほどの優先事項である場合、これは、チームの作業を導くためのクラウド導入フレームワークの最適なセクションではない可能性があります。 データのイノベーションの作業はすべて、既存のソース データの移行に関連したガイダンスのメリットが得られます。 ただし、その作業のより広範囲な焦点は追加のデータ ソースのイングレスや統合に存在します。 そのガイダンスを予測や新しいエクスペリエンスを使用して拡張することは、IaaS 資産の移行よりはるかに重要です。

## <a name="balancing-the-portfolio"></a>ポートフォリオのバランスを取る

クラウド導入フレームワークのこのセクションでは、読者がバランスの取れたポートフォリオ内の変化に対処するためのさまざまなアプローチを理解するのに役立つ理論を確立します。 [ポートフォリオのバランス](../../expanded-scope/balance-the-portfolio.md)に関する記事は、この理論に基づいた行動に役立つように設計された拡張スコープの 1 つの例です。

## <a name="effort"></a>作業

移行作業は、含まれるワークロードのサイズや複雑さによって大きく異なる場合があります。 数百の仮想マシン (VM) を含む小さなワークロード移行は戦術的なプロセスであり、[Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-overview) などの自動ツールを使用して実装される可能性があります。 逆に、数万のワークロードの大規模なエンタープライズ移行には高度に戦略的なプロセスが必要であり、サービスとしてのプラットフォーム (PaaS) およびサービスとしてのソフトウェア (SaaS) 機能を統合した既存のアプリケーションの広範囲にわたるリファクタリング、再構築、および置き換えが含まれる場合があります。 計画的な移行の[スコープを識別してバランスを取ること](../../expanded-scope/balance-the-portfolio.md)は重要です。

現在の移行プログラムに長期的に影響を与える可能性がある何らかの決定を行う前に、次の意思決定に関する合意を作成することがきわめて重要です。

### <a name="effort-type"></a>作業の種類

大規模な (250 VM を超える) 移行では、合理化の 5 つの R (*リホスト*、*リファクター*、*再設計*、*再構築*、*置き換え*) で説明されているように、資産はさまざまな切り替えオプションを使用して移行されます。

一部のワークロードは*再構築*または*再設計*プロセスを通して最新化され、新機能および技術的な機能を備えたより最新のアプリケーションが作成されます。 その他の資産は*リファクター* プロセスを通ります (コンテナーへの移動や、必ずしもソリューションのコードベースに影響を与えないその他のより最新のホスティングおよび運用アプローチなど)。 一般に、仮想マシンや、より適切に確立されたその他の資産は*リホスト* プロセスを通り、これらの資産がデータセンターからクラウドに移行されます。 一部のワークロードはクラウドに移行される可能性がありますが、代わりに、同じビジネス ニーズを満たすサービス ベースの (SaaS ベースの) クラウド サービスを使用して (たとえば、Exchange Server インスタンスを移行する代わりに Office 365 を使用して) *置き換える*必要があります。

ほとんどのシナリオでは、一部のビジネス イベントにより高い割合の資産を*リホスト* プロセスを使用して一時的に移行させる強制関数が作成され、それらがクラウドに移行された後、他の移行戦略のいずれかを使用したより重要な二次的な切り替えが発生します。 このプロセスは一般に、*クラウド切り替え*と呼ばれます。

[デジタル資産の合理化](../../../digital-estate/calculate.md)のプロセス中に、これらの種類の意思決定が、移行する各資産に適用されます。 ただし、この時点で必要な前提条件は、ベースライン前提条件を作成することです。 5 つの移行戦略のうち、どれが、この移行作業を促進しているビジネス目標またはビジネス成果に最適に整合しているでしょうか? この決定は、移行作業全体を通してガイドの前提条件として機能します。

### <a name="effort-scale"></a>作業のスケール

移行のスケールは、次に重要な前提条件の意思決定です。 1,000 個の資産を移行するために必要なプロセスは、10,000 個の資産を移動するために必要なプロセスとは異なります。 移行作業を開始する前に、次の質問に答えることが重要です。

- **現在、いくつの資産がワークロードの移行をサポートしていますか?** 資産には、データ構造、アプリケーション、VM、および必要な IT アプライアンスが含まれます。 最初の移行の候補には比較的小さなワークロードを選択することをお勧めします。
- **これらの資産のうち、いくつが移行のために計画されていますか?** 持続したエンドユーザーの依存関係が不足しているために、移行プロセス中に一定の割合の資産を終了させることが一般的です。
- **移行可能な資産スケールのトップダウンの見積もりはどれくらいですか?** 移行に含めるワークロードについて、アプリケーション、仮想マシン、データ ソース、IT アプライアンスなどのサポート資産の数を見積もります。 関連する資産の識別に関するガイダンスについては、クラウド導入フレームワークの[デジタル資産](../../../digital-estate/index.md)に関するセクションを参照してください。

### <a name="effort-timing"></a>作業のタイミング

多くの場合、移行は、時間の制約がある説得力のあるビジネス イベントによって促進されます。 たとえば、1 つの一般的な動機としてサードパーティのホスティング契約の終了または更新があります。 移行を必要とする潜在的なビジネス イベントは多数存在しますが、それらには、終了日という 1 つの共通点があります。 アクティビティや速度を適切に計画して検証できるように、近づいているビジネス イベントのタイミングを理解することが重要です。

## <a name="recap"></a>まとめ

先に進む前に、次の前提条件を文書化し、それをクラウド戦略チームおよびクラウド導入チームと共有してください。

- ビジネス成果。
- 役割。 これは、*評価*、*移行*、*最適化*、*セキュリティ保護と管理*の各移行プロセスに対して文書化および改良されます。
- 完了の定義。 これは、*評価*、*移行*、*最適化*、*セキュリティ保護と管理*の各移行プロセスに対して個別に文書化および改良されます。
- 作業の種類。
- 作業のスケール。
- 作業のタイミング。

## <a name="next-steps"></a>次の手順

チームの間でプロセスが理解されたら、技術的な前提条件をレビューする必要があります。 [移行環境計画チェックリスト](./planning-checklist.md)は、技術的な基礎が移行のために準備できていることを確認するために役立ちます。

チームの間でプロセスが理解されたら、技術的な前提条件をレビューする必要があります。[移行計画チェックリスト] は、技術的な基礎が移行のために準備できていることを確認するために役立ちます。

> [!div class="nextstepaction"]
> [移行計画チェックリストをレビューする](./planning-checklist.md)