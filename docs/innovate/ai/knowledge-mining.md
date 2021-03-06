---
title: ナレッジ マイニング
description: 大規模な AI とクラウドネイティブ プラクティスの導入を簡略化するツール、プログラム、コンテンツ (ベスト プラクティス、構成テンプレート、アーキテクチャ ガイダンス)。
author: v-hanki
ms.author: janet
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: think-tank
ms.openlocfilehash: 6131e1c8673bb877c556efb3f6e3d9f293d6b770
ms.sourcegitcommit: d957bfc1fa8dc81168ce9c7d801a8dca6254c6eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95446795"
---
# <a name="knowledge-mining"></a>ナレッジ マイニング

ナレッジ マイニングは、構造化データや非構造化データの中に隠されている分析情報にアクセスするプロセスを簡略化するために設計された、AI の新たなカテゴリです。 ナレッジ マイニングで AI パイプラインの使用プロセスを定義すると、構造化データや非構造化データのセットから、隠れたパターンやアクションにつながる情報をスケーラブルな方法で検出できます。

Azure Cognitive Search は、Web アプリケーション、モバイル アプリケーション、エンタープライズ アプリケーションのプライベートな異種コンテンツに対する豊富な検索エクスペリエンスを追加するための API とツールを開発者に提供するマネージド クラウド ソリューションです。 これには、スコアリング、ファセット、候補、シノニム、地域検索などの機能が用意されており、豊富なユーザー エクスペリエンスを提供します。 Azure Cognitive Search は、組み込みのナレッジ マイニング機能を備えた唯一のクラウド検索サービスでもあります。 Azure Cognitive Search は、取り込み、エンリッチ、調査と分析の手順に従って、ナレッジ マイニング エンリッチメント パイプラインのオーケストレーターとして機能します。

ナレッジ マイニングを使用する主なシナリオを以下に示します。

- **デジタル コンテンツ管理:** コンテンツ カタログの中から関連性のある検索結果を提供すると、顧客がコンテンツをよりすばやく使用できるようにします。
- **カスタマー サポートとフィードバック分析:** ドキュメントから適切な回答をすばやく見つけたり、顧客からの要望のトレンドを検出したりすることで、カスタマー エクスペリエンスを向上させます。
- **データ抽出とプロセス管理:** 重要な情報を抽出して他のビジネス ドキュメントに事前設定すると、ドキュメントの処理が高速化されます。
- **技術的コンテンツのレビューと調査:** ドキュメントを迅速に確認し、重要な情報を抽出すると、情報に基づいた意思決定を行えます。
- **監査とコンプライアンス管理:** ドキュメントに含まれる重要な領域をすばやく識別し、重要なアイデアや情報にフラグを付けます。

## <a name="checklist"></a>チェック リスト

- **概要:** 無料のナレッジ マイニング ソリューション アクセラレータ、ブート キャンプ、ワークショップにアクセスします。

  - [ナレッジ マイニング ソリューション アクセラレータ](https://github.com/Azure-Samples/azure-search-knowledge-mining)
  - [ナレッジ マイニング ワークショップ](https://github.com/Azure-Samples/azure-search-knowledge-mining/tree/master/workshops)
  - [ナレッジ マイニング ブート キャンプ](https://azure.github.io/LearnAI-KnowledgeMiningBootcamp/)
  - [ナレッジ マイニングに関する電子書籍](https://azure.microsoft.com/resources/a-developers-guide-to-building-ai-driven-knowledge-mining-solutions/)

- **Power Skills を使用する:** [Azure Search Power Skills](https://github.com/Azure-Samples/azure-search-power-skills) には、Azure Cognitive Search のカスタム スキルとしてデプロイできる便利な機能が用意されています。 スキルは、独自のカスタム スキルの[テンプレート](https://github.com/Azure-Samples/azure-search-power-skills/blob/master/Template/HelloWorld/README.md)または開始点として使用できます。 また、これらが要件を満たしている場合には、そのまま展開して使用することもできます。 また、[pull request](https://github.com/Azure-Samples/azure-search-power-skills/compare) を送信して独自のものを投稿することもできます。

- **その他のリソースを調べる:**

  - [Azure Cognitive Search の概要](/azure/search/search-what-is-azure-search)
  - [インデックス作成中のテキストとイメージの処理用の組み込みのコグニティブ スキル](/azure/search/cognitive-search-predefined-skills)
  - [Azure Cognitive Search の AI エンリッチメントのドキュメント リソース](/azure/search/cognitive-search-resources-documentation)
  - [AI エンリッチメントに関する設計上のヒントとテクニック](/azure/search/cognitive-search-concept-troubleshooting)
  - [フルテキスト検索](/azure/search/search-lucene-query-architecture)

## <a name="next-steps"></a>次のステップ

その他の AI ソリューション カテゴリを調べる:

- [AI アプリケーションとエージェント](./ai-applications.md)
- [機械学習](./machine-learning.md)
