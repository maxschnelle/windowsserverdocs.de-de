---
title: Initialisieren von Host-Überwachungsdienst mit Admin-vertrauenswürdiger Nachweis
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 664404cb72981e162bca016df14847e684d987c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821831"
---
# <a name="initialize-hgs-using-admin-trusted-attestation"></a>Initialisieren von Host-Überwachungsdienst mit Admin-vertrauenswürdiger Nachweis

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

>[!IMPORTANT]
>Admin-vertrauenswürdiger Nachweis (Active Directory-Modus) ist veraltet, beginnend mit Windows Server-2019. Konfigurieren Sie für Umgebungen, in denen ist TPM-Nachweis nicht möglich, [hosten den schlüsselnachweis](guarded-fabric-initialize-hgs-key-mode.md). Host den schlüsselnachweis bietet eine ähnliche Garantie in den Active Directory-Modus, und es ist leichter einzurichten. 


Diese Schritte hängen davon ab, ob Sie Host-Überwachungsdienst in einer neuen Gesamtstruktur oder einer vorhandenen geschützten Gesamtstruktur initialisieren:

1. [Initialisieren Sie den Host-Überwachungsdienst-Cluster in einer neuen Gesamtstruktur (Standard)](guarded-fabric-initialize-hgs-ad-mode-default.md)

   – Oder –

   [Initialisieren Sie den Host-Überwachungsdienst-Cluster in einer vorhandenen geschützten Gesamtstruktur](guarded-fabric-initialize-hgs-ad-mode-bastion.md)

2. [Konfigurieren von DNS-Weiterleitung in der Fabric-Domäne](guarded-fabric-configuring-fabric-dns.md)

3. [Konfigurieren von DNS-Weiterleitung und eine unidirektionale Vertrauensstellung in der Domäne des Host-Überwachungsdienst](guarded-fabric-configure-dns-forwarding-and-trust.md)



