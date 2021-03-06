---
title: グローバルな展開の成果の例
description: Azure 向けのクラウド導入フレームワークを使用して、クラウド変革のコンテキストにおけるグローバルな展開の成果を理解します。
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 9471b396885c3eb3e29d4e5c9892cf572c8f6f5c
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94996861"
---
<!-- cSpell:ignore Personalizer -->
<!-- docutune:ignore "global reach" -->

# <a name="examples-of-global-reach-outcomes"></a>グローバルな展開の成果の例

[ビジネス成果](./index.md)に関するページで説明したように、見込みがあるさまざまなビジネス上の成果を、企業との変革に取り組むための対話の基盤として役立てることができます。 この記事では、一般的なビジネス手段であるリーチに注目します。 "_リーチ_" という簡潔な用語は、この場合、企業のグローバリゼーション戦略を指します。 会社のグローバル化戦略を理解することは、ビジネスの変革への取り組みによって目指すビジネス成果をより明確に示すことに役立ちます。

Fortune 500 企業と、それより小規模の企業では、30 年以上にわたってサービスと顧客のグローバリゼーションに注力してきました。このグローバリゼーションは引き続き注目を集めているため、ほとんどの企業がグローバル取引に携わる可能性があります。 世界各地のデータセンターのホスティングには、年間の IT 予算の 80% 以上が費やされることがあります。専用回線を使用してそれらのデータセンターを接続するワイド エリア ネットワークには、1 年あたり数百万ドルのコストがかかる場合があります。 そのため、グローバルな運用を支援することは困難でコストがかかります。

クラウド ソリューションを利用すると、グローバル化のコストはクラウド プロバイダーに移ることになります。 Azure では、お客様はデータセンターを購入したりプロビジョニングしたりすることなく、お客様または運用環境と同じリージョンにリソースを迅速にデプロイすることができます。 マイクロソフトは世界最大規模のワイド エリア ネットワークを保有し、世界中のデータセンターを接続しています。 接続とグローバル運用の容量は、世界中のお客様がオン デマンドで使用できます。

## <a name="global-access"></a>グローバル アクセス

新しい市場への進出は、変革時の最も重要なビジネス成果の 1 つです。 長い期間をかけずにリソースを市場に迅速にデプロイできるため、営業と運用のリーダーは過去には考えられていなかった選択肢を模索することができます。

### <a name="manufacturing-example"></a>メーカーの例

ある化粧品メーカーが、トレンドを把握しました。 アジア太平洋地域で営業チームが運営されていないにもかかわらず、その地域にいくつかの製品が出荷されています。 リモートの営業チームが必要とする最低限のシステムは小規模なものですが、待機時間はリモート アクセス ソリューションを妨げることになります。 このトレンドから利益を得るために、営業担当副社長は日本および韓国の営業チームと実験をしたいと考えています。 この会社はクラウド移行を完了しているため、必要なシステムを日本と韓国の両方に数日でデプロイすることができました。 これにより、営業担当副社長はこの地域の収益を 3 か月間で _x%_ 増加させることができました。 これら 2 つの市場は世界の他の地域を上回り続け、地域全体の営業活動に繋がっています。

### <a name="retail-example"></a>小売業の例

製品を世界中に出荷しているオンライン小売業者は、タイム ゾーンを超え、複数の言語で顧客と関わり合うことができます。 この小売業者は、Azure Bot Service と、Translator、Language Understanding (LUIS)、QnA Maker、Text Analytics などの Azure Cognitive Services のさまざまな機能を使用しています。 これにより、顧客は必要な情報を必要なときに、彼らが使用している言語で確実に取得することができます。 小売業者は [Personalizer](https://azure.microsoft.com/services/cognitive-services/personalizer/) サービスを使用して、顧客向けのエクスペリエンスおよびカタログ オファリングをさらにカスタマイズし、地理的なニーズ、好み、および在庫状況が確実に反映されるようにしています。

## <a name="data-sovereignty"></a>データの主権

新たな市場で活動することで、追加のガバナンス制約が生じます。 Azure では、規制対象となる業界やグローバル市場においてお客様が遵守義務を満たせるよう支援する、コンプライアンス認証が提供されています。 詳細については、「[Overview of Microsoft Azure compliance ](https://azure.microsoft.com/overview/trusted-cloud/compliance)」 (Microsoft Azure コンプライアンスの概要) を参照してください。

### <a name="example"></a>例

米国を拠点とするある公益事業者が、カナダで公益事業を提供する契約を獲得しました。 カナダのデータ主権に関する法律では、カナダのデータはカナダ内に留めておく必要があります。 この会社は、クラウド対応のアプリケーション改革に長年取り組んできました。 その結果、彼らのソフトウェアは、完全にスクリプト化された DevOps プロセスを通じてデプロイされました。 その会社はコード ベースにいくつかの軽微な変更を加え、コードの作業用コピーをカナダの Azure データセンターにデプロイし、データ主権のコンプライアンスに準拠して顧客を保持することができました。

## <a name="next-steps"></a>次の手順

詳細については、顧客エンゲージメントの成果に関するページをご覧ください。

> [!div class="nextstepaction"]
> [顧客エンゲージメントの成果](./engagement-outcomes.md)
