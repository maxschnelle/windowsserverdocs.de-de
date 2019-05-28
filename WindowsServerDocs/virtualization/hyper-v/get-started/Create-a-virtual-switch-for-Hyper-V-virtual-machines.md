---
title: Erstellen Sie einen virtuellen Switch für Hyper-V-Computer
description: Enthält Anweisungen zum Erstellen eines virtuellen Switches, die mit dem Hyper-V-Manager oder Windows PowerShell
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: fdc8063c-47ce-4448-b445-d7ff9894dc17
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 2668f9fa21c8efbad455d82c7e110ff89b729187
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222869"
---
# <a name="create-a-virtual-switch-for-hyper-v-virtual-machines"></a>Erstellen Sie einen virtuellen Switch für Hyper-V-Computer

>Gilt für: Windows 10, WindowsServer 2016, Microsoft Hyper-V Server 2016, WindowsServer 2019, Microsoft Hyper-V-Server 2019
  
Ein virtueller Switch kann virtuelle Maschinen auf Hyper-V-Hosts, um die Kommunikation mit anderen Computern erstellt werden. Sie können einen virtuellen Switch erstellen, bei der Erstinstallation von Hyper-V-Rolle unter Windows Server. Um zusätzliche virtuelle Switches erstellen zu können, verwenden Sie die Hyper-V-Manager oder Windows PowerShell. Weitere Informationen zu virtuellen Switches finden Sie unter [virtuellen Hyper-V-Switch](../../hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md).  
  
Netzwerk für virtuelle Computer kann es sich um ein komplexes Thema sein. Und es gibt mehrere neue Features des virtuellen Switches, die möglicherweise Sie verwenden, z. B. möchten [Switch Embedded Teaming (SET)](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md#switch-embedded-teaming-set). Aber grundlegende Netzwerke ist recht einfach. Dieses Thema enthält gerade ausreichend, damit Sie in Hyper-V virtuellen Computern im Netzwerk erstellen können. Um weitere Informationen dazu, wie Sie Ihre Netzwerkinfrastruktur einrichten können, überprüfen Sie die [Netzwerke](../../../networking/Networking.md) Dokumentation.   
  
## <a name="create-a-virtual-switch-by-using-hyper-v-manager"></a>Erstellen eines virtuellen Switches mit dem Hyper-V-Manager  
  
1.  Öffnen Sie Hyper-V-Manager, wählen Sie den Computernamen des Hyper-V-Host.  
  
2.  Wählen Sie **Aktion** > **Manager für virtuelle Switches**.  
  
    ![Screenshot mit der Option des Menüs Aktion > Manager für virtuelle Switches](../media/Hyper-V-Action-VSwitchManager.png)  
  
3.  Wählen Sie den Typ des virtuellen Switches, die Sie möchten.  
  
    |Verbindungstyp|Beschreibung|  
    |-------------------|---------------|  
    |Extern|Erhalten Zugriff von virtuellen Computern, auf ein physisches Netzwerk für die Kommunikation mit Servern und Clients in einem externen Netzwerk. Können virtuelle Computer, auf dem gleichen Hyper-V-Server zu kommunizieren.|  
    |Intern|Ermöglicht die Kommunikation zwischen virtuellen Computern, auf dem gleichen Hyper-V-Server sowie zwischen den virtuellen Computern und das Verwaltungsbetriebssystem.|  
    |Private|Lässt nur die Kommunikation zwischen virtuellen Computern, auf dem gleichen Hyper-V-Server. Ein privates Netzwerk ist isoliert vom externen Netzwerkdatenverkehr auf dem Hyper-V-Server. Diese Art des Netzwerks ist nützlich, wenn Sie eine isolierte Netzwerkumgebung, wie eine isolierte Testdomäne erstellen müssen.|  
  
4.  Wählen Sie **Erstellen des virtuellen Switches**.  
  
5.  Fügen Sie einen Namen für den virtuellen Switch hinzu.  
  
6.  Wenn Sie auf "extern" auswählen, wählen Sie den Netzwerkadapter (NIC), den Sie verwenden möchten und alle anderen Optionen, die in der folgenden Tabelle beschriebenen.  
  
    ![Screenshot mit dem externen Netzwerk-Optionen](../media/Hyper-V-NewVSwitch-ExternalOptions.png)  
  
    |Einstellungsname|Beschreibung|  
    |----------------|---------------|  
    |Gemeinsames Verwenden dieses Netzwerkadapters für das Verwaltungsbetriebssystem zulassen|Wählen Sie diese Option, wenn Sie den Hyper-V-Host gemeinsam zu verwenden des virtuellen Switches zulassen möchten, und NIC oder einem NIC-team mit dem virtuellen Computer. Diese Option aktiviert kann der Host verwenden die Einstellungen, die Sie konfigurieren für den virtuellen Switch wie Quality of Service (QoS)-Einstellungen, Sicherheitseinstellungen oder andere Features des virtuellen Hyper-V-Switches.|  
    |Aktivieren Sie Single-Root i/o-Virtualisierung (SR-IOV)|Wählen Sie diese Option nur, wenn Sie Datenverkehr zu Switch der virtuellen Maschine zu umgehen und direkt an die physische NIC virtueller Computer zulassen möchten Weitere Informationen finden Sie unter [Single-Root i/o Virtualization](https://technet.microsoft.com/library/dn641211.aspx#Sec4) in der Referenz zur Begleit-Poster: Hyper-V-Netzwerke.|  
  
7.  Wenn Netzwerkdatenverkehr isoliert von der Verwaltung von Hyper-V-Hostbetriebssystem oder andere virtuelle Maschinen, die den gleichen virtuellen Switch gemeinsam nutzen möchten, wählen Sie **Identifizierung virtuellen LANS für das Verwaltungsbetriebssystem aktivieren**. Die VLAN-ID an eine beliebige Anzahl ändern können oder übernehmen Sie den Standardwert. Dies ist die virtuellen LAN-ID-Nummer, die im Verwaltungsbetriebssystem für die gesamte Netzwerkkommunikation über diesen logischen Switch verwenden.  
  
    ![Screenshot mit der VLAN-ID-Optionen](../media/Hyper-V-NewSwitch-VLAN.png)  
  
8.  Klicken Sie auf **OK**.  
  
9. Klicken Sie auf **Ja**.  
  
    ![Screenshot mit der Meldung "Ausstehende Änderungen kann die Netzwerkkonnektivität unterbrochen"](../media/Hyper-V-NewVSwitch-DisruptNetwork.png)  
  
## <a name="create-a-virtual-switch-by-using-windows-powershell"></a>Erstellen eines virtuellen Switches mithilfe von Windows PowerShell  
  
1.  Klicken Sie auf dem Windows-Desktop auf die Schaltfläche „Start“, und geben Sie einen beliebigen Teil des Namens **Windows PowerShell** ein.  
  
2.  Mit der rechten Maustaste in Windows PowerShell, und wählen Sie **als Administrator ausführen**.  
  
3.  Suchen von vorhandenen Netzwerkadapter mit der [Get-NetAdapter](https://technet.microsoft.com/library/jj130867.aspx) Cmdlet. Notieren Sie sich mit dem Namen der Netzwerk-Adapter, den Sie für den virtuellen Switch verwenden möchten.  
  
    ```  
    Get-NetAdapter  
    ```  
  
4.  Erstellen eines virtuellen Switches mithilfe der [New-VMSwitch](https://technet.microsoft.com/library/hh848455.aspx) Cmdlet. Z. B. einen externen virtuellen Switch mit dem Namen ExternalSwitch, mit der Ethernet-Netzwerkadapter und **ermöglichen gemeinsames Verwenden dieses Netzwerkadapters Verwaltungsbetriebssystem** aktiviert ist, führen Sie den folgenden Befehl.  
  
    ```  
    New-VMSwitch -name ExternalSwitch  -NetAdapterName Ethernet -AllowManagementOS $true  
    ```  
  
    Führen Sie den folgenden Befehl, um einen internen Switch zu erstellen.  
  
    ```  
    New-VMSwitch -name InternalSwitch -SwitchType Internal  
    ```  
  
    Führen Sie den folgenden Befehl, um einen privaten Switch zu erstellen.  
  
    ```  
    New-VMSwitch -name PrivateSwitch -SwitchType Private  
    ```  
  
Erweiterte Windows PowerShell-Skripts, die verbesserte oder einen neuen virtuellen Switch-Funktionen in Windows Server 2016 zu behandeln, finden Sie unter [Remote Direct Memory Access und Switch Embedded Teaming](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).  

  
## <a name="next-step"></a>Nächster Schritt  
[Erstellen eines virtuellen Computers in Hyper-V](Create-a-virtual-machine-in-Hyper-V.md)  
  


