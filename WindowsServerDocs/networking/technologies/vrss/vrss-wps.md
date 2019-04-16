---
title: Windows PowerShell-Befehlen für RSS- und vRSS
description: In diesem Thema erfahren Sie, wie Sie schnell technische Informationen zu Windows PowerShell-Befehlen für erhalten Seite Skalierung (RSS) und virtuelle RSS (vRSS) zu finden.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 49e93b9f-46d9-4cee-bcda-1c4634893ddd
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/05/2018
ms.openlocfilehash: 10039388009e32c10d71067b835bad65db5607ef
ms.sourcegitcommit: 9ed4c9fe04ebf3ef488170503c9a354c992b6fde
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/03/2018
ms.locfileid: "4339268"
---
# Windows PowerShell-Befehlen für RSS- und vRSS

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie, wie schnell technische Informationen zu Windows PowerShell-Befehlen für virtuelle RSS-\(vRSS\) und Receive Side Scaling \(RSS\) finden.

Verwenden Sie die folgenden RSS-Befehle, um RSS auf einem physischen Computer mit mehreren Prozessoren oder mehreren Kernen konfigurieren. Sie können die gleichen Befehle verwenden, um vRSS auf einem virtuellen Computer konfigurieren \(VM\), die ein unterstütztes Betriebssystem ausgeführt wird. Weitere Informationen finden Sie unter [Netzwerkadapter-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps).

## Konfigurieren von VMQ

vRSS erfordert, dass VMQ aktiviert und konfiguriert ist. Sie können die folgenden Windows PowerShell-Befehle zum Verwalten von VMQ Einstellungen verwenden.

- [Disable-NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/disable-netadaptervmq?view=win10-ps)
- [Enable-NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/enable-netadaptervmq?view=win10-ps)
- [Get-NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/get-netadaptervmq?view=win10-ps)
- [Set-NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/set-netadaptervmq?view=win10-ps)

## Aktivieren und Konfigurieren von RSS auf einen nativen host

Verwenden Sie die folgenden PowerShell-Befehle konfigurieren RSS auf einen nativen Host als auch verwalten RSS auf einem virtuellen Computer oder auf einem Host virtuelle Netzwerkkarte (vNIC). Einige der Parameter für diese Befehle möglicherweise auch Warteschlange des virtuellen Computers \(VMQ\) auf dem Hyper-V-Host betreffen.  

>[!IMPORTANT]
>Aktivieren von RSS auf einem virtuellen Computer oder auf einem Host-vNIC ist eine Voraussetzung für aktivieren und Verwenden von vRSS.

- [Disable-NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/disable-netadapterrss?view=win10-ps)
- [Enable-NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/enable-netadapterrss?view=win10-ps)
- [Get-NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/get-netadapterrss?view=win10-ps)
- [Set-NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterRss?view=win10-ps)

## Aktivieren Sie vRSS auf dem Hyper-V Virtual Switch-port

Zusätzlich zur RSS auf dem virtuellen Computer aktivieren, erfordert vRSS, vRSS auf dem Hyper-V Virtual Switch-Port zu aktivieren. 

Ermitteln Sie die vorhanden Einstellungen für vRSS und aktivieren Sie oder deaktivieren Sie die Funktion für einen virtuellen Computer.

   **Zeigen Sie die aktuellen Einstellungen:** 

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | fl
   ```

   **Aktiviert das Feature:**
   
   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled [$True|$False]
   ```

## Aktivieren oder Deaktivieren von vRSS auf einem Host-vNIC

Ermitteln Sie die vorhanden Einstellungen für vRSS, und aktivieren Sie oder deaktivieren Sie die Funktion für eine Host-vNIC.

   **Zeigen Sie die aktuellen Einstellungen:** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | fl
   ```

   **Aktivieren Sie oder deaktivieren Sie die Funktion:** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled [$True|$False]
   ```

## Konfigurieren des Planung Modus auf dem Hyper-V virtual Switch-port 
>Gilt für: WindowsServer 2019

In Windows Server 2019 können vRSS logischen Prozessoren zum Verarbeiten des Netzwerkverkehrs dynamisch aktualisieren.  Geräte mit unterstützten Treiber verfügen diese scheduling Modus standardmäßig aktiviert. 

Bestimmen des vorhanden scheduling Modus auf einem System, oder ändern Sie den scheduling Modus für einen virtuellen Computer.

   **Zeigen Sie die aktuellen Einstellungen:** 

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | Select 'VRSSQueue'
   ```

   **Festlegen oder Ändern des Planung Modus:**

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```

## Konfigurieren des Planung Modus auf einem Host-vNIC
>Gilt für: WindowsServer 2019

Den vorhanden scheduling Modus ermittelt oder den scheduling Modus für eine Host-vNIC ändern, verwenden Sie die folgenden Windows PowerShell-Befehle:

   **Zeigen Sie die aktuellen Einstellungen:** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | Select 'VRSSQueue'
   ```

   **Festlegen oder Ändern des Planung Modus:** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssQueueSchedulingMode -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```


## Verwandte Themen 
Weitere Informationen finden Sie unter den folgenden Themen.

- [Get-VMNetworkAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmnetworkadapter)
- [Set-VMNetworkAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/set-vmnetworkadapter)

Weitere Informationen finden Sie in der [Virtual Receive Side Scaling (vRSS)](vrss-top.md).