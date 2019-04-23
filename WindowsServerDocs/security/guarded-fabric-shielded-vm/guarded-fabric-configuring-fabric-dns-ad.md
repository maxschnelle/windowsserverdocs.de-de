---
title: Konfigurieren Sie den Fabric-DNS für überwachte Hosts (AD)
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 074b6d09-f16e-49bf-b88a-377139d35067
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 8a2ddc0f2ab495b2500d4bfe48f3ee83c333c769
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842751"
---
# <a name="configure-the-fabric-dns-for-guarded-hosts"></a>Konfigurieren Sie den Fabric-DNS für überwachte hosts

>Gilt für: Windows Server 2016


>[!IMPORTANT]
>AD-Modus ist veraltet, beginnend mit Windows Server-2019. Konfigurieren Sie für Umgebungen, in denen ist TPM-Nachweis nicht möglich, [hosten den schlüsselnachweis](guarded-fabric-initialize-hgs-key-mode.md). Host den schlüsselnachweis bietet eine ähnliche Garantie in den Active Directory-Modus, und es ist leichter einzurichten. 

Ein Fabric-Administrator muss das Fabric konfigurieren, die DNS verwendet, um überwachte Hosts zum Auflösen des Host-Überwachungsdienst-Clusters zu ermöglichen. Der Host-Überwachungsdienst-Cluster muss bereits [eingerichtet, indem der HGS-Administrator](/WindowsServerDocs/virtualization/guarded-fabric-shielded-vm/guarded-fabric-setting-up-the-host-guardian-service-hgs.md).



[!INCLUDE [Configure fabric DNS](../../../includes/guarded-fabric-configure-fabric-dns.md)] 


## <a name="next-step"></a>Nächster Schritt

>[!div class="nextstepaction"]
[Konfigurieren von HGS-DNS und einer unidirektionalen Vertrauensstellung](guarded-fabric-configure-dns-forwarding-and-trust.md)
