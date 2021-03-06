---
title: 移行の前にクラウド コストを見積もる
description: 意思決定と実行アクティビティに影響を与える可能性がある要因と、クラウド コストを見積もるためのさまざまなオプションについて説明します。
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 37f7186e1d74dc9e3995bffbe775bb2111156f2a
ms.sourcegitcommit: 8b82889dca0091f3cc64116f998a3a878943c6a1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89603636"
---
# <a name="estimate-cloud-costs"></a>クラウド コストを見積もる

移行中に、意思決定や実行アクティビティに影響を与える可能性があるいくつかの要因が存在します。 これらのうちのどのオプションが各種の状況に最適かを理解するのに役立つように、この記事では、クラウド コストを見積もるためのさまざまなオプションについて説明します。

## <a name="digital-estate-size"></a>デジタル資産のサイズ

デジタル資産のサイズは、移行の意思決定に直接影響を与えます。 含まれている VM が 250 個未満の移行は、10,000 個を超える VM を含む移行よりはるかに容易に見積もることができます。 最初の移行には小さなワークロードを選択することを強くお勧めします。 これにより、チームはより大きく、かつより複雑なワークロード移行を見積もろうとする前に、単純な移行作業のコストを見積もる方法を学習する機会を得ることができます。

ただし、小さな (1 つのワークロードの) 移行にも引き続き、さまざまな量のサポート資産が含まれる場合があることに注意してください。 移行に含まれる VM が 1,000 個未満の場合は、[Azure Migrate](/azure/migrate/migrate-services-overview) などのツールで十分にインベントリに関するデータを収集し、コストを予測できる可能性があります。 その他のコスト見積もりツールのオプションは、[デジタル資産のコスト計算](../../../digital-estate/calculate.md)に関する記事で説明されています。

デジタル資産が 1,000 個を超える場合でも、引き続き見積もりを 4 つまたは 5 つの実行可能なイテレーションに分解して、見積もりプロセスを管理しやすくすることができます。 より大きな資産、またはより高い予測の精度が必要な場合は、クラウド導入フレームワークの[デジタル資産](../../../digital-estate/index.md)に関するセクションで概要が説明されているような、より包括的なアプローチが必要になる可能性があります。

## <a name="accounting-models"></a>アカウンティング モデル

アカウンティング モデル

従来の IT 調達プロセスに精通している場合は、クラウドでの見積もりが異質に思えるかもしれません。 クラウド テクノロジを導入した場合は、取得が厳格で、構造化された資本コスト モデルから流動的な運営費モデルにシフトします。 従来の資本コスト モデルでは、IT チームは、さまざまなプログラムにまたがる複数のワークロードのための購買力を統合して、これらの各ソリューションをサポートできる共有された IT 資産のプールを集中管理しようとします。 運営費クラウド モデルでは、コストを個々のワークロード、チーム、または事業単位のサポート ニーズに直接帰属させることができます。 このアプローチにより、サポートされる内部顧客へのコストのより直接的な帰属が可能になります。 コストを見積もる場合は、まず、この新しいアカウンティング機能のうちのどれだけが IT チームによって使用されるかを理解することが重要です。

従来の資本コストのアプローチをアカウンティングにレプリケートする場合は、上の「[デジタル資産のサイズ](#digital-estate-size)」のセクションで推奨されているいずれかのアプローチの出力を使用して年間コストの基準を取得します。 次に、その年間コストに会社の標準的なハードウェア更新サイクルを掛けます。 ハードウェア更新サイクルは、会社が古いハードウェアを置き換える速さです (一般には、年数で測定されます)。 年間ランレートにハードウェア更新サイクルを掛けると、資本コスト投資パターンと同様のコスト構造が得られます。

## <a name="next-steps"></a>次のステップ

コストを見積もったら、移行を開始できます。 ただし、移行を開始する前に、パートナーシップおよびサポート オプションを確認することが賢明です。

> [!div class="nextstepaction"]
> [パートナーシップとサポート オプションを理解する](./partnership-options.md)
