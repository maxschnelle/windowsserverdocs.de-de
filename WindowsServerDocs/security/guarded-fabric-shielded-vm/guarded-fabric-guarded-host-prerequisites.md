---
title: Voraussetzungen für geschützte Hosts
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 40c0f6df31061268b1e1ef8c15b0a02b0f50b0de
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447476"
---
# <a name="prerequisites-for-guarded-hosts"></a>Voraussetzungen für überwachte hosts

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Überprüfen Sie die Host-Voraussetzungen für den Modus von nachweisen, dass Sie ausgewählt haben, und klicken Sie dann den nächsten Schritt zum Hinzufügen von überwachten Hosts.

## <a name="tpm-trusted-attestation"></a>TPM-vertrauenswürdiger Nachweis

Geschützte Hosts, die mithilfe von TPM-Modus müssen die folgenden Voraussetzungen erfüllen:

-   **Hardware**: Ein Host ist für die erstmalige Bereitstellung erforderlich. Um Hyper-V-Livemigration für abgeschirmte VMs zu testen, müssen Sie mindestens zwei Hosts verfügen.

    Hosts müssen:
    
    - UNTERSTÜTZT und Second Level Address Translation (SLAT)
    - TPM 2.0
    - UEFI 2.3.1 oder höher
    - Für den Start mit UEFI (nicht BIOS oder "Legacymodus") konfiguriert
    - Sicherer Start aktiviert
        
-   **Betriebssystem**: Windows Server 2016 Datacenter-Edition oder höher

    > [!IMPORTANT]
    > Installieren Sie unbedingt die [– neuestes Kumulatives Update](https://support.microsoft.com/help/4000825/windows-10-and-windows-server-2016-update-history).  

-   **Rollen und Features**: Hyper-V-Rolle und das Feature Hyper-V-Unterstützung für Host-Überwachungsdiensts. Die Hyper-V-Unterstützung für Host-Überwachungsdiensts-Funktion ist nur verfügbar, auf die Datacenter-Editionen von Windows Server. 

> [!WARNING]
> Das Feature Hyper-V-Unterstützung für Host-Überwachungsdiensts ermöglicht die Virtualisierung basierende Schutz der Integrität des Codes, die möglicherweise bei einigen Geräten nicht kompatibel sind. Es wird dringend empfohlen, diese Konfiguration in Ihrem Lab testen, bevor Sie dieses Feature aktivieren. Andernfalls kann es zu unerwarteten Fehlern und sogar zu Datenverlusten oder zu einem Bluescreen (STOP-Fehler) kommen. Weitere Informationen finden Sie unter [kompatible Hardware mit Windows Server-Virtualisierung mit dem Schutz der Codeintegrität](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md).

**Nächster Schritt:** 
> [!div class="nextstepaction"]
> [Erfassen von TPM-Informationen](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)

## <a name="host-key-attestation"></a>Host-schlüsselnachweis

Geschützte Hosts, die mit den schlüsselnachweis Host müssen die folgenden Voraussetzungen erfüllen:

- **Hardware**: Alle Server, die auf Hyper-V beginnt mit Windows Server-2019 ausgeführt werden kann
- **Betriebssystem**: Windows Server 2019 Datacenter Edition
- **Rollen und Features**: Hyper-V-Rolle und die Hyper-V-Unterstützung für Host-Überwachungsdiensts-Funktion 

Der Host kann entweder eine Domäne oder einer Arbeitsgruppe hinzugefügt werden. 

Für den schlüsselnachweis hosten muss die Host-Überwachungsdienst sein 2019 für Windows Server ausgeführt und Arbeiten mit v2-Nachweis werden. Weitere Informationen finden Sie unter [HGS-Voraussetzungen](guarded-fabric-prepare-for-hgs.md#prerequisites). 

**Nächster Schritt:** 
> [!div class="nextstepaction"]
> [Erstellen eines Schlüsselpaars](guarded-fabric-create-host-key.md)

## <a name="admin-trusted-attestation"></a>Admin-vertrauenswürdiger Nachweis

>[!IMPORTANT]
>Admin-vertrauenswürdiger Nachweis (Active Directory-Modus) ist veraltet, beginnend mit Windows Server-2019. Konfigurieren Sie für Umgebungen, in denen ist TPM-Nachweis nicht möglich, [hosten den schlüsselnachweis](#host-key-attestation). Host den schlüsselnachweis bietet eine ähnliche Garantie in den Active Directory-Modus, und es ist leichter einzurichten. 

Hyper-V-Hosts müssen das AD-Modus die folgenden Voraussetzungen erfüllen:

-   **Hardware**: Auf jedem Server, die auf Hyper-V ab Windows Server 2016 ausgeführt werden kann. Ein Host ist für die erstmalige Bereitstellung erforderlich. Um Hyper-V-Livemigration für abgeschirmte VMs zu testen, benötigen Sie mindestens zwei Hosts.

-   **Betriebssystem**: Windows Server 2016 Datacenter edition

    > [!IMPORTANT]
    > Installieren Sie die [– neuestes Kumulatives Update](https://support.microsoft.com/help/4000825/windows-10-and-windows-server-2016-update-history).

-   **Rollen und Features**: Hyper-V-Rolle und die Hyper-V-Unterstützung für Host-Überwachungsdiensts-Funktion, die nur in Windows Server 2016 Datacenter-Edition verfügbar ist. 

> [!WARNING]
> Das Feature Hyper-V-Unterstützung für Host-Überwachungsdiensts ermöglicht die Virtualisierung basierende Schutz der Integrität des Codes, die möglicherweise bei einigen Geräten nicht kompatibel sind. Es wird dringend empfohlen, diese Konfiguration in Ihrem Lab testen, bevor Sie dieses Feature aktivieren. Andernfalls kann es zu unerwarteten Fehlern und sogar zu Datenverlusten oder zu einem Bluescreen (STOP-Fehler) kommen. Weitere Informationen finden Sie unter [kompatible Hardware mit Windows Server 2016-Virtualisierung mit dem Schutz der Codeintegrität](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md).

**Nächster Schritt:** 
> [!div class="nextstepaction"]
> [Speichern Sie überwachte Hosts in einer Sicherheitsgruppe](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)