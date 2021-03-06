---
title: 移行済みのリソースを実稼働に昇格させるための要件
description: Azure 向けのクラウド導入フレームワークを使用し、移行したリソースを実稼働に昇格させるための一般的なタスクと標準の前提条件について説明します。
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 7082380e7b64160071f4304bc5ca3a4d341df24b
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88884676"
---
# <a name="what-is-required-to-promote-a-migrated-resource-to-production"></a>移行済みのリソースを実稼働に昇格させるために何が必要か

実稼働への昇格により、クラウドへのワークロードの移行が完了します。 資産とそのすべての依存関係が昇格した後、実稼働トラフィックが再ルーティングされます。 トラフィックを再ルーティングすると、オンプレミス資産は古いものになり、使用停止にできるようになります。

昇格のプロセスはワークロードのアーキテクチャによって異なります。 ただし、いくつかの一貫した前提条件といくつかの共通のタスクがあります。 この記事ではそれぞれについて説明し、一種の昇格前チェックリストとして機能します。

## <a name="prerequisite-processes"></a>前提条件となるプロセス

実稼働デプロイの前に以下の各プロセスを実行、文書化、および検証する必要があります。

- **[評価](../assess/index.md):** クラウドとの互換性についてワークロードが評価されています。
- **[設計](../assess/architect.md):** 選択したクラウド プロバイダーに合わせて、ワークロードの構造が適切に設計されています。
- **[複製](../migrate/replicate.md):** クラウド環境に資産が複製されています。
- **[ステージング](../migrate/stage.md):** 複製された資産が、クラウド環境のステージングされたインスタンスに復元されています。
- **[ビジネス テスト](./business-test.md):** ワークロードはビジネス ユーザーによって完全にテストおよび検証されています。
- **[事業変更計画](./business-change-plan.md):** 実稼働への昇格に従って行われる変更の計画をビジネスが共有しています。これには、ユーザー導入計画、ビジネス プロセスの変更、トレーニングが必要なユーザー、各種アクティビティのタイムラインを含める必要があります。
- **[準備完了](./ready.md):** 一般に、一連の技術的な変更を昇格前に行う必要があります。

## <a name="best-practices-to-execute-prior-to-promotion"></a>昇格前に実践するベスト プラクティス

多くの場合、昇格プロセスの一環として以下の技術的変更を完了し、文書化する必要があります。

- **ドメインの配置。** 企業のポリシーによっては、ステージングと実稼働に別々のドメインが必要です。 すべての資産が適切なドメインに参加していることを確認します。
- **ユーザー ルーティング。** ユーザーが適切なネットワーク ルート経由でワークロードにアクセスしていることを確認します。一貫したパフォーマンスの期待を検証します。
- **ID の配置。** アプリケーションにルーティングされているユーザーが、アプリケーションをホストするドメイン内で適切なアクセス許可を持っていることを検証します。
- **パフォーマンス。** 予想外の問題を最小限に抑えるために、ワークロードのパフォーマンスの最終検証を実行します。
- **事業継続とディザスター リカバリーの検証。** 適切なバックアップと復旧のプロセスが期待どおりに機能していることを検証します。
- **データ分類。** データ分類を検証し、適切な保護とポリシーが実装されていることを確認します。
- **最高情報セキュリティ責任者 (CISO) の検証。** 情報セキュリティ責任者がワークロード、ビジネス リスク、リスクの許容範囲、および軽減戦略をレビューしたことを検証します。

## <a name="final-step-promote"></a>最終ステップ:昇格

ワークロードには、さまざまなレベルの詳細なレビューと昇格プロセスが必要になります。 ただし、ネットワークの再配置は、すべての昇格リリースに共通する最終ステップとなります。 他のすべての準備が整ったら、DNS レコードまたは IP アドレスを更新して、移行したワークロードにトラフィックをルーティングします。

## <a name="next-steps"></a>次のステップ

ワークロードの昇格によってリリースが完了します。 ただし、移行と並行して、廃止された資産を[使用停止](./decommission.md)してサービスから除外する必要があります。

> [!div class="nextstepaction"]
> [廃止された資産を使用停止する](./decommission.md)
