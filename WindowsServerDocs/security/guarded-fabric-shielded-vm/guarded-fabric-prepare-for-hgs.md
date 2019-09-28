---
title: Prüfen der HGS-Voraussetzungen
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: f4b4d1a8-bf6d-4881-9150-ddeca8b48038
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 9024557dd42ede27144bf10aa5873b6bb12d585c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403485"
---
# <a name="review-prerequisites-for-the-host-guardian-service"></a>Überprüfen der Voraussetzungen für den Host-Überwachungsdienst

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016


In diesem Thema werden die Voraussetzungen für HGS und die ersten Schritte zur Vorbereitung der Bereitstellung von HGS behandelt.

## <a name="prerequisites"></a>Erforderliche Komponenten 

-   **Hardware**: HGS können auf physischen oder virtuellen Computern ausgeführt werden, es werden jedoch physische Computer empfohlen.

    Wenn Sie HGS als physischen Cluster mit drei Knoten (für Verfügbarkeit) ausführen möchten, müssen Sie über drei physische Server verfügen. (Als bewährte Methode für das Clustering sollten die drei Server über eine sehr ähnliche Hardware verfügen.)
  
-   **Betriebssystem**: Beim Nachweis des Host Schlüssels ist Windows Server 2019 Standard oder Datacenter Edition mit einem [v2](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#versioned-attestation-policies)-Nachweis erforderlich. Bei einem TPM-basierten Nachweis können auf HGS Windows Server 2019 oder Windows Server 2016, Standard oder Datacenter Edition ausgeführt werden.

-   **Server Rollen**: Host-Überwachungsdienst und unterstützende Server Rollen.

-   **Konfigurations Berechtigungen/Berechtigungen für die Fabric-Domäne (Host)** : Sie müssen die DNS-Weiterleitung zwischen der Fabric-Domäne (Host) und der HGS-Domäne konfigurieren. 
    
## <a name="upgrading-hgs"></a>Aktualisieren von HGS

Wenn Sie bereits HGS bereitgestellt haben und ein Upgrade des Betriebssystems durchführen möchten, befolgen Sie die Anweisungen zum [Upgrade](guarded-fabric-upgrade-to-2019.md) , um Ihre HGS und Hyper-V-Server auf das neueste Betriebssystem zu aktualisieren.

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Zertifikate für HGS abrufen](guarded-fabric-obtain-certs.md)