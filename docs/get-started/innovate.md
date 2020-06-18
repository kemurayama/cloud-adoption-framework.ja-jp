---
title: 作業を開始しましょう。クラウドで新しい製品やサービスを構築する
description: 新しいクラウド製品とサービスの開発をガイドするアプローチとしてイノベーションの方法論について説明します。
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 79c428da9d0be27c209fcc30686225217832dbe1
ms.sourcegitcommit: bd9872320b71245d4e9a359823be685e0f4047c5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83862502"
---
# <a name="get-started-accelerate-new-product-and-service-innovation-in-the-cloud"></a>作業を開始しましょう。クラウドで新しい製品とサービスのイノベーションを促進する

クラウドで新しい製品やサービスを作成するには、移行とは異なるアプローチが必要です。 Azure 向けのクラウド導入フレームワークにおけるイノベーションの方法論では、新しい製品とサービスの開発をガイドするアプローチが確立されます。

このガイドでは、次の図で強調表示されているクラウド導入フレームワークの各セクションを使用します。 イノベーションは、標準的な移行と比べて予測しづらいものの、広義のクラウド導入計画の文脈には当てはまります。 このガイドは、企業がイノベーションに必要なサポートを提供すると共に、クラウド導入全体でバランスの取れたポートフォリオを形成するために必要な構造を提供するうえで役立ちます。

![クラウドにおけるイノベーション促進の概要](../_images/get-started/innovation-map.png)

## <a name="step-1-document-the-business-strategy"></a>手順 1:ビジネス戦略を文書化する

一般的な阻害要素を回避するには、イノベーションのための明確で簡潔なビジネス戦略を作成します。 動機と期待されるビジネス成果について利害関係者の意見をすり合わせておくことで、クラウド導入チームによる意思決定の方針が決まります。

**成果物:**

- [戦略と計画のテンプレート](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx)を使用して、動機および目標となるビジネス成果を記録します。

<!-- docsTest:ignore "Get started: Accelerate migration" -->

**成果物の完遂をサポートするうえでのガイダンス:**

- [動機](../strategy/motivations.md): 戦略的なすり合わせの第一歩は、イノベーション作業を推進する動機について合意を得ることです。 ビジネスと IT におけるさまざまな利害関係者の動機と共通テーマを把握し、分類することから始めます。
- [ビジネス成果](../strategy/business-outcomes/index.md):動機のすり合わせが済めば、目標となるビジネス成果が見えてきます。 この情報から、変革全体の測定に使用できる明確なメトリックが得られます。
- [ポートフォリオのバランスを取る](../strategy/balance-the-portfolio.md):イノベーションは、すべてのワークロードに適した導入パスではありません。 この導入手法は、アーキテクチャの見直しや完全な再構築が_要求_される新しいカスタムビルドのアプリケーションやワークロードに適しています。 すべてのワークロードについてイノベーションに大きく動機が傾いている場合、適切な投資収益率 (ROI) が確実に得られるようポートフォリオを評価することが大切です。 特定のリソースのモダン化や小規模な再構築作業を革新的なものにすることはできますが、その場合は、「[作業の開始: 移行を促進する](./migrate.md)」に従うことをお勧めします。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド戦略チーム | <li> クラウド導入チーム <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

## <a name="step-2-evaluate-the-business-justification"></a>手順 2:業務上の正当な理由を評価する

ビジネス ケースを作成する最初の段階で、クラウド導入に踏み切った場合に得られる概算の初期リターンを評価します。 この手順の目標は、"クラウドを全面的に導入することは、把握しているデータから、ビジネス上の賢明な判断と言えるか?" というたった 1 つの簡単な質問について、すべての利害関係者が一致した認識を持つことです。 クラウド導入という目標の中で、このイノベーション プロジェクトが、予想されるエンド ユーザーのニーズをどう満たすかについて、この質問を基にチームは共通認識を強めることができます。

**成果物:**

- [戦略と計画のテンプレート](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx)を使用して業務上の正当な理由を記録します。

**成果物の完遂をサポートするうえでのガイダンス:**

- [業務上の正当な理由](../strategy/cloud-migration-business-case.md): クラウドにおけるイノベーションの機会をそれぞれ評価する前に、業務上の正当な理由の大枠を完成させて、全体的な導入計画についての利害関係者の認識を一致させる必要があります。
- [事業価値における合意](../innovate/business-value.md):プロセスの初期段階では、イノベーションの価値を定量化するのが難しい場合があります。 この記事で取り上げる作業は、イノベーションに向けた特定の取り組みのビジネス価値についての共通認識を評価するうえで役立ちます。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド戦略チーム | <li> クラウド導入チーム |

## <a name="step-3-gather-data-and-analyze-assets-and-workloads"></a>手順 3:データを収集して資産とワークロードを分析する

ほとんどの企業では、既存の資産 (アプリケーション、VM、データなど) を使用することによってイノベーションを促進できます。 イノベーションのための計画では、そうした資産がいつ、どのようにクラウドへと移行されるのかを把握しておくことが大切です。

**成果物:**

- 既存インベントリの生データ (アプリケーション、VM、データなど)
- 提案されたイノベーションが既存のインベントリに依存する場合は、次の成果物がすべて揃っている必要があります。
  - 計画されたイノベーションをサポートするうえで必要な関連インベントリの定量分析。
  - イノベーションを実現するうえで必要な関連ワークロードの定性分析。
- イノベーションに向けた取り組みをサポートするうえで必要な新しいインベントリのコストを計算します。
- [戦略と計画のテンプレート](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx)内の業務上の正当な理由を厳密な計算で更新します。

**成果物の完遂をサポートするうえでのガイダンス:**

検出と評価によって、より深いレベルで一致した技術的な認識が得られれば、計画されたイノベーションに必要な依存ワークロードを移行するために使用できるアクション プランの作成に役立ちます。 このシナリオがよく見られるのは、既にあるデータ ソースや一元化されたアプリケーション、必須のサービス レイヤーが、その企業の他のコンテキストでイノベーションを生み出すために必要になるケースです。 依存システムがある場合は、検出と評価のガイドとして次の記事を参照してください。

- [既存システムのインベントリ](../digital-estate/inventory.md): プログラムを用いたデータドリブン アプローチで現在の状態を把握することが最初の手順です。 データを検出、収集することによって、あらゆる評価アクティビティが可能となります。
- [増分型の合理化](../digital-estate/rationalize.md#incremental-rationalization):すべての資産の定性分析に重点を置いて取り組む (場合によってはビジネス ケースまでサポートする) ために、評価作業を効率化します。 そのうえで、最初の 10 個のワークロードの詳細な定性分析を追加します。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド導入チーム | <li> クラウド戦略チーム |

## <a name="step-4-plan-for-migration-of-dependent-assets"></a>手順 4:依存資産の移行を計画する

新しいイノベーションが既存のワークロードや既存の資産に依存する場合でも、クラウド導入計画テンプレートは、プロジェクトのバックログをすばやく作成できるようになっています。 このバックログを編集して、検出結果、合理化、必要なスキル、パートナー契約を反映することができます。

**成果物:**

- バックログ テンプレートをデプロイします。
- テンプレートを更新して、移行する最初の 10 個のワークロードを反映します。
- メンバーとベロシティ (メンバーの時間) を更新して、リリースのタイミングを見積もります。
- タイムラインのリスク:
  - Azure DevOps を使い慣れていないと、このデプロイ プロセスに時間がかかる可能性があります。
  - 各ワークロードで使用できる複雑さとデータも、タイムラインに影響を与える可能性があります。

**成果物の完遂をサポートするうえでのガイダンス:**

- [クラウド導入計画のテンプレート](../plan/template.md): 基本テンプレートをデプロイします。
- [ワークロードの調整](../plan/workloads.md): バックログにワークロードを定義します。
- [作業の調整](../plan/assets.md): バックログの資産とワークロードを調整して、優先度の高いワークロードの作業を明確に定義します。
- [メンバーと時間の調整](../plan/iteration-paths.md): ワークロードのイテレーション、ベロシティ、リリースを確立します。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド導入チーム | <li> クラウド戦略チーム |

## <a name="step-5-align-governance-requirements-to-your-adoption-plan"></a>手順 5:ガバナンスの要件を導入計画に合わせる

計画されたイノベーションについてガバナンス チームと意見交換しておくことには、さまざまな阻害要因を未然に防ぐ効果があります。 新しい画期的なソリューションには、健全なガバナンス プラクティスでは推奨されない手法が要求される場合があります。 そうした必要となる機能の中には、自動ガバナンス適用ツールによってブロックされるものもあります。

**成果物:**

- イノベーションのニーズとガバナンスの制約との間に透明性と合意を形成します。
- 既存のガバナンスの制約に対する変更や例外を反映するために、必要に応じてポリシーとプロセスを更新します。

**成果物の完遂をサポートするうえでのガイダンス:**

次のリンクでは、クラウド ガバナンス チームによって採用されるアプローチを導入チーム向けにわかりやすく説明しています。

- [ガバナンスのアプローチ](../govern/index.md): 企業のポリシーとプロセスについて検討するためのプロセスを概説しています。 そのうえで、クラウド エンタープライズ作業全体でガバナンスを実現するために必要な規範を構築することができます。
- [企業ポリシーの定義](../govern/corporate-policy.md): ビジネス上のリスクを突き止めて軽減します。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド ガバナンス チーム <li> クラウド導入チーム | <li> クラウド戦略チーム <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

## <a name="step-6-define-operational-needs-and-business-commitments"></a>手順 6:運用ニーズとビジネス コミットメントを定義する

計画されたイノベーションについて、長期的な運用上の責任に関する計画を定義します。 確立された管理ベースラインで運用ニーズを十分に満たすことはできるでしょうか。 それができないのであれば、そのイノベーションを支えるテクノロジについて別途、資金運用のための選択肢を評価してください。

**成果物:**

- [Microsoft Azure Well-Architected Review](https://docs.microsoft.com/assessments/?id=azure-architecture-review) に必要事項を記入して、さまざまなアーキテクチャと運用の意思決定を評価します。
- 高度な運用が必要であれば、[運用管理ブック](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx)を調整して反映します。

**成果物の完遂をサポートするうえでのガイダンス:**

- [管理ベースラインの展開](../manage/best-practices.md):クラウド導入フレームワークのこのセクションでは、クラウドでの運用管理へのさまざまな移行について説明します。
- [高度な運用についての詳細を把握する](../manage/design-principles.md): 管理ベースラインの範囲を超える運用方法を紹介します。
- 実際の運用ニーズに対応するために高度な運用が要求される場合、[ビジネス コミットメント](../manage/considerations/business-alignment.md)を評価して、両方のチームに対する運用上の責任を明らかにします。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド運用チーム <li> クラウド導入チーム | <li> クラウド戦略チーム <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

## <a name="step-7-deploy-an-aligned-landing-zone"></a>手順 7:調整済みのランディング ゾーンをデプロイする

クラウドでホストされるすべての資産は、ランディング ゾーンに置かれます。 ランディング ゾーンは、ガバナンス、セキュリティ、運用についての明示的な要件を有している場合もあれば、 他のチームからのサポートが一切ない、まったく新しいサブスクリプションである場合もあります。 どちらのシナリオでも、大切なことは、最初からガバナンスと運用の要件に沿ったランディング ゾーンをまず用意することです。 承認済みのランディング ゾーンを最初から使用することで、チームは、ソリューションが運用環境にリリースされたときではなく、開発の早い段階でポリシー違反を発見できます。 早い段階で発見することによって阻害要因が排除され、変更を実行に移すために必要な時間が導入チームとガバナンス チームにもたらされます。

**成果物:**

- 早期のイノベーション中、リスクが低い初期の実験用に、最初のランディング ゾーンをデプロイします。
- ガバナンス、セキュリティ、運用についての共通認識を確保するために、クラウドのセンター オブ エクセレンスまたは中央 IT と共にリファクタリング計画を作成します。
- タイムラインのリスク:
  - 最初の 10 個のワークロードでは、ガバナンス、運用、セキュリティの要件によって、このプロセスに時間がかかることがあります。 最初のランディング ゾーンと後続のランディング ゾーンの実際のリファクタリングは長い時間がかかりますが、移行作業と並行して行う必要があります。

**成果物の完遂をサポートするうえでのガイダンス:**

- [ランディング ゾーンの選択](../ready/landing-zone/first-landing-zone.md): この記事を使用して、実際の導入パターンに基づいてランディング ゾーンをデプロイするための適切なアプローチを見つけます。 次に、その標準化されたコード ベースをデプロイします。
- [ランディング ゾーンを拡張する](../ready/considerations/index.md): 出発点に関係なく、デプロイされたランディング ゾーンに不足しているものを見極め、リソース編成、セキュリティ、ガバナンス、コンプライアンス、運用に必要なコンポーネントを追加します。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド プラットフォーム チーム <li> クラウド導入チーム | <li> クラウド導入チーム <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

## <a name="step-8-innovate-in-the-cloud"></a>手順 8:クラウドでイノベーションを起こす

イノベーションの方法論は、クラウドでイノベーションを起こすために最もよく使用されるツールと製品の管理手法についてのガイダンスとなります。 この手法には、以下の手順で着手することができます。

**成果物:**

- 顧客の暮らしを豊かにし、ビジネスの価値を高めるテクノロジベースのソリューション。
- クラウドを使用してそれらのソリューションの反復を迅速化し、さらに価値を高めるプロセスとツール。
  - 反復開発のアプローチ。
  - カスタム ビルド アプリケーション。
  - テクノロジベースのエクスペリエンス。
  - IoT を使用した物理的な製品とテクノロジの統合。
  - アンビエント インテリジェンス: 環境への非侵入型テクノロジの統合。
  - Azure Cognitive Services: ビッグ データ、AI、機械学習、予測ソリューション。

**成果物の完遂をサポートするうえでのガイダンス:**

- [事業価値における合意](../innovate/business-value.md):事業価値における直近の合意から 3 か月以上経過した場合、または合意が形成されていない場合は、ここから始めます。
- [Azure イノベーション ガイド](../innovate/innovation-guide/index.md):実用最小限の製品 (MVP) の作成を支援するツールやプロセスについて知り、革新的なソリューションのデプロイを促進するには、Azure イノベーション ガイドを利用します。
- [イノベーションのベスト プラクティス:](../innovate/best-practices/index.md) Azure のサービスを組み合わせてデジタル発明向けのツールチェーンを作成します。
- [フィードバック ループ](../innovate/considerations/adoption.md): インパクトのあるイノベーションを顧客に対して迅速に届ける改善されたフィードバック ループを作成します。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド導入チーム | <li> クラウドのセンター オブ エクセレンス <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

## <a name="value-statement"></a>バリュー ステートメント

このガイドで概説した手順は、皆さんやそのチームが、ビジネス価値の創造、適切なガバナンス、優れた設計を兼ね備えた革新的なソリューションをクラウドで作成するのに役立ちます。

## <a name="next-steps"></a>次のステップ

クラウド導入フレームワークはライフサイクル ソリューションです。 これは、イノベーションの取り組みを開始するのに役立ちます。 また、イノベーションの取り組みをサポートするチームの成熟度を高める効果もあります。 以下に示したチームは、後続の手順を使用して、その作業の成熟度を引き続き高めていくことができます。 これらは並行して行うプロセスであって直線的なものではなく、また阻害要因と考えるべきではありません。 それぞれが会社の全体的なクラウド対応を成熟させる効果を持った、並行したバリュー ストリームなのです。

| チーム | 次のイテレーション |
|---|---|
| クラウド&nbsp;導入&nbsp;チーム | 「[プロセス改善](../innovate/considerations/index.md)」では、顧客に影響を与え、継続的な導入を促進するイノベーションを生み出すためのアプローチについて深く分析します。 |
| クラウド&nbsp;戦略&nbsp;チーム | [戦略の方法論](../strategy/index.md)と[計画の方法論](../plan/index.md)は、導入計画と共に進化する反復的なプロセスです。 これらの概要ページに戻り、引き続きビジネス戦略と技術戦略の反復作業を行います。 |
| クラウド&nbsp;プラットフォーム&nbsp;チーム | [準備の方法論](../ready/index.md)に戻り、移行または他の導入作業をサポートする全体的なクラウド プラットフォームを引き続き発展させます。 |
| クラウド&nbsp;ガバナンス&nbsp;チーム | [ガバナンスの方法論](../govern/index.md)を使用して、ガバナンスのプロセス、ポリシー、規範を引き続き改善します。 |
| クラウド&nbsp;運用&nbsp;チーム | [管理の方法論](../manage/index.md)に基づいて、より充実した運用を Azure で実現します。 |