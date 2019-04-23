---
title: Initialisieren von Host-Überwachungsdienst mit TPM-vertrauenswürdiger Nachweis
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 672054462437b615236dfc4f00c8b20c946f11a7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882331"
---
# <a name="initialize-hgs-using-tpm-trusted-attestation"></a>Initialisieren von Host-Überwachungsdienst mit TPM-vertrauenswürdiger Nachweis

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Diese Schritte hängen davon ab, ob Sie Host-Überwachungsdienst in einer neuen Gesamtstruktur oder einer vorhandenen geschützten Gesamtstruktur initialisieren:

1. [Initialisieren Sie den Host-Überwachungsdienst-Cluster in einer neuen Gesamtstruktur (Standard)](guarded-fabric-initialize-hgs-tpm-mode-default.md)

   – Oder –

   [Initialisieren Sie den Host-Überwachungsdienst-Cluster in einer vorhandenen geschützten Gesamtstruktur](guarded-fabric-initialize-hgs-tpm-mode-bastion.md)

2. [Installieren des vertrauenswürdigen TPM-Stammzertifikate](guarded-fabric-install-trusted-tpm-root-certificates.md)   
3. [Konfigurieren der DNS-Struktur](guarded-fabric-configuring-fabric-dns.md)

