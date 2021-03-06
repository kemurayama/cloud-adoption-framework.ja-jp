---
title: クラウド ガバナンス ガイド
description: あらゆるガバナンス シナリオに対する段階的なアプローチのベスト プラクティスを示すクラウド ガバナンス ガイドを紹介します。
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: a39440dff04e267a80fa085dfdf6c565d33762cb
ms.sourcegitcommit: 8b82889dca0091f3cc64116f998a3a878943c6a1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89604846"
---
# <a name="cloud-governance-guides"></a>クラウド ガバナンス ガイド

このセクションの実用的なガバナンス ガイドでは、前に説明のあった[ガバナンスの方法論](../methodology.md)に基づいて、クラウド導入フレームワークのガバナンス モデルの増分アプローチについて説明します。 クラウド ガバナンス シナリオのニーズに合わせて成長する、クラウド ガバナンスに対するアジャイル手法を確立できます。

## <a name="review-and-adopt-cloud-governance-best-practices"></a>クラウド ガバナンスのベスト プラクティスを確認して採用する

クラウド導入体験を開始するには、次のガバナンス ガイドのいずれかを選択してください。 各ガイドでは、架空の顧客の一連の経験を基にして、ベスト プラクティスのセットの概要を説明しています。 クラウド導入フレームワークのガバナンス モデルの増分アプローチについて初めて読む場合は、いずれかのベスト プラクティスのセットを採用する前に、ガバナンス理論の高レベルの概要に関する以下の説明を確認してください。

- [標準的なガバナンス ガイド](./standard/index.md):推奨される 2 つのサブスクリプション モデルに基づく大半の組織向けのガイドです。複数のリージョンでのデプロイ向けですが、パブリック クラウドおよびソブリンまたは政府機関クラウドは対象ではありません。

> [!div class="nextstepaction"]
> [標準的なガバナンス ガイド](./standard/index.md)

- [複雑な企業向けのガバナンス ガイド](./complex/index.md):複数の独立した IT 事業部門で管理されている企業やパブリック クラウドおよびソブリンまたは政府機関クラウドにまたがる企業向けのガイドです。

> [!div class="nextstepaction"]
> [複雑な企業向けのガバナンス ガイド](./complex/index.md)

## <a name="an-incremental-approach-to-cloud-governance"></a>クラウド ガバナンスに対する漸進的アプローチ

## <a name="choose-a-governance-guide"></a>ガバナンス ガイドの選択

ガイドでは、ガバナンス MVP の実装方法が示されます。 さらに、各ガイドでは、クラウド ガバナンス チームがパートナーとしてクラウド導入チームより先行して、導入作業を高速化する方法が示されています。 クラウド導入フレームワークのガバナンス モデルでは、基礎からその後の改善や進化まで、ガバナンスの適用を案内します。

ガバナンス体験を始めるには、次の 2 つのオプションのいずれかを選択します。 オプションは、架空の顧客経験に基づいています。 ナビゲーションを容易にするため、タイトルは企業の複雑さに基づいています。 決定はより複雑になる可能性があります。 次の表では、2 つのオプションの違いの概要を示します。

> [!WARNING]
> より堅牢なガバナンスの開始点が必要になることがあります。 そのような場合は、[CAF エンタープライズ規模のランディング ゾーン](../../ready/enterprise-scale/index.md)を検討してください。 このアプローチは、1,000 を超える資産 (インフラストラクチャ、アプリ、またはデータ) をクラウドでホストするという中期目標 (24 か月以内) を設けている導入チームに焦点を当てています。 CAF エンタープライズ規模のランディング ゾーンは、大規模なクラウド導入の取り組みにおける複雑なガバナンス シナリオの典型的な選択です。
<!-- -->
> [!NOTE]
> どちらのガイドも、ユーザーの実際の状況と完全には一致していない可能性があります。 どちらか近い方のガイドを選択し、開始点として使用してください。 ガイド全体を通して、特定の条件を満たすよう決定をカスタマイズするのに役立つ追加情報が提供されます。

### <a name="business-characteristics"></a>ビジネスの特性

| 特徴 | 標準的な組織 | 複雑な企業 |
|---|---|---|
| 地理的な場所 (国または地理的地域) | 顧客やスタッフは主に 1 つの地理的な場所に存在する | 顧客やスタッフが複数の地理的な場所に存在するか、ソブリン クラウドを必要としている |
| 影響を受ける部署 | 一般的な IT インフラストラクチャを共有する部署 | 一般的な IT インフラストラクチャを共有しない複数の部署。 |
| IT 予算 | 1 つの IT 予算 | 複数の部署や通貨に割り当てられた予算。 |
| IT 投資 | 資本コスト主導型の投資が毎年計画され、通常は、基本的なメンテナンスのみがカバーされる。 | 資本コスト主導型の投資が毎年計画され、多くの場合、メンテナンスおよび 3 年から 5 年ごとの更新サイクルが含まれる。 |

### <a name="current-state-before-adopting-cloud-governance"></a>クラウド ガバナンス採用前に現在の状態

| State | 標準的な企業 | 複雑な企業 |
|---|---|---|
| データセンターまたはサード パーティのホスティング プロバイダー | 5 つ未満のデータセンター | 5 つ以上のデータセンター |
| ネットワーク | WAN なし、または 1 &ndash; 2 つの WAN プロバイダー | 複雑なネットワークまたはグローバル WAN |
| ID | 単一フォレスト、単一ドメイン。 | 複雑、複数フォレスト、複数ドメイン。 |

<!-- docutune:casing "Cost Management" "Security Baseline" -->

### <a name="desired-future-state-after-incremental-improvement-of-cloud-governance"></a>クラウド ガバナンスを段階的に改善した後の求められる将来の状態

| State | 標準的な組織 | 複雑な企業 |
|---|---|---|
| Cost Management: クラウド アカウンティング | ショーバック モデル。 課金は IT で集中管理される。 | チャージバック モデル。 課金は、IT 調達全体に分散できる。 |
| セキュリティ ベースライン: 保護されたデータ | 会社の財務データと IP。 制限された顧客データ。 サード パーティのコンプライアンス要件はない。 | 顧客の財務と個人データの複数のコレクション。 サード パーティのコンプライアンスの考慮が必要な場合がある。 |

## <a name="caf-enterprise-scale-landing-zone"></a>CAF エンタープライズ規模のランディング ゾーン

[CAF エンタープライズ規模のランディング ゾーン](../../ready/enterprise-scale/index.md)は、企業のセキュリティやガバナンスの要件を満たしながら、Azure クラウド プラットフォームの機能を最大限に活用できるアプローチです。

従来のオンプレミス環境と比較すると、Azure を使用することによって、ワークロード開発チームとビジネス スポンサーは、クラウド プラットフォームで提供されるより優れたデプロイの俊敏性を活用できます。 クラウド導入の取り組みが拡大され、ミッション クリティカルなデータとワークロードが組み込まれると、この俊敏性が社内の IT チームで設定されている企業セキュリティとポリシーのコンプライアンス要件と競合する可能性があります。 このことは、ガバナンスと規制に関する既存の高度な要件を持つ大企業に特に当てはまります。

CAF エンタープライズ規模のランディング ゾーンのアーキテクチャでは、企業のクラウド導入の作業時にクラウド導入チームの要件と中央 IT チームの要件との間でバランスを取るのに役立つアーキテクチャ、実装、およびガイダンスによって、導入ライフサイクルの早い段階でこれらの懸案事項に対処することを目的としています。 このアプローチの中心となるのは、共有サービス アーキテクチャと適切に管理されたランディング ゾーンの概念です。

CAF エンタープライズ規模のランディング ゾーンは、ガバナンス ポリシーで必要になる管理プロセス、規制要件、およびセキュリティ プロセスを統合して、Azure プラットフォーム内に独自の "分離クラウド" をデプロイします。 CAF エンタープライズ規模のランディング ゾーンは、この仮想境界内で、一貫性のあるコンプライアンスを確保すると同時にワークロードをデプロイするためのサンプル モデルを提供し、組織における役割と責任の分離をクラウドに実装するための基本的なガイダンスを提供します。

### <a name="caf-enterprise-scale-landing-zone-qualifications"></a>CAF エンタープライズ規模のランディング ゾーンの要件

小規模なチームでも CAF エンタープライズ規模のランディング ゾーンで提供されるアーキテクチャと推奨事項からメリットを得ることができます。 Microsoft が目標とするのは、CAF エンタープライズ規模のランディング ゾーンの実装を継続的に合理化し、小規模なチームにとってより使いやすいものにすることです。 現在、このアプローチは、大規模なクラウド環境を管理する中央の IT チームをガイドするように設計されています。

[CAF エンタープライズ規模のランディング ゾーン](../../ready/enterprise-scale/index.md)のアプローチは、**1,000 を超える資産 (アプリケーション、インフラストラクチャ、またはデータ資産) をクラウドでホストする**という中期目標 (24 か月以内) を設けている導入チームに焦点を当てています。

次の条件を満たす組織については、[CAF エンタープライズ規模のランディング ゾーン](../../ready/enterprise-scale/index.md)で開始することが適切である場合があります。

- 企業が、集中管理された監視機能と監査機能を必要とする規制コンプライアンス要件の影響を受ける。
- 共通のポリシーとガバナンスのコンプライアンス、およびコア サービスに対する集中的な IT 制御を維持する必要がある。
- 所属する業界が複雑なプラットフォームに依存しており、そのプラットフォームを制御するために複雑なコントロールや各分野の深い専門知識が必要になる。 これは、金融、製造、および石油ガス業界の大企業で最も一般的です。
- 既存の IT ガバナンス ポリシーにより、初期段階の導入時であっても、既存の機能とのより厳密な整合性が必要になる。

## <a name="next-steps"></a>次のステップ

次のいずれかのガイドを選択します。

> [!div class="nextstepaction"]
> [標準的な企業のガバナンス ガイド](./standard/index.md)
>
> [複雑な企業向けのガバナンス ガイド](./complex/index.md)
