---
title: 一般的なクラウド運用モデルを確認して比較する
description: 他の企業がどのようにクラウド運用モデルを実装しているかを学び、取り組みを支援するガイダンスを確認します。
author: BrianBlanchard
ms.author: brblanch
ms.date: 08/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: operating-model
ms.openlocfilehash: f4942f91b5ac265679a8cfb6545be9b81d459550
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94995926"
---
# <a name="compare-common-cloud-operating-models"></a>一般的なクラウド運用モデルを比較する

運用モデルは、サポートする対象のビジネスに特定かつ固有であり、それらの現在の要件と制約に基づいています。 しかし、このような独自性は、運用モデルに "_2 つと同じものがない_" ことを示唆するものではありません。 お客様の運用モデルには、いくつかの一般的なパターンがあります。 この記事では、最も一般的な 4 つのパターンについて説明します。

## <a name="operating-model-comparison"></a>運用モデルの比較

次の図は、最も複雑でない (非集中型) から最も複雑 (グローバルな運用) までの複雑さのスコープに基づいて、一般的な運用モデルをマップしています。 次の表は、他のいくつかの属性の相対値に基づいて、同じ運用モデルを比較したものです。

![運用モデルの複雑さの度合い](../_images/operating-model/operating-model-complexity.png)

### <a name="priorities-or-scope"></a>優先事項またはスコープ

クラウド運用モデルは、主に次の 2 つの要素によって推進されます。

- 戦略上の優先事項と動機。
- 管理するポートフォリオのスコープ。

|  | 非集中型の運用 (ops) | 集中型の運用 (ops) | エンタープライズ型の運用 (ops) | 分散型の運用 (ops) |
|--|--|--|--|--|
| **戦略上の優先事項** | イノベーション | コントロール | 民主化 | 統合 |
| **ポートフォリオのスコープ** | ワークロード | ランディング ゾーン | クラウド プラットフォーム | 完全なポートフォリオ |
| **ワークロード環境** | 複雑度が高い | 複雑度が低い | 複雑度が中程度 | 複雑度が中程度または可変 |
| **ランディング ゾーン** | 該当なし | 複雑度が高い | 複雑度が中程度から低い | 複雑度が低い |
| **基本ユーティリティ** | 該当なし | 該当なし、または少ないサポート | 集中化された、より多くのサポート | 最も多いサポート |
| **クラウド基盤** | 該当なし | 該当なし | ハイブリッド、プロバイダー固有、または地域の基盤 | 分散型と同期 |

- **戦略上の優先事項または [動機](../strategy/motivations.md):** 各運用モデルは、一般的な [クラウド導入の戦略的動機](../strategy/motivations.md)に対応できます。 ただし、一部の運用モデルでは、特定の動機を簡単に実現できます。

- **[ポートフォリオのスコープ](../reference/fundamental-concepts/hosting-hierarchy.md):** 下のポートフォリオ スコープの行は、特定の運用モデルがサポートするように設計されている最大のスコープを示しています。 たとえば、集中型の運用は、少数のランディング ゾーン向けに設計されています。 しかし、その運用モデルに決定した場合、多数のランディング ゾーンや複雑さが変化するランディング ゾーンの設計が必要とされる、大規模で複雑なポートフォリオを管理しようとしている組織に運用上のリスクが発生する可能性があります。

> [!IMPORTANT]
> クラウドの導入は、多くの場合、現在の運用モデルを見直すきっかけとなり、一般的な運用モデルの 1 つから別のどれかに切り替えることにつながることがあります。 しかし、クラウドの導入が唯一のきっかけなのではありません。 ビジネスの優先事項とクラウド導入のスコープによってポートフォリオをどのようにサポートする必要があるかは変わるので、最も適切に整合された運用モデルで他の変化が必要になることもあるでしょう。 取締役会または他の役員会が 5 年から 10 年の事業計画を策定するとき、多くの場合、それらの計画には、運用モデルを調整する (明示的または暗黙的な) 要件が含まれます。 これらの一般的なモデルは意思決定を導くための優れた指針ですが、運用モデルが変化したり、ご自身の要件や制約を満たすためにこれらのモデルのいずれかをカスタマイズしたりすることが必要になる場合があることに注意してください。

### <a name="accountability-alignment"></a>責任の整合

多くのチームと個人が、さまざまな機能をサポートするための責務を果たしますが、それぞれの一般的な運用モデルでは、意思決定とその結果に対する最終的な責任を 1 つのチームまたは 1 人の個人に割り当てます。 このアプローチは、運用モデルの資金調達方法と、各機能にどのレベルのサポートを提供するかに影響します。

||非集中型の運用 |集中型の運用  |エンタープライズ型の運用          |分散型の運用|
|---------              |---------      |---------    |---------          |---------|
|**ビジネスの整合**|[ワークロード チーム](../organize/cloud-adoption.md)|[中央のクラウド戦略](../organize/cloud-strategy.md)|[CCoE](../organize/cloud-center-of-excellence.md)|可変 - [幅広いクラウド戦略チームを編成?](../get-started/team/cloud-strategy.md)|
|**[クラウド運用](../organize/cloud-operations.md)**|[ワークロード チーム](../organize/cloud-adoption.md)|[中央 IT](../organize/central-it.md)|[CCoE](../organize/cloud-center-of-excellence.md)|ポートフォリオ分析に基づく - [ビジネス アラインメント](../manage/considerations/business-alignment.md)と[ビジネス コミットメント](../manage/considerations/commitment.md)に関するページを参照|
|**[クラウド ガバナンス](../organize/cloud-governance.md)**|[ワークロード チーム](../organize/cloud-adoption.md)|[中央 IT](../organize/central-it.md)|[CCoE](../organize/cloud-center-of-excellence.md)|[複数レイヤーのガバナンス](../govern/guides/complex/multiple-layers-of-governance.md)|
|**[クラウドのセキュリティ](../organize/cloud-security.md)**|[ワークロード チーム](../organize/cloud-adoption.md)|[セキュリティ オペレーション センター (SOC)](../organize/cloud-security-operations-center.md)|[CCoE](../organize/cloud-center-of-excellence.md) + [SOC](../organize/cloud-security-operations-center.md)|混合 - 「[セキュリティ戦略を定義する](../strategy/define-security-strategy.md)」を参照|
|**[クラウドの自動化と DevOps](../organize/cloud-automation.md)**|[ワークロード チーム](../organize/cloud-adoption.md)|[中央 IT](../organize/central-it.md) または該当なし|[CCoE](../organize/cloud-center-of-excellence.md)|ポートフォリオ分析に基づく - [ビジネス アラインメント](../manage/considerations/business-alignment.md)と[ビジネス コミットメント](../manage/considerations/commitment.md)に関するページを参照|

### <a name="accelerate-operating-model-implementation-in-azure"></a>Azure での運用モデル実装の加速

[運用モデルの定義](./define.md)に関するページで説明しているように、クラウド導入フレームワークの各手法によって、運用モデルの各側面を反復的に開発するための構造化されたパスが提供されます。 最も関連性のある方法に従うと、クラウド運用モデルのギャップに起因する導入の阻害要因を取り除くのに役立ちます。

ただし、次の表で説明するように、運用モデルの実装を加速させる方法があります。

|  | 非集中型の運用 | 集中型の運用 | エンタープライズ型の運用 | 分散型の運用 |
|--|--|--|--|--|
| **開始ポイント** | [Azure Well-Architected Framework (WAF)](/azure/architecture/framework/) | Azure ランディングゾーン: [小規模から始めるオプション](../ready/landing-zone/implementation-options.md) | Azure ランディング ゾーン: [CAF エンタープライズ規模](../ready/enterprise-scale/implementation.md) | [ビジネスの整合](../manage/considerations/business-alignment.md) |
| **イテレーション** | ワークロードに重点を置くと、チームは WAF 内で反復することができます。 | 小規模から始めるオプションでは、各手法で追加の反復が必要ですが、それはクラウド導入の取り組みが成熟するにつれて実行できます。 | 参照実装に示されているように、今後の反復では通常、小規模な構成の追加に重点を置きます。 | [Azure ランディングゾーンの実装オプション](../ready/landing-zone/implementation-options.md)を確認し、運用のベースラインに最も合ったオプションを使用して開始します。 そのオプションの設計原則に定義された反復パスに従います。 |

## <a name="decentralized-operations"></a>分散型運用

![分散型運用](../_images/operating-model/decentralized-operations.png)

運用は常に複雑です。 運用のスコープを 1 つのワークロードまたは少数のワークロードの集合に制限することで、その複雑さをコントロールできます。 そのため、一般的な運用モデルのうち最も複雑さが少ないのは非集中型の運用です。 この形式の運用では、すべてのワークロードが専任のワークロード チームによって個別に運用されます。

- **優先事項:** 複数のワークロードの間での集中管理または標準化よりも、イノベーションを優先します。
- **明らかな利点:** 設計、構築、運用を完全にコントロールするワークロードとビジネスのチームを配置することによって、イノベーションの速度を最大化します。
- **明らかに不利な点:** 次のものが減少: ワークロード間の標準化、共有サービスによるスケール メリット、一貫したガバナンスの集中化したコンプライアンスの取り組み。
- **リスク:** このアプローチでは、ワークロードのポートフォリオを管理する際にリスクが生じます。 ワークロード チームは、中央 IT 機能に特化した専門のチームを持っている可能性が低いため、この運用モデルは、一部の組織 (特にサードパーティのコンプライアンス要件に従う必要がある企業) からリスクの高いオプションと見なされています。
- **ガイダンス:** 非集中型の運用は、ワークロード レベルの意思決定に限定されます。 Microsoft Azure Well-Architected Framework は、そのスコープ内で行われる意思決定をサポートするように設計されています。 クラウド導入フレームワーク内のプロセスとガイダンスによって、非集中型の運用では必要とされないオーバーヘッドが追加される可能性があります。

### <a name="advantages-of-decentralized-operations"></a>非集中型の運用の利点

- **コスト管理:** 運用コストを 1 つの部署に簡単に対応付けることができます。 ワークロード固有の運用を使用するとワークロードをよりいっそう最適化できます。
- **責務:** 通常、この形式の運用は、オーバーヘッドを最小限にするために自動化に大きく依存しています。 責務は、リリース管理のための DevOps とパイプラインにフォーカスしたものになる傾向があります。 これにより、デプロイが高速化され、開発中のフィードバック サイクルが短くなります。
- **標準化:** ソース コードとデプロイ パイプラインを使用して、リリースごとに環境を標準化する必要があります。
- **運用のサポート:** 運用に影響を与える意思決定は、そのワークロードのニーズにのみ関係するため、運用上の意思決定が簡略化されます。 運用のスコープが狭いことから、DevOps コミュニティの多数の人は、これが最も純粋な形式の運用であると主張するでしょう。
- **専門知識:** DevOps チームと開発チームは、このアプローチによって最も権限を与えられ、市場の変化の促進に対して経験する抵抗が最も少なくなります。
- **ランディング ゾーンの設計:** 特定の運用上の利点はありません。
- **基本ユーティリティ:** 特定の運用上の利点はありません。
- **職務の分離:** 特定の運用上の利点はありません。

### <a name="disadvantages-of-decentralized-operations"></a>非集中型の運用の不利な点

- **コスト管理:** 企業コストを計算しづらくなります。 集中化したガバナンス チームが存在しないので、統一されたコスト制御や最適化を実装することが難しくなります。 大規模な場合、このモデルはコストが高くなる可能性があります。デプロイされた資産と人員の割り当てが各ワークロードで重複している可能性があるためです。
- **責務:** 集中化したサポート チームが存在しないことは、ガバナンス、セキュリティ、運用、変更管理についてワークロード チームが全面的に責務を負うことを意味します。 それらのタスクがコード レビューおよびリリース パイプラインで自動化されていない場合、これは不利です。
- **標準化:** ワークロードのポートフォリオ全体の標準化が一定せず、一貫性がなくなる可能性があります。
- **運用のサポート:** 多くの場合、スケール メリットはありません。 複数のワークロード間での統一されたベスト プラクティスと同様。
- **専門知識:** チーム メンバーは、アプリケーションの設計と構成におけるガバナンス、セキュリティ、運用、変更管理に関する意思決定について、賢明で倫理的な意思決定を行い、より大きな責務を果たします。 必要な専門知識を強化するために Microsoft Azure Well-Architected Review と Azure Well-Architected Framework を頻繁に検討する必要があります。
- **ランディング ゾーンの設計:** ランディング ゾーンはワークロード固有ではなく、このアプローチでは考慮されません。
- **基本ユーティリティ:** ワークロード間で共有される基本サービスは、あるとしても少数であるため、スケール メリットは低下します。
- **職務の分離:** DevOps チームと開発チームに対する要件が高く、それらのチームでの昇格された特権の使用回数が増加します。 職務の分離が必要な場合、このアプローチでの運用には、DevOps の成熟度への多大な投資が必要になります。

## <a name="centralized-operations"></a>集中型の運用

![集中型の運用](../_images/operating-model/centralized-operations.png)

安定した状態の環境では、個々のワークロードのアーキテクチャや個別の運用要件をそれほど重視する必要はないかもしれません。 集中型の運用は、主に安定した状態のワークロードで構成されるテクノロジ環境の標準です。 安定した運用状態の例としては、商用市販の成果物 (COTS) であるアプリケーションや、リリースの頻度が低い、定着しているカスタム アプリケーションなどがあります。 変化率が更新プログラムとパッチからなる標準の頻度で (イノベーションの高い変化率ではなく) 決まる場合、運用の集中化は、ポートフォリオを管理するための効果的な手段です。

- **優先事項:** イノベーションよりも集中管理を優先します。 また、最新のクラウド運用オプションへのカルチャの変化よりも、既存の運用プロセスの継続を優先します。
- **明らかな利点:** 集中化により、スケール メリット、最高レベルのコントロール、標準化された運用が導入されます。 このアプローチは、特定の構成でクラウド運用を既存の運用やプロセスに統合することが必要なクラウド環境に最適です。 このアプローチは、中程度のアーキテクチャの複雑さとコンプライアンス要件を持つ、数百のワークロードからなるポートフォリオがあるチームを集中化する場合に最も有利です。
- **明らかに不利な点:** 大規模ワークロードのポートフォリオの需要に合わせてスケーリングすることで、運用環境のワークロードに関する運用上の意思決定を行う集中化したチームに大きな負担がかかる場合があります。 技術資産のスケーリングで今後 18 か月から 24 か月以内にクラウド上の VM、アプリケーション、またはデータ ソースが 1,000 を超える規模になると予想される場合は、エンタープライズ型モデルを検討する必要があります。
- **リスク:** このアプローチにより、集中化が少数のサブスクリプション (多くの場合、1 つの運用サブスクリプション) に制限されます。 クラウド導入過程において、後から、導入計画に干渉する可能性のある大幅なリファクタリングが発生するリスクがあります。 具体的には、将来の大幅なやり直しを避けるために、セグメント化、環境の境界、ID ツール、その他の基本要素を考慮する必要があります。
- **ガイダンス:** "小規模から始めて拡張する" という開発速度に整合した Azure ランディング ゾーンの実装オプションを使用すると、妥当な開始点になります。 それらを使用して、導入作業を加速できます。 成功させるには、受け入れ可能なリスク許容範囲内での早期導入の取り組みをガイドする明確なポリシーを確立する必要があります。 統制と管理の手法によって、並行して運用を成熟させるプロセスが作成されます。 それらの手順はステージ ゲートとして機能し、運用が成熟するにつれてより高いリスクを許容する前に完了する必要があるます。

### <a name="advantages-of-centralized-operations"></a>集中型の運用の利点

- **コスト管理:** 複数のワークロード間で共有サービスを集中化することで、スケール メリットが生じ、重複するタスクが排除されます。 中央のチームは、エンタープライズ規模のサイズ調整と規模の最適化により、コスト削減をより迅速に実装できます。
- **責務:** 専門知識と標準化を中央に集中させることにより、安定性の向上、運用のパフォーマンス向上、変更に関連した障害のリスク低減につながる可能性があります。 これにより、ワークロードにフォーカスしたチームに対する広範なスキル育成の負担が軽減されます。
- **標準化:** 一般的に、運用の標準化とコストが最も少ないのは集中型モデルです。これは、重複するシステムやタスクが少ないためです。
- **運用のサポート:** 複雑さを軽減し、運用を集中化することで、小規模な IT チームによる運用のサポートが容易になります。
- **専門知識:** サポート チームの集中化により、セキュリティ、リスク、ガバナンス、運用の各分野の専門家が、ビジネス上の重要な意思決定を推進できるようになります。
- **ランディング ゾーンの設計:** 中央 IT 部門は、複雑さを軽減するために、ランディング ゾーンとサブスクリプションの数を最小限に抑える傾向があります。 ランディング ゾーンの設計は、前のデータセンターの設計を模倣する傾向があるため、移行時間が短縮されます。 導入が進むにつれて、共有リソースを別のサブスクリプションまたはプラットフォームの基盤に移すことができます。
- **基本ユーティリティ:** 既存のデータセンターの設計をクラウドに取り込むことにより、オンプレミスのツールと運用を模倣した基本的な共有サービスが得られます。 オンプレミス運用が主要な運用モデルである場合、これは利点となる可能性があります (以下の不利な点に注意してください)。 そうすることで移行時間が短縮され、スケール メリットを活用し、オンプレミスとクラウドでホストされるワークロード間で一貫した運用プロセスを実現できます。 このアプローチにより、短期間の複雑さと労力が軽減され、小規模なチームが少ない学習曲線でクラウド運用をサポートできるようになります。
- **職務の分離:** 集中型の運用では、職務の分離は明確です。 中央 IT 部門が運用環境のコントロールを維持し、そのため他のチームからの昇格されたアクセス許可の必要性が軽減されます。 これにより、昇格された特権を持つアカウントの数が減り、侵害の影響範囲を削減できます。

### <a name="disadvantages-of-centralized-operations"></a>集中型の運用の不利な点

- **コスト管理:** 中央のチームが、ワークロード レベルで影響のある最適化を実現するワークロード アーキテクチャを十分に理解していることはほとんどありません。 これにより、適切に調整されたワークロード運用によって得られるコスト削減の量が制限されます。 さらに、ワークロード アーキテクチャを理解していないことが原因で、集中化したコスト最適化によって、適切に設計されたワークロードのパフォーマンス、規模、またはその他の柱に直接影響が及ぶ可能性があります。 エンタープライズ規模のコスト変更を高プロファイルのワークロードに適用する前に、中央 IT チームは Microsoft Azure Well-Architected Review を完了して検討する必要があります。
- **責務:** 運用環境のサポートとアクセスを集中化すると、増加した運用上の負担が少数の人員にかかる可能性があります。 また、デプロイされたワークロードの詳細なレビューを実行し、セキュリティ、ガバナンス、コンプライアンスに関する詳細な要件に準拠していることを確認するために、それらの個人に大きな負担がかかります。
- **標準化:** 中央 IT のアプローチでは、中央の IT スタッフを直線的に増員することなく標準化を拡張することは困難です。
- **運用のサポート:** 上記の欠点とリスクではありません。 このアプローチで最も不利な点は、イノベーションを優先する大幅な規模と変化に関連しています。
- **専門知識:** この種類の環境では、開発者と DevOps の専門家が過小評価されたり、制約を受けすぎたりする可能性があります。
- **ランディング ゾーンの設計:** データセンターの設計は、前述のアプローチの制約に基づいていますが、それらはクラウドに必ずしも当てはまるわけではありません。 このアプローチに従うと、環境のセグメント化を再考し、イノベーションのチャンスを広げる機会が減少します。 また、ランディング ゾーンのセグメント化が欠如していることで、侵害の可能性が高まり、ガバナンスおよびコンプライアンス順守の複雑さが増し、クラウド導入過程の後半で導入の阻害要因が生じる可能性があります。 上記のリスクのセクションを参照してください。
- **基本ユーティリティ:** デジタル変革の過程で、クラウドが主要な運用モデルになる可能性があります。 オンプレミスの運用向けに構築された中央のツールを保持することで、運用を最新化する機会と運用効率の向上を促進する機会が減少します。 導入プロセスの早い段階で運用を最新化しないと選択しても、クラウド導入過程で後からプラットフォームの基礎となるサブスクリプションを作成することによって克服できますが、その取り組みは、事前に計画されていない複雑でコストと時間がかかるものになる可能性があります。
- **職務の分離:** 一般的に、集中型の運用は 2 つのパスのうちいずれかに従い、どちらもイノベーションを妨げる可能性があります。
  - **オプション 1:** 中央 IT 部門の外部のチームは、運用環境を模倣した開発環境への制限付きアクセスを許可されます。 このオプションは実験の妨げになります。
  - **オプション 2:** チームは、サポートされていない環境で開発とテストを行います。 このオプションは、デプロイ プロセスの妨げになり、デプロイ後の統合テストが遅れます。

## <a name="enterprise-operations"></a>エンタープライズ型の運用

![エンタープライズ型の運用](../_images/operating-model/enterprise-operations.png)

エンタープライズ型の運用は、すべてのクラウド運用に推奨されるターゲットの状態です。 エンタープライズ型の運用では、意思決定と責務を民主化して、コントロールの必要性とイノベーションのバランスを取ります。 中央 IT 部門は、より効率的なクラウドのセンター オブ エクセレンスつまり CCoE チームによって置き換えられます。そのチームはワークロード チームをサポートし、彼らの行動をコントロールしたり制限したりするのではなく、彼らに意思決定の責任を持たせます。 ワークロード チームには、適切に定義されたガードレールの範囲内でイノベーションを推進するために、より多くの権限と責務が与えられます。

- **優先事項:** 技術に関する意思決定の民主化を優先します。 技術に関する意思決定の民主化によって、以前は中央 IT 部門が担っていた責務が、必要に応じてワークロード チームに移行されます。 この優先事項の変化を実現するために、意思決定は、人間が実行するレビュー プロセスに依存することが少なくなり、クラウド ネイティブ ツールを使用した自動レビュー、ガバナンス、適用により多く依存するようになります。
- **明らかな利点:** 環境のセグメント化と職務の分離によって、コントロールとイノベーションのバランスを取ることができます。 集中型の運用では、コンプライアンスの強化や安定した状態の運用を必要とするワークロードや、より大きなセキュリティ リスクを表すワークロードに対して、集中化した運用を維持できます。 逆に、このアプローチでは、より高度なイノベーションを必要とするワークロードと環境については、集中管理を削減できます。 より大きなポートフォリオではコントロールとイノベーションのバランスを取るのに苦労する可能性が高いものですが、この柔軟性により、運用上の問題を削減しながら数千のワークロードに簡単に拡張できます。
- **明らかに不利な点:** オンプレミスで正常に機能したものが、エンタープライズ型のクラウド運用では適切に機能しない可能性があります。 運用に対するこのアプローチでは、多くの面で変更が必要になります。 多くの場合、制御権と責務におけるカルチャの変化が最大の課題です。 カルチャの変化に続く運用の変化は、実装、成熟、安定化に時間と献身的な努力を要します。 アーキテクチャの変化は、そうしなければ安定しないワークロードで必要になる場合があります。 ツールの変化は、カルチャ、運用、アーキテクチャの変化を強化およびサポートするために必要です。これには、主要なクラウド プロバイダーとの契約が必要になる場合があります。 これらの変更の前に行われる導入作業には、一般的なリファクタリング作業を超える大幅な修正が必要になる場合があります。
- **リスク:** このアプローチでは、変更戦略に対する役員のコミットメントが必要です。 また、学習曲線を克服し、必要な変化を実現するために、技術チームからのコミットメントも必要です。 長期的な利点を実現するには、ビジネス、CCoE または中央 IT、ワークロード チームの間に長期的な連携が必要です。
- **ガイダンス:** "エンタープライズ規模" として定義された Azure ランディング ゾーン実装オプションには、Azure のクラウド ネイティブ ツールを使用して技術的な変更を実現する方法を示す参照実装が用意されています。 エンタープライズ規模のアプローチでは、それらの実装を最大限に活用するために必要な運用とカルチャの変化についてチームをガイドします。 その同じアプローチを使用して、参照アーキテクチャを調整し、導入戦略とコンプライアンスの制約に合わせて環境を構成できます。 エンタープライズ規模の実装が完了したら、統制と管理の手法を使用してプロセスを定義し、特定の運用ニーズに合わせてコンプライアンスと運用の機能を拡張することができます。

### <a name="advantages-of-enterprise-operations"></a>エンタープライズ型の運用の利点

- **コスト管理:** 中央のチームはポートフォリオ間の最適化を行い、より高度なワークロードの最適化については個々のワークロード チームに責任を持たせます。 ワークロードにフォーカスしたチームは、意思決定を行う権限を与えられ、それらの意思決定がコストにマイナスの影響を及ぼす場合が明確化されています。 中央のチームとワークロード チームは、コストに関する意思決定について、適切なレベルで責任を共有します。
- **責務:** 中央のチームは、クラウド ネイティブ ツールを使用してガードレールを定義、適用、自動化します。 ワークロード チームの作業は、CCoE の自動化とプラクティスによって促進されます。 そのうえで、ワークロード チームは、イノベーションを推進し、それらのガードレール内で意思決定を行うための権限を与えられます。
- **標準化:** 集中化したガードレールと基本サービスによって、規模に関係なく、すべての環境にわたって一貫性が実現されます。
- **運用のサポート:** 集中型の運用のサポートを必要とするワークロードは、安定した状態のコントロールを持つ環境に分割されます。 職務のセグメント化と分離によって権限を与えられたワークロード チームが、独自の専用環境で運用サポートの責任を負います。 自動化されたクラウド ネイティブ ツールを使用して、ベースライン オファリングに対する集中化した運用サポートにより、すべての環境の最小限の運用ベースラインを保証します。
- **専門知識:** セキュリティ、リスク、ガバナンス、運用などのコア サービスの集中化により、適切な集中管理された専門知識が確保されます。 明確なプロセスとガードレールによって、ワークロード チームのすべてのメンバーに対して教育と権限を与え、より詳細な意思決定ができるようにすることで、集中化したエキスパートの影響力が拡大されます。
- **ランディング ゾーンの設計:** ランディング ゾーンの設計では、ポートフォリオのニーズを複製し、クラウドでワークロードを運用するために必要とされる明確なセキュリティ、ガバナンス、責任の境界を確立します。 セグメント化のプラクティスは、前のデータセンターの設計によって作成された制約に似ているとは言えません。 エンタープライズ型の運用では、ランディング ゾーンの設計はあまり複雑ではないため、迅速なスケーリングが可能になり、セルフサービスの需要に対する障壁を低減することができます。
- **基本ユーティリティ:** 基本ユーティリティは、プラットフォーム基盤と呼ばれる個別の集中管理されるサブスクリプションでホストされます。 中央のツールをユーティリティサービスとして各ランディング ゾーンに "パイプ" でつなぎます。 ランディング ゾーンから基本ユーティリティを分離すると、一貫性とスケール メリットが最大化され、集中管理される責務とワークロード レベルの責務が明確に区別されます。
- **職務の分離:** 基本ユーティリティとランディング ゾーンとの間の職務の分離が明確になることは、運用に対してこのアプローチを取ることの最大の利点の 1 つです。 クラウド ネイティブ ツールと妥当なプロセスを使用することで、中央に集中させたチームとワークロード チームの間で、Just-In-Time アクセスおよび適切なコントロールのバランスが可能になります。そのバランスは、個別のランディング ゾーンと、それらのランディング ゾーン セグメントでホストされているワークロードの要件に基づきます。

### <a name="disadvantages-of-enterprise-operations"></a>エンタープライズ型の運用の不利な点

- **コスト管理:** 中央のチームは、ランディング ゾーン内で運用の変更を行うために、ワークロード チームにより大きく依存します。 この変化によって、予算超過が発生するリスクが生じ、実際の支出規模の適正化が遅れる可能性があります。 予想外のコストを発生させないように、コスト管理プロセス、明確な予算、自動制御、定期的なレビューを事前に用意しておく必要があります。
- **責務:** エンタープライズ型の運用では、チーム間で責務と責任を明確にするために、中央のチームとワークロード チームにより多くのカルチャと運用の要件が必要です。
- 従来の変更管理プロセスまたは変更諮問委員会 (cabs) は、この運用モデルで必要とされるペースとバランスを維持する可能性は低くなります。 これらのプロセスは、クラウドの導入を安全に拡張するプロセスと手順の自動化に反映される必要があります。
- 変化に対するコミットメントの欠如は、まず交渉と、責務の整合に現れます。 責務の変化に対する整合ができないということは、短期間のクラウド導入の取り組みで中央 IT の運用モデルが必要になる可能性があることを示しています。
- **標準化:** 集中管理されたガードレールまたは自動化への投資の欠如によって、手動のレビュー プロセスでは克服しにくい標準化のリスクが生じます。 さらに、ランディング ゾーン内のワークロードとプラットフォーム基盤の共有サービス間の運用上の依存関係によって、アップグレード サイクルまたは将来のバージョンの基本ユーティリティでの標準化のリスクが高くなります。 プラットフォーム基盤のリビジョン中は、サポートされているすべてのランディング ゾーンとそれらがホストするワークロードについて、改善または自動化されたテストが必要です。
- **運用のサポート:** 自動化および集中化された運用によって提供される運用ベースラインは、影響が少ない、または重要度の低いワークロードの場合は十分でしょう。 ただし、複雑なまたは重要度の高いワークロードに対しては、ワークロード チームやその他の形式での専任の運用が必要になる可能性があります。 これにより、運用の予算に変化が必要になることがあります。そのため、部署は、それらの形式の高度な運用に対して運用経費を割り当てる必要があります。 中央の IT 部門のみに運用コストの責任を持たせる必要がある場合は、エンタープライズ型の運用を実装するのは困難です。
- **専門知識:** 中央 IT チームのメンバーは、以前に手動プロセスを通じて提供された中央コントロールの自動化に関する専門知識を獲得する必要があります。 また、それらのチームは、分岐、マージ、デプロイのパイプラインについて理解すると共に、環境を定義するために、コードとしてのインフラストラクチャの手法のスキルを身に付けなければならない場合もあります。 少なくともプラットフォーム自動化チームは、クラウドのセンター オブ エクセレンスまたは中央の運用チームによる意思決定に対応するために、これらのスキルを必要とします。 ワークロード チームは、意思決定を管理するコントロールとプロセスに関連した追加の知識を獲得する必要があります。
- **ランディング ゾーンの設計:** ランディング ゾーンの設計は基本ユーティリティに依存します。 取り組みの重複 (または自動化されたガバナンスでのエラーや競合) を回避するために、各ワークロードにフォーカスしたチームは、設計に含まれているものと禁止されているものを理解する必要があります。 また、柔軟性を得るために、ランディング ゾーンの設計に例外プロセスを織り込む必要もあります。
- **基本ユーティリティ:** 基本ユーティリティを集中化するには、オプションを検討し、さまざまな導入計画に合わせて拡張できるソリューションを開発するために時間がかかります。 そのため早期導入の作業が遅れる可能性がありますが、プロセス後半での加速と阻害要因の回避によって長期的には相殺されるはずです。
- **職務の分離:** 職務の明確な分離を保証するには、成熟した ID 管理プロセスが必要です。 ユーザー、グループ、オンボードおよびオフボード活動の適切な整合に関連する追加のメンテナンスが発生する場合があります。 昇格された特権での Just-In-Time アクセスに対応するために、新しいプロセスが必要になる可能性があります。

## <a name="distributed-operations"></a>分散型の運用

![分散型の運用](../_images/operating-model/complex-operations.png)

既存の運用モデルが細分化されすぎていて組織全体を新しい運用モデルに移行できない可能性があります。 それ以外に、グローバルな運用やさまざまなコンプライアンス要件によって、特定の部署に変化を起こすことが妨げられることがあります。 そのような企業では、分散型の運用アプローチが必要になる場合があります。 これは、これまでに説明した 1 つ以上の運用モデルの統合が必要であるため、はるかに複雑なアプローチです。

あまりお勧めできませんが、さまざまな部署の疎集合で構成されている組織では、運用に対してこのアプローチが必要になる場合があります。 特に、それらの部署が顧客セグメントまたは地域運用の多様な基盤にまたがっている場合です。

- **優先事項:** 複数の既存の運用モデルの統合。
- 時間をかけて組織全体を前述のいずれかの運用モデルに移行することに重点を置いた移行状態。
- 組織が大きすぎるか、複雑すぎるために 1 つの運用モデルに整合できない場合の、長期的な運用アプローチ。
- **明らかな利点:** 各部署の共通の運用モデル要素の統合。 運用の単位を階層にグループ化し、一貫性のある反復可能なプロセスを使用して運用を成熟させるのに役立つ手段を創出します。
- **明らかに不利な点:** 複数の運用モデル間での一貫性と標準化を長期にわたって維持することは困難です。 この運用アプローチを利用するには、ポートフォリオについて、およびテクノロジ ポートフォリオのさまざまなセグメントがどのように運用されるかについて深く理解している必要があります。
- **リスク:** 主要な運用モデルへのコミットメントがないと、チーム間で混乱が生じる可能性があります。 この運用モデルは、1 つの運用モデルに整合させる方法がない場合にのみ使用してください。
- **ガイダンス:** [ビジネス アラインメント](../manage/considerations/business-alignment.md)に関する記事に記載されている方法を使用して、ポートフォリオの詳細なレビューを使用して開始します。 ポートフォリオを望ましい状態の運用モデル (非集中型、集中型、またはエンタープライズ型) でグループ化するように注意してください。
- 運用モデルのグループ化を反映した管理グループ階層を作成し、その後、地域、部署、またはその他の基準を表すその他の組織パターンを作成して、最も一般的でないバケットから最も一般的なバケットまでワークロード クラスターをマップします。
- ワークロードと運用モデルの整合性を評価し、最初に最も関連性の高い運用モデル クラスターを見つけます。 管理グループ階層のそのノード下にあるすべてのワークロードに対して、その運用モデルにマップされているガイダンスに従います。
- 統制と管理の手法を使用して、階層のさまざまなポイントで共通する企業ポリシーおよび必要とされる運用管理のプラクティスを見つけます。 共通の Azure ポリシーを適用して、共有されている企業ポリシーを自動化します。
- それらの Azure ポリシーはさまざまなデプロイでテストされているので、さらに多くのワークロードにそれらのポリシーを適用して管理グループ階層の上位に移動することを試み、共通点と個別の運用ニーズを見つけます。
- このアプローチは、時間の経過と共に他のさまざまな運用モデル全体に拡張し、一連の共通するポリシーと手順を通じてチームを統合する運用モデルを定義するのに役立ちます。

このアプローチの利点と不利な点は、意図的に空白にしています。 ポートフォリオのビジネスへの整合を完了した後、利点と不利な点については、上記の主要な運用モデルのセクションを参照してください。

## <a name="next-steps"></a>次のステップ

運用モデルに関連した用語について説明します。 運用モデルが企業計画という、より大きなテーマにどのように適合するかが、用語によって理解しやすくなります。

> [!div class="nextstepaction"]
> [運用モデルの用語](./compare.md)

ランディング ゾーンによってクラウド導入環境の基礎構成要素が提供されるしくみについて説明します。

> [!div class="nextstepaction"]
> [一般的なクラウド運用モデルを比較する](../ready/landing-zone/index.md)
