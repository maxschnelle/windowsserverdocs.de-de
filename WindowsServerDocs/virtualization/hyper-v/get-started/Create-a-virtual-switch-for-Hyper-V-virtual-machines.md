---
title: Erstellen eines virtuellen Switches für virtuelle Hyper-V-Computer
description: Enthält Anweisungen zum Erstellen eines virtuellen Switches mit dem Hyper-V-Manager oder Windows PowerShell.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: fdc8063c-47ce-4448-b445-d7ff9894dc17
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: f1a814060e763545411b5c4345367638a5161ac2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392923"
---
# <a name="create-a-virtual-switch-for-hyper-v-virtual-machines"></a>Erstellen eines virtuellen Switches für virtuelle Hyper-V-Computer

>Gilt für: Windows 10, Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019
  
Mit einem virtuellen Switch können virtuelle Maschinen, die auf Hyper-V-Hosts erstellt wurden, mit anderen Computern kommunizieren. Wenn Sie die Hyper-V-Rolle unter Windows Server installieren, können Sie einen virtuellen Switch erstellen. Verwenden Sie zum Erstellen zusätzlicher virtueller Switches den Hyper-V-Manager oder Windows PowerShell. Weitere Informationen zu virtuellen Switches finden Sie unter [virtueller Hyper-V-Switch](../../hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md).  
  
Das Netzwerk virtueller Computer kann ein komplexer Betreff sein. Außerdem gibt es mehrere neue Features für virtuelle Switches, die Sie verwenden können, wie z. b. [Switch Embedded Teaming (Set)](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md#switch-embedded-teaming-set). Das grundlegende Netzwerk ist jedoch relativ einfach. Dieses Thema behandelt genau genug, sodass Sie vernetzte virtuelle Maschinen in Hyper-V erstellen können. Weitere Informationen zum Einrichten der Netzwerkinfrastruktur finden Sie in der Dokumentation zum [Netzwerk](../../../networking/Networking.md) .   
  
## <a name="create-a-virtual-switch-by-using-hyper-v-manager"></a>Erstellen eines virtuellen Switches mit dem Hyper-V-Manager  
  
1.  Öffnen Sie Hyper-v-Manager, und wählen Sie den Computernamen des Hyper-v-Hosts aus.  
  
2.  Wählen Sie **Action** > **Virtual Switch Manager**aus.  
  
    ![Screenshot, der die Menü Options Aktion > Virtual Switch Manager anzeigt](../media/Hyper-V-Action-VSwitchManager.png)  
  
3.  Wählen Sie den gewünschten virtuellen Switch aus.  
  
    |Verbindungstyp|Beschreibung|  
    |-------------------|---------------|  
    |Extern|Ermöglicht virtuellen Computern den Zugriff auf ein physisches Netzwerk, um mit Servern und Clients in einem externen Netzwerk zu kommunizieren. Ermöglicht, dass virtuelle Maschinen auf demselben Hyper-V-Server miteinander kommunizieren können.|  
    |Intern|Ermöglicht die Kommunikation zwischen virtuellen Maschinen auf demselben Hyper-V-Server und zwischen den virtuellen Computern und dem Verwaltungs Host Betriebssystem.|  
    |Private|Ermöglicht nur die Kommunikation zwischen virtuellen Maschinen auf demselben Hyper-V-Server. Ein privates Netzwerk ist vom gesamten externen Netzwerk Datenverkehr auf dem Hyper-V-Server isoliert. Diese Art von Netzwerk ist nützlich, wenn Sie eine isolierte Netzwerkumgebung wie eine isolierte Test Domäne erstellen müssen.|  
  
4.  Wählen Sie **virtuellen Switch erstellen**aus.  
  
5.  Fügen Sie einen Namen für den virtuellen Switch hinzu.  
  
6.  Wenn Sie extern auswählen, wählen Sie den Netzwerkadapter (NIC) aus, den Sie verwenden möchten, sowie alle weiteren Optionen, die in der folgenden Tabelle beschrieben werden.  
  
    ![Screenshot mit den externen Netzwerkoptionen](../media/Hyper-V-NewVSwitch-ExternalOptions.png)  
  
    |Einstellungsname|Beschreibung|  
    |----------------|---------------|  
    |Gemeinsames Verwenden dieses Netzwerkadapters für das Verwaltungsbetriebssystem zulassen|Wählen Sie diese Option aus, wenn Sie zulassen möchten, dass der Hyper-V-Host die Verwendung des virtuellen Switches und der NIC bzw. des NIC-Teams mit dem virtuellen Computer gemeinsam verwenden kann. Wenn dieses Feature aktiviert ist, kann der Host jede der Einstellungen verwenden, die Sie für den virtuellen Switch konfigurieren, wie z. b. Quality of Service Einstellungen (QoS), Sicherheitseinstellungen oder andere Features des virtuellen Hyper-V-Switches.|  
    |Aktivieren einer e/a-Virtualisierung mit Einzel Stamm (SR-IOV)|Wählen Sie diese Option nur aus, wenn Sie zulassen möchten, dass der virtuelle Computer den Switch der virtuellen Maschine umgeht und direkt zur physischen NIC wechselt. Weitere Informationen finden Sie unter [Single-root-e/a-Virtualisierung](https://technet.microsoft.com/library/dn641211.aspx#Sec4) in der Poster-Begleit Referenz: Hyper-V-Netzwerke.|  
  
7.  Wenn Sie Netzwerk Datenverkehr vom Betriebssystem des Verwaltungs-Hyper-V-Hosts oder von anderen virtuellen Computern, die denselben virtuellen Switch verwenden, isolieren möchten, wählen Sie **virtuelle LAN-Identifizierung für Verwaltungs Betriebssystem aktivieren aus**. Sie können die VLAN-ID in eine beliebige Zahl ändern oder die Standardeinstellung überlassen. Dies ist die virtuelle LAN-ID, die vom Verwaltungs Betriebssystem für die gesamte Netzwerkkommunikation über diesen virtuellen Switch verwendet wird.  
  
    ![Screenshot, der die VLAN-ID-Optionen anzeigt](../media/Hyper-V-NewSwitch-VLAN.png)  
  
8.  Klicken Sie auf **OK**.  
  
9. Klicken Sie auf **Ja**.  
  
    ![Screenshot mit der Meldung "ausstehende Änderungen können die Netzwerk Konnektivität stören"](../media/Hyper-V-NewVSwitch-DisruptNetwork.png)  
  
## <a name="create-a-virtual-switch-by-using-windows-powershell"></a>Erstellen eines virtuellen Switches mithilfe von Windows PowerShell  
  
1.  Klicken Sie auf dem Windows-Desktop auf die Schaltfläche „Start“, und geben Sie einen beliebigen Teil des Namens **Windows PowerShell** ein.  
  
2.  Klicken Sie mit der rechten Maustaste auf Windows PowerShell, und wählen Sie **als Administrator ausführen**.  
  
3.  Suchen Sie nach vorhandenen Netzwerkadaptern, indem Sie das Cmdlet " [Get-netadapter](https://technet.microsoft.com/library/jj130867.aspx) " ausführen. Notieren Sie sich den Namen des Netzwerkadapters, den Sie für den virtuellen Switch verwenden möchten.  
  
    ```  
    Get-NetAdapter  
    ```  
  
4.  Erstellen Sie einen virtuellen Switch mithilfe des Cmdlets [New-VMSwitch](https://technet.microsoft.com/library/hh848455.aspx) . Führen Sie beispielsweise den folgenden Befehl aus, um einen externen virtuellen Switch mit dem Namen externalswitch zu erstellen, indem Sie den Ethernet-Netzwerkadapter verwenden und das **Verwaltungs Betriebssystem zulassen, dass dieser Netzwerkadapter** aktiviert ist.  
  
    ```  
    New-VMSwitch -name ExternalSwitch  -NetAdapterName Ethernet -AllowManagementOS $true  
    ```  
  
    Führen Sie den folgenden Befehl aus, um einen internen Switch zu erstellen.  
  
    ```  
    New-VMSwitch -name InternalSwitch -SwitchType Internal  
    ```  
  
    Führen Sie den folgenden Befehl aus, um einen privaten Switch zu erstellen.  
  
    ```  
    New-VMSwitch -name PrivateSwitch -SwitchType Private  
    ```  
  
Erweiterte Windows PowerShell-Skripts, die verbesserte oder neue virtuelle Switchfeatures in Windows Server 2016 abdecken, finden Sie unter [Remote Direct Memory Access und Switch Embedded Teaming](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).  

  
## <a name="next-step"></a>Nächster Schritt  
[Erstellen eines virtuellen Computers in Hyper-V](Create-a-virtual-machine-in-Hyper-V.md)  
  


