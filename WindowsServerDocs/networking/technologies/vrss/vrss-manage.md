---
title: Verwalten von vRSS
description: In diesem Thema verwenden Sie die Windows PowerShell-Befehle zum Verwalten von vRSS auf virtuellen Computern (VMs) und auf Hyper-V-Hosts an.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0fe5bfc3-591f-4a19-b98a-0668d4c9f93a
ms.localizationpriority: medium
manager: dougkim
ms.date: 09/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8af800608bee7037b48141a7a2edb0c872a7aac0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856191"
---
# <a name="manage-vrss"></a>Verwalten von vRSS

In diesem Thema verwenden Sie die Windows PowerShell-Befehle zum Verwalten von vRSS auf virtuellen Computern \(VMs\) und auf Hyper\-V-Hosts.

>[!NOTE]
>Weitere Informationen zu den Befehlen in diesem Thema erwähnt, finden Sie unter [Windows PowerShell-Befehle für RSS und vRSS](vrss-wps.md).

## <a name="vmq-on-hyper-v-hosts"></a>VMQ auf dem Hyper-V-Hosts

Auf dem Hyper-V-Host müssen Sie die Schlüsselwörter verwenden, die steuern die VMQ-Prozessoren.

**Zeigen Sie die aktuellen Einstellungen an:** 

```PowerShell
Get-NetAdapterVmq
```

**Konfigurieren Sie die VMQ-Einstellungen:** 

```PowerShell
Set-NetAdapterVmq
```


## <a name="vrss-on-hyper-v-switch-ports"></a>vRSS auf Hyper-V-Switchports

Auf dem Hyper-V-Host müssen Sie auch vRSS auf dem Hyper aktivieren\-virtuellen V-Switchport.

**Zeigen Sie die aktuellen Einstellungen an:**

```PowerShell
Get-VMNetworkAdapter <vm-name> | fl

Get-VMNetworkAdapter -ManagementOS | fl
```
    
Beide der folgenden Einstellungen muss **"true"**. 

- VrssEnabledRequested: True
- VrssEnabled: True
    
>[!IMPORTANT]
>Unter bestimmten Umständen Ressource Einschränkung einem virtuellen Hyper\-virtuellen V-Switchport ist möglicherweise nicht diese Funktion nicht aktiviert haben. Dies ist ein temporäres Problem, und die Funktion zu einem späteren Zeitpunkt möglicherweise verfügbar.
>
>Wenn **VrssEnabled** ist **"true"**, und klicken Sie dann das Feature, für diese Hyper aktiviert ist\-V Virtual Switch Port –, also für diesen virtuellen Computer oder die vNIC.

**Konfigurieren Sie die Porteinstellungen vRSS Switch:**

```PowerShell
Set-VMNetworkAdapter <vm-name> -VrssEnabled $TRUE
    
Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
```

## <a name="vrss-in-vms-and-host-vnics"></a>vRSS auf VMs und Host-vNICs

Sie können die gleichen Befehle, die für das systemeigene RSS verwendet werden, um die Konfigurationseinstellungen vRSS auf VMs und Host-vNICs, das ist auch die Möglichkeit zum Aktivieren von RSS für Host-vNICs.  

**Zeigen Sie die aktuellen Einstellungen an:**

```PowerShell
Get-NetAdapterRSS
```

**Konfigurieren Sie vRSS-Einstellungen:**

```PowerShell
Set-NetAdapterRss
```

>[!NOTE]
> Das Festlegen des Profils innerhalb des virtuellen Computers wirkt sich nicht die Planung der Arbeit. Hyper\-V erleichtert die Planung, Entscheidungen zu treffen und ignoriert das Profil auf dem virtuellen Computer.

## <a name="disable-vrss"></a>Deaktivieren Sie vRSS

Sie können vRSS, um die zuvor genannten Einstellungen deaktivieren, deaktivieren.

- Deaktivieren Sie VMQ, für die physische NIC oder dem virtuellen Computer.

  >[!CAUTION]
  >Deaktivieren VMQ auf dem physischen NIC stark wirkt sich auf die Fähigkeit Ihrer Hyper\-V-Host zum Verarbeiten eingehender Pakete.

- Deaktivieren Sie vRSS für einen virtuellen Computer, auf dem Hyper\-Port die Hyper V-Switches\-V-Host.

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled $FALSE
   ```

- Deaktivieren Sie vRSS für einen Host-vNIC für die Hyper\-Port die Hyper V-Switches\-V-Host.

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $FALSE
   ```

- Deaktivieren von RSS auf dem virtuellen Computer \(oder Host-vNIC\) innerhalb des virtuellen Computers \(oder auf dem Host\)

   ```PowerShell
   Disable-NetAdapterRSS *
   ```
