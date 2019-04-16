---
title: Verwalten von vRSS
description: In diesem Thema verwenden Sie die Windows PowerShell-Befehle zum vRSS auf virtuellen Computern (VMs) und Hyper-V-Hosts verwalten.
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
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133836"
---
# Verwalten von vRSS

In diesem Thema verwenden Sie die Windows PowerShell-Befehle zum vRSS in virtuelle Computer \(VMs\) und auf Hyper-V-Hosts verwalten.

>[!NOTE]
>Weitere Informationen zu den Befehlen in diesem Thema genannten finden Sie unter [Windows PowerShell-Befehlen für RSS- und vRSS](vrss-wps.md).

## VMQ auf Hyper-V-Hosts

Auf dem Hyper-V-Host müssen Sie die Schlüsselwörter verwenden, die die VMQ Prozessoren steuern.

**Zeigen Sie die aktuellen Einstellungen an:** 

```PowerShell
Get-NetAdapterVmq
```

**Konfigurieren Sie die VMQ-Einstellungen:** 

```PowerShell
Set-NetAdapterVmq
```


## vRSS auf Hyper-V-Switchports

Auf dem Hyper-V-Host müssen Sie auch vRSS auf dem Hyper-V Virtual Switch-Port aktivieren.

**Zeigen Sie die aktuellen Einstellungen an:**

```PowerShell
Get-VMNetworkAdapter <vm-name> | fl

Get-VMNetworkAdapter -ManagementOS | fl
```
    
Beide der folgenden Einstellungen sollten **"true"** sein. 

- VrssEnabledRequested: True
- VrssEnabled: True
    
>[!IMPORTANT]
>Unter bestimmten Umständen Ressource Einschränkung möglicherweise ein Hyper-V Virtual Switch-Port nicht dieses Feature aktiviert werden. Dies ist ein vorübergehender Zustand, und das Feature möglicherweise zu einem späteren Zeitpunkt zur Verfügung gestellt.
>
>Wenn **VrssEnabled** **"true ist"**, und klicken Sie dann die Funktion für diesen Hyper-V Virtual Switch-Port aktiviert ist – d. h. für diesen virtuellen Computer oder vNIC.

**Konfigurieren Sie die Switch-Port vRSS Einstellungen:**

```PowerShell
Set-VMNetworkAdapter <vm-name> -VrssEnabled $TRUE
    
Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
```

## vRSS im virtuellen Computer und Host-vNICs

Sie können die gleichen Befehle für systemeigene RSS um vRSS um Einstellungen zu konfigurieren in VMs und Host-vNICs, also auch die Möglichkeit zum Aktivieren von RSS auf Host-vNICs verwendet.  

**Zeigen Sie die aktuellen Einstellungen an:**

```PowerShell
Get-NetAdapterRSS
```

**Konfigurieren Sie vRSS Einstellungen:**

```PowerShell
Set-NetAdapterRss
```

>[!NOTE]
> Festlegen des Profils innerhalb des virtuellen Computers hat keinen Einfluss auf die Planung der Arbeit. Hyper-V entscheidet, alle scheduling und das Profil innerhalb des virtuellen Computers ignoriert.

## VRSS deaktivieren

Sie können vRSS zum Deaktivieren von den zuvor genannten Einstellungen deaktivieren.

- Deaktivieren Sie VMQ für der physischen NIC oder den virtuellen Computer.

  >[!CAUTION]
  >Deaktivieren von VMQ auf den physischen wirkt sich auf NIC stark die Fähigkeit von Ihrem Hyper-V-Host, eingehende Pakete zu behandeln.

- Deaktivieren Sie vRSS für einen virtuellen Computer auf dem Hyper-V Virtual Switch-Port auf dem Hyper-V-Host.

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled $FALSE
   ```

- Deaktivieren Sie vRSS für eine Host-vNIC auf dem Hyper-V Virtual Switch-Port auf dem Hyper-V-Host.

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $FALSE
   ```

- Deaktivieren von RSS auf dem virtuellen Computer \(or host vNIC\) innerhalb des virtuellen Computers \ (oder auf die Host\)

   ```PowerShell
   Disable-NetAdapterRSS *
   ```
