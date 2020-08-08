---
title: Verwalten von vRSS
description: In diesem Thema verwenden Sie die Windows PowerShell-Befehle, um vrss auf virtuellen Computern (VMS) und auf Hyper-V-Hosts zu verwalten.
ms.topic: article
ms.assetid: 0fe5bfc3-591f-4a19-b98a-0668d4c9f93a
ms.localizationpriority: medium
manager: dougkim
ms.date: 09/05/2018
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 553be94dd3fe94a74ee9deb84a5ac6d47265afec
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955537"
---
# <a name="manage-vrss"></a>Verwalten von vRSS

In diesem Thema verwenden Sie die Windows PowerShell-Befehle zum Verwalten von vrss auf virtuellen \( Computern \) und Hyper- \- V-Hosts.

>[!NOTE]
>Weitere Informationen zu den in diesem Thema erwähnten Befehlen finden Sie unter [Windows PowerShell-Befehle für RSS und vrss](vrss-wps.md).

## <a name="vmq-on-hyper-v-hosts"></a>VMQ auf Hyper-V-Hosts

Auf dem Hyper-V-Host müssen Sie die Schlüsselwörter zum Steuern der VMQ-Prozessoren verwenden.

**Anzeigen der aktuellen Einstellungen:**

```PowerShell
Get-NetAdapterVmq
```

**Konfigurieren Sie die VMQ-Einstellungen:**

```PowerShell
Set-NetAdapterVmq
```


## <a name="vrss-on-hyper-v-switch-ports"></a>vrss auf Hyper-V-Switchports

Auf dem Hyper-v-Host müssen Sie auch vrss auf dem virtuellen Hyper- \- v-Switchport aktivieren.

**Anzeigen der aktuellen Einstellungen:**

```PowerShell
Get-VMNetworkAdapter <vm-name> | fl

Get-VMNetworkAdapter -ManagementOS | fl
```

Beide der folgenden Einstellungen sollten " **true**" lauten.

- Vrssenabledrequessiert: true
- Vrssaktivierte: true

>[!IMPORTANT]
>Unter einigen Ressourcen Einschränkungs Bedingungen ist \- es für einen virtuellen Hyper-V-Switchport möglicherweise nicht aktiviert, dass diese Funktion aktiviert ist. Dies ist eine temporäre Bedingung, und die Funktion kann zu einem späteren Zeitpunkt verfügbar werden.
>
>Wenn " **vrssaktivierte** " den Wert " **true**" hat, wird das Feature für diesen virtuellen Hyper-V-Switchport aktiviert, d \- . –. für diese VM oder vNIC.

**Konfigurieren der Switchport-vrss-Einstellungen:**

```PowerShell
Set-VMNetworkAdapter <vm-name> -VrssEnabled $TRUE

Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
```

## <a name="vrss-in-vms-and-host-vnics"></a>vrss auf VMS und Host-vNICs

Sie können dieselben Befehle verwenden, die für das systemeigene RSS-Format verwendet werden, um vrss-Einstellungen auf virtuellen Computern und Host-vNICs zu konfigurieren. Dies ist auch die Möglichkeit zum Aktivieren von RSS auf Host-vNICs

**Anzeigen der aktuellen Einstellungen:**

```PowerShell
Get-NetAdapterRSS
```

**Konfigurieren von vrss-Einstellungen:**

```PowerShell
Set-NetAdapterRss
```

>[!NOTE]
> Das Festlegen des Profils innerhalb der VM wirkt sich nicht auf die Planung der Arbeit aus. Hyper \- -V trifft alle Planungsentscheidungen und ignoriert das Profil innerhalb der VM.

## <a name="disable-vrss"></a>Deaktivieren von vrss

Sie können vrss deaktivieren, um die zuvor erwähnten Einstellungen zu deaktivieren.

- Deaktivieren Sie VMQ für die physische NIC oder den virtuellen Computer.

  >[!CAUTION]
  >Das Deaktivieren von VMQ auf der physischen NIC wirkt sich schwerwiegend auf die Fähigkeit Ihres Hyper- \- V-Hosts aus, eingehende Pakete zu verarbeiten.

- Deaktivieren Sie vrss für eine VM auf dem Hyper- \- v-Switch für virtuelle Switches auf dem Hyper- \- v-Host.

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled $FALSE
   ```

- Deaktivieren Sie vrss für eine Host-vNIC auf dem virtuellen Hyper- \- v-Switchport auf dem Hyper- \- v-Host.

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $FALSE
   ```

- Deaktivieren von RSS auf dem virtuellen Computer \( oder der Host-vNIC \) innerhalb des virtuellen Computers \( oder auf dem Host\)

   ```PowerShell
   Disable-NetAdapterRSS *
   ```
