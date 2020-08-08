---
title: Empfangssegmentzusammenfügung im vSwitch
description: Receive Segment Sammel (RSC) im Vswitch ist eine Funktion in Windows Server 2019 und dem Windows 10-Update vom Oktober 2018, mit der die CPU-Auslastung des Hosts reduziert und der Durchsatz für virtuelle Arbeits Auslastungen erhöht wird, indem mehrere TCP-Segmente in weniger, aber größere Segmente zusammengestellt werden. Die Verarbeitung von weniger großen Segmenten (zusammen Fügung) ist effizienter als die Verarbeitung zahlreicher, kleiner Segmente.
manager: dougkim
ms.topic: article
ms.author: dacuo
author: dcuomo
ms.date: 09/07/2018
ms.openlocfilehash: 66f0f72dc6a577030ad43103e5f9d08a9458e64d
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87995102"
---
# <a name="rsc-in-the-vswitch"></a>RSC im Vswitch
>Gilt für: Windows Server 2019

Receive Segment Sammel (RSC) im Vswitch ist eine Funktion in Windows Server 2019 und dem Windows 10-Update vom Oktober 2018, mit der die CPU-Auslastung des Hosts reduziert und der Durchsatz für virtuelle Arbeits Auslastungen erhöht wird, indem mehrere TCP-Segmente in weniger, aber größere Segmente zusammengestellt werden. Die Verarbeitung von weniger großen Segmenten (zusammen Fügung) ist effizienter als die Verarbeitung zahlreicher, kleiner Segmente.

Windows Server 2012 und höher enthielt eine nur-Hardware-Auslagerung-Version (implementiert im physischen Netzwerkadapter) der Technologie, die auch als Empfangs Segment Zusammenfassung bezeichnet wird. Diese offloaded-Version von RSC ist in neueren Windows-Versionen weiterhin verfügbar. Es ist jedoch nicht mit virtuellen Workloads kompatibel und wurde deaktiviert, sobald ein physischer Netzwerkadapter an einen Vswitch angefügt wurde. Weitere Informationen zur reinen Hardware Version von RSC finden Sie unter [Receive Segment Coalescing (RSC)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh997024(v=ws.11)).

## <a name="scenarios-that-benefit-from-rsc-in-the-vswitch"></a>Szenarien, die von RSC im Vswitch profitieren

Workloads, deren Datenpfad einen virtuellen Switch durchläuft, profitiert von diesem Feature.

Zum Beispiel:

-   Virtuelle Netzwerkkarten für Hosts einschließlich:

    -   Softwaredefiniertes Netzwerk

    -   Hyper-V-Host

    -   Speicherplätze DAS

-   Virtuelle Hyper-V-Gast-NICs

-   Software-Defined Networking-GRE-Gateways

-   Container

Workloads, die mit dieser Funktion nicht kompatibel sind, umfassen Folgendes:

-   Software-Defined Networking-IPSec-Gateways

-   SR-IOV-aktivierte virtuelle NICs

-   SMB Direct

## <a name="configure-rsc-in-the-vswitch"></a>RSC im Vswitch konfigurieren


Auf externen vSwitches ist RSC standardmäßig aktiviert.

**Anzeigen der aktuellen Einstellungen:**

```PowerShell
Get-VMSwitch -Name vSwitchName | Select-Object *RSC*
```

**Aktivieren oder Deaktivieren von RSC im Vswitch**


>[!IMPORTANT]
>Wichtig: RSC im Vswitch kann dynamisch aktiviert und deaktiviert werden, ohne Auswirkungen auf vorhandene Verbindungen zu haben.


**RSC im Vswitch deaktivieren**

```PowerShell
Set-VMSwitch -Name vSwitchName -EnableSoftwareRsc $false
```

**RSC im Vswitch erneut aktivieren**

```PowerShell
Set-VMSwitch -Name vSwitchName -EnableSoftwareRsc $True
```
Weitere Informationen finden Sie unter [Set-VMSwitch](/powershell/module/hyper-v/set-vmswitch?view=win10-ps).