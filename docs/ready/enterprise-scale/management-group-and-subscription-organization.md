---
title: 管理グループとサブスクリプションの組織
description: 管理グループとサブスクリプションの編成。
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: think-tank
ms.openlocfilehash: 06ff80acc1da04697fbf42ef0e50ac9768a79e94
ms.sourcegitcommit: d957bfc1fa8dc81168ce9c7d801a8dca6254c6eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95447219"
---
# <a name="management-group-and-subscription-organization"></a>管理グループとサブスクリプションの組織

![管理グループの階層を示す図。](./media/sub-org.png)

"_図 1:管理グループの階層。_

## <a name="define-a-management-group-hierarchy"></a>管理グループの階層を定義する

Azure Active Directory (Azure AD) テナント内の管理グループの構造では組織のマッピングがサポートされてており、組織で大規模な Azure の導入を計画するときは十分に検討する必要があります。

**設計上の考慮事項:**

- 管理グループを使用すると、Azure Policy を介してポリシーとイニシアティブの割り当てを集約できます。
- 管理グループのツリーでは、[最大 6 レベルの深さ](/azure/governance/management-groups/overview#hierarchy-of-management-groups-and-subscriptions)までサポートできます。 この制限には、テナント ルート レベルまたはサブスクリプション レベルは含まれません。
- 管理グループの操作の RBAC 認可は既定で有効になっていないため、Azure AD テナント内のどのプリンシパル (ユーザー、サービス プリンシパル) も新しい管理グループを作成できます。
- 既定では、新しいサブスクリプションはすべてルート管理グループに配置されます。

**設計上の推奨事項:**

- できる限り、管理グループの階層は、3 ないし 4 レベル以下のある程度フラットなものにします。 この制限により、管理のオーバーヘッドと複雑さが軽減されます。
- 組織の構造を深い入れ子になった管理グループ階層に複製しないようにします。 管理グループは、ポリシーの割り当てと課金のために使用する必要があります。 このアプローチには、エンタープライズ規模のアーキテクチャで意図する目的のために管理グループを使用する必要があります。これにより、同じ管理グループ レベルで同じ種類のセキュリティとコンプライアンスを必要とするワークロードに対して Azure ポリシーが提供されます。
- ルート レベルの管理グループの下に管理グループを作成して、ホストするワークロード (アーキタイプ) の種類と、セキュリティ、コンプライアンス、接続性、機能のニーズに基づくワークロードの種類を表します。 このグループ化構造により、セキュリティ、コンプライアンス、接続、機能について同じ設定を必要とするすべてのワークロードに対し、管理グループ レベルで適用される一連の Azure ポリシーを使用できます。
- Azure Policy で適用または追加できるリソース タグを使用して、管理グループ階層全体のクエリと階層間の水平移動を行うことができます。 これにより、複雑な管理グループ階層を使用しなくても、検索のニーズに合わせてリソースをグループ化できます。
- ユーザーが Azure をすぐに試すことができるように、最上位レベルのサンドボックス管理グループを作成します。 次にユーザーは、運用環境でまだ許可されていない可能性があるリソースを試すことができます。 サンドボックスは、開発、テスト、運用の各環境から分離されています。
  - 最上位レベルのサンドボックス管理グループの詳細なガイダンスについては、[実装ガイドライン](./implementation-guidelines.md#sandbox-governance-guidance)をご覧ください。
- 管理グループ管理操作、サブスクリプション管理操作、ロールの割り当てを実行するには、専用のサービス プリンシパル名 (SPN) を使用します。 SPN を使用することは、昇格された権利を持つユーザーの数が減り、最小特権ガイドラインに従うということになります。
- 上記の SPN にルート レベルでのアクセス権を付与するには、ルート管理グループのスコープ (`/`) で `User Access Administrator` Azure ロールベースのアクセス制御 (RBAC) ロールを割り当てます。 SPN にアクセス許可を付与した後は、`User Access Administrator` ロールを安全に削除できます。 これにより、SPN のみが `User Access Administrator` ロールの一部となります。
- ルート管理グループのスコープ (`/`) で、前述の SPN に `Contributor` アクセス許可を割り当てると、テナント レベルの操作が可能になります。 このアクセス許可レベルでは、その SPN を使用して、組織内の任意のサブスクリプションに対するリソースのデプロイと管理を確実に行うことができます。
- 共通プラットフォーム ポリシーと RBAC の割り当てをサポートするには、ルート管理グループの下に `Platform` 管理グループを作成します。 このグループ化構造では、Azure 基盤に使用されるサブスクリプションにさまざまなポリシーを確実に適用できます。 また、共通リソースの課金が、1 つの基盤サブスクリプション セットで確実に集中管理されます。
- ルート管理グループのスコープ (`/`) で行われる Azure Policy の割り当ての数を制限します。 この制限により、下位レベルの管理グループで継承されるポリシーのデバッグが最小限に抑えられます。
- 管理グループの階層設定で RBAC 認可を有効にして、特権のあるユーザーのみがテナントの管理グループを操作できるようにします。
- 新しいサブスクリプションに対して既定の専用管理グループを構成して、ルート管理グループの下にサブスクリプションが配置されないようにします。

## <a name="subscription-organization-and-governance"></a>サブスクリプションの編成とガバナンス

サブスクリプションは、Azure 内での管理、課金、スケールの単位です。 大規模な Azure 導入を計画するときに、重要な役割を果たします。 このセクションは、重要な要素に基づいて、サブスクリプション要件を把握し、ターゲット サブスクリプションを設計する場合に役立ちます。 それらの要素とは、環境の種類、所有権とガバナンス モデル、組織構造、アプリケーション ポートフォリオです。

**設計上の考慮事項:**

- サブスクリプションは、Azure ポリシーを割り当てるための境界として機能します。 たとえば、支払いカード業界 (PCI) のワークロードなど、セキュリティで保護されたワークロードには、通常、コンプライアンスを実現するために追加のポリシーが必要です。 管理グループを使用して PCI コンプライアンスを必要とするワークロードをグループ化する代わりに、サブスクリプションで同じ分離を実現できます。 これにより、少数のサブスクリプションが含まれる管理グループが多数作成されるのを防ぐことができます。
- サブスクリプションはスケール ユニットとして機能します。これにより、コンポーネントのワークロードをプラットフォームの[サブスクリプション制限](/azure/azure-subscription-service-limits)内でスケーリングできます。 ワークロードの設計セッションの間に、サブスクリプションのリソース制限を考慮してください。
- サブスクリプションによって、ガバナンスと分離のための管理境界が提供され、問題が明確に分離されます。
- Azure AD テナントで Enterprise Agreement 加入契約サブスクリプションだけを使用するよう制限するために実行できる (将来的に自動化が予定されている) 手動プロセスがあります。 このプロセスにより、ルート管理グループのスコープでの Microsoft Developer Network サブスクリプションの作成が防止されます。

**設計上の推奨事項:**

- ビジネス ニーズや優先度に合わせて民主化された管理のユニットとして、サブスクリプションを扱います。
- サブスクリプションの所有者に各自のロールと責任を認識させます。
  - 1 年間に 4 回または 2 回、Azure AD Privileged Identity Management でアクセス レビューを実行し、ユーザーが顧客組織内を移動することで特権が急増しないことを確認します。
  - 予算の支出とリソースの使用を完全に所有します。
  - ポリシーのコンプライアンスを保証し、必要に応じて修復します。
- 新しいサブスクリプションの要件を特定するときは、次の原則を使用します。
  - **スケールの制限:** サブスクリプションは、コンポーネントのワークロードがプラットフォームのサブスクリプション制限内でスケーリングされるときのスケール ユニットとして機能します。 たとえば、ハイパフォーマンス コンピューティング、IoT、SAP などの大規模で特殊なワークロードはすべて、制限 (Azure Data Factory の統合に対する 50 個の制限など) を回避するために個別のサブスクリプションを使用するのに適しています。
  - **管理の境界:** サブスクリプションによって、ガバナンスと分離のための管理境界が提供されます。これにより、問題を明確に分離することができます。 たとえば、開発、テスト、運用などのさまざまな環境は、多くの場合、管理の観点から分離されます。
  - **ポリシーの境界:** サブスクリプションは、Azure ポリシーの割り当ての境界として機能します。 たとえば、PCI などのセキュリティ保護されたワークロードでは、通常、コンプライアンスを実現するために追加のポリシーが必要になります。 別個のサブスクリプションが使用されている場合、この追加のオーバーヘッドを全体的に考慮する必要はありません。 同様に、開発環境では、運用環境と比較して、追加のポリシーが必要になります。
  - **ターゲット ネットワーク トポロジ:** 仮想ネットワークは、サブスクリプション間で共有することはできませんが、仮想ネットワーク ピアリングや Azure ExpressRoute などのさまざまなテクノロジを使用して接続することができます。 新しいサブスクリプションが必要かどうかを判断するときには、相互通信が必要なワークロードを検討してください。
- 大規模な管理グループの構造およびポリシー要件に合わせて、管理グループにサブスクリプションをグループ化します。 グループ化により、ポリシーと RBAC 割り当てのセットが同じであるサブスクリプションでは、確実に管理グループからそれらが継承されるようにして、重複する割り当てを回避できます。
- `Platform` 管理グループで専用の管理サブスクリプションを設定し、Azure Monitor Log Analytics ワークスペースや Azure Automation Runbook などのグローバル管理機能をサポートします。
- 必要に応じて、`Platform` 管理グループで専用の ID サブスクリプションを設定し、Windows Server Active Directory ドメイン コントローラーをホストします。
- `Platform` 管理グループで専用の接続サブスクリプションを設定し、Azure Virtual WAN ハブ、プライベート ドメイン ネーム システム (DNS)、ExpressRoute 回線、その他のネットワーク リソースをホストします。 専用のサブスクリプションによって、すべての基盤ネットワーク リソースが一緒に請求され、他のワークロードから分離されることが保証されます。
- 硬直したサブスクリプション モデルを避け、代わりに柔軟な条件を設定して、組織全体でサブスクリプションをグループ化します。 この柔軟性により、組織の構造とワークロードの構成が変化したときに、既存のサブスクリプションの固定したセットを使用するのではなく、新しいサブスクリプション グループを作成できることが保証されます。 1 つのサイズがサブスクリプションのすべてに適合するわけではありません。 ある部署で動作するものが、別の部署では機能しない場合があります。 アプリケーションによっては、同じランディング ゾーンのサブスクリプション内で共存する場合もあれば、独自のサブスクリプションを必要とする場合もあります。

## <a name="configure-subscription-quota-and-capacity"></a>サブスクリプションのクォータと容量を構成する

各 Azure リージョンに含めることができるリソースの数には制限があります。 大量のリソースを必要とするエンタープライズ規模で Azure の導入を検討するときは、十分な容量と SKU を使用できることと、取得された容量を認識および監視できることを確実にしてください。

**設計上の考慮事項:**

- ワークロードに必要な各サービスについて、Azure プラットフォームでの制限とクォータを考慮します。
- 選択した Azure リージョンで必要な SKU を利用できるかどうかを検討します。 たとえば、新しい機能は特定のリージョンでしか使用できない場合があります。 VM など、特定のリソースに対する特定の SKU の可用性は、リージョンによって異なる場合があります。
- サブスクリプションのクォータは容量の保証ではなく、リージョンごとに適用されることを考慮します。

**設計上の推奨事項:**

- サブスクリプションをスケール ユニットとして使用し、必要に応じてリソースとサブスクリプションをスケールアウトします。 これにより、必要なときにスケールアウトに必要なリソースをワークロードで使用できるようになり、Azure プラットフォームでのサブスクリプションの制限に達することがなくなります。
- 必要なリージョンで予約容量を優先するには、予約インスタンスを使用します。 これにより、特定のリージョンでそのリソースが大量に必要になったときでも、ご利用のワークロードに必要な容量が確保されます。
- カスタム ビューを使用してダッシュボードを設定し、使用されている容量レベルを監視します。 容量使用率が重大レベルに達した場合のアラートを設定します (たとえば、CPU 使用率 90%)。
- サブスクリプションのプロビジョニングの一環として、クォータ増量のサポート リクエストを送ります (たとえば、サブスクリプションで使用可能な合計 VM コア数)。 このアプローチによって、ワークロードで既定の制限を超える量が必要になる前に、クォータ制限が確実に設定されます。
- 必要なサービスと機能が、選択したデプロイ リージョンで利用可能であることを確認します。

## <a name="establish-cost-management"></a>コスト管理を確立する

技術資産のコストの透明性は、すべての大規模なエンタープライズ組織にとって重要な管理上の課題となります。 このセクションでは、大規模な Azure 環境でコストの透明性を実現する方法に関する主要な側面について説明します。

**設計上の考慮事項:**

- Azure App Service Environment や Azure Kubernetes Service など、高密度を実現するためには共有することが必要な場合がある、共有のサービスとしてのプラットフォーム (PaaS) リソースが関係する場合は、チャージバック モデルが必要になることがあります。
- コストを最適化するには、非運用ワークロードのシャットダウン スケジュールを使用します。
- Azure Advisor を使用して、コストの最適化に関する推奨事項を確認します。

**設計上の推奨事項:**

- コスト集計には、Azure Cost Management + Billing を使用します。 アプリケーション所有者が使用できるようにします。
- Azure リソース タグを使用して、コストの分類とリソースのグループ化を行います。 タグを使用すれば、サブスクリプションを共有するワークロード、または複数のサブスクリプションにまたがる特定のワークロードに対して、チャージバック メカニズムを使用できます。
