---
title: データセンターで Azure のガバナンスを実行する
description: データセンター内の Azure Stack Hub 上で実行されている Azure インスタンスのガバナンス方法について説明します。
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 117b21cde2fccbb1e823986d91528cca0dfa21f7
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94994702"
---
# <a name="govern-an-azure-instance-in-your-datacenter"></a>データセンターで Azure のガバナンスを実行する

パブリックおよびプライベートのクラウド プラットフォームにまたがるハイブリッド ソリューションのガバナンスは複雑な作業です。 Azure Stack Hub デプロイは、データセンターで実行されている Azure のユーザー独自のプライベート インスタンスであるため、そのような複雑さは本質的に軽減されています。

とはいえ、クラウド導入フレームワークの[ガバナンス手法](../../govern/index.md)で概説されているビジネス プロセス、規範、および多くのベスト プラクティスは、Azure Stack Hub を使用したハイブリッド ガバナンスにも適用できます。 Azure のパブリック クラウド バージョンで使用される多くのクラウドネイティブ ツールは、Azure Stack Hub デプロイでも使用できます。

## <a name="azure-stack-hub-governance-considerations"></a>Azure Stack Hub のガバナンスに関する考慮事項

次の一連のブログでは、組織で Azure Stack Hub にクラウド ガバナンスの概念を実装する方法について説明しています。

- [組織向けサービス](https://azure.microsoft.com/blog/azure-stack-iaas-part-seven/): リソース グループ、ロールベースのアクセス制御 (RBAC)、変更の監査、ロック、タグなど。
- [セキュリティ サービス](https://azure.microsoft.com/blog/azure-stack-iaas-part-four/): 既定のファイアウォール、制限、VM の更新と修正プログラムの管理、マルウェアの状態など。
- [DevOps オプション](https://azure.microsoft.com/blog/azure-stack-iaas-part-seven-2/): コードとしてのインフラストラクチャ、PowerShell およびコマンドライン インターフェイスを使用したポータル、Azure Application Insights、Azure DevOps および Jenkins との統合など。

## <a name="governance-toolchain-for-azure-stack-hub"></a>Azure Stack Hub のガバナンス ツールチェーン

クラウドネイティブ ガバナンス ツールを Azure Stack Hub 環境に適用するためのガイダンスについては、次を参照してください。

- [Azure Resource Manager テンプレートと Desired State Configuration](/azure-stack/user/azure-stack-arm-templates?view=azs-2002)
- [PowerShell](/azure-stack/user/azure-stack-powershell-overview?view=azs-2002)
- [Azure Policy](/azure-stack/user/azure-stack-policy-module?view=azs-2002)
- [役割ベースのアクセス制御](/azure-stack/user/azure-stack-manage-permissions?view=azs-2002)

## <a name="next-steps"></a>次のステップ

クラウド導入の取り組みの特定の要素に関するガイダンスについては、以下を参照してください。

- [Azure Stack Hub の管理](./manage.md)
