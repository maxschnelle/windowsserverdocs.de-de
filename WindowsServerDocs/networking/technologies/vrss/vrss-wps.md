---
title: Windows PowerShell-Befehle für RSS und vrss
description: In diesem Thema erfahren Sie, wie Sie technische Referenzinformationen zu Windows PowerShell-Befehlen für die Empfangs seitige Skalierung (Receive Side Scaling, RSS) und Virtual RSS (vrss) schnell finden.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 49e93b9f-46d9-4cee-bcda-1c4634893ddd
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/05/2018
ms.openlocfilehash: bb915f72e53d28c73a9c2e405b3b0edd656953db
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405279"
---
# <a name="windows-powershell-commands-for-rss-and-vrss"></a>Windows PowerShell-Befehle für RSS und vrss

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie technische Referenzinformationen zu Windows PowerShell-Befehlen für die Empfangs seitige Skalierung \(RSS\) und virtuellen RSS \(vrss-\)schnell finden.

Verwenden Sie die folgenden RSS-Befehle, um RSS auf einem physischen Computer mit mehreren Prozessoren oder mehreren Kernen zu konfigurieren. Sie können die gleichen Befehle zum Konfigurieren von vrss auf einem virtuellen Computer \(VM-\) verwenden, auf dem ein unterstütztes Betriebssystem ausgeführt wird. Weitere Informationen finden Sie unter [Netzwerk Adapter-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps).

## <a name="configure-vmq"></a>Konfigurieren von VMQ

vrss erfordert, dass VMQ aktiviert und konfiguriert ist. Sie können die folgenden Windows PowerShell-Befehle verwenden, um VMQ-Einstellungen zu verwalten.

- [Deaktivieren von-netadaptervmq](https://docs.microsoft.com/powershell/module/netadapter/disable-netadaptervmq?view=win10-ps)
- [Enable-netadaptervmq](https://docs.microsoft.com/powershell/module/netadapter/enable-netadaptervmq?view=win10-ps)
- [Get-netadaptervmq](https://docs.microsoft.com/powershell/module/netadapter/get-netadaptervmq?view=win10-ps)
- [Set-netadaptervmq](https://docs.microsoft.com/powershell/module/netadapter/set-netadaptervmq?view=win10-ps)

## <a name="enable-and-configure-rss-on-a-native-host"></a>Aktivieren und Konfigurieren von RSS auf einem nativen Host

Verwenden Sie die folgenden PowerShell-Befehle, um RSS auf einem nativen Host zu konfigurieren und RSS auf einem virtuellen Computer oder auf einer virtuellen Host-NIC (VNIC) zu verwalten. Einige der Parameter dieser Befehle können sich auch auf Warteschlange für virtuelle Computer \(VMQ-\) auf dem Hyper-V-Host auswirken.  

>[!IMPORTANT]
>Das Aktivieren von RSS auf einem virtuellen Computer oder auf einer Host-vNIC ist eine Voraussetzung für die Aktivierung und Verwendung von vrss.

- [Deaktivieren Sie-netadapterrss.](https://docs.microsoft.com/powershell/module/netadapter/disable-netadapterrss?view=win10-ps)
- [Enable-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/enable-netadapterrss?view=win10-ps)
- [Get-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/get-netadapterrss?view=win10-ps)
- [Set-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterRss?view=win10-ps)

## <a name="enable-vrss-on-the-hyper-v-virtual-switch-port"></a>Aktivieren von vrss auf dem Port des virtuellen Hyper\-V-Switches

Zusätzlich zur Aktivierung von RSS auf dem virtuellen Computer erfordert vrss, dass Sie vrss auf dem virtuellen Hyper\-V-Switchport aktivieren. 

Bestimmen Sie die aktuellen Einstellungen für vrss, und aktivieren oder deaktivieren Sie die Funktion für eine VM.

   **Anzeigen der aktuellen Einstellungen:** 

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | fl
   ```

   **Aktiviert das Feature:**
   
   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled [$True|$False]
   ```

## <a name="enable-or-disable-vrss-on-a-host-vnic"></a>Aktivieren oder Deaktivieren von vrss auf einer Host-vNIC

Bestimmen Sie die aktuellen Einstellungen für vrss, und aktivieren oder deaktivieren Sie die Funktion für eine Host-vNIC.

   **Anzeigen der aktuellen Einstellungen:** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | fl
   ```

   **Aktivieren oder Deaktivieren der Funktion:** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled [$True|$False]
   ```

## <a name="configure-the-scheduling-mode-on-the-hyper-v-virtual-switch-port"></a>Konfigurieren des Planungsmodus auf dem virtuellen Hyper-V-Switchport 
>Gilt für: Windows Server 2019

In Windows Server 2019 kann vrss die logischen Prozessoren aktualisieren, die für die dynamische Verarbeitung des Netzwerk Datenverkehrs verwendet werden.  Für Geräte mit unterstützten Treibern ist dieser Planungsmodus standardmäßig aktiviert. 

Bestimmen Sie den aktuellen Planungsmodus auf einem System, oder ändern Sie den Planungsmodus für eine VM.

   **Anzeigen der aktuellen Einstellungen:** 

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | Select 'VRSSQueue'
   ```

   **Legen Sie den Planungsmodus fest, oder ändern Sie ihn:**

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```

## <a name="configure-the-scheduling-mode-on-a-host-vnic"></a>Konfigurieren des Planungsmodus auf einer Host-vNIC
>Gilt für: Windows Server 2019

Verwenden Sie die folgenden Windows PowerShell-Befehle, um den aktuellen Planungsmodus zu bestimmen oder den Planungsmodus für eine Host-vNIC zu ändern:

   **Anzeigen der aktuellen Einstellungen:** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | Select 'VRSSQueue'
   ```

   **Legen Sie den Planungsmodus fest, oder ändern Sie ihn:** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssQueueSchedulingMode -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```


## <a name="related-topics"></a>Verwandte Themen 
Weitere Informationen finden Sie in den folgenden Referenz Themen.

- [Get-vmnetworkadapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmnetworkadapter)
- [Set-vmnetworkadapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/set-vmnetworkadapter)

Weitere Informationen finden Sie unter [virtuelle Empfangs seitige Skalierung (Virtual Receive Side Scaling, vrss)](vrss-top.md).