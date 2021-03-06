---
title: クラウド ガバナンス機能を理解する
description: クラウド ガバナンス チームの機能について、ソース、スコープ、成果物を含めて理解します。
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: e0072ca4e2c1606024c992088fe38618498b2625
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2020
ms.locfileid: "94712308"
---
<!-- docutune:ignore IS -->

# <a name="cloud-governance-functions"></a>クラウド ガバナンス機能

クラウド ガバナンス チームは、リスクとリスクの許容範囲が適切に評価され、管理されていることを請け合います。 このチームにより、ビジネスで許容できないリスクが確実に正しく特定されます。 このチームのメンバーは、リスクを企業の管理ポリシーに転換します。

必要なビジネス成果に応じて、完全なクラウド ガバナンスの機能を実現するために必要なスキルには以下が含まれます。

- IT ガバナンス
- エンタープライズ アーキテクチャ
- Security
- IT 運用
- IT インフラストラクチャ
- ネットワーク
- ID
- 仮想化
- 事業継続とディザスター リカバリー
- IT 部門のアプリケーション所有者
- 財務の所有者

これらのベースライン機能は、現在のリリースと将来のリリースに関連するリスクを識別するのに役立ちます。 これらの取り組みは、リスクの評価、潜在的な影響の把握、およびリスクの許容度に関する意思決定を行うのに役立ちます。 その際、[クラウド移行チーム](./cloud-migration.md)のニーズの変化を反映するように計画を迅速に更新します。

## <a name="preparation"></a>準備

- [ガバナンスの方法論](../govern/index.md)を確認します。
- [ガバナンス ベンチマーク評価](../govern/benchmark.md)を行います。
- [Azure のセキュリティの概要](/learn/modules/intro-to-security-in-azure):クラウド内のインフラストラクチャとデータの保護に関する基本的な概念について学習します。 自分の役割と Azure によって自動的に処理されることについて理解します。
- [コストを管理する](../organize/cost-conscious-organization.md)ためにグループ間で連携する方法について理解します。

## <a name="minimum-scope"></a>最小スコープ

- 計画によって発生する[ビジネス リスク](../govern/policy-compliance/risk-tolerance.md)を把握します。
- [リスクに対するビジネスの許容度](../govern/policy-compliance/risk-tolerance.md)を明らかにします。
- [ガバナンス MVP](../govern/guides/index.md) の作成を支援します。

クラウド ガバナンスのアクティビティには、次の参加者が関与します。

- 中間管理層のリーダーと重要な役割を担っている直接的な協力者が、ビジネスを代表してリスク許容度の評価を支援します。
- クラウド ガバナンス機能は、[クラウド戦略チーム](./cloud-strategy.md)の拡張によって提供されます。 CIO とビジネス リーダーがクラウド戦略機能への参加を求められるように、彼らの直属の部下には、クラウド ガバナンスのアクティビティへの参加が求められます。
- ビジネス ユニットのメンバーとして基幹業務のリーダーと緊密に連携する従業員には、企業リスクや技術的リスクに関して意思決定を行う権限を与える必要があります。
- クラウド変革の技術的側面を理解している情報技術 (IT) および情報セキュリティ (IS) の担当者は、クラウド ガバナンス機能の提供を常時担当するのではなく、交代で担当してもかまいません。

## <a name="deliverable"></a>成果物

クラウド ガバナンスの使命は、変革とリスク軽減という相対する効果のバランスを取ることです。 さらに、クラウド ガバナンスでは、[クラウド移行チーム](./cloud-migration.md)によるデータと資産の分類と導入を管理するアーキテクチャ ガイドラインの認識が確実に行われるようにします。 ガバナンス チームまたは担当者は、[クラウド センター オブ エクセレンス](../organize/cloud-center-of-excellence.md)と連携して、自動化されたアプローチでクラウド環境の管理も行います。

**毎月の継続的なタスク:**

- 各リリースで生じる[ビジネス リスク](../govern/policy-compliance/risk-tolerance.md)を把握します。
- [リスクに対するビジネスの許容度](../govern/policy-compliance/risk-tolerance.md)を明らかにします。
- [ポリシーとコンプライアンスの要件](../govern/policy-compliance/index.md)の段階的な改善を支援します。

**ミーティングの開催:**

クラウド ガバナンス チームの各メンバーが費やす時間は、彼らの毎日のスケジュールの大きな割合を占めることになります。 協力の範囲はミーティングやフィードバック サイクルに限定されません。

## <a name="out-of-scope"></a>対象範囲外

導入規模が拡大するにつれて、クラウド ガバナンス チームは、イノベーションと同じペースを保つことが困難になる可能性があります。 これが特に当てはまるのは、コンプライアンス、運用、またはセキュリティの要件が厳しい環境です。 これが起こった場合は、責任の一部を既存の IT チームに移して、ガバナンス チームのスコープを減らすことができます。

## <a name="next-steps"></a>次のステップ

大規模な組織では、IT ガバナンスの専任チームを置いている場合があります。 このチームは、IT ポートフォリオ全体のリスク管理を専門に手がけます。 このようなチームが存在していれば、次に示す成熟度モデルを迅速に促進できます。 一方で、IT ガバナンス チームには、クラウド ガバナンス モデルを確認して、クラウドでのガバナンスのわずかな変化を理解することが推奨されます。 クラウドに対する企業ポリシーの拡張やクラウド ガバナンスの 5 つの規範に関連する記事が重要です。

**ガバナンスなし:** 組織はしばしば、ガバナンスに関する明確な計画を立てずにクラウドに移行します。 やがて、セキュリティ、コスト、スケール、運用に関する懸念が生じ、ガバナンス モデルの必要性や、そのモデルに関連するプロセスの担当者が必要であることが会話に上り始めます。 こうした会話を懸念が生じる前に開始することは常に、"ガバナンスなし" というアンチパターンを克服するための望ましい第一歩となります。 企業ポリシーの定義に関するセクションは、こうした会話の促進に役立ちます。

**ガバナンスの阻害:** セキュリティ、コスト、スケール、運用に関する懸念を未解決のままにすると、プロジェクトやビジネス目標が行き詰まることになります。 適切なガバナンスが欠如していると、利害関係者やエンジニアの間に恐怖、不安、疑念が生じます。 早い段階でアクションを起こして、この流れを止める必要があります。 クラウド導入フレームワークで規定されている 2 つのガバナンス ガイドに従って、小規模から始め、制限的なポリシーを最初に設定して不安を最小限に抑え、ガバナンスを段階的に成熟させることができます。 複雑な企業向けのガイドまたは標準企業向けのガイドを選んでください。

**ボランティアによるガバナンス:** どの企業にも意欲的な人はいるものです。 この勇敢な人たちは、自ら志願して、チームが失敗から学ぶことができるように協力します。 特に小規模な企業では、ここからガバナンスがスタートすることがよくあります。 この意欲的な人たちは、問題の解決を進んで引き受け、クラウド導入チームが一貫性のあるしっかりしたベスト プラクティスを策定できるように後押しします。

こうした個人による取り組みは、"ガバナンスなし" や "ガバナンスの阻害" のシナリオに比べてはるかに優れています。 この取り組みは推奨されるべきですが、このアプローチをガバナンスと混同しないようにする必要があります。 適切なガバナンスによって、優れたガバナンス アプローチの目標である一貫性の確保を図るには、散発的なサポートだけでは不十分です。 この規範の策定にあたっては、クラウド ガバナンスの 5 つの規範に関するガイダンスが参考になります。

**クラウド カストディアン (管理者):** この呼び名は、初期段階のガバナンスに精通する多くのクラウド アーキテクトにとって名誉に値します。 ガバナンス プラクティスが動き出した時点では、その成果がガバナンス ボランティアと変わらないように思われます。 ただし、1 つの基本的な違いがあります。 クラウド カストディアンの念頭にはプランがあります。 この成熟段階では、それまでにクラウド アーキテクトが起こした混乱状態をチームが整理しています。 ただし、クラウド カストディアンは、適切に構成された企業ポリシーに沿ってこの取り組みを進めます。 また、ガバナンス MVP に関する記事で説明されているようなガバナンス ツールを利用します。

クラウド カストディアンとガバナンス ボランティアのもう 1 つの根本的な違いは、リーダーシップからのサポートがある点です。 ボランティアは、学びと実践の追求に予想以上の時間を取られます。 リーダーシップからサポートを得られるクラウド カストディアンは、日常的な職務を減らして、通常の配分時間をクラウド ガバナンスの向上に費やすことができます。

**クラウド ガーディアン (守護者):** ガバナンス プラクティスが固まり、クラウド導入チームによって受け入れられると、クラウド ガバナンス チームの役割と同じように、ガバナンスに精通するクラウド アーキテクトの役割も多少変化します。 一般に、成熟したプラクティスには、ガバナンスの実装で保護の強化を図る他の分野の専門家が注目します。

両者の違いは微妙ですが、ガバナンス重視の IT カルチャを構築する際に重要な区別です。 クラウド管理人 (custodian) は革新的なクラウド アーキテクトがもたらした混乱を解決します。2 つの役割には当然ながら摩擦があり、目標は相反します。 クラウド管理人がクラウドを安全に保ってくれるおかげで、クラウド アーキテクトはより迅速に、混乱を少なくしながら前進することができます。

クラウド ガーディアンは、高度なガバナンス アプローチでプラットフォームのデプロイを加速するとともに、チームが環境のニーズに自ら対応できるように支援してチームの機動力を高めます。 このように高度な機能の例は、セキュリティ ベースラインの改善など、ガバナンス MVP の段階的な向上に見られます。

**クラウド アクセラレータ (推進者):** クラウド ガーディアンとクラウド カストディアンは、環境やプラットフォーム、あるいは各種アプリケーションのコンポーネントのデプロイまでも加速させるために、必然的にスクリプトやガバナンス ツールを活用します。 ガバナンスの責任を一元化するだけでなく、このようなスクリプトを厳選して共有することで、これらのアーキテクトは IT 部門全体で大きな敬意を集めるようになります。

ガバナンス実践者が自ら厳選したスクリプトをオープンに共有することで、技術プロジェクトを迅速に提供し、ワークロードのアーキテクチャにガバナンスを組み込めるようになります。 ワークロードにこうした効果をもたらし、優れたデザイン パターンをサポートすることで、クラウド アクセラレータはガバナンス スペシャリストへとランクアップします。

**グローバル ガバナンス:** IT ニーズがグローバルに分散している組織では、さまざまな地域で運用とガバナンスに大きなずれが生じている可能性があります。 ビジネス ユニットの要望や地域的なデータ主権の要件が原因で、ガバナンスのベスト プラクティスが、必要な運用の妨げになることもあります。 このようなシナリオでは、ガバナンス モデルを階層化することで、最低限の一貫性の確保とガバナンスの地域化を実現できます。 複数レイヤーのガバナンスに関する記事には、このレベルの成熟度に到達するための知見が掲載されています。

企業はそれぞれにユニークであり、そのガバナンス ニーズも同様です。 組織に合った成熟度レベルを選び、クラウド導入フレームワークを利用して、そこに到達するためのプラクティス、プロセス、ツールを導入してください。

クラウド ガバナンスが成熟するにつれて、チームはより速いペースでクラウドを導入できるようになります。 クラウド導入の取り組みを継続すると、IT 運用が成熟していきます。 クラウド運用チームを結成するか、ガバナンスが運用開発の一部となるようにクラウド運用チームと連携します。

[クラウド ガバナンス チーム](../get-started/team/cloud-governance.md)または[クラウド運用チーム](../get-started/team/cloud-operations.md)の開始についての詳細を参照してください。

[初期のクラウド ガバナンスの基盤](../govern/initial-foundation.md)を確立したら、[ガバナンスの基盤の改善](../govern/foundation-improvements.md)に関する記事のベスト プラクティスを使用して導入計画を進めて、リスクを回避します。
