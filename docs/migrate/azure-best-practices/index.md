---
title: Azure クラウド移行のベスト プラクティスのチェックリスト
description: Azure クラウド移行のチェックリストを参照して、クラウド移行のベスト プラクティスに合わせて Azure ツールを実装する方法を確認してください。
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: seo-azure-migrate
ms.openlocfilehash: f90c1ef74d63d282270eeb022ca6e4ec54300071
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94996079"
---
# <a name="azure-cloud-migration-best-practices-checklist"></a>Azure クラウド移行のベスト プラクティスのチェックリスト

Azure への移行に関心がある場合は、クラウド導入フレームワークの [Azure 移行ガイド](../azure-migration-guide/index.md)から始めてください。 このガイドでは、仮想マシンをクラウドに移行するための一連のツールおよび基本的なアプローチについて説明します。

次のチェックリストは、基本的なクラウドネイティブ ツールを超える Azure クラウド移行のベスト プラクティスを示しています。 移行の範囲が [Azure 移行ガイド](../azure-migration-guide/index.md)の範囲を超える可能性のある、一般的に複雑な領域をまとめています。

## <a name="migration-best-practices-for-business-driven-scope-expansion"></a>ビジネス主導のスコープ拡張に関する移行のベスト プラクティス

- **[グローバル市場をサポートする](./multiple-regions.md):** 業務は、異なるデータ主権要件がある複数の地域で行われています。 その要件を満たすには、移行段階の前提条件の確認と資産の分散に考慮事項を追加する必要があります。

## <a name="migration-best-practices-for-technology-driven-scope-expansion"></a>テクノロジ主導のスコープ拡張に関する移行のベスト プラクティス

- **[VMware の移行](./vmware-host.md):** VMware ホストを移行すると、移行プロセス全体を高速化できます。 移行された各 VMware ホストでは、複数のワークロードをクラウドに移動できます。 移行後は、これらの VM とワークロードを VMware に維持したり、最新のクラウド機能に移行したりすることができます。
- **[SQL Server の移行](./sql-migration.md):** SQL Server のインスタンスを移行すると、移行プロセス全体を高速化できます。 移行された各インスタンスでは、複数のデータベースとサービスを移動できるため、複数のワークロードを加速させる可能性があります。
- **[複数のデータセンター](./multiple-datacenters.md):** 複数のデータセンターの移行は、かなり複雑になります。 移動の各プロセス (評価、移行、最適化、管理) では、より複雑な環境用に準備するために、追加の考慮事項について検討します。
- **[データ要件がネットワーク容量を超える](./network-capacity-exceeded.md):** 企業がクラウドへの移行を選択する理由は、多くの場合、既存のデータセンターの容量、速度、または安定性に満足できなくなったためです。 残念ながら、こうした同じ制約によって移行プロセスが複雑になり、評価および移行プロセス段階で追加の計画が必要になります。
- **[ガバナンスまたはコンプライアンスの戦略](./governance-or-compliance.md):** ガバナンスとコンプライアンスが移行の成功に不可欠な場合は、IT ガバナンス チームとクラウド導入チームの間で追加の調整が必要です。

## <a name="additional-migration-best-practices"></a>その他の移行のベスト プラクティス

- [Azure に移行されたワークロードのネットワークを設定する](./migrate-best-practices-networking.md)
- [移行インフラストラクチャをデプロイする](./contoso-migration-infrastructure.md)
- [Azure に移行するワークロードのコストとサイズ](./migrate-best-practices-costs.md)
- [Azure への移行のスケーリング](./contoso-migration-scale.md)

## <a name="next-steps"></a>次のステップ

Azure 移行のベスト プラクティスを確認する際には、次が良い開始点です。

> [!div class="nextstepaction"]
> [複数のデータセンター](./multiple-datacenters.md)
