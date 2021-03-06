---
title: Azure に移行されたワークロードのネットワークの設定に関するベスト プラクティス
description: Azure 向けのクラウド導入フレームワークを使用し、移行されたワークロードのネットワークを設定するためのベスト プラクティスについて説明します。
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: deb75877c22c1e813c99b876da0d6aa8d64bd184
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94996249"
---
<!-- cSpell:ignore NSGs CIDR FQDNs BGP's ACLs WAFs -->

# <a name="best-practices-to-set-up-networking-for-workloads-migrated-to-azure"></a>Azure に移行されたワークロードのネットワークの設定に関するベスト プラクティス

移行を計画して設計するときは、移行自体に加えて、Azure ネットワークの設計と実装が最も重要なステップの 1 つです。 この記事では、Azure のサービスとしてのインフラストラクチャ (IaaS) およびサービスとしてのプラットフォーム (PaaS) の実装に移行するときのネットワークに関するベスト プラクティスについて説明します。

> [!IMPORTANT]
> この記事で説明するベスト プラクティスと考え方は、Azure プラットフォームと、記事の執筆時点で利用できるサービスの機能に基づいています。 特徴や機能は時間の経過と共に変化します。 お客様のデプロイにすべての推奨事項が当てはまるとは限らないため、お客様にとって適切なものを選択してください。

## <a name="design-virtual-networks"></a>仮想ネットワークを設計する

Azure では、次の機能を備えた仮想ネットワークが提供されます。

- Azure のリソースは、仮想ネットワークを通して相互に、セキュリティで保護された非公開の通信を直接行います。
- インターネット通信を必要とする VM およびサービスに対する仮想ネットワークにエンドポイント接続を構成することができます。
- 仮想ネットワークは、ご使用のサブスクリプション専用の Azure クラウドを論理的に分離したものです。
- 各 Azure サブスクリプションと Azure リージョン内に複数の仮想ネットワークを実装できます。
- 各仮想ネットワークは、他の仮想ネットワークから分離されています。
- 仮想ネットワークには、[RFC 1918](https://tools.ietf.org/html/rfc1918) で定義されている、CIDR 表記で表されたプライベート IP アドレスとパブリック IP アドレスを含めることができます。 仮想ネットワークのアドレス空間内に指定されたパブリック IP アドレスは、インターネットから直接アクセスすることはできません。
- 仮想ネットワークは、仮想ネットワーク ピアリングを使用して相互に接続できます。 接続される仮想ネットワークが配置されるリージョンは、同一でも異なっていてもかまいません。 したがって、ある仮想ネットワーク内のリソースは、他の仮想ネットワーク内のリソースに接続できます。
- Azure では、既定で、仮想ネットワーク内のサブネット、接続されている仮想ネットワーク、オンプレミス ネットワーク、インターネットの間でトラフィックがルーティングされます。

仮想ネットワーク トポロジを計画するときは、IP アドレス空間の配置方法、ハブ アンド スポーク ネットワーク トポロジの実装方法、仮想ネットワークをサブネットに分割する方法、DNS の設定、Azure Availability Zones の実装を検討する必要があります。

## <a name="best-practice-plan-ip-addressing"></a>ベスト プラクティス:IP アドレス指定を計画する

移行の一環として仮想ネットワークを作成するときは、仮想ネットワークの IP アドレス空間を計画することが重要です。

各仮想ネットワークに対して CIDR 範囲の `/16` より大きいアドレス空間を割り当てないようにする必要があります。 仮想ネットワークでは、65,536 個の IP アドレスを使用できます。 `/16` より小さいプレフィックス (131,072 個のアドレスを含む `/15` など) を割り当てると、余剰分の IP アドレスは他で使用できなくなります。 RFC 1918 で定義されているプライベート範囲内であっても、IP アドレスを無駄にしないことが重要です。

計画に関するその他のヒントは次のとおりです。

- 仮想ネットワーク アドレス空間は、オンプレミス ネットワークの範囲と重複しないようにする必要があります。
- アドレスが重複していると、ネットワークに接続できなくなったり、ルーティングが正常に動作しなくなったりする可能性があります。
- ネットワークが重複する場合は、ネットワークを設計し直す必要があります。
- ネットワークを設計し直すことがどうしてもできない場合は、ネットワーク アドレス変換 (NAT) が役に立ちます。 ただし、できるだけ避けるか制限するようにしてください。

**詳細情報:**

- [Azure Virtual Network の概要](/azure/virtual-network/virtual-networks-overview)を読む。
- [Azure Virtual Network に関する FAQ](/azure/virtual-network/virtual-networks-faq) を確認する。
- [Azure Stack ネットワーク](/azure/azure-resource-manager/management/azure-subscription-service-limits)についてご確認ください。

## <a name="best-practice-implement-a-hub-and-spoke-network-topology"></a>ベスト プラクティス:ハブ アンド スポーク ネットワーク トポロジを実装する

ハブ アンド スポーク ネットワーク トポロジでは、ID やセキュリティなどのサービスを共有しながら、ワークロードを分離します。 ハブは、接続の中心点として機能する Azure 仮想ネットワークです。 スポークは、ピアリングを使用してハブ仮想ネットワークに接続する仮想ネットワークです。 共有サービスはハブにデプロイされ、個々のワークロードはスポークとしてデプロイされます。

以下、具体例に沿って説明します。

- ハブ アンド スポーク トポロジを Azure に実装すると、オンプレミス ネットワークへの接続、ファイアウォール、仮想ネットワーク間の分離などの共通サービスが一元化されます。 ハブ仮想ネットワークでは、オンプレミス ネットワークへの接続の中心点と、スポーク仮想ネットワークでホストされているワークロードによって使用されるサービスをホストするための場所が提供されます。
- ハブスポーク構成は、通常、大企業で使用されます。 小規模なネットワークでは、もっと単純な設計にしてコストと複雑さを軽減することを検討してください。
- スポーク仮想ネットワークを使用すると、ワークロードを分離し、各スポークを他のスポークから切り離して管理できます。 各ワークロードには、複数の階層と、Azure ロード バランサーで接続された複数のサブネットを含めることができます。
- ハブとスポークの仮想ネットワークは異なるリソース グループに実装でき、異なるサブスクリプションに実装することもできます。 異なるサブスクリプションに属する仮想ネットワークをピアリングする場合、サブスクリプションを同じまたは異なる Azure Active Directory (Azure AD) テナントに関連付けることができます。 これにより、各ワークロードを分散管理しながら、ハブ ネットワークで維持されているサービスを共有できます。

![ハブ アンド スポーク トポロジの図](./media/migrate-best-practices-networking/hub-spoke.png)
_図 1: ハブ アンド スポーク トポロジ。_

**詳細情報:**

- [ハブとスポークのトポロジ](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)について読む。
- Azure で [Windows VM](/azure/architecture/reference-architectures/n-tier/windows-vm) と [Linux VM](/azure/architecture/reference-architectures/n-tier/linux-vm) を実行するためのネットワークの推奨事項を確認する。
- [仮想ネットワーク ピアリング](/azure/virtual-network/virtual-network-peering-overview)について学習する。

## <a name="best-practice-design-subnets"></a>ベスト プラクティス:サブネットを設計する

仮想ネットワーク内で分離を実現するには、仮想ネットワークを 1 つ以上のサブネットに分割し、各サブネットに仮想ネットワークのアドレス空間の一部を割り当てます。

- 各仮想ネットワーク内には複数のサブネットを作成することができます。
- 既定では、Azure は仮想ネットワーク内のすべてのサブネット間でネットワーク トラフィックをルーティングします。
- サブネットの決定は、技術的要件と組織的要件に基づきます。
- サブネットを作成するには CIDR 表記を使用します。

サブネットのネットワーク範囲を決めるときは、各サブネットの 5 個の IP アドレスは Azure によって確保されており、使用できないということに注意してください。 たとえば、使用可能な最小のサブネットである `/29` (8 個の IP アドレス) を作成する場合、Azure によって 5 個のアドレスが確保されます。 この場合、サブネット上のホストに割り当てることができる使用可能なアドレスは 3 個だけです。 ほとんどの場合、最小のサブネットとして `/28` を使用します。

**例:**

この表では、計画的な移行のためにアドレス空間 `10.245.16.0/20` をサブネットに分割した仮想ネットワークの例を示します。

| Subnet | CIDR | アドレス | 使用法 |
| --- | --- | --- | --- |
| `DEV-FE-EUS2` | `10.245.16.0/22` | 1019 | フロントエンドまたは Web 層の VM |
| `DEV-APP-EUS2` | `10.245.20.0/22` | 1019 | アプリケーション層の VM |
| `DEV-DB-EUS2` | `10.245.24.0/23` | 507 | データベース VM |

**詳細情報:**

- [サブネットの設計](/azure/virtual-network/virtual-network-vnet-plan-design-arm#segmentation)について学習する。
- 架空の会社の Contoso が[移行用に自社のネットワーク インフラストラクチャを準備した](/azure/migrate/contoso-migration-infrastructure)方法を学習する。

## <a name="best-practice-set-up-a-dns-server"></a>ベスト プラクティス:DNS サーバーをセットアップする

仮想ネットワークをデプロイすると、Azure によって既定で DNS サーバーが追加されます。 これにより、仮想ネットワークを迅速に構築してリソースをデプロイできます。 ただし、この DNS サーバーでは、その仮想ネットワーク上のリソースに対してのみサービスが提供されます。 複数の仮想ネットワークを接続する場合、または仮想ネットワークからオンプレミス サーバーに接続する場合は、追加の名前解決機能が必要です。 たとえば、仮想ネットワーク間で DNS 名を解決するには、Active Directory が必要になる場合があります。 これを行うには、Azure に独自のカスタム DNS サーバーをデプロイします。

- 仮想ネットワーク内の DNS サーバーは、Azure の再帰的リゾルバーに DNS クエリを転送できます。 これにより、その仮想ネットワーク内のホスト名を解決することができます。 たとえば、Azure で実行しているドメイン コントローラーでは、それ自体のドメインに対する DNS クエリに応答し、他のすべてのクエリを Azure に転送できます。
- DNS 転送により、VM ではオンプレミスのリソース (ドメイン コントローラー経由) と Azure で提供されるホスト名 (フォワーダー使用) の両方を参照できます。 仮想 IP アドレス `168.63.129.16` を使用して、Azure の再帰的リゾルバーにアクセスできます。
- また、DNS 転送により、仮想ネットワーク間の DNS 解決も可能になり、オンプレミスのマシンで Azure によって提供されるホスト名を解決できるようになります。
  - VM のホスト名を解決するために、DNS サーバー VM は、同じ仮想ネットワークに存在し、Azure にホスト名のクエリを転送するように構成されている必要があります。
  - DNS サフィックスは仮想ネットワークごとに異なるため、条件付きの転送ルールを使用し、解決のために正しい仮想ネットワークに DNS クエリを送信します。
- 独自の DNS サーバーを使用する場合は、仮想ネットワークごとに複数の DNS サーバーを指定できます。 また、ネットワーク インターフェイス (Azure Resource Manager の場合) またはクラウド サービス (クラシック デプロイ モデルの場合) ごとに複数の DNS サーバーを指定することもできます。
- ネットワーク インターフェイスまたはクラウド サービスに対して指定された DNS サーバーは、仮想ネットワークに対して指定された DNS サーバーよりも優先されます。
- Azure Resource Manager では、仮想ネットワークとネットワーク インターフェイスに対して DNS サーバーを指定できますが、仮想ネットワークでのみ設定を使用するのがベスト プラクティスです。

    ![仮想ネットワークの DNS サーバーのスクリーンショット。](./media/migrate-best-practices-networking/dns2.png)
    "_図 2:仮想ネットワークの DNS サーバー。_ "

**詳細情報:**

- [独自の DNS サーバーを使用するときの名前解決](/azure/migrate/contoso-migration-infrastructure)について学習する。
- [DNS の名前付け規則と制限事項](../../ready/azure-best-practices/naming-and-tagging.md)について学習する。

## <a name="best-practice-set-up-availability-zones"></a>ベスト プラクティス:Availability Zones を設定する

Availability Zones により、高可用性が向上し、アプリケーションとデータがデータセンターの障害から保護されます。 Availability Zones は、Azure リージョン内の一意の物理的な場所です。 それぞれのゾーンは、独立した電源、冷却手段、ネットワークを備えた 1 つまたは複数のデータセンターで構成されています。 回復性を確保するため、有効になっているリージョンにはいずれも最低 3 つのゾーンが別個に存在しています。 Availability Zones は 1 リージョン内で物理的に分離されているため、データセンターで障害が発生した場合でもアプリケーションとデータを保護できます。

Availability Zones を設定する際に注意する必要があるいくつかの追加の点を次に示します。

- ゾーン冗長サービスによってアプリケーションとデータが Availability Zones 全体にレプリケートされ、単一障害点から保護されます。

- Availability Zones を使用することで、Azure による 99.99% VM アップタイムの SLA が実現されます。

    ![Azure リージョン内の Availability Zones の図。](./media/migrate-best-practices-networking/availability-zone.png)

    "_図 3:Availability Zones。_ "

- コンピューティング、ストレージ、ネットワーク、およびデータ リソースを 1 つのゾーン内に併置し、他のゾーンにレプリケートすることによって、高可用性を計画し、移行アーキテクチャに組み込むことができます。 Availability Zones をサポートしている Azure サービスは、次の 2 つのカテゴリに分類されます。
  - **ゾーン ベース サービス:** リソースは、VM、マネージド ディスク、IP アドレスなどの特定のゾーンに関連付けます。
  - **ゾーン冗長サービス:** リソースは、ゾーン冗長ストレージや Azure SQL Database などのゾーン間で自動的にレプリケートされます。
- ゾーン ベースのフォールト トレランスを提供するために、インターネットに接続されたワークロードまたはアプリケーション層を備えた標準の Azure Load Balancer インスタンスをデプロイできます。

    ![標準のロード バランサーの図](./media/migrate-best-practices-networking/load-balancer.png)"_図 4: ロード バランサー。_ "

**詳細情報:**

- [Availability Zones の概要](/azure/availability-zones/az-overview)を読む。

## <a name="design-hybrid-cloud-networking"></a>ハイブリッド クラウド ネットワークを設計する

移行を成功させるには、オンプレミスの企業ネットワークを Azure に接続することが重要です。 これによりハイブリッド クラウド ネットワークと呼ばれる常時接続が作成されて、Azure クラウドから企業ユーザーにサービスが提供されます。 この種のネットワークを作成するには 2 つのオプションがあります。

- **サイト間 VPN:** 互換性のあるオンプレミスの VPN デバイスと、仮想ネットワークにデプロイされた Azure VPN Gateway の間に、サイト間 VPN 接続を確立します。 承認されたオンプレミスのリソースはすべて、仮想ネットワークにアクセスできます。 サイト間通信は、インターネット経由で暗号化されたトンネルを通して送信されます。
- **Azure ExpressRoute:** ExpressRoute パートナーを介して、オンプレミス ネットワークと Azure の間に、Azure ExpressRoute 接続を確立します。 この接続は非公開であり、トラフィックはインターネットを経由しません。

**詳細情報:**

- [ハイブリッド クラウド ネットワーク](/azure/architecture/reference-architectures/hybrid-networking/vpn)の詳細を確認する。

## <a name="best-practice-implement-a-highly-available-site-to-site-vpn"></a>ベスト プラクティス:高可用性のサイト間 VPN を実装する

サイト間 VPN を実装するには、Azure で VPN ゲートウェイを設定します。

- VPN ゲートウェイは仮想ネットワーク ゲートウェイの特定の種類です。 Azure 仮想ネットワークとオンプレミスの場所の間で、パブリック インターネットを介して暗号化されたトラフィックを送信します。
- VPN ゲートウェイでは、Microsoft ネットワークを介して Azure の仮想ネットワーク間で暗号化されたトラフィックを送信することもできます。
- 各仮想ネットワークには VPN ゲートウェイを 1 つだけ作成できます。
- 同じ VPN ゲートウェイに対して複数の接続を作成することができます。 複数の接続を作成すると、利用できるゲートウェイ帯域幅がすべての VPN トンネルによって共有されます。

すべての Azure VPN ゲートウェイは、アクティブ/スタンバイ構成の 2 つのインスタンスから成ります。

- アクティブなインスタンスに対して計画メンテナンスまたは計画外の中断が発生すると、フェールオーバーが実施され、スタンバイ インスタンスへの引き継ぎが自動的に行われます。 このインスタンスにより、サイト間接続またはネットワーク間接続が再開されます。
- 切り替えでは、短い中断が発生します。
- 計画メンテナンスの場合は、10 ～ 15 秒以内に接続が復元されます。
- 予期しない問題の場合は、接続の復旧にかかる時間は長くなり、最悪の場合は最大で 1 分 30 秒かかります。
- ゲートウェイへのポイント対サイト VPN クライアント接続が切断され、ユーザーはクライアント マシンから再接続する必要があります。

サイト間 VPN を設定する場合:

- VPN が接続するオンプレミス ネットワークとアドレス範囲が重複していない仮想ネットワークが必要です。
- ネットワーク内にゲートウェイ サブネットを作成します。
- VPN ゲートウェイを作成し、ゲートウェイの種類 (VPN) と、ゲートウェイがポリシーベースかルートベースかを指定します。 ルート ベースの VPN は、機能が豊富で将来も対応できると考えられます。
- オンプレミスにローカル ネットワーク ゲートウェイを作成し、オンプレミスの VPN デバイスを構成します。
- 仮想ネットワーク ゲートウェイとオンプレミス デバイスの間に、フェールオーバー サイト間 VPN 接続を作成します。 ルート ベースの VPN を使用すると、Azure に対してアクティブ/パッシブ接続またはアクティブ/アクティブ接続できます。 また、ルートベースのオプションでは、(任意のコンピューターからの) サイト間接続と (1 台のコンピューターからの) ポイント対サイト接続の両方が同時にサポートされます。
- 使用するゲートウェイ SKU を指定します。 これは、ワークロードの要件、スループット、機能、および SLA に依存します。
- ボーダー ゲートウェイ プロトコル (BGP) はオプション機能です。 これを Azure ExpressRoute とルートベースの VPN ゲートウェイで使用して、対象のオンプレミス BGP ルートを仮想ネットワークに伝達できます。

![サイト間 VPN の図](./media/migrate-best-practices-networking/vpn.png)
"_図 5: サイト間 VPN。_ "

**詳細情報:**

- [互換性のあるオンプレミス VPN デバイス](/azure/vpn-gateway/vpn-gateway-about-vpn-devices)を確認する。
- [Azure VPN ゲートウェイの概要](/azure/vpn-gateway/vpn-gateway-about-vpngateways)を読む。
- [高可用性 VPN 接続](/azure/vpn-gateway/vpn-gateway-highlyavailable)について学習する。
- [VPN ゲートウェイの計画と設計](/azure/vpn-gateway/vpn-gateway-plan-design)について学習する。
- [VPN ゲートウェイの設定](/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsku)を確認する。
- [ゲートウェイの SKU](/azure/vpn-gateway/vpn-gateway-about-vpngateways#gwsku) を確認する。
- [Azure VPN ゲートウェイでの BGP の設定](/azure/vpn-gateway/vpn-gateway-bgp-overview)について読む。

### <a name="best-practice-configure-a-gateway-for-vpn-gateways"></a>ベスト プラクティス:VPN ゲートウェイ用にゲートウェイを構成する

Azure で VPN ゲートウェイを作成するときは、`GatewaySubnet` という名前の特別なサブネットを使用する必要があります。 このサブネットを作成するときは、これらのベスト プラクティスに注意してください。

- `GatewaySubnet` のプレフィックスの最大長は 29 (例: `10.119.255.248/29`) です。 現在の推奨事項は、27 (例: `10.119.255.224/27`) のプレフィックス長を使用することです。
- ゲートウェイ サブネットのアドレス空間を定義するときは、仮想ネットワーク アドレス空間の最後の部分を使用します。
- Azure ゲートウェイ サブネットを使用するときは、VM または Azure Application Gateway などの他のデバイスをゲートウェイ サブネットにデプロイしないでください。
- このサブネットにはネットワーク セキュリティ グループ (NSG) を割り当てないでください。 ゲートウェイが機能を停止する原因になります。

**詳細情報:**

- [このツールを使用](https://gallery.technet.microsoft.com/scriptcenter/Address-prefix-calculator-a94b6eed)して IP アドレス空間を決定する。

## <a name="best-practice-implement-azure-virtual-wan-for-branch-offices"></a>ベスト プラクティス:ブランチ オフィス用に Azure Virtual WAN を実装する

複数の VPN 接続がある場合、Azure Virtual WAN は、Azure を介して最適化および自動化されたブランチ間接続を提供するネットワーク サービスです。

- Virtual WAN を使用すると、ブランチ デバイスへの接続と構成を行って Azure と通信できます。 これは、手動で行うことも、Azure Virtual WAN パートナーを介して好みのプロバイダー デバイスを使用して行うこともできます。
- 推奨プロバイダー デバイスを使用すると、使いやすさ、接続性、および構成管理を実現できます。
- Azure Virtual WAN の組み込みダッシュボードにはすぐに使用できるトラブルシューティング用分析情報が用意されているため、時間を節約でき、大規模なサイト間接続を簡単に追跡できます。

**詳細情報:** [Azure Virtual WAN](/azure/virtual-wan/virtual-wan-about) について学習する。

### <a name="best-practice-implement-expressroute-for-mission-critical-connections"></a>ベスト プラクティス:ミッション クリティカルな接続用に ExpressRoute を実装する

Azure ExpressRoute サービスでは、仮想 Azure データセンターとオンプレミス ネットワークの間にプライベート接続を作成することで、お使いのオンプレミスのインフラストラクチャが Microsoft クラウドに拡張されます。 実装の詳細をいくつか次に示します。

- ExpressRoute 接続では、任意の環境間 (IP VPN) のネットワーク、ポイント ツー ポイント イーサネット ネットワーク、または接続プロバイダーを使用できます。 パブリック インターネットは経由しません。
- ExpressRoute 接続では、強固なセキュリティ、信頼性、高い速度 (最大 10 Gbps)、および一貫した待機時間が提供されます。
- ExpressRoute では、ユーザーはプライベート接続に関連付けられたコンプライアンス規則のベネフィットを得られるので、仮想データセンターに適しています。
- より広い帯域幅が必要な場合は、ExpressRoute Direct を使用すると、100 Gbps で Microsoft ルーターに直接接続することができます。
- ExpressRoute では、BGP を使用して、オンプレミス ネットワーク、Azure インスタンス、Microsoft パブリック アドレスの間でルートが交換されます。

通常、ExpressRoute 接続のデプロイでは、ExpressRoute サービス プロバイダーと連携する必要があります。 迅速に開始するために、最初にサイト間 VPN を使用して、仮想データセンターとオンプレミスのリソースの間で接続を確立するのが一般的です。 次に、サービス プロバイダーとの物理的な相互接続が確立されたら、ExpressRoute 接続に移行します。

**詳細情報:**

- ExpressRoute の[概要](/azure/expressroute/expressroute-introduction)を読む。
- [ExpressRoute Direct](/azure/expressroute/expressroute-erdirect-about) について学習する。

### <a name="best-practice-optimize-expressroute-routing-with-bgp-communities"></a>ベスト プラクティス:BGP コミュニティで ExpressRoute のルーティングを最適化する

ExpressRoute 回線が複数あるとき、Microsoft への接続経路は複数存在します。 その結果、ルーティングが最適ではなくなり、ユーザーのネットワークから Microsoft へのトラフィックのパスと、Microsoft からユーザーのネットワークへのパスが長くなる可能性があります。 ネットワーク パスが長くなるほど、遅延は大きくなります。 待ち時間は、アプリケーションのパフォーマンスとユーザー エクスペリエンスに直接影響します。

**例:**

例を見てみましょう。

- 米国のロサンゼルスとニューヨーク市にそれぞれ 1 つオフィスがあります。
- オフィスは WAN で接続されています。WAN は、自社のバックボーン ネットワークでも、サービス プロバイダーの IP VPN でもかまいません。
- また ExpressRoute 回線が 2 つ存在します。1 つは `West US` に、もう 1 つは `East US` にあり、それらも WAN に接続されています。 オフィスから Microsoft のネットワークには、明らかに 2 とおりの接続経路があります。

**問題**:

ここで、`West US` と `East US` の両方に Azure のデプロイ (Azure App Service など) があるとします。

- 最適なエクスペリエンスのため、各オフィスのユーザーが最も近い Azure サービスにアクセスできるようにしたいと思います。
- そのため、ロサンゼルスのユーザーは Azure `West US` に接続し、ニューヨークのユーザーは Azure `East US` に接続するようにします。
- これは、東海岸のユーザーに対しては機能しますが、西海岸のユーザーには機能しません。 問題点:
  - 各 ExpressRoute 回線では、Azure `East US` (`23.100.0.0/16`) と Azure `West US` (`13.100.0.0/16`) 両方のプレフィックスがアドバタイズされています。
  - どのプレフィックスがどのリージョンからのものかがわからないと、プレフィックスの処理を変えることができません。
  - WAN ネットワークでは、両方のプレフィックスが `West US` より `East US` に近いものと見なすことができるため、両方のオフィスのユーザーが `East US` の ExpressRoute 回線にルーティングされます。 これにより、ロサンゼルス オフィスのユーザーのエクスペリエンスが悪くなります。

![間違った回線を経由するルート パスが設定された VPN の図](./media/migrate-best-practices-networking/bgp1.png)
"_図 6: BGP コミュニティの最適化されていない接続。_ "

**解決方法:**

両方のオフィスに対するルーティングを最適化するには、どちらのプレフィックスが Azure `West US` からのもので、どちらが Azure `East US` からのものかを知る必要があります。 この情報は、BGP コミュニティ値を使用してコード化できます。

- 各 Azure リージョンに一意の BGP コミュニティ値を割り当てます。 たとえば、`East US` は 12076:51004、`West US` は 12076:51006 のように割り当てます。
- このようにすると、どのプレフィックスがどの Azure リージョンに属しているかが明確になり、優先 ExpressRoute 回線を構成できます。
- BGP を使用してルーティング情報を交換しているので、BGP のローカル優先設定を使用してルーティングを制御できます。
- この例では、`West US` で `13.100.0.0/16` に割り当てるローカル設定の値を `East US` よりも大きくします。 同様に、`East US` で `23.100.0.0/16` に割り当てるローカル設定の値を `West US` よりも大きくします。
- この構成により、Microsoft に対して両方のパスを使用できる場合、ロサンゼルスのユーザーは西部の回線を使用して `West US` リージョンに接続し、ニューヨークのユーザーは東部の回線を使用して `East US` リージョンに接続します。

![正しい回線を経由するルート パスが設定された VPN の図](./media/migrate-best-practices-networking/bgp2.png)
"_図 7: BGP コミュニティの最適化された接続。_ "

**詳細情報:**

- [ルーティングの最適化](/azure/expressroute/expressroute-optimize-routing)について学習する。

## <a name="secure-virtual-networks"></a>仮想ネットワークをセキュリティで保護する

仮想ネットワークをセキュリティ保護する責任は、Microsoft とユーザーの両方にあります。 Microsoft では、多くのネットワークの機能だけでなく、リソースの安全性を確保するサービスが提供されています。 仮想ネットワークのセキュリティを設計する場合は、境界ネットワークを実装すること、フィルター処理とセキュリティ グループを使用すること、リソースと IP アドレスへのアクセスをセキュリティで保護すること、および攻撃に対する保護を実装することをお勧めします。

**詳細情報:**

- [ネットワーク セキュリティのベスト プラクティスの概要](/azure/security/fundamentals/network-best-practices)を読む。
- [セキュリティで保護されたネットワークを設計する](/azure/virtual-network/virtual-network-vnet-plan-design-arm#security)方法を学習する。

<!-- docutune:casing "IDS/IPS" -->

## <a name="best-practice-implement-an-azure-perimeter-network"></a>ベスト プラクティス:Azure 境界ネットワークを実装する

Microsoft は、クラウド インフラストラクチャの保護に多額の投資を行っていますが、ユーザーも自身のクラウド サービスとリソース グループを保護する必要があります。 セキュリティの多層アプローチにより、最大限の保護が実現されます。 境界ネットワークを設けることは、その防御戦略の重要な部分です。

- 境界ネットワークでは、内部のネットワーク リソースが信頼されていないネットワークから保護されます。
- インターネットに公開される最も外側の層になります。 一般にインターネットとエンタープライズ インフラストラクチャの間に配置され、通常は両方の側で何らかの保護が行われます。
- 一般的なエンタープライズ ネットワーク トポロジでは、コア インフラストラクチャは複数層のセキュリティ デバイスを備えた境界で厳重に防備されています。 各層の境界は、デバイスとポリシー適用ポイントで構成されます。
- 各層には、ファイアウォール、サービス拒否 (DoS) 防止、侵入検出または侵入防止システム (IDS または IPS)、VPN デバイスなどのネットワーク セキュリティ ソリューションを組み合わせたものを含めることができます。
- 境界ネットワークでのポリシーの適用では、ファイアウォール ポリシー、アクセス制御リスト (ACL)、または特定のルーティングを使用できます。
- 受信トラフィックは、インターネットから到着すると、防御ソリューションの組み合わせによってインターセプトされて処理されます。 このソリューションでは、正当な要求はネットワークに入るのを許可されますが、攻撃や有害なトラフィックはブロックされます。
- 受信トラフィックは、境界ネットワーク内のリソースに直接ルーティングできます。 境界ネットワークのリソースでは、ネットワークのより深い場所にある他のリソースと通信し、検証後にトラフィックをネットワークに転送できます。

2 つのセキュリティ境界がある企業ネットワークにおける単一のサブネット境界ネットワークの例を次に示します。

![Azure Virtual Network 境界ネットワークのデプロイの図。](./media/migrate-best-practices-networking/perimeter.png)
"_図 8: 境界ネットワークのデプロイ。_ "

**詳細情報:**

- [Azure とオンプレミス データセンターの間への境界ネットワークをデプロイする](/azure/architecture/reference-architectures/dmz/secure-vnet-dmz)方法をご覧ください。

## <a name="best-practice-filter-virtual-network-traffic-with-nsgs"></a>ベスト プラクティス:NSG を使用して仮想ネットワーク トラフィックをフィルター処理する

ネットワーク セキュリティ グループ (NSG) には、リソースとの間でやり取りされるトラフィックをフィルター処理する複数の受信および送信セキュリティ規則が含まれます。 フィルター処理は、送信元と宛先の IP アドレス、ポート、およびプロトコルで行うことができます。

- NSG には、何種類かの Azure リソースへの受信ネットワーク トラフィック (またはリソースからの送信ネットワーク トラフィック) を許可または拒否するセキュリティ規則が含まれます。 各規則で、送信元と送信先、ポート、およびプロトコルを指定することができます。
- 5 タプル情報 (送信元、送信元ポート、宛先、宛先ポート、プロトコル) を使用して、優先度に従って NSG 規則が評価されて、トラフィックが許可または拒否されます。
- 既存の接続に対するフロー レコードが作成されます。 そのフロー レコードの接続の状態に基づいて、通信が許可または拒否されます。
- フロー レコードにより NSG はステートフルになることができます。 たとえば、ポート 80 経由の任意のアドレスに対する送信セキュリティ規則を指定する場合、送信トラフィックへの応答に対する受信セキュリティ規則は必要はありません。 通信が外部から開始された場合は、受信セキュリティ規則のみを指定する必要があります。
- 反対の場合も同じです。 ポートで受信トラフィックが許可されている場合、そのポートでのトラフィックに応答するために、送信セキュリティ規則を指定する必要はありません。
- フローを有効にしたセキュリティ規則を削除したとき、既存の接続は中断されません。 接続が停止されるとトラフィック フローは中断され、少なくとも数分間は、どちらの方向にもトラフィックが流れません。
- NSG を作成するときは、必要最小限の数だけ作成します。

### <a name="best-practice-secure-northsouth-and-eastwest-traffic"></a>ベスト プラクティス:North/South および East/West トラフィックをセキュリティ保護する

仮想ネットワークをセキュリティで保護するには、攻撃ベクトルを考慮します。 以下の点に注意してください。

- サブネットの NSG のみを使用すると環境は簡素化されますが、セキュリティ保護されるのはサブネットに入ってくるトラフィックだけです。 これは North/South トラフィックと呼ばれます。
- 同じサブネット上の VM 間のトラフィックは、East/West トラフィックと呼ばれます。
- 両方の保護の形式を利用して、外部からアクセスするハッカーが同じサブネット内に存在するマシンを攻撃しようとしても阻止されるようにすることが重要です。

### <a name="use-service-tags-on-nsgs"></a>NSG でサービス タグを使用する

サービス タグは、IP アドレスのプレフィックスのグループを表します。 サービス タグを使用すると、NSG ルールを作成するときの複雑さを軽減できます。

- 規則を作成するときは、特定の IP アドレスの代わりにサービス タグを使用できます。
- サービス タグに関連付けられているアドレス プレフィックスの管理は Microsoft が行い、アドレスが変化するとサービス タグは自動的に更新されます。
- 独自のサービス タグを作成したり、タグに含まれる IP アドレスを指定したりすることはできません。

サービス タグを使用すると、Azure サービスのグループに規則を割り当てるときの手作業がなくなります。 たとえば、Web サーバーが含まれるサブネットに Azure SQL Database へのアクセスを許可する場合は、ポート 1433 に対するアウトバウンド規則を作成して、**Sql** サービス タグを使用できます。

- この **Sql** タグは、Azure SQL Database サービスおよび Azure SQL Data Warehouse サービスのアドレス プレフィックスを表します。
- 値として **Sql** を指定した場合、SQL へのトラフィックが許可または拒否されます。
- 特定のリージョンの **Sql** へのアクセスのみを許可する場合は、そのリージョンを指定することができます。 たとえば、米国東部リージョンの Azure SQL Database へのアクセスのみを許可する場合は、サービス タグに **Sql.EastUS** と指定できます。
- タグはサービスだけを表し、サービスの特定のインスタンスは表しません。 たとえば、タグは Azure SQL Database サービスを表しますが、特定の SQL データベースやサーバーは表しません。
- このタグで表されるすべてのアドレス プレフィックスは、**Internet** タグでも表されます。

**詳細情報:**

- [ネットワーク セキュリティ グループ (NSG)](/azure/virtual-network/security-overview) の概要を読む。
- [NSG に使用可能なサービス タグ](/azure/virtual-network/security-overview#service-tags)を確認する。

## <a name="best-practice-use-application-security-groups"></a>ベスト プラクティス:アプリケーション セキュリティ グループを使用する

アプリケーション セキュリティ グループを使用すると、アプリケーションの構造の自然な拡張として、ネットワーク セキュリティを構成できます。

- アプリケーション セキュリティ グループに基づいて、VM をグループ化し、ネットワーク セキュリティ ポリシーを定義できます。
- アプリケーション セキュリティ グループでは、明示的な IP アドレスを手動でメンテナンスすることなく、セキュリティ ポリシーを大規模に再利用することができます。
- アプリケーション セキュリティ グループによって明示的な IP アドレスと複数の規則セットの複雑さが処理されるので、ユーザーはビジネス ロジックに専念することができます。

**例:**

![アプリケーション セキュリティ グループの図](./media/migrate-best-practices-networking/asg.png)
"_図 9: アプリケーション セキュリティ グループの例。_ "

| ネットワーク インターフェイス | アプリケーション セキュリティ グループ |
| --- | --- |
| `NIC1` | `AsgWeb` |
| `NIC2` | `AsgWeb` |
| `NIC3` | `AsgLogic` |
| `NIC4` | `AsgDb` |

この例の各ネットワーク インターフェイスは 1 つのアプリケーション セキュリティ グループだけに属していますが、実際には、Azure の制限に従って、1 つのインターフェイスが複数のグループに属することができます。 NSG に関連付けられているネットワーク インターフェイスはありません。 `NSG1` は両方のサブネットに関連付けられており、次の規則を含んでいます。

| 規則の名前 | 目的 | 詳細 |
| --- | --- | --- |
| `Allow-HTTP-Inbound-Internet` | インターネットから Web サーバーへのトラフィックを許可します。 インターネットからの受信トラフィックは `DenyAllInbound` 既定セキュリティ規則によって拒否されるので、`AsgLogic` または `AsgDb` アプリケーション セキュリティ グループでは追加の規則は必要ありません。 | 優先度: `100`<br><br> ソース: `internet` <br><br> 送信元ポート: `*` <br><br> 宛先: `AsgWeb` <br><br> 宛先ポート: `80` <br><br> プロトコル: `TCP` <br><br> アクセス: `Allow` |
| `Deny-Database-All` | `AllowVNetInBound` デフォルト セキュリティ規則では、同じ仮想ネットワーク内にあるリソース間の通信がすべて許可されます。 この規則は、すべてのリソースからのトラフィックを拒否するために必要です。 | 優先度: `120` <br><br> ソース: `*` <br><br> 送信元ポート: `*` <br><br> 宛先: `AsgDb` <br><br> 宛先ポート: `1433` <br><br> プロトコル: `All` <br><br> アクセス: `Deny` |
| `Allow-Database-BusinessLogic` | `AsgLogic` アプリケーション セキュリティ グループから `AsgDb` アプリケーション セキュリティ グループへのトラフィックを許可します。 この規則の優先度は、`Deny-Database-All` 規則より高いため、この規則が最初に処理されます。 そのため、`AsgLogic` アプリケーション セキュリティ グループからのトラフィックは許可され、他のすべてのトラフィックはブロックされます。 | 優先度: `110` <br><br> ソース: `AsgLogic` <br><br> 送信元ポート: `*` <br><br> 宛先: `AsgDb` <br><br> 宛先ポート: `1433` <br><br> プロトコル: `TCP` <br><br> アクセス: `Allow` |

アプリケーション セキュリティ グループを送信元または送信先として指定されている規則は、アプリケーション セキュリティ グループのメンバーであるネットワーク インターフェイスにのみ適用されます。 ネットワーク インターフェイスがアプリケーション セキュリティ グループのメンバーでない場合、ネットワーク セキュリティ グループがサブネットに関連付けられていても、規則はネットワーク インターフェイスに適用されません。

**詳細情報:**

- [アプリケーション セキュリティ グループ](/azure/virtual-network/security-overview#application-security-groups)について学習する。

### <a name="best-practice-secure-access-to-paas-by-using-virtual-network-service-endpoints"></a>ベスト プラクティス:仮想ネットワーク サービス エンドポイントを使用して PaaS へのアクセスをセキュリティで保護する

仮想ネットワーク サービス エンドポイントにより、対象の仮想ネットワークの非公開アドレス空間と ID が、直接接続によって Azure サービスに拡張されます。

- エンドポイントを使用することで、アクセスを仮想ネットワークのみに限定して重要な Azure サービス リソースを保護できます。 仮想ネットワークから Azure サービスへのトラフィックは常に、Azure のバックボーン ネットワーク上に残ります。
- 仮想ネットワークの非公開アドレス空間は重複することがあるため、仮想ネットワークからのトラフィックを一意に識別するためには使用できません。
- 対象の仮想ネットワークでサービス エンドポイントを有効にした後は、Azure サービス リソースに仮想ネットワーク規則を追加することで、このサービス リソースをセキュリティで保護できます。 こうして、リソースへのパブリック インターネット アクセスを完全に排除し、仮想ネットワークからのトラフィックのみを許可することにより、セキュリティが強化されます。

![サービス エンドポイントの図。](./media/migrate-best-practices-networking/endpoint.png)
"_図 10: サービス エンドポイント。_ "

**詳細情報:**

- [仮想ネットワーク サービス エンドポイント](/azure/virtual-network/virtual-network-service-endpoints-overview)について学習する。

## <a name="best-practice-control-public-ip-addresses"></a>ベスト プラクティス:パブリック IP アドレスを管理する

Azure 内のパブリック IP アドレスは、VM、ロード バランサー、アプリケーション ゲートウェイ、VPN ゲートウェイと関連付けることができます。

- パブリック IP アドレスを使用すると、インターネット リソースから Azure リソースへの受信通信を許可したり、Azure リソースからインターネットへの送信通信を許可したりすることができます。
- パブリック IP アドレスは Basic SKU または Standard SKU で作成されますが、それらの間にはいくつかの相違点があります。 Standard SKU は任意のサービスに割り当てることができますが、通常は、VM、ロード バランサー、およびアプリケーション ゲートウェイで構成されます。
- Basic パブリック IP アドレスには NSG が自動的に構成されないことに注意することが重要です。 自分で構成して、アクセスを制御する規則を割り当てる必要があります。 Standard SKU の IP アドレスでは、既定で NSG が作成されて、規則が割り当てられます。
- ベスト プラクティスとしては、VM ではパブリック IP アドレスを構成しないようにする必要があります。
  - ポートを開く必要がある場合は、ポート 80 や 443 など、Web サービスに対するものだけにする必要があります。
  - SSH (22) や RDP (3389) などの標準のリモート管理ポートは、他のすべてのポートと共に、NSG を使用して拒否に設定する必要があります。
- Azure Load Balancer または Azure Application Gateway の後方に VM を配置するのがよい方法です。 その後、リモート管理ポートへのアクセスが必要な場合は、Azure Security Center で Just-In-Time VM アクセスを使用できます。

**詳細情報:**

- [Azure でのパブリック IP アドレス](/azure/virtual-network/virtual-network-ip-addresses-overview-arm#public-ip-addresses)
- [Just-In-Time を使用した仮想マシン アクセスの管理](/azure/security-center/security-center-just-in-time)

## <a name="take-advantage-of-azure-security-features-for-networking"></a>Azure のネットワークに対するセキュリティ機能を利用する

Azure には、Azure Firewall、Web Application Firewall、Network Watcher などの、プラットフォームレベルのセキュリティ機能があります。

## <a name="best-practice-deploy-azure-firewall"></a>ベスト プラクティス:Azure Firewall をデプロイする

Azure Firewall は、お使いの仮想ネットワーク リソースを保護するのに役立つ、クラウドベースのマネージド ネットワーク セキュリティ サービスです。 これは、組み込みの高可用性とクラウドによる無制限のスケーラビリティを備えた、完全にステートフルなマネージド ファイアウォールです。

![Azure Firewall の図。](./media/migrate-best-practices-networking/firewall.png)
"_図 11: Azure Firewall。_ "

このサービスをデプロイする場合は、次のいくつかの点に注意してください。

- Azure Firewall では、アプリケーションとネットワークの接続ポリシーを、サブスクリプションと仮想ネットワークをまたいで一元的に作成、適用、記録することができます。
- Azure Firewall では、対象の仮想ネットワーク リソースに静的パブリック IP アドレスを使用します。 これにより、対象の仮想ネットワークから送信されるトラフィックを外部のファイアウォールで識別できます。
- Azure Firewall は、ログ記録と分析を行うために Azure Monitor と完全に統合されます。
- Azure Firewall 規則を作成する場合は、FQDN タグを使用することをお勧めします。
  - FQDN タグは、よく知られた Microsoft サービスに関連付けられている FQDN のグループを表します。
  - FQDN タグを使用すると、必要な送信ネットワーク トラフィックがファイアウォールを通過するのを許可できます。
- たとえば、手動で Windows Update ネットワーク トラフィックがファイアウォールを通過できるようにするには、複数のアプリケーション規則を作成する必要があります。 FQDN タグを使用して、アプリケーション規則を作成し、Windows Update のタグを組み込みます。 この規則を適用すると、Microsoft Windows Update エンドポイントへのネットワーク トラフィックは、ファイアウォールを通過できます。

**詳細情報:**

- [Azure Firewall の概要](/azure/firewall/overview)を読む。
- [Azure Firewall の FQDN タグ](/azure/firewall/fqdn-tags)について学習します。

## <a name="best-practice-deploy-web-application-firewall"></a>ベスト プラクティス:Web アプリケーション ファイアウォールをデプロイする

Web アプリケーションが、一般的な既知の脆弱性を悪用した悪意のある攻撃の的になるケースが増えています。 悪用には、SQL インジェクション攻撃やクロス サイト スクリプティング攻撃などが含まれます。 アプリケーション コードでこのような攻撃を防ぐことは困難な場合があり、厳格な保守、パッチの適用、アプリケーション トポロジの複数のレイヤーでの監視が必要になることもあります。

Azure Application Gateway の機能である Web アプリケーション ファイアウォール (WAF) を使用すると、セキュリティの管理がはるかに簡単になり、脅威や侵入からの保護を行うアプリケーション管理者の役に立ちます。 個々の Web アプリケーションをセキュリティで保護するのではなく、1 か所に既知の脆弱性の修正プログラムを適用することで、さらに迅速にセキュリティの脅威に対応できます。 既存のアプリケーション ゲートウェイは、Web アプリケーション ファイアウォールに対応したアプリケーション ゲートウェイに簡単に変換できます。

WAF についての追加の注意事項を次に示します。

- WAF では、一般的な悪用や脆弱性からの Web アプリケーションの一元的な保護が提供されます。
- WAF を使用するために自分のコードを変更する必要はありません。
- Application Gateway の後方にある複数の Web アプリを同時に保護できます。
- WAF は Azure Security Center と統合されています。
- アプリケーションの要件に合わせて WAF の規則と規則グループをカスタマイズすることができます。
- ベスト プラクティスとしては、Azure VM 上のアプリケーションや Azure App Service のアプリケーションなど、Web に接続されているすべてのアプリケーションの前方で WAF を使用する必要があります。

**詳細情報:**

- [WAF](/azure/application-gateway/waf-overview) について学習する。
- [WAF の制限事項と除外事項](/azure/application-gateway/application-gateway-waf-configuration)を確認する。

## <a name="best-practice-implement-azure-network-watcher"></a>ベスト プラクティス:Azure Network Watcher を実装する

Azure Network Watcher には、Azure 仮想ネットワーク内のリソースと通信を監視するためのツールが用意されています。 たとえば、VM とエンドポイント (別の VM や FQDN など) との間の通信を監視できます。 また、仮想ネットワーク内のリソースやリソースの関係を表示したり、ネットワーク トラフィックの問題を診断したりすることもできます。

![Network Watcher のスクリーンショット。](./media/migrate-best-practices-networking/network-watcher.png)
"_図 12: Network Watcher。_ "

追加の詳細情報を以下にいくつか示します。

- Network Watcher を使用すると、VM にサインインすることなく、ネットワークの問題を監視して診断できます。
- アラートを設定することでパケット キャプチャをトリガーし、パケット レベルでのパフォーマンスの情報にリアルタイムでアクセスできます。 問題が見つかったら、詳細に調査できます。
- ベスト プラクティスとしては、Network Watcher を使用して NSG のフロー ログを確認する必要があります。
  - Network Watcher で NSG のフロー ログを表示すると、NSG を通過するイングレスおよびエグレス IP トラフィックに関する情報を見ることができます。
  - フロー ログは JSON 形式で書き込まれています。
  - フロー ログには、規則ごとの送受信フローと、フローが適用されるネットワーク インターフェイス (NIC) が示されます。 さらに、フローに関する 5 タプル情報 (送信元 IP、宛先 IP、送信元ポート、宛先ポート、プロトコル)、およびトラフィックが許可されたか拒否されたかが記載されます。

**詳細情報:**

- [Network Watcher の概要](/azure/network-watcher)を読む。
- [NSG のフロー ログ](/azure/network-watcher/network-watcher-nsg-flow-logging-overview)の詳細を確認する。

## <a name="use-partner-tools-in-azure-marketplace"></a>Azure Marketplace のパートナー ツールを使用する

複雑なネットワーク トポロジでは、特定のネットワーク仮想アプライアンス (NVA) で Microsoft パートナーからのセキュリティ製品を使用する場合があります。

- NVA とは、ファイアウォール、WAN 最適化、その他のネットワーク機能を実行する VM です。
- NVA により、仮想ネットワークのセキュリティとネットワークの機能が強化されます。 高可用性ファイアウォール、侵入防止、侵入検出、WAF、WAN 最適化、ルーティング、負荷分散、VPN、証明書管理、Active Directory、および多要素認証のためにデプロイできます。
- NVA は、[Azure Marketplace](https://azuremarketplace.microsoft.com) の多数のベンダーから入手できます。

## <a name="best-practice-implement-firewalls-and-nvas-in-hub-networks"></a>ベスト プラクティス:ハブ ネットワークにファイアウォールと NVA を実装する

ハブでは通常、Azure Firewall、ファイアウォール ファーム、または WAF を通して (インターネットにアクセスできる) 境界ネットワークを管理します。 次の表は、これらの比較を示しています。

| ファイアウォールの種類 | 詳細 |
| --- | --- |
| WAF | Web アプリケーションは一般的であり、脆弱性や潜在的な悪用の影響を受ける傾向があります。 WAF は、Web アプリケーション (HTTP、HTTPS) に対する攻撃を検出するように設計されています。 従来のファイアウォール テクノロジと比較すると、WAF は内部 Web サーバーを脅威から保護する特定の機能セットを備えています。 |
| Azure Firewall | NVA ファイアウォール ファームのように、Azure Firewall では、一般的な管理メカニズムとセキュリティ規則セットを使用して、スポーク ネットワークでホストされているワークロードが保護されます。 Azure Firewall は、オンプレミスのネットワークへのアクセスを制御するのにも役立ちます。 Azure Firewall にはスケーラビリティが組み込まれています。 |
| NVA ファイアウォール | Azure Firewall と同様に、NVA ファイアウォール ファームでは、一般的な管理メカニズムとセキュリティ規則セットを使用して、スポーク ネットワークでホストされているワークロードが保護されます。 NVA ファイアウォールは、オンプレミスのネットワークへのアクセスを制御するのにも役立ちます。 NVA ファイアウォールは、ロード バランサーの後方で手動スケーリングできます。 <br><br> NVA ファイアウォールは WAF ほど特化したソフトウェアではありませんが、エグレスおよびイングレスのあらゆる種類のトラフィックをフィルター処理して検査する広範な適用範囲を備えています。 |

インターネットから送信されるトラフィックとオンプレミスから送信されるトラフィックには、それぞれ異なる Azure ファイアウォール (または NVA) のセットを使用することをお勧めします。 両方にただ 1 つのファイアウォールのセットを使うと、2 つのネットワーク トラフィック セットの間にセキュリティ境界が提供されないため、セキュリティ リスクになります。 個別のファイアウォール レイヤーを使用すると、セキュリティ規則のチェックの複雑さが軽減され、規則と受信ネットワーク要求の対応が明確です。

**詳細情報:**

- [Azure 仮想ネットワークでの NVA の使用](/azure/architecture/reference-architectures/dmz/secure-vnet-dmz)について学習する。

## <a name="next-steps"></a>次のステップ

他のベスト プラクティスを確認します。

- 移行後のセキュリティと管理の[ベスト プラクティス](./migrate-best-practices-security-management.md)。
- 移行後のコスト管理の[ベスト プラクティス](./migrate-best-practices-costs.md)。
