---
title: 複雑な企業のガバナンス:リソースの整合性の規範の改善
description: Azure 向けクラウド導入フレームワークを使用して、ガバナンス ベースラインを向上させ、リスクを修正するための復旧、サイズ変更、監視の制御について説明します。
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 894485d38dc14d6619375c12a5154021f14f50f9
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88880681"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-resource-consistency-discipline"></a>複雑な企業向けのガバナンス ガイド: リソースの整合性の規範の改善

この記事では、ミッション クリティカルなアプリケーションをサポートするために、ガバナンス MVP にリソース整合性コントロールを追加することによって、話を進めます。

## <a name="advancing-the-narrative"></a>物語を進める

クラウド導入チームは、保護されたデータを移動するための要件をすべて満たしました。 これらが適用されると、SLA コミットメントがビジネスで有効になり、IT 運用からのサポートが必要になります。 2 つのデータ センターを移行するチームの背後で、複数のアプリケーション開発および BI のチームが、新しいソリューションを実稼働させるための準備を整えました。 IT 運用は、クラウド運用が初めてで、既存の運用プロセスを迅速に統合する必要があります。

### <a name="changes-in-the-current-state"></a>現在の状態の変化

- IT では、保護されたデータを含む実稼働ワークロードを Azure に積極的に移動しています。 優先度が低いワークロードの一部により、実稼働トラフィックが処理されています。 IT 運用が、ワークロードをサポートする準備が整ったことを承認した時点で、さらに多くのものを削減できます。
- アプリケーション開発チームは、実稼働トラフィックへの準備が完了しています。
- BI チームは、3 つの事業部門の操作を実行するシステムに、予測と洞察を統合する準備を完了しました。

### <a name="incrementally-improve-the-future-state"></a>将来の状態を段階的に改善する

- IT 運用は、クラウド運用が初めてで、既存の運用プロセスを迅速に統合する必要があります。
- 現在や将来の状態が変わると、新しいリスクが現れるため、新しいポリシー ステートメントが必要になります。

## <a name="changes-in-tangible-risks"></a>具体的なリスクの変化

**業務の中断:** 新しいプラットフォームにはつきもののリスクがあり、ミッション クリティカルなビジネス プロセスの中断の原因となります。 IT 運用チームと、さまざまなクラウド導入を実施するチームは、クラウド運用の経験がそれほどありません。 このことは中断のリスクを増大させるため、修正とガバナンスが必要です。

このビジネス上のリスクは、いくつかの技術的リスクに発展する可能性があります

1. 運用プロセスが不整合の場合、すぐに検出または軽減できない停止が発生する可能性があります。
2. 外部からの侵入またはサービス拒否攻撃により、ビジネスが中断させられる可能性があります。
3. ミッション クリティカルな資産が適切に検出されていないため、適切に運用されていない可能性があります。
4. 未検出やラベル誤りのある資産が、既存の運用管理プロセスでサポートされない可能性があります。
5. デプロイされた資産の構成が、期待どおりのパフォーマンスを達成しない可能性があります。
6. ログへの記録が正しく行われず、集中管理もされていないため、パフォーマンスの問題の修復に対応できなくなる可能性があります。
7. 復旧ポリシーが守られない、または予想よりも長い時間がかかる可能性があります。
8. 一貫性のないデプロイ プロセスによってセキュリティの間隙が発生し、それがデータ流出または中断につながる可能性があります。
9. 構成ドリフトやパッチの適用漏れによって意図しないセキュリティの間隙が発生し、それがデータ流出または中断につながる可能性があります。
10. 定義済みの SLA の要件や確約済みの復旧要件を構成が満たすことができない可能性があります。
11. デプロイ済みのオペレーティング システムまたはアプリケーションが、OS およびアプリケーションのセキュリティ強化要件を満たせない可能性があります。
12. 複数のチームがクラウドで作業しているため、不整合のリスクがあります。

## <a name="incremental-improvement-of-the-policy-statements"></a>ポリシー ステートメントの段階的な改善

ポリシーに対する次の変更は、新しいリスクを修正して導入をガイドするのに役立ちます。 長いリストのように見えますが、これらのポリシーの採用は思ったよりは簡単である場合があります。

1. デプロイされたすべての資産を、重要性とデータ機密性によって分類する必要があります。 分類は、クラウドへのデプロイ前に、クラウド ガバナンス チームとアプリケーション所有者によってレビューされることになります。
2. ミッション クリティカルなアプリケーションが存在するサブネットをファイアウォール ソリューションで保護します。このソリューションは、侵入の検知と攻撃への対応ができることが必要です。
3. ガバナンス ツールでは、セキュリティ ベースライン チームによって定義されたネットワーク構成要件を監査し、適用する必要があります。
4. ミッション クリティカルなアプリケーションや保護データに関連するすべての資産がリソース減耗と最適化のための監視対象となっていることを、ガバナンス ツールが検証する必要があります。
5. ミッション クリティカルなアプリケーションや保護されるデータのすべてについて適切なレベルのログ データが収集されていることを、ガバナンス ツールで検証する必要があります。
6. ミッション クリティカルなアプリケーションと保護されるデータのためのバックアップ、復旧、SLA 準拠が正しく実装されていることを、ガバナンス プロセスで検証する必要があります。
7. 仮想マシンのデプロイは承認されたイメージのみとなるように、ガバナンス ツールが制限する必要があります。
8. ミッション クリティカルなアプリケーションをサポートするデプロイ済み資産のすべてについて自動更新が**禁止**されていることを、ガバナンス ツールが強制する必要があります。 違反は運用管理チームがレビューし、運用ポリシーに従って修復する必要があります。 自動的に更新されない資産は、それらのサーバーを迅速かつ効率的に更新するために、IT 運用によって所有されているプロセスに含める必要があります。
9. コスト、重要性、SLA、アプリケーション、データ分類に関連するタグ付けをガバナンス ツールで検証する必要があります。 すべての値を、クラウド ガバナンス チームが管理する定義済みの値に合わせる必要があります。
10. すべての資産にわたって一貫性を保証するために、デプロイ時点の監査と定期的な監査をガバナンス プロセスに含める必要があります。
11. クラウドのデプロイに影響を及ぼす可能性があるトレンドおよび悪用をセキュリティ チームが定期的にレビューし、クラウドで使用されるセキュリティ ベースライン ツールの更新を提供する必要があります。
12. 本番へのリリースの前に、すべてのミッション クリティカルなアプリケーションと保護データを所定の運用監視ソリューションに追加する必要があります。 選択した IT 運用ツールで検出できない資産は、本番用としてリリースすることはできません。 資産を検出可能にするために必要な変更を、関係するデプロイ プロセスに対して行う必要があります。将来のデプロイで資産が確実に検出可能となるようにするためです。
13. 検出されたら、資産がパフォーマンス要件を満たしているかを検証するために、運用管理チームが資産のサイズ設定を検証します。
14. デプロイされた資産の継続的なガバナンスを保証するために、デプロイ ツールはクラウド ガバナンス チームの承認を受ける必要があります。
15. デプロイ スクリプトのメンテナンスは、クラウド ガバナンス チームが定期的なレビューと監査のためにアクセスできる中央リポジトリで行われる必要があります。
16. デプロイ済みの資産が SLA と復旧の要件に合わせて適切に構成されていることを、ガバナンス レビュー プロセスで検証する必要があります。

## <a name="incremental-improvement-of-the-best-practices"></a>ベスト プラクティスの段階的な改善

記事のこのセクションでは、ガバナンス MVP の設計を改善して、新しい Azure ポリシーおよび Azure Cost Management と Billing の実装を含めます。 これら 2 つの設計変更を組み合わせることで、会社の新しいポリシー ステートメントを実現します。

この架空の例の体験では、保護されたデータの変化が既に発生していることが前提となります。 そのベスト プラクティスに基づき、次の項目によって運用監視の要件が追加され、ミッション クリティカルなアプリケーションのサブスクリプションが準備されます。

**企業 IT サブスクリプション:** 以下を企業 IT サブスクリプションに追加します。これはハブとして機能します。

1. クラウド運用チームは、外部の依存関係として、運用監視ツール、ビジネス継続性およびディザスター リカバリー (BCDR) ツール、および自動修復ツールを定義する必要があります。 その後、クラウド ガバナンス チームは、必要な検出プロセスをサポートできます。
    1. このユース ケースでは、クラウド運用チームは Azure Monitor をミッション クリティカルなアプリケーションの監視の主要ツールとして選択しました。
    2. またチームは、プライマリ BCDR ツールとして Azure Site Recovery を選択しました。
2. Azure Site Recovery の実装。
    1. バックアップおよび復旧プロセスのために Azure Site Recovery コンテナーを定義してデプロイします。
    2. 各サブスクリプションでのコンテナーの作成のために、Azure リソース管理テンプレートを作成します。
3. Azure Monitor の実装。
    1. ミッション クリティカルなサブスクリプションが特定されたら、Log Analytics ワークスペースを作成できます。

**個々のクラウド導入サブスクリプション:** 以下により、監視ソリューションで各サブスクリプションを確実に検出し、BCDR プラクティスに含めることができます。

1. ミッション クリティカルなノードのための Azure Policy:
    1. 標準ロールのみの使用を監査し、強制します
    2. すべてのストレージ アカウントに対する暗号化の適用を監査し、強制します。
    3. ネットワーク インターフェイスごとに、承認されたネットワーク サブネットおよび仮想ネットワークの使用を監査し、実施します。
    4. ユーザー定義のルーティング テーブルの制限を監査し、実施します。
    5. Windows と Linux の仮想マシンに対する Log Analytics エージェントのデプロイを監査し、強制します。
2. Azure のブループリント:
    1. `mission-critical-workloads-and-protected-data` という名前のブループリントを作成します。 このブループリントは、保護されたデータ ブループリントに加えて、資産も適用します。
    2. このブループリントに新しい Azure ポリシーを追加します。
    3. ミッション クリティカルなアプリケーションをホストする予定のサブスクリプションにこのブループリントを適用します。

## <a name="conclusion"></a>まとめ

これらのプロセスおよび変更をガバナンス MVP に追加することで、リソース ガバナンスに関連した多くのリスクを修正しやすくなります。 同時に、クラウド対応運用を支援するために必要な回復、サイズ設定、および監視のコントロールが追加されます。

## <a name="next-steps"></a>次のステップ

クラウド導入が拡大し、ビジネス価値が高まる一方で、リスクやクラウド ガバナンスのニーズも変わります。 このガイドの架空の会社の場合、次の契機となるのは、クラウドへの資産が 1,000 を超えるデプロイの規模になったとき、または毎月の支出が 10,000 米ドルを超えたときです。 この時点で、クラウド ガバナンス チームは、コスト管理のコントロールを追加します。

> [!div class="nextstepaction"]
> [コスト管理の規範の改善](./cost-management-improvement.md)
