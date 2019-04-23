---
title: Voraussetzungen für die Host-Überwachungsdienst
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: f4b4d1a8-bf6d-4881-9150-ddeca8b48038
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: dddf694aaceab93bd102456dbe86df17a001cb01
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879881"
---
# <a name="review-prerequisites-for-the-host-guardian-service"></a>Überprüfen der Voraussetzungen für die Host-Überwachungsdienst

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016


Dieses Thema behandelt die Host-Überwachungsdienst-Voraussetzungen und die ersten Schritte zur Vorbereitung der Bereitstellung des Host-Überwachungsdienst.

## <a name="prerequisites"></a>Vorraussetzungen 

-   **Hardware**: Host-Überwachungsdienst auf physischen oder virtuellen Computern ausgeführt werden können, physische Computer werden jedoch empfohlen.

    Wenn Sie Host-Überwachungsdienst als physischen Cluster drei Knoten (für Verfügbarkeit) ausführen möchten, müssen Sie drei physische Server verfügen. (Als bewährte Methode für das clustering, sollte die drei Server sehr ähnlichen Hardware haben.)
  
-   **Betriebssystem**: Host-schlüsselnachweis erfordert Windows Server 2019 Standard oder Datacenter Edition arbeiten, mit [v2-Nachweis](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#versioned-attestation-policies). Für TPM-basierten nachweisen können die Host-Überwachungsdienst 2019 für Windows Server oder Windows Server 2016 Standard oder Datacenter Edition ausführen.

-   **Serverrollen**: Host-Überwachungsdienst und die-Serverrollen unterstützen.

-   **Konfiguration Berechtigungen und die richtigen Berechtigungen für die Domäne (Host)-Fabric**: Sie müssen die DNS-Weiterleitung zwischen den Fabric (Host) und der Host-Überwachungsdienst-Domäne zu konfigurieren. 
    
## <a name="upgrading-hgs"></a>Aktualisieren die Host-Überwachungsdienst

Wenn Sie Host-Überwachungsdienst bereits bereitgestellt haben und das Betriebssystem ein Upgrade ausführen möchten, führen Sie die [Upgradeanweisungen](guarded-fabric-upgrade-to-2019.md) zum Aktualisieren der Host-Überwachungsdienst und Hyper-V-Server auf das neueste Betriebssystem.

## <a name="next-step"></a>Nächster Schritt

>[!div class="nextstepaction"]
[Abrufen von Zertifikaten für die Host-Überwachungsdienst](guarded-fabric-obtain-certs.md)