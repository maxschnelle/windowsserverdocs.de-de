---
title: Empfangen von Segmentkoaleszenz (RSC) im vSwitch
description: Empfangen von Segment Coalescing (RSC) in der vSwitch ist ein Feature in Windows Server-2019 und Windows 10 Oktober 2018 aktualisieren, dass der Host-CPU-Auslastung und erhöhen den Durchsatz für virtuelle auslastungen reduziert durch die Zusammenfügung mehrerer TCP-Segmente in weniger aber größere Segmente. Die Verarbeitung von weniger große Segmente mit (vereinigt) ist effizienter als die Verarbeitung zahlreicher kleinen Segmenten.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ''
ms.author: dacuo
author: shortpatti
ms.date: 09/07/2018
ms.openlocfilehash: 667e795e398443cadd4c966cc31e65eeee4962f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827781"
---
# <a name="rsc-in-the-vswitch"></a>RSC in vSwitches
>Gilt für: Windows Server 2019

Empfangen von Segment Coalescing (RSC) in der vSwitch ist ein Feature in Windows Server-2019 und Windows 10 Oktober 2018 aktualisieren, dass der Host-CPU-Auslastung und erhöhen den Durchsatz für virtuelle auslastungen reduziert durch die Zusammenfügung mehrerer TCP-Segmente in weniger aber größere Segmente. Die Verarbeitung von weniger große Segmente mit (vereinigt) ist effizienter als die Verarbeitung zahlreicher kleinen Segmenten.

WindowsServer 2012 und höher enthalten eine Version hardwarespezifischen Auslagerung der Technologie auch bekannt als Empfang zusammengeführter Segmente (implementiert in den physischen Netzwerkadapter). Dieser ausgelagerten RSC-Version ist weiterhin verfügbar, in höheren Versionen von Windows. Es ist jedoch nicht kompatibel mit virtueller arbeitsauslastungen und wurde deaktiviert, sobald ein vSwitch ein physischen Netzwerkadapter zugeordnet ist. Weitere Informationen zu der Hardware reine Softwareversion von RSC, finden Sie unter [erhalten Segment Coalescing (RSC)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh997024(v=ws.11)).

## <a name="scenarios-that-benefit-from-rsc-in-the-vswitch"></a>Szenarien, die über RSC in vSwitches profitieren

Workloads, deren Datenpfad mit einen virtuellen Switch durchläuft, profitiert von dieser Funktion.

Zum Beispiel:

-   Virtuelle NICs des Hosts einschließlich:

    -   Software-Defined Networking

    -   Hyper-V-Host

    -   Direkte Speicherplätze

-   Virtuelle Hyper-V-Gast-NICs

-   Software-Defined Networking-GRE-Gateways

-   Container

Workloads, die nicht mit diesem Feature kompatibel sind enthalten:

-   Software-Defined Networking-IPSEC-Gateways

-   SR-IOV aktiviert virtuelle NICs

-   SMB Direct

## <a name="configure-rsc-in-the-vswitch"></a>Konfigurieren von RSC in vSwitches


RSC ist standardmäßig auf externe vSwitches aktiviert.

**Zeigen Sie die aktuellen Einstellungen an:**

```PowerShell
Get-VMSwitch -Name vSwitchName | Select-Object *RSC*
```

**Aktivieren oder Deaktivieren von RSC in vSwitches**


>[!IMPORTANT]
>Wichtig: RSC in vSwitches aktiviert, und klicken Sie auf die im laufenden Betrieb ohne Auswirkungen auf vorhandene Verbindungen deaktiviert werden kann.


**RSC in vSwitches deaktivieren**

```PowerShell
Set-VMSwitch -Name vSwitchName -EnableSoftwareRsc $false
```

**Erneutes Aktivieren von RSC ins vSwitches**

```PowerShell
Set-VMSwitch -Name vSwitchName -EnableSoftwareRsc $True
```
Weitere Informationen finden Sie unter [Set-VMSwitch](https://docs.microsoft.com/powershell/module/hyper-v/set-vmswitch?view=win10-ps).
