---
title: Initialisieren von HGS mithilfe von TPM-vertrauenswürdigem Nachweis
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: b8ceebe63a586ec95b502dfea12f99d174549448
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856613"
---
# <a name="initialize-hgs-using-tpm-trusted-attestation"></a>Initialisieren von HGS mithilfe von TPM-vertrauenswürdigem Nachweis

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Diese Schritte sind abhängig davon, ob Sie HGS in einer neuen Gesamtstruktur oder in einer vorhandenen geschützten Gesamtstruktur initialisieren:

1. [Initialisieren des HGS-Clusters in einer neuen Gesamtstruktur (Standard)](guarded-fabric-initialize-hgs-tpm-mode-default.md)

   – Oder –

   [Initialisieren des HGS-Clusters in einer vorhandenen geschützten Gesamtstruktur](guarded-fabric-initialize-hgs-tpm-mode-bastion.md)

2. [Installieren Sie vertrauenswürdige TPM-Stamm Zertifikate.](guarded-fabric-install-trusted-tpm-root-certificates.md)   
3. [Konfigurieren des Fabric-DNS](guarded-fabric-configuring-fabric-dns.md)

