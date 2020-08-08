---
title: Konfigurieren und Anzeigen von VLAN-Einstellungen für virtuelle Hyper-V-Switchports
description: In diesem Thema erfahren Sie mehr über bewährte Methoden zum Konfigurieren und Anzeigen von Einstellungen für virtuelle lokale Netzwerke (VLAN) auf einem virtuellen Hyper-V-Switchport in Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 69e0e28a-98ae-4ade-bd27-ce2ad7eb310f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ac7d3f4ea17e35b42d974d1e29c692e8510c35ef
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87995701"
---
# <a name="configure-and-view-vlan-settings-on-hyper-v-virtual-switch-ports"></a>Konfigurieren und Anzeigen von VLAN-Einstellungen für virtuelle Hyper-V-Switchports

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema finden Sie bewährte Methoden zum Konfigurieren und Anzeigen von Einstellungen für virtuelle lokale Netzwerke (VLAN) auf einem virtuellen Hyper-V-Switchport.

Wenn Sie VLAN-Einstellungen auf virtuellen Hyper-v-Switchports konfigurieren möchten, können Sie entweder Windows &reg; Server 2016 Hyper-v-Manager oder System Center Virtual Machine Manager (VMM) verwenden.

Wenn Sie VMM verwenden, verwendet VMM den folgenden Windows PowerShell-Befehl, um den Switchport zu konfigurieren.

```
Set-VMNetworkAdapterIsolation <VM-name|-managementOS> -IsolationMode VLAN -DefaultIsolationID <vlan-value> -AllowUntaggedTraffic $True
```
Wenn Sie VMM nicht verwenden und den Switchport in Windows Server konfigurieren, können Sie die Hyper-V-Manager-Konsole oder den folgenden Windows PowerShell-Befehl verwenden.
```
Set-VMNetworkAdapterVlan <VM-name|-managementOS> -Access -VlanID <vlan-value>
```

Aufgrund dieser zwei Methoden zum Konfigurieren der VLAN-Einstellungen auf virtuellen Hyper-V-Switchports ist es möglich, dass beim Versuch, die Einstellungen für den Switchport anzuzeigen, angezeigt wird, dass die VLAN-Einstellungen nicht konfiguriert sind, auch wenn Sie konfiguriert sind.

## <a name="use-the-same-method-to-configure-and-view-switch-port-vlan-settings"></a>Verwenden Sie dieselbe Methode, um Switchport-VLAN-Einstellungen zu konfigurieren und anzuzeigen.

Um sicherzustellen, dass diese Probleme nicht auftreten, müssen Sie die gleiche Methode zum Anzeigen der VLAN-Einstellungen für den Switchport verwenden, die Sie zum Konfigurieren der VLAN-Einstellungen für den Switchport verwendet haben.

Gehen Sie folgendermaßen vor, um die Port Einstellungen für den VLAN-Switch zu konfigurieren und anzuzeigen:

- Wenn Sie VMM oder den Netzwerk Controller zum Einrichten und Verwalten Ihres Netzwerks verwenden und Sie Software-Defined Networking (SDN) bereitgestellt haben, müssen Sie die **vmnetworkadapterisolation** -Cmdlets verwenden.
- Wenn Sie Windows Server 2016 Hyper-V-Manager oder Windows PowerShell-Cmdlets verwenden und keine Software-Defined Networking (SDN) bereitgestellt haben, müssen Sie die **vmnetworkadaptervlan** -Cmdlets verwenden.

### <a name="possible-issues"></a>Mögliche Probleme

Wenn Sie diese Richtlinien nicht befolgen, stoßen Sie möglicherweise auf die folgenden Probleme.

- In Fällen, in denen Sie Sdn bereitgestellt haben und VMM, Network Controller oder die **vmnetworkadapterisolation** -Cmdlets verwenden, um VLAN-Einstellungen auf einem virtuellen Hyper-v-Switchport zu konfigurieren: Wenn Sie den Hyper-v-Manager verwenden oder **vmnetworkadaptervlan** zum Anzeigen der Konfigurationseinstellungen verwenden, werden die VLAN-Einstellungen in der Stattdessen müssen Sie das Cmdlet **Get-vmnetworkisolation** verwenden, um die VLAN-Einstellungen anzuzeigen.
- In Fällen, in denen Sie keinen Sdn bereitgestellt haben und stattdessen die VLAN-Einstellungen mithilfe des Hyper-v-Managers oder der **vmnetworkadaptervlan** -Cmdlets auf einem virtuellen Hyper-V-Switchport konfigurieren: Wenn Sie das **Get-vmnetworkisolation** -Cmdlet zum Anzeigen der Konfigurationseinstellungen verwenden, werden die VLAN-Einstellungen in der Befehlsausgabe Stattdessen müssen Sie das Cmdlet **Get vmnetworkadaptervlan** verwenden, um die VLAN-Einstellungen anzuzeigen.

Es ist auch wichtig, nicht zu versuchen, dieselben VLAN-Einstellungen für den Switchport mithilfe beider Konfigurations Methoden zu konfigurieren. Wenn Sie dies tun, ist der Switchport falsch konfiguriert, und das Ergebnis ist möglicherweise ein Fehler bei der Netzwerkkommunikation.

### <a name="resources"></a>Ressourcen

Weitere Informationen zu den in diesem Thema erwähnten Windows PowerShell-Befehlen finden Sie in den folgenden Themen:

- [Set-vmnetworkadapterisolation](/powershell/module/hyper-v/set-vmnetworkadapterisolation?view=win10-ps)
- [Get-vmnetworkadapterisolation](/powershell/module/hyper-v/get-vmnetworkadapterisolation?view=win10-ps)
- [Set-vmnetworkadaptervlan](/powershell/module/hyper-v/set-vmnetworkadaptervlan?view=win10-ps)
- [Get-vmnetworkadaptervlan](/powershell/module/hyper-v/get-vmnetworkadaptervlan?view=win10-ps)