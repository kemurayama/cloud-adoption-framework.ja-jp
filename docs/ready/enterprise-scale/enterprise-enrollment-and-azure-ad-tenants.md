---
title: エンタープライズ登録と Azure Active Directory テナント
description: エンタープライズ登録と Azure Active Directory テナント。
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: a5c9f562e521ec1e04b598b9c2c55deceb72e45e
ms.sourcegitcommit: 9b183014c7a6faffac0a1b48fdd321d9bbe640be
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85076975"
---
# <a name="enterprise-enrollment-and-azure-active-directory-tenants"></a>エンタープライズ登録と Azure Active Directory テナント

## <a name="planning-for-enterprise-enrollment"></a>エンタープライズ登録の計画

エンタープライズ登録は、エンタープライズ契約と呼ばれることも多く、Microsoft と、お客様が Azure を使用する方法との取引関係を表しています。 これは、すべてのお客様のサブスクリプションにわたる請求の基礎となり、お客様の資産管理に影響を及ぼします。 エンタープライズ登録は EA とも呼ばれ、Azure エンタープライズ ポータルを使用して管理されます。 Azure エンタープライズ登録は、多くの場合、部門、アカウント、サブスクリプションなど、組織の階層を表します。 この階層は、組織内のコスト登録グループを表します。

![Azure EA の階層](./media/ea.png)
_図 1: Azure エンタープライズ登録の階層。_

- 部門は、コストを論理的なグループに分け、部門レベルで予算またはクォータを設定するために役立ちます (注: クォータは強制されず、レポート目的で使用されます)。

- アカウントは、Azure エンタープライズ ポータルの組織単位です。サブスクリプションの管理とレポートへのアクセスに使用できます。

- サブスクリプションは、Azure エンタープライズ ポータルの最小単位です。 これらは、サービス管理者によって管理される Azure サービスのコンテナーです。 組織によって Azure サービスがデプロイされる場所です。

- エンタープライズ登録ロールによって、ユーザーは職務的なロールにリンクされます。 これらのロールは次のとおりです。
  - エンタープライズ管理者
  - 部門管理者
  - アカウント所有者
  - サービス管理者
  - 通知の連絡先

**設計上の考慮事項:**

- 登録には、顧客サブスクリプションの管理を統制する階層的な組織構造があります。

- 複数の顧客環境を EA アカウント レベルで分離して、包括的な分離をサポートできます。

- 1 つの登録に複数の管理者を任命することができます。

- 各サブスクリプションには、関連付けられたアカウント所有者が必要です。

- 各アカウント所有者は、そのアカウントでプロビジョニングされたサブスクリプションのサブスクリプション所有者になります。

- サブスクリプションは、常に 1 つのアカウントにのみ属することができます。

- サブスクリプションは、所定の一連の条件に基づいて一時停止される場合があります。

**設計上の推奨事項:**

- すべてのアカウントの種類に認証の種類 `Work or school account` のみを使用します。 `Microsoft account (MSA)` のアカウントの種類は使用しないでください。

- 通知が適切なグループ メール ボックスに送信されるように、通知の連絡先メール アドレスを設定します。

- 各アカウントに予算を割り当て、予算に関連するアラートを設定します。

- 組織は、職務、部門、地理、マトリックス、チーム構造など、さまざまな構造を持つことがあります。 組織構造を使用して、組織構造をエンタープライズ登録にマップします。

- 事業領域に独立した IT 機能がある場合は、IT の新しい部門を作成します。

- サブスクリプションおよび関連する Azure リソースに対する管理者アクセスの急増を防ぐために、登録内のアカウント所有者数を制限し、最小限に抑えます。

- 複数の Azure Active Directory (Azure AD) テナントが使用されている場合は、アカウント所有者が、アカウントのサブスクリプションがプロビジョニングされているものと同じテナントに関連付けられていることを確認します。

- 包括的な分離をサポートするために、EA アカウント レベルで Enterprise Dev/Test および運用環境を設定します。

- 通知アカウントのメール アドレスに送信された通知メールは無視しないでください。 Microsoft は、EA 全体にわたる重要な連絡をこのアカウントに送信します。

- Azure AD で EA アカウントの移動または名前変更を行わないでください。

- EA ポータルを定期的に監査し、アクセスできるユーザーを確認し、可能な限り Microsoft アカウントを使用しないようにします。

## <a name="define-azure-ad-tenants"></a>Azure AD テナントを定義する

Azure AD テナントによって ID とアクセス管理が提供されます。これはセキュリティ体制の重要な部分であり、認証および承認されたユーザーが、自身がアクセス許可を持つリソースのみにアクセスできるようにするものです。 Azure AD からは、Azure にデプロイされたアプリケーションやサービスだけでなく、Azure の外部にデプロイされたサービスやアプリケーション (オンプレミスやサードパーティのクラウド プロバイダーなど) にもこれらのサービスが提供されます。 Azure AD は、Microsoft 365 や Azure Marketplace などのサービスとしてのソフトウェア (SaaS) アプリケーションでも使用されます。 オンプレミスの Active Directory を既に使用している組織では、既存のインフラストラクチャを使用し、Azure AD と統合することで認証をクラウドに拡張できます。 各 Azure AD ディレクトリには 1 つ以上のドメインがあります。 ディレクトリには複数のサブスクリプションを関連付けることができますが、Azure AD テナントは 1 つだけです。

Azure AD の設計段階では、組織で資格情報を管理する方法や、人、アプリケーション、プログラムによるアクセスを制御する方法など、基本的なセキュリティの質問を確認することが重要です。

**設計上の考慮事項:**

- 1 つエンタープライズ登録で複数の Azure AD テナントを機能させることができます。

**設計上の推奨事項:**

- 選択した[計画トポロジ](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-topologies)に基づいて Azure AD のシームレスなシングル サインオンを使用します。

- 組織に ID インフラストラクチャがない場合は、まず Azure AD のみの ID デプロイを実装します。 [Azure AD Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services) と [Microsoft エンタープライズ モビリティ + セキュリティ](https://docs.microsoft.com/mem/intune/fundamentals/what-is-intune)を使用するこのようなデプロイによって、デバイスだけでなく SaaS とエンタープライズ アプリケーションのエンドツーエンドの保護を実現できます。

- 多要素認証を使用すると、セキュリティにもう 1 つの層を加え、認証の 2 つ目のバリアを提供することができます。 セキュリティを強化するために、すべての特権アカウントに[多要素認証](https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks)と[条件付きアクセス ポリシー](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)を適用します。

- テナント全体でアカウントがロックアウトされないように、[緊急アクセス用](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-emergency-access)または非常用のアカウントを計画して実装します。

- ID とアクセスの管理には、[Azure AD Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure) を使用します。

- 開発、テスト、運用が ID の観点から分離された環境になる場合は、複数のテナントを使用してテナント レベルでそれらを分離します。

- 強力な ID とアクセス管理の理由があり、プロセスが既に整っている場合を除き、新しい Azure AD テナントの作成は避けてください。