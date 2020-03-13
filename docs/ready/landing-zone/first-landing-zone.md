---
title: Azure ランディング ゾーンに関する考慮事項
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: ランディング ゾーンによってクラウド導入環境の基礎構成要素が提供されるしくみについて説明します。
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: b451ec6f58a684bd4fb5998f1915dc79761b7a44
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2020
ms.locfileid: "78228586"
---
# <a name="first-landing-zone"></a>最初のランディング ゾーン

コードとしてのインフラストラクチャは、ほとんどのクラウド導入作業中の自然な移行です。 クラウドへの最初のランディング ゾーンのデプロイは、コード駆動型環境に移行する際の一般的な出発点となります。 この記事は、_ランディング ゾーン_という用語を理解し、現在の導入ニーズに最適なランディング ゾーンを決定するのに役立ちます。

## <a name="code-first-approach-to-landing-zones"></a>ランディング ゾーンへのコード優先アプローチ

次の図は、ランディング ゾーンのさまざまなオプションを示しています。 次のオプションは、すぐに正しいランディング ゾーンを選択するのに役立ちます。 また、将来のランディング ゾーンのニーズに対するビジョンを確立するのにも役立ちます。

![ランディング ゾーンのオプション​​](../../_images/ready/landing-zone-options.png)

A. コードから開始して、一貫性のある反復可能なランディング ゾーンを作成します。 学習するにつれてリファクタリング (コードとインフラストラクチャの改良) に慣れてきたら、クラウド導入フレームワークの移行ランディング ゾーン ブループリントなどの軽量なコード ベースから始めます。 このアプローチは、導入の成功を加速するとともに、実践的な学習機会を生み出します。 ただし、この種類の初期ランディング ゾーンは、追加のリファクタリングを行わずに機密データやミッション クリティカルなワークロードに使用するようには設計されていません。

B. 導入が拡大し、要件がより明確に識別されるにつれて、導入とプラットフォームの各チームは、学習内容に基づいてランディング ゾーンのリファクタリングを行います。 ランディング ゾーンを展開する過程により、より複雑なコンプライアンスまたはアーキテクチャの要件に対応した環境が準備されます。 「[ランディング ゾーンの展開](../considerations/index.md)」には、リファクタリングの作業に役立つ意思決定ガイドとベスト プラクティスへのリンクが用意されています。 ランディング ゾーンを展開すると、セキュリティ、運用、ガバナンスの要件を満たすのに役立ちます。

C. 一部のクラウド導入計画は、外部のコンプライアンス要件によって管理されます。 これらの要件を満たすための負担を軽減するために、Azure にはいくつかのサンプル Azure Blueprints が用意されています。 一部のサンプルは、最初の初期ブループリントに追加できます。 また、最初のランディング ゾーンとして使用できる特定の実装が含まれているサンプルもあります。

D. パートナーが継続的なマネージド サービスを提供したり、導入計画に基づいて提供するよう契約していたりする場合、通常は独自のランディング ゾーンが提供されます。 パートナーのランディング ゾーンを使用すると、導入作業が加速され、一貫した運用管理要件が確保される可能性があります。 ただし、整合性を確保するために、内部のガバナンスとセキュリティの要件についてはさらに考慮してください。

E. **1000 を超える資産 (アプリ、インフラストラクチャ、またはデータ資産) をクラウドでホストする**という中期目標 (24 か月以内) を持つ導入チームは、プラットフォーム アーキテクチャとランディング ゾーンのガイドとして、クラウド導入フレームワークの NorthStar に目を向ける必要があります。 Northstar は、対象状態のプラットフォーム アーキテクチャやリファレンス実装を含む、より高度なロードマップです。 このロードマップでは、ガバナンスや運用などの並列的な方法論の側面を組み込んで、ミッション クリティカルで、安全、複雑、およびコンプライアンスによって管理された導入に向けて入念な準備を行います。

## <a name="choosing-a-first-landing-zone"></a>最初のランディング ゾーンの選択

最初のランディング ゾーンの選択は、多くの変数によって決まります。 次のグリッドには、最初のランディング ゾーンの一部のオプションと、意志決定に役立つ変数が記載されています。

| ランディング ゾーン                                 | クラウド エクスペリエンス  | スケール             | 検出の時間 | 運用環境の準備 | ハイブリッド             | 機微なデータ     | ミッション クリティカル   | コンプライアンス         |
|----------------------------------------------|-------------------|-------------------|----------------|------------------|--------------------|--------------------|--------------------|--------------------|
| [CAF 移行](./migrate-landing-zone.md)     | クラウドの利用は初めて      | 1,000 未満の資産    | 1 から 5 日    | 制限付きスコープ -> | 展開が必要 | 展開が必要 | 展開が必要 | 展開が必要 |
| [CAF Terraform](./terraform-landing-zone.md) | 各種テンプレート | 各種テンプレート | 10 から 20 週間 | 制限付きスコープ -> | モジュールが利用可能  | モジュールが利用可能  | モジュールが利用可能  | モジュールが利用可能  |

次の表では、より技術的な意志決定プロセスをガイドするために、若干異なる視点から同じランディング ゾーンを示しています。

| ランディング ゾーン                                 | ハブ                          | スポーク    | クラウド モデル | テクノロジ      |
|----------------------------------------------|------------------------------|----------|-------------|-----------------|--|--|--|
| [CAF 移行](./migrate-landing-zone.md)     | リファクタリングが必要            | Included | Azure のみ  | Azure Blueprint |
| [CAF Terraform](./terraform-landing-zone.md) | NorthStar モジュールに含まれている | Included | マルチクラウド  | Terraform       |

## <a name="next-steps"></a>次のステップ

まだ、最初のランディング ゾーンとしてどちらを選択すべきか分からない場合は、[CAF 移行ランディング ゾーン ブループリント](./migrate-landing-zone.md)から始めることをお勧めします。

> [!div class="nextstepaction"]
> [CAF 移行ランディング ゾーン ブループリント](./migrate-landing-zone.md)