---
title: 組織の配置を管理する
description: Azure のクラウド導入フレームワークを使用して、組織の配置を確立および維持する方法を学習します。
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 4cceead66e21442458f277b7ac0debbd2742ddfd
ms.sourcegitcommit: 670dd77efe02ed20275732248e0fa2aae2196805
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2020
ms.locfileid: "91621537"
---
# <a name="manage-organizational-alignment"></a>組織の配置を管理する

クラウド導入は、人員が適切に組織化されていなければ達成できません。 クラウド導入の成功は、適切なスキルを持つ人員が、明確に定義された業務目標に沿って、適切に管理された環境おいて、適切な種類の作業を遂行することによって実現します。 クラウドの効果的な運用モデルを実現するには、人員が適切に配置された組織構造を確立することが重要です。 この記事では、適切な組織構造を確立して維持するためのアプローチを 4 つのステップで概説します。

次の演習は、クラウド導入を支援するランディング ゾーンの作成プロセスのガイダンスとして役立ちます。

| <span title="アイコン">&nbsp;</span> | <span title="説明">&nbsp;</span> |
|--|--|
| <br> :::image type="icon" source="../_images/icons/1.png"::: | <br> [構造の種類](#structure-type):実際の運用モデルに最も適した組織構造の種類を定義します。 |
| <br> :::image type="icon" source="../_images/icons/2.png"::: | <br> [クラウドの職務](#understand-required-cloud-functions):クラウドの導入と運用に必要なクラウドの職能について説明します。 |
| <br> :::image type="icon" source="../_images/icons/3.png"::: | <br> [チーム構造を成熟させる](./organization-structures.md):さまざまなクラウドの職務を遂行できるチームを定義します。 |
| <br> :::image type="icon" source="../_images/icons/4.png"::: | <br> [RACI マトリックス](./raci-alignment.md):明確に定義された役割は、どのような運用モデルにおいても重要な側面です。 提供されている RACI マトリックスを使用して、クラウド運用モデルのさまざまな機能について、実行責任、説明責任、協業、および報告の役割を各チームにマップします。 |

## <a name="structure-type"></a>構造の種類

以下の組織構造は、必ずしも組織図にマップする必要はありません。 通常、組織図には、命令と統制の管理構造が反映されています。 対照的に、以下の組織構造は、役割と責任の整合を取るように設計されています。 アジャイルなマトリックス組織では、これらの構造は仮想チームとして表現するのが最も適切と言えます。 これらの組織構造を組織図で表すことができないことを示唆する制限はありませんが、これは、効果的な運用モデルを作成するために必ずしも必要というわけではありません。

組織の配置を管理するための最初のステップは、以下の組織構造をどのように実現するかを決定することです。

- **組織図の配置:** 管理階層、マネージャーの責任、およびスタッフの配置は、組織の構造に合わせて調整されます。
- **仮想チーム:** 管理構造と組織図は変更されません。 代わりに、仮想チームが作成され、必要な職務が割り当てられます。
- **混合モデル:** 多くの場合、変革の目標を達成するには、組織図と仮想チームの配置を組み合わせて使用する必要があります。

## <a name="understand-required-cloud-functions"></a>必要なクラウドの職務の概要

クラウドの導入と長期的な運用モデルを成功させるために必要なクラウドの職務の一覧を以下に示します。 これらのことを理解すると、人員配置と成熟度に基づいて組織構造に合わせることができます。

- [クラウド戦略](./cloud-strategy.md):技術的な変更をビジネス ニーズに合わせます。
- [クラウド導入](./cloud-adoption.md):技術的なソリューションを提供します。
- [クラウド ガバナンス](./cloud-governance.md):リスクを管理します。
- [中央 IT チーム](./central-it.md):既存の IT スタッフからのサポート。
- [クラウド運用](./cloud-operations.md):採用されたソリューションをサポートおよび運用します。
- [クラウドのセンター オブ エクセレンス](./cloud-center-of-excellence.md):導入の品質、速度、回復性を向上させます。
- [クラウド プラットフォーム](./cloud-platform.md):プラットフォームを運用し、成熟させます。
- [クラウド自動化](./cloud-automation.md):導入とイノベーションを促進します。
- [クラウド セキュリティ](./cloud-security.md):情報セキュリティ リスクを管理します。

これらの各職務は、明示的に、または定義されたチーム構造に従って、ある程度まで、クラウド導入のあらゆる作業で遂行されます。

導入のニーズが拡大すると、それに伴ってバランスと構造を生み出すニーズも高まります。 そうしたニーズを満たすために、企業は多くの場合、組織構造を成熟させるプロセスに従います。

![組織の成熟サイクル](../_images/ready/org-ready-maturity.png)

[組織構造の成熟度の決定](./organization-structures.md)に関する記事では、成熟度の各レベルについてさらに詳しく説明しています。

組織構造の決定を経時的に追跡するために、[RACI テンプレート](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/organize/raci-template.xlsx)をダウンロードして変更します。
