---
title: Cost Management のメトリック、インジケーター、およびリスク許容度
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: クラウド ガバナンスと関連した Cost Management の説明
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: be1d4456ac8924c87241089c637fa3aacc38fb47
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032071"
---
# <a name="cost-management-metrics-indicators-and-risk-tolerance"></a>Cost Management のメトリック、インジケーター、およびリスク許容度

この記事は、Cost Management に関連したビジネスのリスク許容度の定量化を支援することを目的にしています。 メトリックとインジケーターを定義すると、Cost Management 規範の成熟への投資を行うためのビジネス ケースの作成に役立ちます。

## <a name="metrics"></a>メトリック

Cost Management は一般に、コストに関連したメトリックに重点を置いています。 リスク分析の一部として、現在どれだけのリスクに直面しているかや、コスト管理への投資がクラウド導入戦略にとってどれくらい重要かを判断するために、クラウド ベースのワークロードに対する現在の支出および計画的な支出に関連したデータを収集する必要があります。

コスト管理規範内のリスク許容度の評価に役立てるために収集する必要がある有用なメトリックの例を以下に示します。

- **年間の支出:** クラウド プロバイダーによって提供されるサービスに対する年間の総コスト。
- **月単位の支出:** クラウド プロバイダーによって提供されるサービスに対する月単位の総コスト。
- **予測された支出と実際の支出の比率:** 予測された支出と実際の支出 (月単位または年間) を比較した比率。
- **導入のペース (MOM) の比率:** 月ごとのクラウド コスト内の差分の割合 (%)。
- **累積コスト:** 月初から始まる、発生した日単位の支出の合計。
- **支出の傾向:** 予算に対する支出の傾向。

## <a name="risk-tolerance-indicators"></a>リスク許容度インジケーター

開発/テストや試験的な最初のワークロードなど、小規模なデプロイの早い段階では、コスト管理に関するリスクは比較的低くなる可能性があります。 デプロイされる資産が増えるにつれ、リスクは増大し、ビジネスのリスク許容度は低下する可能性があります。 さらに、資産を構成したり、クラウドにデプロイしたりする権限が与えられたクラウド導入チームが増えてくると、リスクは増大し、許容度が低下します。 逆に、Cost Management 規範を発展させると、人びとはクラウド導入フェーズからより革新的な新しいテクノロジのデプロイへと進むことができます。

クラウド導入の早い段階では、ビジネスを遂行して、リスク許容度のベースラインを決定します。 ベースラインが得られたら、Cost Management 規範への投資をトリガーする条件を決定する必要があります。 これらの条件は、組織ごとに異なる可能性があります。

[ビジネス リスク](./business-risks.md)を識別した後は、ビジネスを遂行して、これらのリスクを増大させる可能性のあるトリガーを識別するために使用できるベンチマークを特定します。 ビジネスでさらに Cost Management に投資する必要があることを示すために、上で説明したようなメトリックとリスク許容度のベースラインをどのように比較したらよいかを表すいくつかの例を次に示します。

- **コミットメント主導 (最も一般的):** クラウド ベンダーに今年 X,000,000 ドルを支出することをコミットしている会社。 この会社には、ビジネスがその支出目標を 20% を上回って超えることがなく、かつそのコミットメントの少なくとも 90% を使用することを確実にするための Cost Management 規範が必要です。
- **割合のトリガー:** クラウドへの支出が自社の運用システムに対して安定している会社。 _x %_ を超えて変化する場合は、コスト管理規範が賢明な投資になります。
- **オーバープロビジョニングのトリガー:** 自社のデプロイ済みのソリューションがオーバープロビジョニングされていることを確信している会社。 この会社がプロビジョニングと資産使用率の適切な整合を示すことができるまでは、Cost Management が優先度の高い投資です。
- **月単位の支出のトリガー:** 月あたり x,000 ドルを超える支出が非常に大きいコストと見なされる会社。 特定の月に支出がその金額を超えた場合、この会社は Cost Management に投資する必要があります。
- **年間の支出のトリガー:** クラウドの実験に年間 X,000 ドルを支出できる IT 研究開発予算を持つ会社。 この会社はそのクラウドで運用環境のワークロードを実行できますが、予算がその金額を超えていない場合は、まだ試験的なソリューションであると見なされます。 それを超えたら、予算を運用環境への投資のように扱い、支出を厳密に管理する必要があります。
- **運用経費を認めない (一般的ではない):** 運用経費を認めない会社では、開発/テスト ワークロードをデプロイする前に、コスト管理を行う準備を整える必要があります。

## <a name="next-steps"></a>次の手順

[クラウド管理テンプレート](./template.md)を使用して、現在のクラウド導入計画に整合するメトリックと許容度インジケーターを文書化します。

クラウドの導入計画に合致する特定のビジネス上のリスクに対処するポリシーを作成するための開始点として、コスト管理ポリシーのサンプルを確認します。

> [!div class="nextstepaction"]
> [サンプル ポリシーの確認](./policy-statements.md)