---
title: クラウド移行の業務上の妥当性
description: Azure 向けのクラウド導入フレームワークを使用して、クラウド移行を目指す業務上の正当な理由を明らかにするための第一歩を学びます。
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: governance
ms.openlocfilehash: dea15cfe0abfcfbb8a7771149a4a734dd0d278d9
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88884812"
---
# <a name="build-a-business-justification-for-cloud-migration"></a>クラウド移行の業務上の妥当性をまとめ

クラウド移行の際には、クラウドへの転換の取り組みから早期に投資収益率 (ROI) を生み出すことができます。 しかし、具体的な関連コストと利益を示して業務上の正当な理由を明確にまとめるのは、複雑なプロセスです。 この記事は、クラウド移行の結果に適合する財務モデルを作成するために、どのようなデータが必要であるかを考える助けになります。 最初に、よくある間違いを組織が回避できるように、クラウド移行に関する根拠のない説をいくつか解消しておきましょう。

## <a name="dispelling-cloud-migration-myths"></a>クラウド移行に関する根拠のない説を解消する

### <a name="myth-the-cloud-is-always-cheaper"></a>通説:クラウドは常に低コストである

一般に、クラウドで稼働するデータセンターはオンプレミスで稼働するデータセンターよりも常に低コストであると認識されています。 この思い込みは概ね真実ですが、そうでない場合もあります。 クラウドの運用コストの方が高くなることもあります。 これらのコストが高くなるのは、多くの場合、問題のあるコスト管理、不適切なシステム アーキテクチャ、プロセスの重複、特殊なシステム構成、またはスタッフ コストの増加によるものです。 幸い、これらの問題の多くを軽減して早期の ROI を生み出すことができます。 「[業務上妥当である理由をまとめる](#build-the-business-justification)」のガイダンスに従うことで、これらの不適切な点を見つけて回避することができます。 ここに示したその他の根拠のない説を解消することも役立ちます。

### <a name="myth-everything-should-go-into-the-cloud"></a>通説:すべてのものをクラウドに移行する必要がある

実際には、いくつかのビジネス上の要因からハイブリッド型ソリューションを選択することにつながる可能性があります。 ビジネス モデルの構築を終える前に、[デジタル資産に関する記事](../digital-estate/5-rs-of-rationalization.md)の説明に従って、初回の定量分析を完了しておくのが賢明です。 合理化に関連する個々の定量的要因の詳細については、「[合理化の 5 R](../digital-estate/5-rs-of-rationalization.md)」を参照してください。 どのアプローチでも、容易に取得されるインベントリ データと簡潔な定量分析を使用して、クラウドではコストが高くなる可能性があるワークロードまたはアプリケーションを識別します。 これらのアプローチでは、ハイブリッド ソリューションが必要となるであろう依存関係やトラフィック パターンも識別できます。

### <a name="myth-mirroring-my-on-premises-environment-will-help-me-save-money-in-the-cloud"></a>通説:オンプレミス環境のミラーリングは、クラウドでのコスト削減に役立つ

企業のデジタル資産計画の間に、プロビジョニングされた環境の 50% を超える未使用の容量が検出されるという例もあります。 クラウドで、現在のプロビジョニングに合わせて資産がプロビジョニングされる場合、コストの削減を実現するのは困難でます。 デプロイする資産のサイズは、プロビジョニングのパターンではなく、使用パターンに合わせて削減することを検討します。

### <a name="myth-server-costs-drive-business-cases-for-cloud-migration"></a>通説:サーバーのコストが、クラウド移行のビジネス ケースを促進する要因になる

この思い込みは正しい場合があります。 一部の企業にとって、サーバーに関連する継続的な資本コストを減らすことが重要です。 しかし、これは複数の要因に左右されます。 ハードウェアの更新周期が 5 年から 8 年の企業であれば、クラウド移行によるメリットがすぐには得られない場合があります。 更新周期が標準化されている企業や強制的に更新を実施する企業では、よりすばやく損益分岐点に到達できます。 どちらの場合も、その他の費用が、移行を正当化する経済的きっかけとなる可能性があります。 以下に、企業がサーバーのみまたは VM のみの観点でコストを捉える場合に見過ごされることが多いコストの例をいくつか示します。

- 仮想化、サーバー、およびミドルウェアのソフトウェアのコストが多額になる場合があります。 クラウド プロバイダーを利用すると、これらのコストの一部がなくなります。 仮想化のコストを削減するクラウド プロバイダーの 2 つの例は、[Azure ハイブリッド特典](https://azure.microsoft.com/pricing/hybrid-benefit/#services)と [Azure Reservations](https://azure.microsoft.com/reservations) プログラムです。
- 障害に起因する業務上の損失は、ハードウェアやソフトウェアのコストをすぐに上回る可能性があります。 現在のデータ センターが不安定な場合は、業務部門と協力して、機会コストや実際の業務コストの観点から障害の影響を定量化します。
- 環境コストも重要になる場合があります。 米国の平均的家族の場合、住宅が最大の投資であり、家計の中で最大のコストを占めます。 多くの場合、データセンターにも同じことが当てはまります。 不動産、設備、およびユーティリティのコストは、オンプレミスのコストの相当な部分を占めます。 データセンターが廃止されると、それらの設備を転用することができます。または、企業がそのコストから完全に解放される可能性もあります。

### <a name="myth-an-operating-expense-model-is-better-than-a-capital-expense-model"></a>通説:操業費用モデルは資本支出モデルより好ましい

[会計結果](./business-outcomes/fiscal-outcomes.md)に関する記事で説明したように、操業費用モデルは好ましいものである場合があります。 しかし、中には操業費用を否定的に考える業界もあります。 操業費用についての会話に関して、会計部門と事業部門のより緊密な統合のきっかけとなる例をいくつか以下に示します。

- 企業で資本的な資産をビジネス上の評価を高める要因と見なす場合、資本支出の削減はマイナスの結果になることがあります。 一般的な標準ではありませんが、こうした考えが最もよく見られるのは、小売業界、製造業界、および建築業界です。
- 未公開株式投資会社や資本流入を求めている企業では、操業費用の増加をマイナスの結果と見なす場合があります。
- 企業で販売利益の向上や売却済商品の原価 (COGS) の削減を非常に重視している場合、操業費用はマイナスの結果となる可能性があります。

企業は、資本支出よりも操業費用の方が好ましいと考える可能性が高いです。 たとえば、このアプローチは、キャッシュ フローの改善、設備投資の削減、資産保有の削減を試みている企業には好意的に受け取られる可能性があります。

業務上の正当な理由を、資本支出から操業費用への転換に焦点を合わせて説明する前に、どちらが自社にとって良いのかを把握します。 会計と調達からの視点は、多くの場合、主張を財務上の目標に対して整合させる助けになります。

### <a name="myth-moving-to-the-cloud-is-like-flipping-a-switch"></a>通説:クラウドへの移行はスイッチを切り替えるようなものである

移行は、大きな手動での労力を要する技術的変革です。 業務上妥当である理由をまとめるとき、特にそれが、時間が重要であるような理由のときには、資産の移行にかかる時間を長くする可能性がある以下の側面について考慮してください。

- **帯域幅の制限:** 現在のデータセンターおよびクラウド プロバイダー間の帯域幅の量は、移行時のタイムラインを左右します。
- **テスト タイムライン:** 企業でアプリケーションをテストし、対応性とパフォーマンスを確実にするには、時間がかかる場合があります。 パワー ユーザーとテスト プロセスを整合させることが重要です。
- **移行タイムライン:** 移行を実装するために必要な時間と労力によって、コストが増加し、遅延が発生する可能性があります。 従業員や契約パートナーの割り当てによってもプロセスが遅れることがあります。 計画ではこれらの割り当てを考慮する必要があります。

技術的、文化的な懸案事項のために、クラウドの導入速度が低下する場合があります。 時間が、業務上妥当である理由の重要な側面である場合、適切な計画が最善の軽減策です。 計画時には、次の 2 つの方法でタイムラインに関するリスクを軽減できます。

- 導入の技術的制約について理解することに時間とエネルギーを投じます。 迅速な移行を求める圧力が高い場合もありますが、現実的なタイムラインとすることが重要です。
- 文化や人に関わる懸案事項が発生した場合、技術的制約よりも重大な影響があります。 クラウドの導入によって変化が生じ、それが望ましい変革が生み出されます。 残念ながら、人は変化を恐れるときがあり、計画に合わせるために追加の支援が必要な場合もあります。 変化に反対しているチームの重要人物を特定して早期に関与させます。

対応性を最大化し、タイムラインのリスクを最大限に軽減するには、ビジネス価値とビジネス上の結果をしっかり対応させることで、経営陣の関係者の準備を整えます。 これらの関係者が、この変革に伴う変化を理解できるように助けます。 最初から明確であるようにして、期待は現実的なものとします。 人やテクノロジがプロセスを遅らせている場合は、経営陣の支援を取り付けるのが容易になります。

## <a name="build-the-business-justification"></a>業務上の正当な理由の構築

次のプロセスでは、クラウド移行の業務上の妥当性をまとめる方法を定義します。 計算と財務条件の詳細については、[財務モデル](./financial-models.md)に関する記事を参照してください。

最上位のレベルでは、業務上妥当である理由の数式は単純です。 しかし、数式の作成に必要とされる難解なデータ ポイントを整合するのが難しい場合があります。 基本レベルでは、業務上の正当な理由は、提案された技術的変更に関連する投資収益 (ROI) を中心としたものになります。 ROI の一般的な数式は次のようになります。

![ROI = (投資利益 – 投資のコスト) / 投資のコスト](../_images/strategy/formula-roi.png)

この式の右辺の入力変数について移行固有の数式の見方を取得できるように解明できます。 この記事の残りのセクションでは、考慮に入れるいくつかの考慮事項について説明します。

## <a name="migration-specific-initial-investment"></a>移行固有の初期投資

- クラウド プロバイダーは、クラウドへの投資を見積もる計算ツールを提供しています。 Microsoft では、[Azure 料金計算ツール](https://azure.microsoft.com/pricing/calculator)を提供しています。
- 一部のクラウド プロバイダーは、コスト差分計算ツールも提供しています。 Microsoft は、[Azure の総保有コスト (TCO) 計算ツール](https://azure.microsoft.com/pricing/tco/calculator)を提供しています。
- より洗練されたコスト構造が対象であれば、[デジタル資産計画](../digital-estate/index.md)を実施することを検討してください。
- 移行のコストを見積もります。
- トレーニングの機会を設けることが予想される場合はコストを見積もります。 それらのコストを軽減するために、[Microsoft Learn](/learn) が役立つ場合があります。
- 一部の企業では、既存のスタッフが費やす時間を初期コストに含める必要があります。 手引きについては、財務部門に問い合わせてください。
- 確認のため、追加コストや負担コストがないか、財務部門に相談します。

## <a name="migration-specific-revenue-deltas"></a>移行固有の収益差分

移行の業務上の正当な理由を作成するストラテジストは、この側面を見落としがちです。 一部の領域では、クラウドによってコストを削減できます。 しかし、どのような変革の場合も、最終的な目標は長期にわたってより良い結果を生み出すことです。 長期的な収益の向上について理解するために、下流への影響を考慮してください。 現在は使用できないが、移行後に自社で利用できるようになる新しいテクノロジには何がありますか。 従来のテクノロジへの依存関係によって、どのようなプロジェクトやビジネス目標ブロックされていますか。 テクノロジへの高い資本支出を保留にして、待機状態になっているプログラムはどれですか。

クラウドによって利用可能になる機会を検討したら、事業部門と協力して、それらの機会から見込まれる収益の増加を計算します。

## <a name="migration-specific-cost-deltas"></a>移行固有のコスト差分

提案された移行に起因する、コストに対するすべての変更を計算します。 コスト差分の種類の詳細については、「[クラウド変革のための財務モデルを作成する](./financial-models.md)」を参照してください。 クラウド プロバイダーは、多くの場合、コスト差分計算ツールを提供しています。 [Azure 総保有コスト (TCO) 計算ツール](https://azure.microsoft.com/pricing/tco/calculator)は 1 つの例です。

クラウド移行によって削減される可能性があるコストのその他の例:

- データセンターの廃止または縮小 (環境コスト)
- 消費される電力の削減 (環境コスト)
- ラックの廃止 (物理的資産の回復)
- ハードウェア更新の回避 (コストの回避)
- ソフトウェア更新の回避 (運用コストの削減またはコストの回避)
- ベンダーの統合 (運用コストの削減と潜在的ソフト コストの削減)

## <a name="when-roi-results-are-surprising"></a>ROI の結果が意外な場合

クラウド移行の ROI が期待に合っていない場合は、この記事の冒頭に記載した、よく聞かれる根拠のない説を再検討することをお勧めします。

ただし、必ずしもコスト削減が可能でない場合があることを理解しておくことが重要です。 一部のアプリケーションでは、クラウドで運用するとオンプレミスよりも多くのコストがかかります。 これらのアプリケーションは、分析の結果を大幅にゆがめることがあります。

ROI が 20% を下回る場合は、[合理化](../digital-estate/rationalize.md)に特に注意して、[デジタル資産計画](../digital-estate/index.md)を実施することを検討してください。 定量分析中に、各アプリケーションを見直して、結果をゆがめるワークロードを見つけます。 それらのワークロードは、計画から削除することが理にかなっている場合があります。 使用状況のデータを入手できる場合は、使用状況に一致するように VM のサイズを縮小することを検討してください。

ROI がまだ想定外の場合は、マイクロソフトの営業担当者の支援を求めるか、[経験豊富なパートナーを雇います](https://azure.microsoft.com/migration/support)。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [クラウド変革のための財務モデルを作成する](./financial-models.md)
