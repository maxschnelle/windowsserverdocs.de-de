---
title: Voraussetzungen für geschützte Hosts
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: fdd97b90ccfe770564e834f54461a31e2c41a2ea
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856703"
---
# <a name="prerequisites-for-guarded-hosts"></a>Voraussetzungen für geschützte Hosts

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Überprüfen Sie die Host Voraussetzungen für den Nachweis Modus, den Sie ausgewählt haben, und klicken Sie dann auf den nächsten Schritt, um geschützte Hosts hinzuzufügen.

## <a name="tpm-trusted-attestation"></a>TPM-vertrauenswürdiger Nachweis

Geschützte Hosts, die den TPM-Modus verwenden, müssen die folgenden Voraussetzungen erfüllen:

-   **Hardware**: für die erste Bereitstellung ist ein Host erforderlich. Zum Testen der Hyper-V-Live Migration für abgeschirmte VMS müssen Sie über mindestens zwei Hosts verfügen.

    Hosts müssen über Folgendes verfügen:
    
    - IOMMU und Second Level Address Translation (slat)
    - TPM 2.0
    - UEFI 2.3.1 oder höher
    - Konfiguriert für den Start mit UEFI (nicht im BIOS-oder Legacy Modus)
    - Sicherer Start aktiviert
        
-   **Betriebssystem**: Windows Server 2016 Datacenter Edition oder höher

    > [!IMPORTANT]
    > Stellen Sie sicher, dass Sie das [neueste kumulative Update](https://support.microsoft.com/help/4000825/windows-10-and-windows-server-2016-update-history)installieren.  

-   **Rolle und Features**: Hyper-v-Rolle und die Hyper-v-Unterstützung des Host-Überwachungs Diensts. Die Hyper-V-Unterstützung des Host-Überwachungs Diensts ist nur in den Datacenter-Editionen von Windows Server verfügbar. 

> [!WARNING]
> Die Hyper-V-Unterstützung des Host-Überwachungs Diensts ermöglicht den virtualisierungsbasierten Schutz der Code Integrität, der möglicherweise mit einigen Geräten nicht kompatibel ist. Wir empfehlen dringend, diese Konfiguration in Ihrem Lab zu testen, bevor Sie diese Funktion aktivieren. Andernfalls kann es zu unerwarteten Fehlern und sogar zu Datenverlusten oder zu einem Bluescreen (STOP-Fehler) kommen. Weitere Informationen finden Sie unter [kompatible Hardware mit Windows Server-virtualisierungsbasierter Schutz der Code Integrität](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md).

**Nächster Schritt:** 
> [!div class="nextstepaction"]
> [TPM-Informationen erfassen](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)

## <a name="host-key-attestation"></a>Host Schlüssel Nachweis

Geschützte Hosts, die den Host Schlüssel Nachweis verwenden, müssen die folgenden Voraussetzungen erfüllen:

- **Hardware**: jeder Server, der Hyper-V ab Windows Server 2019 ausführen können soll
- **Betriebssystem**: Windows Server 2019 Datacenter Edition
- **Rolle und Features**: Hyper-v-Rolle und die Hyper-v-Unterstützung des Host-Überwachungs Diensts 

Der Host kann entweder einer Domäne oder einer Arbeitsgruppe hinzugefügt werden. 

Bei einem Host Schlüssel Nachweis muss auf HGS Windows Server 2019 ausgeführt werden, und es muss ein v2-Nachweis ausgeführt werden. Weitere Informationen finden Sie unter [Voraussetzungen für HGS](guarded-fabric-prepare-for-hgs.md#prerequisites). 

**Nächster Schritt:** 
> [!div class="nextstepaction"]
> [Erstellen eines Schlüssel Paars](guarded-fabric-create-host-key.md)

## <a name="admin-trusted-attestation"></a>Admin-vertrauenswürdiger Nachweis

>[!IMPORTANT]
>Der admin-Trusted Nachweis (AD-Modus) ist ab Windows Server 2019 veraltet. Für Umgebungen, in denen ein TPM-Nachweis nicht möglich ist, konfigurieren Sie den [Host Schlüssel](#host-key-attestation)Nachweis. Der Host Schlüssel Nachweis bietet eine ähnliche Garantie für den AD-Modus und ist einfacher einzurichten. 

Hyper-V-Hosts müssen die folgenden Voraussetzungen für den AD-Modus erfüllen:

-   **Hardware**: alle Server, die Hyper-V ausführen können, beginnen mit Windows Server 2016. Ein Host ist für die erste Bereitstellung erforderlich. Um die Hyper-V-Live Migration für abgeschirmte VMS zu testen, benötigen Sie mindestens zwei Hosts.

-   **Betriebssystem**: Windows Server 2016 Datacenter Edition

    > [!IMPORTANT]
    > Installieren Sie das [neueste kumulative Update](https://support.microsoft.com/help/4000825/windows-10-and-windows-server-2016-update-history).

-   **Rolle und Features**: Hyper-v-Rolle und die Hyper-v-Unterstützung des Host-Überwachungs Features, die nur in Windows Server 2016 Datacenter Edition verfügbar ist. 

> [!WARNING]
> Die Hyper-V-Unterstützung des Host-Überwachungs Diensts ermöglicht den virtualisierungsbasierten Schutz der Code Integrität, der möglicherweise mit einigen Geräten nicht kompatibel ist. Wir empfehlen dringend, diese Konfiguration in Ihrem Lab zu testen, bevor Sie diese Funktion aktivieren. Andernfalls kann es zu unerwarteten Fehlern und sogar zu Datenverlusten oder zu einem Bluescreen (STOP-Fehler) kommen. Weitere Informationen finden Sie unter [kompatible Hardware mit Windows Server 2016 Virtualization-basierter Schutz der Code Integrität](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md).

**Nächster Schritt:** 
> [!div class="nextstepaction"]
> [Geschützte Hosts in einer Sicherheitsgruppe platzieren](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)