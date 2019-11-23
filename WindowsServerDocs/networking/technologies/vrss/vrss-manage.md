---
title: Verwalten von vRSS
description: In diesem Thema verwenden Sie die Windows PowerShell-Befehle, um vrss auf virtuellen Computern (VMS) und auf Hyper-V-Hosts zu verwalten.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0fe5bfc3-591f-4a19-b98a-0668d4c9f93a
ms.localizationpriority: medium
manager: dougkim
ms.date: 09/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9d528f7e658d61f613eedc635fb81d8f18fd59aa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405168"
---
# <a name="manage-vrss"></a>Verwalten von vRSS

In diesem Thema verwenden Sie die Windows PowerShell-Befehle zum Verwalten von vrss in virtuellen Computern \(VMS\) und auf Hyper\-V-Hosts.

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

Auf dem Hyper-V-Host müssen Sie auch vrss auf dem virtuellen Hyper\-V-Switch-Port aktivieren.

**Anzeigen der aktuellen Einstellungen:**

```PowerShell
Get-VMNetworkAdapter <vm-name> | fl

Get-VMNetworkAdapter -ManagementOS | fl
```
    
Beide der folgenden Einstellungen sollten " **true**" lauten. 

- Vrssenabledrequessiert: true
- Vrssaktivierte: true
    
>[!IMPORTANT]
>Unter einigen Ressourcen Einschränkungs Bedingungen kann es vorkommen, dass diese Funktion für einen virtuellen Hyper\-V-Switchport nicht aktiviert ist. Dies ist eine temporäre Bedingung, und die Funktion kann zu einem späteren Zeitpunkt verfügbar werden.
>
>Wenn " **vrssaktivierte** " den Wert " **true**" hat, wird das Feature für diesen virtuellen Hyper\-V-Switchport aktiviert, d. –. für diese VM oder vNIC.

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
> Das Festlegen des Profils innerhalb der VM wirkt sich nicht auf die Planung der Arbeit aus. Hyper\-V trifft alle Planungsentscheidungen und ignoriert das Profil innerhalb der VM.

## <a name="disable-vrss"></a>Deaktivieren von vrss

Sie können vrss deaktivieren, um die zuvor erwähnten Einstellungen zu deaktivieren.

- Deaktivieren Sie VMQ für die physische NIC oder den virtuellen Computer.

  >[!CAUTION]
  >Die Deaktivierung von VMQ auf der physischen NIC wirkt sich schwerwiegend auf die Fähigkeit Ihres Hyper\-V-Hosts aus, eingehende Pakete zu verarbeiten.

- Deaktivieren Sie vrss für einen virtuellen Computer auf dem Hyper-v-\-v-Switch auf dem Hyper\-v-Host.

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled $FALSE
   ```

- Deaktivieren Sie vrss für eine Host-vNIC auf dem Hyper\-v-Switch für virtuelle Switches auf dem Hyper\-v-Host.

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $FALSE
   ```

- Deaktivieren Sie RSS auf der VM-\(oder Host-vNIC\) innerhalb der VM \(oder auf dem Host\)

   ```PowerShell
   Disable-NetAdapterRSS *
   ```
