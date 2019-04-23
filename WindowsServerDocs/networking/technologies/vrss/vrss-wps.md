---
title: Windows PowerShell-Befehle für RSS und vRSS
description: In diesem Thema erfahren Sie, wie ein, um technische Referenzinformationen zu Windows PowerShell-Befehle für erhalten empfangsseitige Skalierung (RSS) und virtuelle RSS (vRSS) schnell zu finden.
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833261"
---
# <a name="windows-powershell-commands-for-rss-and-vrss"></a>Windows PowerShell-Befehle für RSS und vRSS

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema erfahren Sie, wie Sie schnell von technischen Referenzinformationen zu Windows PowerShell-Befehle für die empfangsseitige Skalierung \(RSS\) und virtuelle \(vRSS\).

Verwenden Sie die folgenden RSS-Befehle, um RSS auf einem physischen Computer mit mehreren Prozessoren oder mehreren Kernen zu konfigurieren. Sie können die gleichen Befehle verwenden, so konfigurieren Sie vRSS auf einem virtuellen Computer \(VM\) , ein unterstütztes Betriebssystem ausgeführt wird. Weitere Informationen finden Sie unter [Netzwerkadapter-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps).

## <a name="configure-vmq"></a>Konfigurieren der VMQ

vRSS erfordert, dass VMQ aktiviert und konfiguriert ist. Sie können folgende Windows PowerShell-Befehle verwenden, um VMQ-Einstellungen zu verwalten.

- [Disable-NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/disable-netadaptervmq?view=win10-ps)
- [Enable-NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/enable-netadaptervmq?view=win10-ps)
- [Get-NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/get-netadaptervmq?view=win10-ps)
- [Set-NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/set-netadaptervmq?view=win10-ps)

## <a name="enable-and-configure-rss-on-a-native-host"></a>Aktivieren und Konfigurieren von RSS auf ein nativer host

Verwenden Sie die folgenden PowerShell-Befehle zum Konfigurieren von RSS für ein nativer Host sowie zum Verwalten von RSS, die auf einem virtuellen Computer oder auf einem Host virtuelle Netzwerkkarte (vNIC). Einige der Parameter für diese Befehle beeinträchtigt auch die Warteschlange für virtuelle Maschinen \(VMQ\) auf dem Hyper-V-Host.  

>[!IMPORTANT]
>Aktivieren von RSS, die auf einem virtuellen Computer oder auf einen Host-vNIC ist eine Voraussetzung für die Aktivierung und Verwendung von vRSS.

- [Disable-NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/disable-netadapterrss?view=win10-ps)
- [Enable-NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/enable-netadapterrss?view=win10-ps)
- [Get-NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/get-netadapterrss?view=win10-ps)
- [Set-NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterRss?view=win10-ps)

## <a name="enable-vrss-on-the-hyper-v-virtual-switch-port"></a>Aktivieren Sie vRSS auf dem Hyper\-V Virtual Switch Port

Zusätzlich zum Aktivieren von RSS auf dem virtuellen Computer müssen vRSS, müssen Sie vRSS auf dem Hyper aktivieren\-virtuellen V-Switchport. 

Ermitteln der Einstellungen für die vorhanden für vRSS und aktivieren oder deaktivieren Sie das Feature für einen virtuellen Computer.

   **Zeigen Sie die aktuellen Einstellungen an:** 

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | fl
   ```

   **Die Funktion aktiviert:**
   
   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled [$True|$False]
   ```

## <a name="enable-or-disable-vrss-on-a-host-vnic"></a>Aktivieren Sie oder deaktivieren Sie vRSS auf einen Host-vNIC

Ermitteln der Einstellungen für die vorhanden für vRSS, und aktivieren oder deaktivieren Sie das Feature für einen Host-vNIC.

   **Zeigen Sie die aktuellen Einstellungen an:** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | fl
   ```

   **Aktivieren Sie oder deaktivieren Sie des Features:** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled [$True|$False]
   ```

## <a name="configure-the-scheduling-mode-on-the-hyper-v-virtual-switch-port"></a>Konfigurieren Sie den scheduling-Modus auf dem virtuellen Hyper-V-Switchport 
>Gilt für: Windows Server 2019

In Windows Server-2019 können vRSS die logischen Prozessoren verwendet, um die Netzwerkdatenverkehr zu verarbeiten, dynamisch aktualisieren.  Geräte mit unterstützten Treibern haben dieser Planung Modus standardmäßig aktiviert. 

Bestimmen der vorhanden scheduling-Modus auf einem System, oder ändern Sie den Modus der Planung für einen virtuellen Computer.

   **Zeigen Sie die aktuellen Einstellungen an:** 

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | Select 'VRSSQueue'
   ```

   **Festlegen Sie oder ändern Sie den scheduling-Modus:**

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```

## <a name="configure-the-scheduling-mode-on-a-host-vnic"></a>Konfigurieren Sie den scheduling-Modus auf einen Host-vNIC
>Gilt für: Windows Server 2019

Um zu bestimmen, den vorhanden scheduling-Modus oder den scheduling-Modus für einen Host-vNIC zu ändern, verwenden Sie die folgenden Windows PowerShell-Befehle:

   **Zeigen Sie die aktuellen Einstellungen an:** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | Select 'VRSSQueue'
   ```

   **Festlegen Sie oder ändern Sie den scheduling-Modus:** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssQueueSchedulingMode -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```


## <a name="related-topics"></a>Verwandte Themen 
Weitere Informationen finden Sie unter den folgenden Referenzthemen.

- [Get-VMNetworkAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmnetworkadapter)
- [Set-VMNetworkAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/set-vmnetworkadapter)

Weitere Informationen finden Sie unter [virtuelle empfangsseitige Skalierung (vRSS)](vrss-top.md).