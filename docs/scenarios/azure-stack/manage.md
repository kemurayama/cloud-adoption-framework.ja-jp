---
title: Azure Stack Hub で実行されているワークロードを管理する
description: Azure Stack Hub で実行されているワークロードを管理する方法について説明します。
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 58d3f1eee0ea3514ccf3b9ee99f30fb7bcef978e
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452766"
---
# <a name="manage-workloads-running-on-azure-stack-hub"></a>Azure Stack Hub で実行されているワークロードを管理する

パブリックおよびプライベートのクラウド プラットフォームにまたがるハイブリッド ソリューションの運用と管理は複雑で、ビジネスの運営にリスクが生じる可能性があります。 Azure Stack Hub はデータセンターで実行されている Azure の独自のプライベート インスタンスであるため、ハイブリッド操作のリスクは大幅に削減されます。

クラウド導入フレームワークの[管理手法](../../manage/index.md)に概説されているように、推奨される運用管理アクティビティでは、以下の主な役割に重点を置いています。 これらの同じ役割は、Azure Stack Hub をサポートする運用管理チームにも当てはまります。

- **インベントリと可視性:** 複数のクラウドをまたいで資産の目録を作成します。 各資産の実行状態が見えるようにします。
- **運用のコンプライアンス:** 各状態が適切に構成され、条文に制御された環境で実行されるよう、コントロールとプロセスを確立します。
- **保護と復旧:** 管理対象のすべての資産が保護され、ベースライン管理ツールで復旧できるようにします。
- **拡張ベースライン オプション:** ビジネス ニーズを満たす可能性があるベースラインへの一般的な追加オプションを評価します。
- **プラットフォームの運用:** 十分に定義されたサービス カタログと集中管理型のプラットフォームを使用して管理ベースラインを拡張します。
- **ワークロードの運用:** 管理ベースラインを拡張し、ミッション クリティカルなワークロードに集中的に取り組みます。

## <a name="azure-stack-hub-operations-management-considerations"></a>Azure Stack Hub の運用管理に関する考慮事項

標準の運用管理アクティビティの中には、少し異なる技術的な考慮事項を必要とするものがあります。 以下の記事では、これらの考慮事項について概説します。

- [セルフサービス サポート](https://azure.microsoft.com/blog/azure-stack-iaas-part-five/)は、顧客を対象としており、ブート診断、スクリーンショット、シリアル ログ、メトリックなどが含まれます。
- [ゲスト管理](https://azure.microsoft.com/blog/azure-stack-iaas-part-one/)には、VM 拡張機能、カスタム コードを実行する機能、ソフトウェア インベントリ、変更の追跡などが含まれます。
- [ビジネス継続性](https://azure.microsoft.com/blog/azure-stack-iaas-part-four/)は、VM のバックアップとディザスター リカバリー オプションにより実現されます。

## <a name="next-step-integrate-this-strategy-into-your-cloud-adoption-journey"></a>次のステップ: この戦略をクラウド導入の取り組みに統合する

Azure Stack Hub の移行が動作状態になると、Azure のパブリック クラウドで Azure Stack Hub またはその他の移行シナリオを使用して、次の移行の繰り返しを開始できます。

- [Azure Stack Hub 移行の計画](./plan.md)
- [環境の準備](./ready.md)
- [Azure Stack Hub のワークロードを評価する](./migrate-assess.md)
- [Azure Stack Hub にワークロードをデプロイする](./migrate-deploy.md)
- [Azure Stack Hub のガバナンス](./govern.md)
- [Azure Stack Hub の管理](./manage.md)