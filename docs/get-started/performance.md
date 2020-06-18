---
title: 作業を開始しましょう。ポートフォリオ全体で一貫したパフォーマンスを確保する
description: パフォーマンスの維持、期待値の設定、組織的連携の確立など、ポートフォリオ全体にわたるパフォーマンス管理の基礎について説明します。
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: b200fb8dee07c016338beed9b9356d00e26a8abd
ms.sourcegitcommit: 070e6a60f05519705828fcc9c5770c3f9f986de5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83814343"
---
# <a name="get-started-ensure-consistent-performance-across-a-portfolio"></a>作業を開始しましょう。ポートフォリオ全体で一貫したパフォーマンスを確保する

ワークロードのポートフォリオ全体で十分なパフォーマンスを確保するにはどうすればよいのでしょうか。 このガイドの手順は、このレベルのパフォーマンスを維持するためのプロセスを確立する際に役立ちます。

パフォーマンスは、他の役割や機能にも依存します。 この記事では、関与するチーム間の連携の確立に役立つサポート機能について説明します。

ポートフォリオ全体で一貫したパフォーマンスを確保するうえで最も一般的なアプローチは、運用管理の一元化です。 運用プラクティスに関する決定事項によって、運用ベースラインと全体的な改善点が明確になります。

このガイドの最初の手順は、運用チームの最初の一歩を手助けするものです。 後続の手順では、ワークロードのポートフォリオ全体でのエンタープライズ パフォーマンスに向けて共有された取り組みに企業全体が着手できるよう支援します。

![エンタープライズ パフォーマンス管理の概要](../_images/get-started/performance-map.png)

## <a name="step-1-establish-operations-management-requirements"></a>手順 1:運用管理の要件を規定する

Azure 用の Microsoft クラウド導入フレームワークにまとめられている運用管理ベースラインでは、一貫した運用を確保するための一連の制御とクラウドネイティブの運用ツールが提供されます。 そのベースラインを自動化ツールで拡張することにより、ポートフォリオ全体で一貫したパフォーマンス要件を満たすためのパフォーマンス監視と自動化が実現されます。

**成果物:**

- パフォーマンスの期待値からの逸脱に関連した自動修復タスクを含むように管理ベースラインを改善します。
- パフォーマンス要件を満たすために、ワークロード固有のデータ パターンやアーキテクチャの変更が必要な場合、ワークロード固有の運用によって、より優れたパフォーマンス管理が可能となります。
- [運用管理ブック](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx)で、IT ポートフォリオ全体にわたる運用上の決定事項を文書化します。 **[Baseline]\(ベースライン\)** タブの **[Operational Compliance]\(運用のコンプライアンス\)** セクションに、パフォーマンスの自動化に関する決定事項を含めることに重点を置きます。

**成果物の完遂をサポートするうえでのガイダンス:**

- [管理ベースラインの改善](../manage/azure-management-guide/enhanced-baseline.md)に関する記事では、Azure Automation などのツールを使用して、パフォーマンスに関連した強化を追加する例を取り上げています。 このアプローチは、サポート資産のサイズとスケールの基本的な変更によって一貫したパフォーマンスを維持するのに役立ちます。
- [ワークロード固有の運用](../manage/azure-management-guide/platform-specialization.md)に関する記事では、Microsoft Azure Well-Architected Review を使用して、特定のワークロードの自動化に関するガイダンスを提供します。 パフォーマンス管理のこのアプローチは、ワークロード固有のデータによって運用上のアクションを促進する必要がある場合に特に役立ちます。
- 前述のガイダンスは、[管理ベースライン](../manage/considerations/discipline.md)の既存の実装で、ワークロードの完全なポートフォリオがサポートされていることを前提としています。

> [!NOTE]
> クラウド導入ライフサイクル全体におけるさまざまな判断がパフォーマンスに直接影響します。 以降の手順では、IT ポートフォリオ全体でパフォーマンスを上げるために必要な連携と支援について概説します。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド運用チーム | <li> クラウド戦略チーム <li> クラウド導入チーム <li> クラウド ガバナンス チーム <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

## <a name="step-2-consistent-application-of-the-management-baseline"></a>手順 2:管理ベースラインを一貫性をもって適用する

管理ベースラインが改善されたら、それらの改善がリソースの整合性ガバナンス規範にも適用されるようにすることが重要です。 そうすることで、管理下のすべての環境に対し、改善されたベースラインが確実に適用されます。

**成果物:**

- 対象となるすべてのシステムに、改善された管理ベースラインが適切に適用されていることを確認します。
- [リソースの整合性規範テンプレート](../govern/resource-consistency/template.md)で、リソースの整合性のポリシー、プロセス、設計ガイダンスを文書化します。

**成果物の完遂をサポートするうえでのガイダンス:**

- すべてのワークロードとリソースが、[適切な名前付けおよびタグ付け規則](../ready/azure-best-practices/naming-and-tagging.md)に従っていることを確認します。 "重要度" のタグに特に重点を置いて、[Azure Policy を使用してタグ付け規則を適用](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags)します。
- クラウド ガバナンスを初めて使用する場合は、ガバナンス手法を使用して、[ガバナンスのポリシー、プロセス、規範](../govern/index.md)を確立します。
- コスト管理ガバナンス規範を初めて使用する場合は、[コスト管理の改善に関する記事](../govern/guides/complex/cost-management-improvement.md)に従って検討してください。特に、[実装](../govern/guides/complex/cost-management-improvement.md#incremental-improvement-of-the-best-practices)に関するセクションを重点的にお読みください。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド ガバナンス チーム | <li> クラウド戦略チーム <li> クラウド運用チーム <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

## <a name="step-3-define-strategy"></a>手順 3:戦略を定義する

戦略的な決定は、パフォーマンスに直接影響を及ぼし、その影響は導入ライフサイクル全体と長期的な運用に波及します。 戦略を明確にすることで、パフォーマンスへの取り組みがポートフォリオ全体で向上します。 また、この明確化によって、ワークロードの特殊化と高度な運用がある程度必要とされるワークロードを運用チームが把握しやすくなります。

**成果物:**

- [戦略と計画のテンプレート](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx)に、動機、成果、業務上の正当な理由を記録します。
- 管理ベースラインによって、クラウド導入の戦略的な方向性に沿った運用サポートが確実に提供されるようにします。

**成果物の完遂をサポートするうえでのガイダンス:**

- [動機を把握する](../strategy/motivations.md): 重要なビジネス イベントや、移行の動機によっては、コストが重視される傾向があり、後のすべての作業でコスト管理の重要性が高まります。 一方、イノベーションまたは移行による成長に関連した未来志向の動機の場合、営業収益がより重視されます。 動機を把握することで、コスト管理にどの程度の優先度を置くべきかが理解しやすくなります。
- [ビジネス成果](../strategy/business-outcomes/index.md):一部の財政上の成果では、コストが極端に重視される傾向があります。 目的の成果を財務メトリックに対応付ける場合は、初期段階でコスト管理ガバナンス規範に投資してください。
- [業務上の正当な理由](../strategy/cloud-migration-business-case.md): 業務上の正当な理由は、クラウド導入の財務計画の概要を示します。 これは、最初の予算作成に役立つ情報源となる可能性があります。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド戦略チーム | <li> クラウド ガバナンス チーム <li> クラウド運用チーム <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

## <a name="step-4-assess-and-plan-for-workload-adoption"></a>手順 4:ワークロードの導入を評価、計画する

デジタル資産 (既存の IT ポートフォリオの分析) は、業務上の正当な理由の検証に役立ち、IT ポートフォリオの詳細を把握できるようになります。 導入計画により、導入時のアクティビティのタイムラインが明確になります。 計画とデジタル資産分析の整合性を確保することで、運用管理における将来の依存関係を計画する手段が得られます。

また、計画を理解することで、クラウド運用チームを開発サイクルに招きます。 チームは、ワークロードを運用するために必要な管理ベースラインに対する変更を評価し、計画することができます。

**成果物:**

- [戦略と計画のテンプレート](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx)を更新して、デジタル資産分析によってもたらされた変更を反映します。
- クラウド運用チームと連携して、短期的および長期的な導入計画における各ワークロードの重要度とビジネスへの影響を明確に定義します。
- クラウド運用チームと連携して、オペレーション レディネスのタイムラインを確立します。

**成果物の完遂をサポートするうえでのガイダンス:**

- [インベントリの収集](../digital-estate/inventory.md): 導入前に、デジタル資産を分析するためのデータ ソースを確立します。
- [ベスト プラクティス - Azure Migrate](../plan/contoso-migration-assessment.md): Azure Migrate を使用してインベントリを収集します。
- [増分型の合理化](../digital-estate/rationalize.md#incremental-rationalization):増分型の合理化を進める中で、定量分析を使用して、予算編成のためにクラウドの候補を特定します。
- [コスト モデルと予測モデルの対応付け](../digital-estate/calculate.md): Azure Cost Management を使用して、[予算を作成](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)することにより、コスト モデルと予測モデルを対応付けます。
- [クラウド導入計画の作成](../plan/plan-intro.md#build-your-cloud-adoption-plan): 実用的なワークロード、資産、タイムラインの詳細を含む計画を作成します。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド戦略チーム | <li> クラウド ガバナンス チーム <li> クラウド運用チーム <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

## <a name="step-5-expand-the-landing-zones"></a>手順 5:ランディング ゾーンを拡張する

クラウド導入フレームワークの準備方法では、クラウドでワークロードをホストするランディング ゾーンの開発に重点を置いています。 ランディング ゾーンの実装中は、さまざまな意思決定が運用に影響を及ぼす可能性があります。

ランディング ゾーンを見直して、よりよい運用を実現するために、クラウド運用チームに助言を求めます。 また、ランディング ゾーンの設計に影響を及ぼす可能性のある設計ガイダンスと "リソースの整合性" ポリシーを理解するために、クラウド ガバナンス チームにも助言を求めます。

**成果物:**

- 短期的な導入計画で、ワークロードをホストできる 1 つ以上のランディング ゾーンをデプロイします。
- すべてのランディング ゾーンが運用の決定事項とリソースの整合性の要件に沿っていることを確認します。

**成果物の完遂をサポートするうえでのガイダンス:**

- [ランディング ゾーンの運用を改善する](../ready/considerations/landing-zone-operations.md): ランディング ゾーン内での運用を改善するためのベスト プラクティス。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド導入チーム | <li> クラウド運用チーム <li> クラウド戦略チーム <li> クラウド ガバナンス チーム <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

## <a name="step-6-adoption"></a>手順 6:導入

長期的な運用は、移行とイノベーションの取り組みの中で行った意思決定の影響を受けることがあります。 導入プロセスの初期段階で一貫した整合性を維持することで、運用リリースに対する障壁を取り除くことができます。 また、新しいソリューションを運用管理プラクティスにオンボードするために必要な作業が削減されます。

**成果物:**

- リソースの整合性ポリシーを使用して、運用環境のデプロイの運用準備状況をテストします。
- リソースの整合性の設計ガイダンスと運用の要件に準拠していることを確認します。
- 高度な運用の要件を[運用管理ブック](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx)で文書化します。

**成果物の完遂をサポートするうえでのガイダンス:**

- [環境の準備状況チェックリスト](../migrate/migration-considerations/prerequisites/planning-checklist.md)
- [昇格前のチェックリスト](../migrate/migration-considerations/optimize/ready.md)
- [運用リリースのチェックリスト](../migrate/migration-considerations/optimize/promote.md)

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド導入チーム | <li> クラウド戦略チーム <li> クラウド運用チーム <li> クラウド戦略チーム <li> クラウド ガバナンス チーム <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

## <a name="value-statement"></a>バリュー ステートメント

上記の手順によって、企業全体およびホストされているすべてのリソースでパフォーマンスを確保するための制御とプロセスを実装できます。