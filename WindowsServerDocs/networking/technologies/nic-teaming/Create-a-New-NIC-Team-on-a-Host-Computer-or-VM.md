---
title: Erstellen eines neuen NIC-Teams auf einem Host Computer oder einer VM
description: In diesem Thema erstellen Sie ein neues NIC-Team auf einem Host Computer oder auf einem virtuellen Hyper-V-Computer (VM), auf dem Windows Server 2016 ausgeführt wird.
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-nict
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4caaa86-5799-4580-8775-03ee213784a3
ms.author: pashort
author: shortpatti
ms.date: 09/13/2018
ms.openlocfilehash: f1e7e27100d801d226adf79e078d8b16ddbcd308
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401923"
---
# <a name="create-a-new-nic-team-on-a-host-computer-or-vm"></a>Erstellen eines neuen NIC-Teams auf einem Host Computer oder einer VM

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erstellen Sie ein neues NIC-Team auf einem Host Computer oder auf einem virtuellen Hyper-V-Computer (VM), auf dem Windows Server 2016 ausgeführt wird.  

## <a name="network-configuration-requirements"></a>Anforderungen an die Netzwerkkonfiguration  
Bevor Sie ein neues NIC-Team erstellen können, müssen Sie einen Hyper-V-Host mit zwei Netzwerkadaptern bereitstellen, die mit verschiedenen physischen Switches verbunden sind. Außerdem müssen Sie die Netzwerkadapter mit IP-Adressen konfigurieren, die sich im selben IP-Adressbereich befinden.  

Die Anforderungen für den physischen Switch, den virtuellen Hyper-V-Switch, das LAN (Local Area Network) und den NIC-Team Vorgang zum Erstellen eines NIC-Teams auf einem virtuellen Computer lauten wie folgt:  

-   Der Computer, auf dem Hyper-V ausgeführt wird, muss über mindestens zwei Netzwerkadapter verfügen.  

-   Wenn Sie die Netzwerkadapter mit mehreren physischen Switches verbinden, müssen sich die physischen Switches im gleichen Layer 2-Subnetz befinden.  

-   Sie müssen den Hyper-v-Manager oder Windows PowerShell verwenden, um zwei externe virtuelle Hyper-v-Switches zu erstellen, die jeweils mit einem anderen physischen Netzwerkadapter verbunden sind.  

-   Die VM muss eine Verbindung mit beiden externen virtuellen Switches herstellen, die Sie erstellen.  

-   Der NIC-Team Vorgang in Windows Server 2016 unterstützt Teams mit zwei Mitgliedern auf virtuellen Computern. Sie können größere Teams erstellen, aber es gibt keine Unterstützung.

-   Wenn Sie ein NIC-Team in einem virtuellen Computer konfigurieren, müssen Sie einen **Teaming-Modus** von _Switch Independent_ und den **Lasten Ausgleichs Modus** _Address Hash_auswählen. 

## <a name="step-1-configure-the-physical-and-virtual-network"></a>Schritt 1 Konfigurieren des physischen und des virtuellen Netzwerks  
In diesem Verfahren erstellen Sie zwei externe virtuelle Hyper-V-Switches, verbinden eine VM mit den Switches und konfigurieren dann die VM-Verbindungen mit den Switches.  

### <a name="prerequisites"></a>Erforderliche Komponenten

Sie müssen Mitglied der Gruppe " **Administratoren**" oder einer entsprechenden Gruppe sein.  

### <a name="procedure"></a>Prozedur

1.  Öffnen Sie auf dem Hyper-v-Host den Hyper-v-Manager, und klicken Sie unter Aktionen auf **Manager für virtuelle**Switches.  

   ![Manager für virtuelle Switches](../../media/Create-a-New-NIC-Team-in-a-VM/nict_hv.jpg)  

2.  Stellen Sie im Manager für virtuelle Switches sicher, dass **extern** ausgewählt ist, und klicken Sie dann auf **virtuellen Switch erstellen**.  

   ![Virtuellen Switch erstellen](../../media/Create-a-New-NIC-Team-in-a-VM/nict_hv_02.jpg)  

3.  Geben Sie unter Eigenschaften für virtuelle Switches einen **Namen** für den virtuellen Switch ein, und fügen Sie bei Bedarf **Notizen** hinzu.  

4.  Wählen Sie unter **Verbindungstyp**in **externer Netzwerk**den physischen Netzwerkadapter aus, an den Sie den virtuellen Switch anfügen möchten.  

5.  Konfigurieren Sie zusätzliche Switch-Eigenschaften für die Bereitstellung, und klicken Sie dann auf **OK**.  

6.  Erstellen Sie einen zweiten externen virtuellen Switch, indem Sie die vorherigen Schritte wiederholen. Verbinden Sie den zweiten externen Switch mit einem anderen Netzwerkadapter.  

7.  Klicken Sie im Hyper-V-Manager unter **Virtual Machines**mit der rechten Maustaste auf die VM, die Sie konfigurieren möchten, und klicken Sie dann auf **Einstellungen**.  

   Das Dialogfeld VM- **Einstellungen** wird geöffnet.

8.  Stellen Sie sicher, dass der virtuelle Computer nicht gestartet wurde. Wenn Sie gestartet wurde, führen Sie vor dem Konfigurieren der VM ein Herunterfahren aus.  

8.  Klicken Sie unter **Hardware**auf **Netzwerk Adapter**.  

   ![Netzwerkkarte](../../media/Create-a-New-NIC-Team-in-a-VM/nict_hvs_01.jpg)  

9. Wählen Sie in den Eigenschaften des **Netzwerkadapters** einen der virtuellen Switches aus, den Sie in den vorherigen Schritten erstellt haben, und **Klicken Sie dann**auf übernehmen.  

    ![Wählen Sie einen virtuellen Switch aus.](../../media/Create-a-New-NIC-Team-in-a-VM/nict_hvs_02.jpg)  

10. Klicken Sie unter **Hardware**auf das Pluszeichen (+) neben **Netzwerk Adapter**. 

11. Klicken Sie auf **Erweiterte Features** , um den NIC-Team Vorgang mithilfe der grafischen Benutzeroberfläche zu aktivieren. 

    >[!TIP]
    >Sie können NIC-Teaming auch mit einem Windows PowerShell-Befehl aktivieren: 
    >
    >```PowerShell
    >Set-VMNetworkAdapter -VMName <VMname> -AllowTeaming On
    >```

    a. Wählen Sie **dynamisch** für Mac-Adresse aus. 

    b. Klicken Sie hier, um **geschütztes Netzwerk**auszuwählen. 

    c. Klicken Sie hier, um **die Option diesen Netzwerkadapter als Teil eines Teams im Gast Betriebssystem zu aktivieren**. 

    d. Klicken Sie auf **OK**.  

    ![Hinzufügen eines Netzwerkadapters zu einem Team](../../media/Create-a-New-NIC-Team-in-a-VM/nict_hvs_05.jpg)  

13. Wenn Sie einen zweiten Netzwerkadapter hinzufügen möchten, klicken Sie im Hyper-V-Manager in **Virtual Machines**mit der rechten Maustaste auf denselben virtuellen Computer, und klicken Sie dann auf **Einstellungen**.  

    Das Dialogfeld VM- **Einstellungen** wird geöffnet.

14. Klicken Sie unter **Hardware hinzufügen**auf **Netzwerk Adapter**, und klicken Sie dann auf **Hinzufügen**.  

   ![Netzwerkadapter hinzufügen](../../media/Create-a-New-NIC-Team-in-a-VM/nict_hvs_06.jpg)  

15. Wählen Sie unter **Netzwerk Adapter** Eigenschaften den zweiten virtuellen Switch aus, den Sie in den vorherigen Schritten erstellt haben, **und klicken Sie**dann auf übernehmen.  

   ![Anwenden eines virtuellen Switches](../../media/Create-a-New-NIC-Team-in-a-VM/nict_hvs_07.jpg)  

16. Klicken Sie unter **Hardware**auf das Pluszeichen (+) neben **Netzwerk Adapter**. 

17. Klicken Sie auf **Erweiterte Features**, Scrollen Sie nach unten zum **NIC**-Team Vorgang, und klicken Sie **dann auf Netzwerkadapter als Teil eines Teams im Gast Betriebssystem aktivieren**. 

18. Klicken Sie auf **OK**.  

_**Gratul!**_  Sie haben das physische und virtuelle Netzwerk konfiguriert.  Nun können Sie mit dem Erstellen eines neuen NIC-Teams fortfahren.  

## <a name="step-2-create-a-new-nic-team"></a>Schritt 2 Erstellen eines neuen NIC-Teams

Wenn Sie ein neues NIC-Team erstellen, müssen Sie die Eigenschaften des NIC-Teams konfigurieren:  

-   Teamname  

-   Mitglieds Adapter  

-   Team Vorgangs Modus  

-   Lasten Ausgleichs Modus  

-   Standby-Adapter  

Optional können Sie auch die primäre Team Schnittstelle konfigurieren und eine virtuelle LAN-Nummer (VLAN) konfigurieren.  

Weitere Informationen zu diesen Einstellungen finden Sie unter [NIC Teaming Settings](nic-teaming-settings.md).

### <a name="prerequisites"></a>Erforderliche Komponenten

Sie müssen Mitglied der Gruppe " **Administratoren**" oder einer entsprechenden Gruppe sein.  

### <a name="procedure"></a>Prozedur

1. Klicken Sie im Server-Manager auf **Lokaler Server**.  

2. Suchen Sie im **Eigenschaften** Bereich in der ersten Spalte den **NIC**-Team Vorgang, und klicken Sie dann auf den Link **deaktiviert** .  

   Das Dialogfeld **NIC** -Team Vorgang wird geöffnet.

   ![Dialogfeld "NIC-Teamvorgang"](../../media/Create-a-New-NIC-Team/nict_02_nicteaming.jpg)

3. Wählen Sie unter **Adapter und Schnittstellen**den Netzwerkadapter aus, den Sie einem NIC-Team hinzufügen möchten.  

4. Klicken Sie auf **Tasks**, und klicken Sie **auf dem neuen Team hinzufügen**.  

   Das Dialogfeld **Neues Team** wird geöffnet und zeigt Netzwerkadapter und Teammitglieder an.

5. Geben Sie unter **Teamname**einen Namen für das neue NIC-Team ein, und klicken Sie dann auf **zusätzliche Eigenschaften**.  

6. Wählen Sie unter **zusätzliche Eigenschaften**Werte für folgende Aktionen aus:

   - Team Vorgangs **Modus**. Die Optionen für den Team Vorgangs Modus sind **Switch Independent** und **Switch Dependent**. Der Switch-abhängige Modus umfasst den **statischen** Team Vorgang und das **Link Aggregation Control Protocol (LACP)** . 

     - **Wechsel unabhängig.** [!INCLUDE [switch-independent-shortdesc-include](../../includes/switch-independent-shortdesc-include.md)]

     - **Wechseln Sie von abhängig.** [!INCLUDE [switch-dependent-shortdesc-include](../../includes/switch-dependent-shortdesc-include.md)] 


       |                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
       |----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
       |              **Statischer Teaming**              |                                                                                                                                              Erfordert, dass Sie sowohl den Switch als auch den Host manuell konfigurieren, um zu bestimmen, welche Links das Team bilden. Da es sich hierbei um eine statisch konfigurierte Lösung handelt, gibt es kein zusätzliches Protokoll, das es dem Switch und dem Host unterstützt, nicht ordnungsgemäß konfigurierte Kabel oder andere Fehler zu identifizieren, die zu einem Fehler des Teams führen könnten. Dieser Modus wird im Allgemeinen von Switches der Serverklasse unterstützt.                                                                                                                                              |
       | **Link Aggregation Control Protocol (LACP)** | Im Gegensatz zum statischen Team Vorgang identifiziert der LACP-Team Vorgangs Modus dynamisch Verknüpfungen, die zwischen dem Host und dem Switch verbunden sind. Diese dynamische Verbindung ermöglicht die automatische Erstellung eines Teams und, in der Praxis, die Erweiterung und Reduzierung eines Teams einfach durch die Übertragung oder den Empfang von LACP-Paketen aus der Peer Entität. Alle Server Klassen Switches unterstützen LACP, und alle erfordern, dass der Netzwerk Operator LACP auf dem Switchport administrativ aktiviert. Wenn Sie einen Teaming-Modus von LACP konfigurieren, wird der NIC-Team Vorgang immer im aktiven Modus von LACP mit einem kurzen Timer ausgeführt.  Derzeit ist keine Option verfügbar, um den Timer zu ändern oder den LACP-Modus zu ändern. |

       ---

   - **Lasten Ausgleichs Modus**. Die Optionen für den Lasten Ausgleichs-Verteilungsmodus sind **Adress Hash**, **Hyper-V-Port**und **dynamisch**.

     - **Adress Hash.** [!INCLUDE [address-hash-shortdesc-include](../../includes/address-hash-shortdesc-include.md)]

     - **Hyper-V-Port.** [!INCLUDE [hyper-v-port-shortdesc-include](../../includes/hyper-v-port-shortdesc-include.md)]

     - **Schem.** [!INCLUDE [dynamic-shortdesc-include](../../includes/dynamic-shortdesc-include.md)]

   - **Standby-Adapter**. Die Optionen für den standbyadapter sind **None (alle Adapter aktiv)** oder Ihre Auswahl eines bestimmten Netzwerkadapters im NIC-Team, das als standbyadapter fungiert.

   > [!TIP]  
   > Wenn Sie ein NIC-Team in einem virtuellen Computer (VM) konfigurieren, müssen Sie einen Team Vorgangs **Modus** von _Switch Independent_ und den **Lasten Ausgleichs Modus** _Address Hash_auswählen.  

7. Wenn Sie den Namen der primären Team Schnittstelle konfigurieren oder dem NIC-Team eine VLAN-Nummer zuweisen möchten, klicken Sie auf den Link rechts neben der **primären Team Schnittstelle**.  

    Das Dialogfeld **neue Team Schnittstelle** wird geöffnet.

    ![Neue Team Schnittstelle](../../media/Create-a-New-NIC-Team/nict_newteaminterface.jpg)

8. Führen Sie je nach Ihren Anforderungen einen der folgenden Schritte aus:  

   -   Geben Sie einen tnic-Schnittstellennamen an.  

   -   VLAN-Mitgliedschaft konfigurieren: Klicken Sie auf **bestimmtes VLAN** , und geben Sie die VLAN-Informationen ein. Wenn Sie z. b. dieses NIC-Team der Buchhaltungs-VLAN-Nummer 44 hinzufügen möchten, geben Sie Accounting 44-VLAN ein.   

9. Klicken Sie auf **OK**.  

_**Gratul!**_  Sie haben ein neues NIC-Team auf einem Host Computer oder einer VM erstellt.

## <a name="related-topics"></a>Verwandte Themen

- [NIC](NIC-Teaming.md)-Team Vorgang: In diesem Thema erhalten Sie einen Überblick über den NIC-Team Vorgang (Network Interface Card) in Windows Server 2016. Mit dem NIC-Team Vorgang können Sie zwischen einem und 32 physischen Ethernet-Netzwerkadaptern in einem oder mehreren softwarebasierten virtuellen Netzwerkadaptern gruppieren. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.   

- [NIC-Team Vorgang MAC-Adress Verwendung und-Verwaltung](NIC-Teaming-MAC-Address-Use-and-Management.md): Wenn Sie ein NIC-Team mit dem Switch-unabhängigen Modus und entweder Address Hash oder Dynamic Load Distribution konfigurieren, verwendet das Team die Media Access Control (Mac)-Adresse des primären NIC-Teammitglieds für ausgehenden Datenverkehr. Das primäre NIC-Team Mitglied ist ein Netzwerkadapter, der vom Betriebssystem aus der anfänglichen Gruppe von Team Mitgliedern ausgewählt wird.

- [Einstellungen für NIC](nic-teaming-settings.md)-Team Vorgänge: In diesem Thema erhalten Sie einen Überblick über die NIC-Team Eigenschaften, z. b. Team-und Lasten ausgleichsmodi. Außerdem erhalten Sie Informationen über die standbyadaptereinstellung und die Eigenschaft "primäre Team Schnittstelle". Wenn Sie über mindestens zwei Netzwerkadapter in einem NIC-Team verfügen, müssen Sie keinen Standby-Adapter für die Fehlertoleranz festlegen.

- [Problem](Troubleshooting-NIC-Teaming.md)Behandlung beim NIC-Team Vorgang: In diesem Thema wird erläutert, wie Sie Probleme mit dem NIC-Team Vorgang beheben, wie z. b. Hardware, physische switchwertgeräte und das Deaktivieren oder Aktivieren von Netzwerkadaptern mithilfe von Windows PowerShell. 

---