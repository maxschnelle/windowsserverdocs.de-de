---
title: Erstellen eines neuen NIC-Teams auf einem Host oder virtuellen Computer
description: In diesem Thema erstellen Sie einen neuen NIC-Teams auf einem Hostcomputer oder in einer Hyper-V-Computer (VM) unter Windows Server 2016.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-nict
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4caaa86-5799-4580-8775-03ee213784a3
ms.author: pashort
author: shortpatti
ms.date: 09/13/2018
ms.openlocfilehash: 3518436f08a0e7fe0ea8fed06724b11df6acccea
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864631"
---
# <a name="create-a-new-nic-team-on-a-host-computer-or-vm"></a>Erstellen eines neuen NIC-Teams auf einem Host oder virtuellen Computer

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema erstellen Sie einen neuen NIC-Teams auf einem Hostcomputer oder in einer Hyper-V-Computer (VM) unter Windows Server 2016.  

## <a name="network-configuration-requirements"></a>Netzwerkanforderungen  
Vor der Erstellung eines neuen NIC-Teams, müssen Sie einen Hyper-V-Host mit zwei Netzwerkadaptern bereitstellen, die mit verschiedenen physischen Switches verbunden sind. Sie müssen auch die Netzwerkadapter mit IP-Adressen konfigurieren, die aus der gleichen IP-Adressbereich stammen.  

Der physische Switch, den virtuellen Hyper-V-Switch, lokale Netzwerk (LAN) und NIC-Teamvorgang von Anforderungen zum Erstellen eines NIC-Teams auf einem virtuellen Computer sind:  
  
-   Der Computer mit Hyper-V muss es sich um mindestens zwei Netzwerkadapter verfügen.  
  
-   Wenn die Netzwerkadapter auf mehrere physische Switches zu verbinden, müssen die physischen Switches im gleichen Schicht-2-Subnetz sein.  
  
-   Sie müssen die Hyper-V-Manager oder Windows PowerShell verwenden, um zwei externer virtueller Hyper-V-Switches zu erstellen, jeweils mit einem anderen physischen Netzwerkadapter verbunden sind.  
  
-   Der virtuelle Computer muss für beide externen virtuellen Switches verbunden, die Sie erstellen.  
  
-   NIC-Teamvorgang Teams mit zwei Membern auf virtuellen Computern, in Windows Server 2016 unterstützt. Sie können größere Teams erstellen, aber wird nicht unterstützt.
  
-   Wenn Sie einen NIC-Teams auf einem virtuellen Computer konfigurieren, müssen Sie auswählen einer **teammodus** von _Switchunabhängig_ und ein **Lastenausgleichsmodus** von _Adresshash_. 



## <a name="step-1-configure-the-physical-and-virtual-network"></a>Schritt 1 Konfigurieren des physischen und virtuellen Netzwerks  
In diesem Verfahren erstellen zwei externer virtueller Hyper-V-Switches, verbinden ein virtuellen Computers mit den Switches, und konfigurieren Sie dann auf die virtuellen Computer Verbindungen mit den Switches.  
 

### <a name="prerequisites"></a>Vorraussetzungen
  
Sie müssen Mitglied **Administratoren**, oder entspricht.  
  
### <a name="procedure"></a>Prozedur
  
1.  Öffnen Sie auf dem Hyper-V-Host, Hyper-V-Manager, und klicken Sie unter Aktionen auf **Manager für virtuelle Switches**.  
  
    ![Manager für virtuelle Switches](../../media/Create-a-New-NIC-Team-in-a-VM/nict_hv.jpg)  
  
2.  Im Manager für virtuelle Switches, stellen Sie sicher, dass **externe** ausgewählt ist, und klicken Sie dann auf **virtuellen Switch erstellen**.  
  
    ![Erstellen des virtuellen Switches](../../media/Create-a-New-NIC-Team-in-a-VM/nict_hv_02.jpg)  
  
3.  Geben Sie in den Eigenschaften für den virtuellen Switch ein **Namen** für das virtuelle wechseln, und fügen **Anmerkungen zu dieser** je nach Bedarf.  
  
4.  In **Verbindungstyp**im **externes Netzwerk**, wählen Sie den physischen Netzwerkadapter, den virtuellen Switch angefügt werden soll.  
  
5.  Konfigurieren Sie zusätzliche Schalter-Eigenschaften für die Bereitstellung, und klicken Sie dann auf **OK**.  
  
6.  Erstellen Sie einen zweite externen virtuellen Switch, indem Sie die vorherigen Schritte wiederholen. Verbinden Sie den zweiten externen Switch auf einen anderen Netzwerkadapter an.  
  
7.  In Hyper-V-Manager unter **VMs**, mit der rechten Maustaste des virtuellen Computers, die Sie konfigurieren möchten, und klicken Sie dann auf **Einstellungen**.<p>Der virtuelle Computer **Einstellungen** Dialogfeld wird geöffnet.  

8.  Stellen Sie sicher, dass der virtuelle Computer nicht gestartet wurde. Wenn es gestartet wurde, führen Sie Herunterfahren, bevor die Konfiguration des virtuellen Computers.  
  
8.  In **Hardware**, klicken Sie auf **Netzwerkadapter**.  
  
    ![Netzwerkkarte](../../media/Create-a-New-NIC-Team-in-a-VM/nict_hvs_01.jpg)  
  
9. In **Netzwerkadapter** Eigenschaften, wählen Sie eine der die virtuellen Switches, die Sie in den vorherigen Schritten erstellt haben, und klicken Sie dann auf **übernehmen**.  
  
    ![Wählen Sie einen virtuellen switch](../../media/Create-a-New-NIC-Team-in-a-VM/nict_hvs_02.jpg)  
  
10. In **Hardware**, klicken Sie auf das Pluszeichen (+) neben erweitern **Netzwerkadapter**. 

11. Klicken Sie auf **erweiterte Features** zum NIC-Teamvorgang aktivieren, indem Sie die grafische Benutzeroberfläche. 

    >[!TIP]
    >Sie können auch mit einem Windows PowerShell-Befehl NIC-Teamvorgang aktivieren: 
    >
    >```PowerShell
    >Set-VMNetworkAdapter -VMName <VMname> -AllowTeaming On
    >```
   
    a. Wählen Sie **dynamische** für MAC-Adresse. 

    b. Klicken Sie auf **geschützten Netzwerk**. 

    c. Klicken Sie auf **aktivieren Sie dieses Netzwerkadapters als Teil eines Teams im Gast-Betriebssystems werden**. 

    d. Klicken Sie auf **OK**.  
  
    ![Fügen Sie einen Netzwerkadapter zu einem team](../../media/Create-a-New-NIC-Team-in-a-VM/nict_hvs_05.jpg)  
  
13. Um einen zweiten Netzwerkadapter, die in Hyper-V-Manager hinzuzufügen **VMs**mit der rechten Maustaste auf den gleichen virtuellen Computer, und klicken Sie dann auf **Einstellungen**.<p>Der virtuelle Computer **Einstellungen** Dialogfeld wird geöffnet.  
  
14. In **Hardware hinzufügen**, klicken Sie auf **Netzwerkadapter**, und klicken Sie dann auf **hinzufügen**.  
  
    ![Fügen Sie einen Netzwerkadapter hinzu.](../../media/Create-a-New-NIC-Team-in-a-VM/nict_hvs_06.jpg)  
  
15. In **Netzwerkadapter** Eigenschaften, wählen Sie den zweiten virtuellen Switch, den Sie in den vorherigen Schritten erstellt haben, und klicken Sie dann auf **übernehmen**.  
  
    ![Wenden Sie einen virtuellen switch](../../media/Create-a-New-NIC-Team-in-a-VM/nict_hvs_07.jpg)  
  
16. In **Hardware**, klicken Sie auf das Pluszeichen (+) neben erweitern **Netzwerkadapter**. 

17. Klicken Sie auf **erweiterte Features**, scrollen Sie zum **NIC-Teamvorgang**, und klicken Sie auf **aktivieren Sie dieses Netzwerkadapters als Teil eines Teams im Gast-Betriebssystems werden**. 

18. Klicken Sie auf **OK**.  
  
_**Herzlichen Glückwunsch!**_  Sie haben die physische und virtuelle Netzwerk konfiguriert.  Jetzt können Sie fortfahren, um das Erstellen eines neuen NIC-Teams.  

## <a name="step-2-create-a-new-nic-team"></a>Schritt 2 Erstellen eines neuen NIC-Teams
  
Bei der Erstellung eines neuen NIC-Teams müssen Sie die NIC-Team-Eigenschaften konfigurieren:  
  
-   Teamname  
  
-   Mitgliederadapter  
  
-   Teammodus  
  
-   Lastenausgleichsmodus  
  
-   Standby-adapter  
  
Sie können optional auch der primären teamschnittstelle konfigurieren und eine Anzahl der virtuellen LAN (VLAN) konfigurieren.  
  
Weitere Informationen zu diesen Einstellungen finden Sie unter [NIC-Teamvorgang-Einstellungen](nic-teaming-settings.md).

### <a name="prerequisites"></a>Vorraussetzungen

Sie müssen Mitglied **Administratoren**, oder entspricht.  
  
### <a name="procedure"></a>Prozedur
  
1.  Klicken Sie im Server-Manager auf **Lokaler Server**.  
  
2.  In der **Eigenschaften** Bereich, in der ersten Spalte gesucht werden soll **NIC-Teamvorgang**, und klicken Sie dann auf die **deaktiviert** Link.<p>Die **NIC-Teamvorgang** Dialogfeld wird geöffnet.<p>![NIC-Teamvorgang (Dialogfeld)](../../media/Create-a-New-NIC-Team/nict_02_nicteaming.jpg)  
  
3.  In **Adapter und Schnittstellen**, wählen Sie eine oder mehrere Netzwerkadapter, die Sie einem NIC-Team hinzufügen möchten.  
  
4.  Klicken Sie auf **Aufgaben**, und klicken Sie auf **hinzufügen für neue Teamprojekte**.<p>Die **neues Team** Dialogfeld wird geöffnet und zeigt an, Netzwerkadapter und Teammitglieder.  
  
5.  In **Teamname**, geben Sie einen Namen für das neue NIC-Team, und klicken Sie dann auf **zusätzliche Eigenschaften**.  
  
6.  In **zusätzliche Eigenschaften**, wählen Sie Werte für:

    - **Teamvorgangsmodus**. Die Optionen für den teammodus sind **Switchunabhängig** und **abhängige Schalter**. Die abhängige Schalter-Modus schließt **statischer Teamvorgang** und **Link Aggregation Control Protocol (LACP)**. 
      
      - **Switch-unabhängig.** [!INCLUDE [switch-independent-shortdesc-include](../../includes/switch-independent-shortdesc-include.md)]
      
      - **Wechseln Sie abhängig.** [!INCLUDE [switch-dependent-shortdesc-include](../../includes/switch-dependent-shortdesc-include.md)] 
      
        | | |
        |---|---|
        |**Statischer Teamvorgang** | Erfordert, dass Sie manuell konfigurieren, sowohl den Switch als auch der Host identifizieren, welche Links das Team bilden. Da es sich um eine statisch konfigurierte Lösung handelt, gibt es kein zusätzliches Protokoll bei den Switch und der Host Identifizierung falsch angeschlossen, Kabel oder anderer Fehler, die das Team zu einem Fehler beim Ausführen verursachen können. Dieser Modus wird im Allgemeinen von Switches der Serverklasse unterstützt. |
        |**Link Aggregation Control Protocol (LACP)** |Im Gegensatz zu statischer Teamvorgang identifiziert LACP-teamvorgangsmodus dynamisch Links, die zwischen dem Host und dem Switch verbunden sind. Diese dynamische Verbindung ermöglicht die automatische Erstellung eines Teams und, theoretisch jedoch selten in der Praxis, Erweiterung und Reduzierung eines Teams einfach durch die Übertragung oder des Empfangs von LACP-Paketen, von der peerentität. Alle Switches der Serverklasse unterstützt LACP, und alle der Netzwerk-Operator, um LACP am Port Switches aktivieren durch den Administrator erfordern. Wenn Sie eine teammodus von LACP konfigurieren, arbeitet der NIC-Teamvorgang immer im aktiven Modus des LACP mit einem kurzen Timer.  Keine Option ist derzeit verfügbar ist, den Timer oder Ändern des LACP-Modus. |
        ---
    
    - **Lastenausgleichsmodus**. Die Optionen des Lastenausgleichs-Verteilungsmodus **Adresshash**, **Hyper-V-Port**, und **dynamische**.
    
       - **Adresshash.** [!INCLUDE [address-hash-shortdesc-include](../../includes/address-hash-shortdesc-include.md)]
       
       - **Hyper-V-Port.** [!INCLUDE [hyper-v-port-shortdesc-include](../../includes/hyper-v-port-shortdesc-include.md)]
       
       - **Dynamic.** [!INCLUDE [dynamic-shortdesc-include](../../includes/dynamic-shortdesc-include.md)]
    
    - **Standby-Adapter**. Die Optionen für die Standby-Adapter sind **keine (alle Adapter aktiv)** oder Ihre Auswahl für einen bestimmten Netzwerkadapter im NIC-Team, die als Standby-Adapter dient.
   
   > [!TIP]  
   > Wenn Sie einen NIC-Teams auf einem virtuellen Computer (VM) konfigurieren, müssen Sie auswählen einer **teammodus** von _Switchunabhängig_ und ein **Lastenausgleichsmodus** von  _Behandeln von Hash_.  
  
7.  Wenn Sie den Schnittstellennamen primären Team konfigurieren oder eine VLAN-Nummer des NIC-Teams zuweisen möchten, klicken Sie auf die Verknüpfung mit der rechten Seite des **primären teamschnittstelle**.<p>Die **neue teamschnittstelle** Dialogfeld wird geöffnet.<p>![Neue teamschnittstelle](../../media/Create-a-New-NIC-Team/nict_newteaminterface.jpg)  
  
8.  Führen Sie eine der folgenden Schritte aus, je nach Ihren Anforderungen:  
  
    -   Geben Sie einen Namen der tNIC-Schnittstelle ein.  
  
    -   Konfigurieren Sie die VLAN-Mitgliedschaft: Klicken Sie auf **spezifischen VLAN** , und geben Sie die VLAN-Informationen. Wenn dieses NIC-Teams mit dem buchhaltungs-VLAN hinzufügen möchten Zahl, z. B. 44 Typ Buchhaltungs-44 - VLAN.   
  
9. Klicken Sie auf **OK**.  

_**Herzlichen Glückwunsch!**_  Sie haben einen neuen NIC-Teams auf einem Host oder virtuellen Computer erstellt.

## <a name="related-topics"></a>Verwandte Themen
- [NIC-Teamvorgang](NIC-Teaming.md): In diesem Thema stellen wir Ihnen in Windows Server 2016 einen Überblick über die Windows-Verwaltungsinstrumentation (Network Interface Card, NIC)-Teamvorgang. NIC-Teamvorgang ermöglicht Ihnen, zwischen 1 und 32 gruppieren, physische Ethernet-Netzwerkadapter in ein oder mehrere softwarebasierte virtuelle Netzwerkadapter. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.   

- [NIC-Teamvorgang-MAC-Adresse und -Verwaltung](NIC-Teaming-MAC-Address-Use-and-Management.md): Beim Konfigurieren eines NIC-Teams mit unabhängigen Modus wechseln und adresshash oder dynamische lastverteilung steuern das Team verwendet, die die MAC-Adresse (MAC) des primären Mitglieds-NIC-Team für ausgehenden Datenverkehr. Dem primären NIC-Team-Mitglied ist, einen Netzwerkadapter, die vom Betriebssystem aus den anfänglichen Satz von Team-Mitglieder ausgewählt wird.

- [Einstellungen für die NIC-Teamvorgang](nic-teaming-settings.md): In diesem Thema haben wir bieten Ihnen einen Überblick über den NIC-Team-Eigenschaften, z. B. Teamvorgang und Lastenausgleich Modi zu laden. Sie haben zudem Details über die Standby-adaptereinstellung und die Eigenschaft des primären Team-Schnittstelle. Wenn Sie in einem NIC-Team über mindestens zwei Netzwerkadapter verfügen, müssen Sie keinen Standby-Adapter für die Fehlertoleranz zu bestimmen.

- [Problembehandlung bei der NIC-Teamvorgang](Troubleshooting-NIC-Teaming.md): In diesem Thema werden Möglichkeiten zum Beheben von NIC-Teamvorgang, z. B. Hardware, Wertpapiere der physische Switch und das Deaktivieren oder aktivieren Netzwerkadapter, die mithilfe von Windows PowerShell beschrieben. 

---