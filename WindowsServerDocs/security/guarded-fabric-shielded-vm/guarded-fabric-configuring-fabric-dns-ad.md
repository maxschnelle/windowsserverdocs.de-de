---
title: Konfigurieren des Fabric-DNS für überwachte Hosts (AD)
ms.prod: windows-server
ms.topic: article
ms.assetid: 074b6d09-f16e-49bf-b88a-377139d35067
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 208fe5c3919d61e0d00be9ccf2f5ae86eaa5ea8d
ms.sourcegitcommit: acfdb7b2ad283d74f526972b47c371de903d2a3d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87769658"
---
# <a name="configure-the-fabric-dns-for-guarded-hosts-ad"></a>Konfigurieren des Fabric-DNS für überwachte Hosts (AD)

>Gilt für: Windows Server 2016


>[!IMPORTANT]
>Der AD-Modus ist ab Windows Server 2019 veraltet. Für Umgebungen, in denen ein TPM-Nachweis nicht möglich ist, konfigurieren Sie den [Host Schlüssel](guarded-fabric-initialize-hgs-key-mode.md)Nachweis. Der Host Schlüssel Nachweis bietet eine ähnliche Garantie für den AD-Modus und ist einfacher einzurichten.

Ein fabricadministrator muss das Fabric-DNS benötigt, damit überwachte Hosts den HGS-Cluster auflösen können.
Der HGS-Cluster muss bereits [vom HGS-Administrator eingerichtet](/WindowsServerDocs/virtualization/guarded-fabric-shielded-vm/guarded-fabric-setting-up-the-host-guardian-service-hgs.md)sein.



[!INCLUDE [Configure fabric DNS](../../../includes/guarded-fabric-configure-fabric-dns.md)]


## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Konfigurieren von HGS DNS und einer unidirektionalen Vertrauensstellung](guarded-fabric-configure-dns-forwarding-and-trust.md)
