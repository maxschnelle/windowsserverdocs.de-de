---
title: Initialisieren von HGS mithilfe des vom Administrator vertrauenswürdigen Nachweis
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 491754e8bcaad4524084604b78c7c6ed0fdee295
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402355"
---
# <a name="initialize-hgs-using-admin-trusted-attestation"></a>Initialisieren von HGS mithilfe des vom Administrator vertrauenswürdigen Nachweis

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

>[!IMPORTANT]
>Der admin-Trusted Nachweis (AD-Modus) ist ab Windows Server 2019 veraltet. Für Umgebungen, in denen ein TPM-Nachweis nicht möglich ist, konfigurieren Sie den [Host Schlüssel](guarded-fabric-initialize-hgs-key-mode.md)Nachweis. Der Host Schlüssel Nachweis bietet eine ähnliche Garantie für den AD-Modus und ist einfacher einzurichten. 


Diese Schritte sind abhängig davon, ob Sie HGS in einer neuen Gesamtstruktur oder in einer vorhandenen geschützten Gesamtstruktur initialisieren:

1. [Initialisieren des HGS-Clusters in einer neuen Gesamtstruktur (Standard)](guarded-fabric-initialize-hgs-ad-mode-default.md)

   – Oder –

   [Initialisieren des HGS-Clusters in einer vorhandenen geschützten Gesamtstruktur](guarded-fabric-initialize-hgs-ad-mode-bastion.md)

2. [Konfigurieren der DNS-Weiterleitung in der Fabric-Domäne](guarded-fabric-configuring-fabric-dns.md)

3. [Konfigurieren der DNS-Weiterleitung und einer unidirektionalen Vertrauensstellung in der HGS-Domäne](guarded-fabric-configure-dns-forwarding-and-trust.md)



