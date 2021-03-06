---
title: クラウド管理
description: Azure のクラウド導入フレームワークを使用して、効果的なクラウド管理のために必要なビジネスおよび技術的なアプローチを開発する方法を学習します。
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 63912eb0c629bad8539cf5346611fc3e0923a133
ms.sourcegitcommit: 412b945b3492ff3667c74627524dad354f3a9b85
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94879635"
---
# <a name="cloud-management-in-the-cloud-adoption-framework"></a>クラウド導入フレームワークにおけるクラウド管理

[クラウド戦略](../strategy/index.md)を提供するには、十分な計画、準備、導入が必要です。 しかし、これは具体的なビジネスの結果を提供する、デジタル資産の継続的な運用です。 クラウド ソリューションにおいて信頼性の高い、適切に管理された運用を計画していなければ、これらの取り組みによる価値はほとんどありません。 次の演習は、進行中の運用を行うクラウド管理を提供するために必要なビジネスおよび技術的なアプローチを開発するのに役立ちます。

## <a name="get-started"></a>はじめに

クラウド導入ライフサイクルのこのフェーズの準備として、フレームワークからは、次の演習が提案されます。

| <span title="アイコン">&nbsp;</span> | <span title="説明">&nbsp;</span> |
|--|--|
| <br> :::image type="icon" source="../_images/icons/1.png"::: | <br> [管理ベースラインの確立](./azure-management-guide/index.md):運用管理に対する最小限のコミットメントを提供するために必要な重要度の分類、クラウド管理ツール、プロセスを定義します。 |
| <br> :::image type="icon" source="../_images/icons/2.png"::: | <br> [ビジネス コミットメントの定義](./considerations/business-alignment.md):サポートされているワークロードを文書化して、ビジネスに対する運用上のコミットメントを確立し、各ワークロードに対するクラウド管理への投資に同意します。 |
| <br> :::image type="icon" source="../_images/icons/3.png"::: | <br> [管理ベースラインの展開](./best-practices.md):ビジネス コミットメントと運用上の決定に基づいて、含まれているベスト プラクティスを活用し、必要なクラウド管理ツールを実装します。 |
| <br> :::image type="icon" source="../_images/icons/4.png"::: | <br> [高度な運用と設計の原則](./design-principles.md):より高いレベルのビジネス コミットメントを必要とするプラットフォームやワークロードでは、回復性と信頼性のコミットメントを提供するために、より深いアーキテクチャ レビューが必要になる場合があります。 |

前の手順では、クラウド導入フレームワークの管理手法を実行するためのアクションにつながるアプローチを作成します。

![クラウド導入フレームワークの管理手法](../_images/manage/caf-manage.png)

[ビジネスの整合](./considerations/business-alignment.md)に関する記事で説明されているように、すべてのワークロードがミッション クリティカルであるとは限りません。 どのポートフォリオ内でも、さまざまな運用管理のニーズがあります。 ビジネス アライメントの取り組みは、ビジネスへの影響を把握し、ビジネスにおける管理コストを交渉して、最も適切な運用管理プロセスとツールを確保するために役立ちます。

クラウド導入フレームワークの管理セクションのガイダンスには、次の 2 つの目的があります。

- お客様がよく経験する一般的なエクスペリエンスを表す、アクションにつながる運用管理のアプローチの例を示します。
- ビジネス コミットメントに基づいて、カスタマイズされた管理ソリューションを作成するのに役立ちます。

この内容は、クラウド運用チームが使用することを目的としています。 また、クラウド運用またはクラウド設計の原則で強力な基盤を開発する必要があるクラウド設計者も対象としています。

クラウド導入フレームワークのコンテンツは、企業のビジネス、テクノロジ、および文化に影響を与えます。 クラウド導入フレームワークのこのセクションは主に、IT 運用、IT ガバナンス、財務、事業部門のリーダー、ネットワーク、ID、クラウド導入のチームを対象としています。 これらの役割の人々に対するさまざまな依存関係には、このガイダンスを使用しているクラウド アーキテクトによる促進的アプローチが必要です。 これらのチームでの円滑化が、1 回限りの作業であることはめったにありません。

クラウド アーキテクトは、これらの対象ユーザーをまとめる思想的リーダーおよび進行役の役割を果たします。 このガイドのコレクションの内容は、クラウド アーキテクトが適切な対象ユーザーと適切なコミュニケーションを取り、必要な決定を促すことをサポートするために設計されています。 クラウドによって実現されるビジネスの変革は、ビジネスと IT 全体にわたる意思決定を導くクラウド アーキテクトによって決まります。

クラウド導入フレームワークの各セクションは、クラウド アーキテクトの役割のさまざまな専門性やバリエーションを表しています。 クラウド導入フレームワークのこのセクションは、デプロイ ソリューションの運用と管理に対する情熱を持つクラウド アーキテクトを対象として設計されています。 このフレームワーク内で、これらのスペシャリストは、_クラウド運用_ またはまとめて _クラウド運用チーム_ として呼ばれることがよくあります。

このガイドに最初から最後まで従う場合、この内容は、堅牢なクラウド運用戦略を開発するのに役立ちます。 このガイダンスでは、そのような戦略の理論と実装を段階を追って説明します。

手法を適用して、[明確なビジネス コミットメントを確立する](./considerations/business-alignment.md)こともできます。

<!-- TODO: For a crash course on the theory and quick access to Azure implementation, get started with the [governance guides overview](TODO). Using this guidance, you can start small and iteratively improve your governance needs in parallel with cloud adoption efforts. -->
