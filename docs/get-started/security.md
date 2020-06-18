---
title: 作業を開始しましょう。企業環境をセキュリティで保護する
description: クラウド導入の取り組みおよび運用時の重要なポイントでのセキュリティ統合の概要。
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 0ea7caddcc0bcc6e5f2564c2833341b54b9347e3
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83752262"
---
<!-- cSpell:ignore CISO passwordless -->

# <a name="get-started-implement-security-across-the-enterprise-environment"></a>作業を開始しましょう。企業環境全体へのセキュリティの実装

セキュリティにより、ビジネスの機密性、整合性、可用性を保証できるようになります。 セキュリティの取り組みでは、内部と外部の悪意のある意図しない行為に起因する運用への潜在的な影響からの保護に特に重点を置いています。 

このファースト ステップ ガイドでは、サイバーセキュリティ攻撃によるビジネス リスクを軽減または回避するための主要な手順の概要を説明します。 このガイドに従うことで、クラウドでの重要なセキュリティ プラクティスを迅速に確立し、セキュリティをクラウド導入プロセスに組み込むことができます。

このガイドの手順は、クラウド環境とランディング ゾーンのセキュリティ保証をサポートするすべてのロールを対象としています。 タスクには、差し迫ったリスクの軽減の優先順位と、最新のセキュリティ戦略の構築、アプローチの運用化、その戦略の実行に関するガイダンスが含まれます。

このガイドには、Azure 用の Microsoft クラウド導入フレームワークの要素が含まれています。

![企業セキュリティの概要](../_images/get-started/security-map.png)

このガイドの手順に従うと、プロセスの重要なポイントでセキュリティを統合できます。 目標は、クラウド導入における障害を回避し、業務または運用の不要な中断を減らすことです。

Microsoft では、Microsoft Azure に関するこのセキュリティ ガイダンスの実装の促進に役立つ機能とリソースを構築しました。 これらのリソースは、このガイド全体で参照されています。 これらは、セキュリティの確立、監視、適用を支援するように設計されており、頻繁に更新およびレビューされます。

次の図は、セキュリティ ガイダンスとプラットフォーム ツールを使用して、Azure でクラウド資産のセキュリティの可視性と制御を確立するための包括的なアプローチを示しています。 Microsoft ではこのアプローチを推奨しています。

![セキュリティの図](../_images/security/security-diagram.png)

これらの手順を使用して、クラウド資産をセキュリティで保護し、クラウドを使用してセキュリティ運用を最新化するための戦略を計画および実行します。

## <a name="step-1-establish-essential-security-practices"></a>手順 1:重要なセキュリティ プラクティスを確立する

クラウドにおけるセキュリティは、確実なプラクティスから始まります。 既にクラウドで運用している場合でも、将来の導入を計画している場合でも、重要なセキュリティ プラクティスを迅速に確立することが重要です。

明示的な規制コンプライアンス要件を満たすことに加え、ほとんどの組織がクラウドに移行する際に直面するセキュリティの最大の課題に対処するために次の手順が推奨されます。

**成果物とサポートに関するガイダンス:**

- **技術:** 最上位のリスクを軽減し、資産の可視性と制御を向上させるには、管理者向けのパスワードレス認証または多要素認証を有効にするか、クラウド リソースの脅威の防止を有効にします。
  - [管理者向けのパスワードレス認証または多要素認証](https://docs.microsoft.com/azure/architecture/framework/security/critical-impact-accounts#passwordless-or-multi-factor-authentication-for-admins)
  - [セキュリティ運用](https://docs.microsoft.com/azure/architecture/framework/security/security-operations)と [Azure Security Center での脅威の防止](https://docs.microsoft.com/azure/security-center/threat-protection)
- **プロセス:** セキュリティ ロールと責任を割り当て、インシデント対応プロセスを確立することで、セキュリティに関する迅速な意思決定と継続的な改善を可能にします。
  - [責任の明確な線引き](https://docs.microsoft.com/azure/architecture/framework/security/governance#clear-lines-of-responsibility)、[環境を管理するための特権の割り当て](https://docs.microsoft.com/azure/architecture/framework/security/governance#assign-privileges-for-managing-the-environment)、セキュア スコアの運用化 <!-- TODO: Improve this and add link to AAF article -->
  - セキュリティ ロールと責任 <!-- TODO: add link to bookmark -->
  - [インシデント対応のリファレンス ガイド](https://aka.ms/irrg)
- **ユーザー:** クラウド環境への移行時にデプロイおよび運用を適切に行うために必要な教育、ツール、アクセス権をセキュリティ チームに提供します。
  - クラウドとクラウド セキュリティの進化の**概念について、すべてのユーザーを対象に教育する**:
    - [脅威の環境、ロール、デジタル戦略の進化](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#evolution-of-threat-environment-roles--digital-strategies-2004)
    - [セキュリティ、戦略、ツール、脅威のトランスフォーメーション](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#transformation-of-security-strategies-tools--threats-1513)
  - 使用されるプラットフォームのクラウド セキュリティ機能に関する技術的な詳細について、**技術スタッフをトレーニング**します。 Microsoft では、広範な [Azure のセキュリティに関するドキュメント](https://docs.microsoft.com/azure/security)を提供しています。
- **長期的なアーキテクチャに関する決定:** 適切な意思決定を行って、長期的な基盤を確立します。 これらを後で変更するのは難しく、コストがかかります。
  - [企業のセグメント化戦略を構築し、技術アーキテクチャをそれに合わせる (ネットワークのセグメント化や ID のセグメント化など)](https://docs.microsoft.com/azure/architecture/framework/security/network-security-containment#align-network-segmentation-with-enterprise-segmentation-strategy)
  - [単一のエンタープライズ ディレクトリ](https://docs.microsoft.com/azure/architecture/framework/security/identity#single-enterprise-directory)
  - [サービスの認証戦略](https://docs.microsoft.com/azure/architecture/framework/security/applications-services#prefer-identity-authentication-over-keys)
  - [アクセス許可の割り当て戦略](https://docs.microsoft.com/azure/architecture/framework/security/critical-impact-accounts#avoid-granular-and-custom-permissions)

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド セキュリティ チーム <br><br><br> | <li> クラウド戦略チーム <li> クラウド導入チーム <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

この最初の手順では、ガバナンス チームは、環境間で監視、管理、適用できるセキュリティ ベースラインの作成の調整を開始する必要もあります。 これを構築するための追加のガイダンスについては、手順 4 で後述します。

> [!NOTE]
> 各組織では、独自の最低限の基準を定義する必要があります。 リスク体制とそのリスクに対するその後の許容度は、業界、文化、その他の要因によって大きく異なる可能性があります。 たとえば、銀行では、テスト システムに対する軽微な攻撃であっても、評判を損なう可能性のあるものは許容されない場合があります。 デジタル変革が 3 から 6 か月早まるのなら、その同じリスクを喜んで受け入れる組織もあります。

## <a name="step-2-modernize-the-security-strategy"></a>手順 2:セキュリティ戦略を最新化する

クラウドでの効果的なセキュリティには、現在の脅威環境と、企業資産をホストしているクラウド プラットフォームの性質を反映した戦略が必要です。 明確な戦略により、すべてのチームの取り組みが改善され、安全で持続可能なエンタープライズ クラウド環境が提供されます。 セキュリティ戦略では、定義されたビジネス成果を実現し、許容できるレベルまでリスクを軽減し、従業員の生産性を高める必要があります。

クラウド セキュリティ戦略により、この導入に向けたテクノロジ、プロセス、メンバーの準備に取り組むすべてのチームに明確なガイダンスが提供されます。 この戦略では、クラウドのアーキテクチャおよび技術的機能を伝え、セキュリティ アーキテクチャおよび機能について説明し、チームのトレーニングと教育に影響を与える必要があります。

**成果物:**

この戦略手順は、最終的に文書化して、組織内の多くの利害関係者に簡単に伝えることができるようにする必要があります。 利害関係者には、組織のリーダーシップ チームの役員が含まれる可能性があります。

説明と更新を容易にするために、戦略をプレゼンテーションに取り込むことをお勧めします。 このプレゼンテーションは、文化と選好に応じて、ドキュメントでサポートできます。

- **戦略のプレゼンテーション:** 単一の戦略プレゼンテーションを用意することも、リーダー クラスの対象者向けの概要バージョンを作成することもできます。
  - **完全なプレゼンテーション:** メイン プレゼンテーションまたはオプションの参照スライドに、セキュリティ戦略の要素の完全なセットが含まれている必要があります。
  - **概要:** 上級管理者や取締役会役員向けに使用するバージョンには、リスク選好、最優先事項、許容リスクなど、役割に関連する重要な要素だけを含めます。
- [戦略と計画のテンプレート](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx)で、動機、成果、業務上の正当な理由を記録することもできます。

**セキュリティ戦略を構築するためのベスト プラクティス:**

成功したプログラムでは、これらの要素がセキュリティ戦略プロセスに組み込まれています。

- **ビジネス戦略に厳密に合わせる:** セキュリティの目的はビジネス価値を保護することです。 セキュリティのすべての取り組みをその目的に合わせ、内部抗争を最小限に抑えることが重要です。
  - ビジネス、IT、セキュリティの要件について**共通の理解を形成する**。
  - 回避可能なリスクによる土壇場の危機を回避するために、**初期段階でセキュリティをクラウド導入に組み込む**。
  - **アジャイル アプローチを使用**して最小限のセキュリティ要件を即座に確立し、長期にわたってセキュリティ保証を継続的に改善する。
  - 意図的な事前対応型のリーダーシップ アクションによって、**セキュリティ文化の変化を促進する**。

  詳細については、「[トランスフォーメーション、マインドセット、期待](../strategy/define-security-strategy.md#transformations-mindsets-and-expectations)」を参照してください。

- **セキュリティ戦略を最新化する:** セキュリティ戦略には、最新のテクノロジ環境、現在の脅威の状況、セキュリティ コミュニティ リソースのあらゆる側面に関する考慮事項が含まれている必要があります。
  - クラウドの**共有責任モデルに適応する**。
  - **クラウドのすべての種類とマルチクラウド デプロイを含める**。
  - 不要で有害な摩擦を避けるために、**ネイティブ クラウド コントロールを優先する**。
  - 攻撃者の進化のペースに対応するために、**セキュリティ コミュニティを統合する**。

**追加コンテキストの関連リソース:**

- [脅威の環境、ロール、デジタル戦略の進化](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#evolution-of-threat-environment-roles--digital-strategies-2004)
- [セキュリティ、戦略、ツール、脅威のトランスフォーメーション](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#transformation-of-security-strategies-tools--threats-1513)
- クラウド導入フレームワークの戦略に関する考慮事項:
  - [セキュリティ戦略を最新化する](../strategy/define-security-strategy.md#modernize-your-security-strategy)
  - [サイバーセキュリティの回復力](../strategy/define-security-strategy.md#cybersecurity-resilience)
  - [クラウドでのセキュリティの関係と責任の変化](../strategy/define-security-strategy.md#how-the-cloud-is-changing-security)

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> セキュリティ リーダーシップ チーム (情報セキュリティ最高責任者 (CISO) または同等のもの) | <li> クラウド戦略チーム <li> クラウド セキュリティ チーム <li> クラウド導入チーム <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

**戦略の承認:** 

組織内のビジネス ラインの成果またはリスクについて説明責任を負う経営幹部とビジネス リーダーがこの戦略を承認する必要があります。 組織によっては、このグループに取締役会が含まれる場合があります。

## <a name="step-3-develop-a-security-plan"></a>手順 3:セキュリティ プランを作成する

プランの策定では、成果、マイルストーン、タイムライン、タスク所有者を定義することで、セキュリティ戦略を実行に移します。 また、このプランでは、チームのロールと責任について概説します。

セキュリティ プランとクラウド導入プランを、単独で策定することはできません。 初期段階でクラウド セキュリティ チームをプラン策定サイクルに招いて、セキュリティ問題の検出が遅すぎることによる作業の停止やリスクの増大を防ぐことが重要です。 クラウド プランの策定プロセスに完全に統合することによって得られる、デジタル資産と既存の IT ポートフォリオについて深く理解し、認識したうえでセキュリティ プランを策定することをお勧めします。

**成果物:**

- **セキュリティ プラン:** セキュリティ プランは、クラウドの主要なプラン策定ドキュメントに含まれている必要があります。 セキュリティ プランには、[戦略と計画のテンプレート](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx)を使用したドキュメント、詳細なスライド デッキ、またはプロジェクト ファイルを使用できます。 また、組織の規模、文化、標準的なプラクティスに応じて、これらの形式の組み合わせを使用することもできます。

  セキュリティ プランには、これらの要素がすべて含まれている必要があります。

  - **組織機能のプラン**。チームは、クラウドへの移行によって現在のセキュリティ ロールと責任がどのように変わるのかがわかります。
  - **セキュリティ スキルのプラン**。これは、テクノロジ、ロール、責任の重要な変更点を参照する際にチーム メンバーをサポートするためのものです。
  - **セキュリティ アーキテクチャと機能の技術的なロードマップ**。これは技術チームの指針となります。
  Microsoft では、アーキテクチャとロードマップを構築する際に役立つ、次のようなリファレンス アーキテクチャとテクノロジ機能を提供しています。
    - [Azure コンポーネントとリファレンス モデル](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151)。これは、Azure セキュリティ ロールのプランの策定と設計を促進するためのものです。

      ![Azure 管理モデル](../_images/security/azure-administration-model.png)
      
      ![Azure RBAC モデル](../_images/security/azure-rbac-model.png)
    - [Microsoft サイバーセキュリティ リファレンス アーキテクチャ](https://aka.ms/mcra)。これは、オンプレミスとクラウドのリソースにまたがるハイブリッド エンタープライズ向けのサイバーセキュリティ アーキテクチャを構築するためのものです。
    - [セキュリティ オペレーション センター (SOC) リファレンス アーキテクチャ](https://docs.microsoft.com/security/compass/security-operations-videos-and-decks#part-1-introduction---soc-learnings-strategies-and-technical-integration-2430)。これは、セキュリティの検出、対応、回復を最新化するためのものです。
    - [ゼロ トラスト ユーザー アクセス リファレンス アーキテクチャ](https://docs.microsoft.com/security/ciso-workshop/ciso-workshop-module-3#part-5-zero-trust-user-access-reference-architecture-842)。これは、クラウドの生成用のアクセス制御アーキテクチャを最新化するためのものです。
    - [Azure Security Center](https://docs.microsoft.com/azure/security-center/) と [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/)。これは、クラウド資産をセキュリティで保護するためものです。
  - **セキュリティの意識と教育のプラン**: すべてのチームが、重要なセキュリティに関する基礎知識を身に付けます。
  - **資産の機密度のマーキング**: ビジネスへの影響に合わせた分類を使用して機密性の高い資産を指定します。 この分類は、ビジネス利害関係者、セキュリティ チーム、その他の関係者が共同で構築します。

- **クラウド プランのセキュリティの変更**: クラウド導入プランの他のセクションを更新して、セキュリティ プランによってトリガーされた変更を反映させます。

**セキュリティ プランの策定に関するベスト プラクティス:** プランを策定する際に次のようなアプローチが採用されている場合、セキュリティ プランが成功する可能性が高くなります。

- **ハイブリッド環境を想定する:** これには、SaaS (サービスとしてのソフトウェア) アプリケーションとオンプレミス環境が含まれます。 また、サービスとしてのクラウド インフラストラクチャ (IaaS) プロバイダーと、サービスとしてのプラットフォーム (PaaS) プロバイダーも複数含まれます (該当する場合)。
- **アジャイル セキュリティを導入する:** 最初に最小限のセキュリティ要件を確立し、重要ではないすべての項目を、次の手順の優先順位付けされた一覧に移動します。
これは、従来の 3 から 5 年の詳細なプランにしないでください。 クラウドと脅威環境の変化が速すぎるため、この種のプランは役に立ちません。 実際のプランでは、最初の手順と終了状態を策定することに重点を置く必要があります。
  - 近い将来の**即効性のある成果**: 長期的なイニシアチブを開始する前に大きな効果が得られます。 組織の文化、標準的なプラクティス、その他の要因に応じて、時間枠は 3 から 12 か月になる可能性があります。
  - 目的の最終状態の**明確なビジョン**: これは、各チームの (達成するまでに数年かかる場合がある) プラン策定プロセスの指針となります。
- **プランを広く共有する:** 利害関係者の意識を高め、フィードバックや同意を増やします。
- **戦略成果に合わせる:** プランがセキュリティ戦略に記載されている戦略成果に合っており、その成果が得られるようにします。
- **所有権、説明責任、期限を定める:** 確実に、各タスクの所有者が識別され、特定の期間内にそのタスクを完了することに取り組むようにします。
- **セキュリティの人間的側面とのつながりを持つ:** 変革のこの期間に関係者を関与させ、新たな期待を持たせます。
  - **チーム メンバーの変革を積極的にサポートする:** 以下について明確に伝え、指導します。
    - 習得する必要があるスキル。
    - それらのスキルを習得する必要がある理由 (およびそのメリット)。
    - この知識を得る (および習得に役立つリソースを提供する) 方法。
  
    [戦略と計画のテンプレート](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx)を使用して、プランを文書化できます。 また、チーム メンバーの教育に役立つ、[オンラインの Microsoft セキュリティ トレーニング](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction)を利用できます。
  - **セキュリティ意識を促す:** 関係者を組織の保護に純粋に関与させます。
- **Microsoft ラーニングとガイダンスを確認する:** Microsoft では、組織がクラウドへの変革と最新のセキュリティ戦略を計画する際に役立つ、分析情報と展望を公開しています。 資料には、記録されたトレーニング、ドキュメント、セキュリティのベスト プラクティスと推奨される標準が含まれています。
  プランとアーキテクチャの策定に役立つ技術的なガイダンスについては、[Microsoft のセキュリティ ドキュメント](https://docs.microsoft.com/security)を参照してください。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド セキュリティ チーム | <li> クラウド戦略チーム <li> クラウド ガバナンス チーム <li> 組織内のすべてのリスク チーム <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

**セキュリティ プランの承認:** 

セキュリティ リーダーシップ チーム (CISO または同等の経営幹部) がプランを承認する必要があります。

## <a name="step-4-secure-new-workloads"></a>手順 4:新しいワークロードをセキュリティで保護する

後で環境にセキュリティを組み込むよりも、セキュリティで保護された状態で始める方がはるかに簡単です。 セキュリティで保護された環境にワークロードが移行され、開発とテストが行われるように、セキュリティで保護された構成で始めることを強くお勧めします。

[ランディング ゾーン](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/landing-zone)の実装中は、多くの決定がセキュリティおよびリスク プロファイルに影響する可能性があります。 クラウド セキュリティ チームは、ランディング ゾーンの構成を確認して、組織のセキュリティ ベースラインのセキュリティの標準と要件が確実に満たされるようにする必要があります。

**成果物:**

- 新しいランディング ゾーンが、組織のコンプライアンスとセキュリティの要件を確実に満たすようにします。

**成果物の完遂をサポートするうえでのガイダンス:**

- **既存の要件とクラウドに関する推奨事項を調和させる:** 推奨されるガイダンスから始め、これを独自のセキュリティ要件に適合させます。 既存のオンプレミス ポリシーと標準を適用しようとしたときに問題が発生しました。多くの場合、これらは古いテクノロジやセキュリティ手法を示しているためです。 

  Microsoft では、セキュリティ ベースラインを構築するのに役立つガイダンスを公開しています。
  - [戦略とアーキテクチャに関する Azure のセキュリティ標準](https://docs.microsoft.com/security/compass/compass): 環境のセキュリティ体制を形成するための戦略とアーキテクチャに関する推奨事項。
  - [Azure セキュリティ ベンチマーク](https://docs.microsoft.com/azure/security/benchmarks/introduction): Azure 環境をセキュリティで保護するための特定の構成に関する推奨事項。
  - [Azure セキュリティ ベースラインのトレーニング](https://docs.microsoft.com/learn/modules/create-security-baselines)。
- **ガードレールを提供する:** 保護対策には、自動化されたポリシーの監査と適用を含める必要があります。 これらの新しい環境では、チームは組織のセキュリティ ベースラインの監査と適用の両方に努める必要があります。 これらの取り組みにより、ワークロードの開発時のセキュリティの問題を最小限に抑えることができるだけでなく、ワークロードの継続的インテグレーションと継続的配置 (CI/CD) も実現できます。

  Microsoft では、これを可能にするために Azure でいくつかのネイティブ機能を提供しています。
  - [セキュリティ スコア](https://docs.microsoft.com/azure/security-center/secure-score-security-controls): Azure セキュリティ体制のスコア付けされた評価を使用して、組織内のセキュリティの取り組みとプロジェクトを追跡します。
  - [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview):クラウド アーキテクトと中央 IT グループは、組織の標準、パターン、要件を実装し、これらに準拠した一連の反復可能な Azure リソースを定義できます。
  - [Azure Policy](https://docs.microsoft.com/azure/governance/policy/):これは、他のサービスで使用される可視性と制御の機能の基盤となります。 Azure Policy は、[Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager) に統合されています。これにより、変更を監査し、Azure 内のリソースの作成前、作成中、または作成後にポリシーを適用できます。
- [ランディング ゾーンの運用を改善する](../ready/considerations/landing-zone-security.md): ランディング ゾーン内のセキュリティを強化するためのベスト プラクティスを使用します。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド セキュリティ チーム | <li> クラウド導入チーム <li> クラウド プラットフォーム チーム <li> クラウド戦略チーム <li> クラウド ガバナンス チーム <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

## <a name="step-5-secure-existing-cloud-workloads"></a>手順 5:既存のクラウド ワークロードをセキュリティで保護する

多くの組織では、セキュリティのベスト プラクティスを適用せずに、エンタープライズ クラウド環境に資産を既にデプロイしているため、ビジネス リスクが増大しています。

確実に新しいアプリケーションとランディング ゾーンがセキュリティのベスト プラクティスに従うようにした後に、既存の環境が同じ標準に達するようにすることに重点を置く必要があります。

**成果物:**

- 既存のすべてのクラウド環境とランディング ゾーンが、組織のコンプライアンスとセキュリティの要件を確実に満たすようにします。
- セキュリティ ベースラインのポリシーを使用して、運用環境のデプロイの運用準備をテストします。
- セキュリティ ベースラインの設計ガイダンスとセキュリティ要件への準拠を検証します。

**成果物の完遂をサポートするうえでのガイダンス:**

- 最適な状態として、[手順 4](#step-4-secure-new-workloads) で構築したセキュリティ ベースラインを使用します。 場合によっては、一部のポリシー設定を適用するのではなく、監査のみを行うために調整する必要があります。
- 運用およびセキュリティ リスクのバランスを取ります。 これらの環境では、重要なビジネス プロセスを可能にする運用システムをホストしている可能性があるため、運用ダウンタイムのリスクを回避するために、セキュリティの強化を段階的に行うことが必要な場合があります。
- ビジネスの重要度で、セキュリティ リスクの検出と修復に優先順位を付けます。 侵害された場合にビジネスに大きな影響を与えるワークロードと、リスクにさらされる可能性が高いワークロードから始めます。

詳細については、「[ビジネス クリティカルなアプリケーションを特定して分類する](https://docs.microsoft.com/azure/architecture/framework/security/applications-services?toc=/security/compass/toc.json&bc=/security/compass/breadcrumb/toc.json#identify-and-classify-business-critical-applications)」をご覧ください。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド導入チーム | <li> クラウド導入チーム <li> クラウド戦略チーム <li> クラウド セキュリティ チーム <li> クラウド ガバナンス チーム <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

## <a name="step-6-govern-to-manage-and-improve-security-posture"></a>手順 6:セキュリティ体制の管理と改善のために統制する

すべての最新の規範と同様に、セキュリティは継続的な改善に集中する必要がある反復的なプロセスです。 組織で長期的に集中を維持しないと、セキュリティ体制が崩壊する可能性があります。

セキュリティ要件の一貫した適用は、確実なガバナンス規範と自動化されたソリューションに基づきます。 クラウド セキュリティ チームがセキュリティ ベースラインを定義したら、これらの要件を監査して、すべてのクラウド環境に一貫して適用される (必要に応じて強制される) ようにする必要があります。

**成果物:**

- 組織のセキュリティ ベースラインが、関連するすべてのシステムに確実に適用されるようにします。 [セキュリティ スコア](https://docs.microsoft.com/azure/security-center/secure-score-security-controls)または同様のメカニズムを使用して異常を監査します。
- [セキュリティ ベースライン規範テンプレート](../govern/security-baseline/template.md)で、セキュリティ ベースラインのポリシー、プロセス、設計ガイダンスを文書化します。

**成果物の完遂をサポートするうえでのガイダンス:**

- ベースラインを監視する技術的要素として、[手順 4](#step-4-secure-new-workloads) で構築したセキュリティ ベースラインと監査メカニズムを使用します。 一貫性を確保するために、ユーザーとプロセスの制御によってこれらのベースラインを補完します。
- すべてのワークロードとリソースが、[適切な名前付けおよびタグ付け規則](../ready/azure-best-practices/naming-and-tagging.md)に従っていることを確認します。 "データの機密性" のタグに特に重点を置いて、[Azure Policy を使用してタグ付け規則を適用](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags)します。
- クラウド ガバナンスを初めて使用する場合は、ガバナンス手法を使用して、[ガバナンスのポリシー、プロセス、規範](../govern/index.md)を確立します。

<!-- markdownlint-disable MD033 -->
<br>

| 説明責任チーム | 実行責任チームとサポート チーム |
| --- | --- |
| <li> クラウド ガバナンス チーム | <li> クラウド戦略チーム <li> クラウド セキュリティ チーム <li> クラウドのセンター オブ エクセレンスまたは中央 IT |

## <a name="next-steps"></a>次のステップ

このガイドでは、企業全体のセキュリティ リスクを一貫して管理するために必要な戦略、制御、プロセス、スキル、文化を導入する手順を説明しました。
手順の完了後、クラウド セキュリティの運用モードに入るときは、以下に示す次のステップを検討してください。

- [Microsoft のセキュリティ ドキュメント](https://docs.microsoft.com/security)を確認します。 セキュリティ担当者がサイバーセキュリティ戦略、アーキテクチャ、優先順位付けされたロードマップを策定および改善する際に役立つ技術的なガイダンスが提供されます。
- [Azure サービスの組み込みセキュリティ コントロール](https://docs.microsoft.com/azure/security/fundamentals/security-controls)に関する記事で、セキュリティ情報を確認します。
- 「[Azure で利用できるセキュリティ サービスとテクノロジ](https://docs.microsoft.com/azure/security/azure-security-services-technologies)」で、Azure セキュリティ ツールとサービスを確認します。
- [Microsoft Trust Center](https://www.microsoft.com/trustcenter/guidance/risk-assessment)を確認します。 ここには、規制コンプライアンス プロセスの一環としてリスク評価を行う際に役立つ広範なガイダンス、レポート、関連ドキュメントが含まれています。
- セキュリティ要件を容易に満たすために使用できるサードパーティ ツールを確認します。 「[Azure Security Center でのセキュリティ ソリューションの統合](https://docs.microsoft.com/azure/security-center/security-center-partner-integration)」をご覧ください。