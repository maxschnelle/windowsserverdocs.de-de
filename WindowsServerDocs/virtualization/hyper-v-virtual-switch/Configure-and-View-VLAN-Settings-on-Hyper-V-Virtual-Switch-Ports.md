---
title: Konfigurieren und Anzeigen von VLAN-Einstellungen für virtuelle Hyper-V-Switchports
description: Sie können in diesem Thema verwenden, um bewährte Methoden für die Konfiguration und Anzeige von Einstellungen des virtuellen LAN (VLAN) auf einem virtuellen Hyper-V-Switch Port in Windows Server 2016 zu erfahren.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: article
ms.assetid: 69e0e28a-98ae-4ade-bd27-ce2ad7eb310f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1e4843b0ffee86d728736ae212b953bb7c8552c0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820551"
---
# <a name="configure-and-view-vlan-settings-on-hyper-v-virtual-switch-ports"></a>Konfigurieren und Anzeigen von VLAN-Einstellungen für virtuelle Hyper-V-Switchports

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um bewährte Methoden für die Konfiguration und Anzeige von Einstellungen des virtuellen LAN (VLAN) auf einem virtuellen Hyper-V-Switch Port zu erfahren.

Wenn Sie die VLAN-Einstellungen für virtuelle Hyper-V-Switch-Ports konfigurieren möchten, können Sie entweder Windows&reg; Server 2016 Hyper-V-Manager oder System Center Virtual Machine Manager (VMM).

Wenn Sie VMM verwenden, verwendet VMM die folgenden Windows PowerShell-Befehl den Switchport konfigurieren.

```
Set-VMNetworkAdapterIsolation <VM-name|-managementOS> -IsolationMode VLAN -DefaultIsolationID <vlan-value> -AllowUntaggedTraffic $True
```
Wenn Sie VMM nicht verwenden und den Switchport in Windows Server konfigurieren, können Sie die Hyper-V-Manager-Konsole oder den folgenden Windows PowerShell-Befehl.
```
Set-VMNetworkAdapterVlan <VM-name|-managementOS> -Access -VlanID <vlan-value>
```

Aufgrund dieser zwei Methoden für VLAN-Einstellungen für den virtuellen Hyper-V-Switch-Ports konfigurieren ist es möglich, wenn Sie versuchen, die Switch-Port-Einstellungen anzeigen, es für Sie angezeigt wird, die VLAN-Einstellungen nicht konfiguriert sind, auch wenn sie konfiguriert sind –.

## <a name="use-the-same-method-to-configure-and-view-switch-port-vlan-settings"></a>Verwenden Sie die gleiche Methode zum Konfigurieren und Anzeigen der Switch Port VLAN-Einstellungen

Um sicherzustellen, dass Sie keine dieser Probleme auftreten, müssen Sie dieselbe Methode verwenden, die Switch Port VLAN-Einstellungen anzeigen, die Sie zum Konfigurieren der Switch Port VLAN-Einstellungen verwendet.

Zum Konfigurieren und Anzeigen von VLAN-Switch Port-Einstellungen, gehen Sie folgendermaßen vor:

- Wenn Sie VMM oder den Netzwerkcontroller zum Einrichten und Verwalten Ihres Netzwerks verwenden und Sie Software Defined Networking (SDN) bereitgestellt haben, müssen Sie die **VMNetworkAdapterIsolation** Cmdlets. 
- Wenn Sie Windows Server 2016 Hyper-V-Manager oder Windows PowerShell-Cmdlets verwenden, und Sie keine Software Defined Networking (SDN) bereitgestellt haben, müssen Sie verwenden die **VMNetworkAdapterVlan** Cmdlets.

### <a name="possible-issues"></a>Mögliche Probleme

Wenn Sie diese Richtlinien nicht befolgen können Sie die folgenden Probleme auftreten.

- In Fällen, in dem Sie SDN bereitgestellt haben, und verwenden Sie VMM, Netzwerkcontroller, oder die **VMNetworkAdapterIsolation** Cmdlets zum Konfigurieren von VLAN-Einstellungen auf einem virtuellen Switch für Hyper-V-Port: Wenn Sie Hyper-V-Manager verwenden oder **Get-VMNetworkAdapterVlan** um die Konfigurationseinstellungen anzuzeigen, wird die Ausgabe des Befehls die VLAN-Einstellungen nicht angezeigt. Sie müssen stattdessen die **Get-VMNetworkIsolation** Cmdlet, um die VLAN-Einstellungen anzuzeigen.
- In Fällen, in dem Sie keine SDN bereitgestellt haben, und verwenden Sie stattdessen Hyper-V-Manager, oder das **VMNetworkAdapterVlan** Cmdlets zum Konfigurieren von VLAN-Einstellungen auf einem virtuellen Switch für Hyper-V-Port: Bei Verwendung der **Get-VMNetworkIsolation** Cmdlet, um die Konfigurationseinstellungen anzuzeigen die Ausgabe des Befehls wird die VLAN-Einstellungen nicht angezeigt. Sie müssen stattdessen die **Get-VMNetworkAdapterVlan** Cmdlet, um die VLAN-Einstellungen anzuzeigen.

Es ist auch wichtig, nicht versuchen, die gleichen Switch Port VLAN-Einstellungen mit beiden Konfigurationsmethoden zu konfigurieren. Wenn Sie dies tun, der Switch-Port ist falsch konfiguriert, und das Ergebnis ist möglicherweise ein Fehler bei der Netzwerkkommunikation.

### <a name="resources"></a>Ressourcen

Weitere Informationen zu den Windows PowerShell-Befehlen, die in diesem Thema erwähnt werden, finden Sie hier:

- [Set-VmNetworkAdapterIsolation](https://technet.microsoft.com/library/dn464283.aspx)
- [Get-VmNetworkAdapterIsolation](https://technet.microsoft.com/library/dn464277.aspx)
- [Set-VMNetworkAdapterVlan](https://technet.microsoft.com/library/hh848475.aspx)
- [Get-VMNetworkAdapterVlan](https://technet.microsoft.com/library/hh848516.aspx)





