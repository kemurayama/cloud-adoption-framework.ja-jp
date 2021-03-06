---
title: デプロイ高速化の規範の概要
description: Azure のクラウド導入フレームワークを使用して、クラウド ガバナンスに関連するデプロイ高速化の規範について説明します。
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 1bc95e74444485a86989c38133943c7cbd7201cc
ms.sourcegitcommit: 26bde9cb5de37383bdfbd682b3676fbcc584081c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2020
ms.locfileid: "89510398"
---
# <a name="deployment-acceleration-discipline-overview"></a>デプロイ高速化の規範の概要

デプロイ高速化とは、[クラウド導入フレームワーク ガバナンス モデル](../index.md)の[クラウド ガバナンスの 5 つの規範](../governance-disciplines.md)のうちの 1 つです。 この規範は、資産の構成またはデプロイを管理するためのポリシーを確立する方法に焦点を当てています。 クラウド ガバナンスの 5 つの規範のうち、デプロイ高速化規範には、デプロイ、構成の調整、およびスクリプトの再利用が含まれます。 これは手動のアクティビティによる場合と、完全に自動化された DevOps アクティビティによる場合があります。 どちらの場合も、ポリシーはほとんど同じままです。 この規範が成熟するにつれて、クラウド ガバナンス チームは、再利用可能な資産の適用によってデプロイを高速化し、クラウド導入に対する障壁を取り除くことで、DevOps およびデプロイ戦略におけるパートナーとしての役割を果たすことができます。

この記事では、クラウド ソリューション実装の計画、構築、導入、運用の各フェーズで企業が経験するデプロイ高速化プロセスについて概説します。 1 つのドキュメントですべてのビジネスのすべての要件を説明することはできません。 そのため、この記事の各セクションでは、推奨される最小および潜在的なアクティビティについて概説します。 これらのアクティビティの目標は、お客様が[ポリシーの MVP](../policy-compliance/index.md#minimum-viable-product-mvp-for-policy) を構築する一方、[増分型のポリシー](../policy-compliance/index.md#incremental-policy-growth)の改善に対するフレームワークを確立できるように支援することです。 クラウド ガバナンス チームは、デプロイ高速化のポジションを向上させるために、これらのアクティビティに投資する金額を決定する必要があります。

> [!NOTE]
> デプロイ高速化の規範は、クラウドベースのリソースを効率的にデプロイおよび構成しているお客様の組織の既存 IT チーム、プロセス、および手順にとって代わるものではありません。 この規範は、クラウド上のご利用のリソースを管理する責任がある IT スタッフが、ビジネス上の潜在的なリスクを特定し、リスクを軽減するときの指針となることを主な目的としています。 ガバナンス ポリシーおよびプロセスの策定時には、行っている計画と確認のプロセスに、関係する IT チームを関与させるようにしてください。

このガイドの主な対象読者は、お客様の組織のクラウド アーキテクトおよびお客様のクラウド ガバナンス チームのその他のメンバーです。 この規範を使用した決定、ポリシー、プロセスには、ビジネス チームと IT チームの該当メンバー (特にクラウド ベースのワークロードのデプロイおよび構成を担当するリーダー) が関与して、議論する必要があります。

## <a name="policy-statements"></a>ポリシー ステートメント

実践的なポリシー ステートメントと、その結果のアーキテクチャの要件は、デプロイ高速化の規範の基盤となります。 [サンプル ポリシー ステートメント](./policy-statements.md)を開始点として使用して、デプロイ高速化のポリシーを定義します。

> [!CAUTION]
> このサンプル ポリシーは、よくあるお客様の体験をもとにしています。 特定のクラウド ガバナンスの要件にこれらのポリシーが合うように調整するには、次の手順を行い、お客様独自のビジネス ニーズに合うポリシー ステートメントを作成してください。

## <a name="develop-governance-policy-statements"></a>ガバナンス ポリシー ステートメントの策定

次の手順を使用すると、クラウド環境内のリソースのデプロイおよび構成を管理するガバナンス ポリシーを定義できます。

| <span title="アイコン">&nbsp;</span> | <span title="説明">&nbsp;</span> |
|--|--|
| <br> ![テンプレート アイコン](../../_images/govern/process-template.png) | <br> [デプロイ高速化規範テンプレート](./template.md):デプロイ高速化の規範を文書化するためのテンプレートをダウンロードします。 |
| <br> ![リスク アイコン](../../_images/govern/process-risks.png) | <br> [ビジネス リスク](./business-risks.md):一般的にデプロイ高速化の規範に関係する動機およびリスクを理解できます。|
| <br> ![メトリック アイコン](../../_images/govern/process-metrics.png) | <br> [インジケーターとメトリック](./metrics-tolerance.md):デプロイ高速化の規範に投資する最適なタイミングであるかどうかを判断するためのインジケーターです。 |
| <br> ![準拠アイコン](../../_images/govern/process-enforce.png) | <br> [ポリシー準拠プロセス](./compliance-processes.md):デプロイ高速化の規範でのポリシー準拠を確保するための推奨の手順です。 |
| <br> ![成熟度アイコン](../../_images/govern/process-maturity.png) | <br> [成熟度](./discipline-improvement.md):クラウドの導入の段階とクラウド管理の成熟度を調整します。|
| <br> ![ツールチェーン アイコン](../../_images/govern/process-toolchain.png) | <br> [ツールチェーン](./toolchain.md):デプロイ高速化の規範をサポートするために実装できる Azure サービスです。 |

## <a name="next-steps"></a>次のステップ

特定の環境で[ビジネス上のリスク](./business-risks.md)を評価する方法の概要です。

> [!div class="nextstepaction"]
> [ビジネス リスクを理解する](./business-risks.md)
