---
title: NIC-Teamvorgang
description: In diesem Thema erhalten Sie einen Überblick über den NIC-Team Vorgang (Network Interface Card) in Windows Server 2016. Mit dem NIC-Team Vorgang können Sie zwischen einem und 32 physischen Ethernet-Netzwerkadaptern in einem oder mehreren softwarebasierten virtuellen Netzwerkadaptern gruppieren. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-nict
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abded6f3-5708-4e35-9a9e-890e81924fec
ms.author: lizross
author: eross-msft
ms.date: 09/10/2018
ms.openlocfilehash: f4d9dd20d626f998bee0a8414c281cd27b2d3dbb
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316447"
---
# <a name="nic-teaming"></a>NIC-Teamvorgang

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erhalten Sie einen Überblick über den NIC-Team Vorgang (Network Interface Card) in Windows Server 2016. Mit dem NIC-Team Vorgang können Sie zwischen einem und 32 physischen Ethernet-Netzwerkadaptern in einem oder mehreren softwarebasierten virtuellen Netzwerkadaptern gruppieren. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.  
  
> [!IMPORTANT]
> Netzwerkadapter für NIC-Team Mitglieder müssen auf demselben physischen Host Computer installiert werden. 

> [!TIP]  
> Ein NIC-Team, das nur einen Netzwerkadapter enthält, kann keinen Lastenausgleich und kein Failover bereitstellen. Allerdings können Sie mit einem Netzwerkadapter den NIC-Team Vorgang für die Trennung von Netzwerk Datenverkehr verwenden, wenn Sie auch virtuelle lokale Netzwerke (Virtual Local Area Networks, VLANs) verwenden.  
  
Wenn Sie Netzwerkadapter in einem NIC-Team konfigurieren, stellen Sie eine Verbindung mit der NIC-Team Vorgangs Lösung Common Core her, die dem Betriebssystem dann einen oder mehrere virtuelle Adapter (auch Team-NICs [tnics] oder Team Schnittstellen genannt) präsentiert. 

Da Windows Server 2016 bis zu 32 Team Schnittstellen pro Team unterstützt, gibt es eine Vielzahl von Algorithmen, die ausgehenden Datenverkehr (Last) zwischen den NICs verteilen.  Die folgende Abbildung zeigt ein NIC-Team mit mehreren tnics.  
  
![Nic-Team mit mehreren tnics](../../media/NIC-Teaming/nict_overview.jpg)  
  
Außerdem können Sie Ihre Team eigenen NICs mit dem gleichen Switch oder anderen Switches verbinden. Wenn Sie NICs mit verschiedenen Switches verbinden, müssen sich beide Switches im gleichen Subnetz befinden.  
  
## <a name="availability"></a>Verfügbarkeit  
NIC-Teaming ist in allen Versionen von Windows Server 2016 verfügbar. Sie können eine Vielzahl von Tools zum Verwalten des NIC-Team Vorgangs auf Computern verwenden, auf denen ein Client Betriebssystem ausgeführt wird, z. b.: • Windows PowerShell-Cmdlets • Remotedesktop • Remoteserver-Verwaltungstools  
  
## <a name="supported-and-unsupported-nics"></a>Unterstützte und nicht unterstützte NICs   
Sie können eine beliebige Ethernet-NIC verwenden, die in einem NIC-Team in Windows Server 2016 den Windows-Hardware Qualifikations-und Logotest (WHQL-Tests) bestanden hat.  
  
Die folgenden NICs können nicht in einem NIC-Team platziert werden:
  
-   Virtuelle Hyper-v-Netzwerkadapter, bei denen es sich um virtuelle Hyper-v-Switchports handelt, die als NICs in der Host Partition verfügbar sind  
  
    > [!IMPORTANT]  
    > Platzieren Sie keine virtuellen Hyper-V-NICs, die in der Host Partition (vNICs) in einem Team verfügbar gemacht werden. Das Teaming von vNICs innerhalb der Host Partition wird in keiner Konfiguration unterstützt. Versuche an Team-vNICs können zu einem vollen Kommunikations Verlust führen, wenn Netzwerkfehler auftreten.  
  
-   Kernel-Debug-Netzwerkadapter (kdnic).  
  
-   NICs, die für den Netzwerkstart verwendet werden.  
  
-   NICs, die andere Technologien als Ethernet verwenden, z. b. WWAN, WLAN/Wi-Fi, Bluetooth und InfiniBand, einschließlich Internet Protocol over InfiniBand (IPoIB) NICs.  
  
## <a name="compatibility"></a>Kompatibilität  
Nic-Team Vorgänge sind mit allen Netzwerktechnologien in Windows Server 2016 mit den folgenden Ausnahmen kompatibel.  
  
-   E **/a-Virtualisierung mit Einzel Stamm (SR-IOV)** . Für SR-IOV werden Daten direkt an die NIC übermittelt, ohne dass Sie über den Netzwerk Stapel (im Fall der Virtualisierung im Host Betriebssystem) übergeben werden. Daher ist es nicht möglich, dass das NIC-Team die Daten überprüfen oder an einen anderen Pfad im Team umleiten kann.  
  
-   **Native Host Quality of Service (QoS)** . Wenn Sie QoS-Richtlinien auf einem systemeigenen oder Host System festlegen und diese Richtlinien Einschränkungen der Mindestbandbreite aufrufen, ist der Gesamtdurchsatz für ein NIC-Team geringer, als wenn die Bandbreiten Richtlinien vorhanden sind.  
  
-   **TCP-Chimney**. TCP-Chimney wird beim NIC-Team Vorgang nicht unterstützt, da TCP Chimney den gesamten Netzwerk Stapel direkt auf die NIC verlagert.  
  
-   **802.1 x-Authentifizierung**. Sie sollten die 802.1 x-Authentifizierung nicht mit NIC-Team Vorgang verwenden, da einige Switches die Konfiguration der 802.1 x-Authentifizierung und des NIC-Team Vorgangs auf demselben Port nicht zulassen.  
  
Informationen zur Verwendung des NIC-Team Vorgangs auf virtuellen Computern (VMS), die auf einem Hyper-V-Host ausgeführt werden, finden Sie unter [Erstellen eines neuen NIC-Teams auf einem Host Computer oder einer](Create-a-New-NIC-Team-on-a-Host-Computer-or-VM.md)virtuellen Maschine.
  
## <a name="virtual-machine-queues-vmqs"></a>Warteschlangen für virtuelle Computer (vmqs)  

Vmqs ist eine NIC-Funktion, die eine Warteschlange für jeden virtuellen Computer bereitstellt.  Wenn Sie Hyper-V aktiviert haben, Sie müssen auch VMQ aktivieren. In Windows Server 2016 verwendet vmqs NIC-Switch-VPORTS mit einer einzelnen Warteschlange, die dem VPort zugewiesen ist, um die gleiche Funktionalität bereitzustellen. 

Abhängig vom switchkonfigurationsmodus und dem Auslastungs Verteilungs Algorithmus zeigt der NIC-Team Vorgang entweder die kleinste Anzahl von verfügbaren und unterstützten Warteschlangen von einem beliebigen Adapter im Team an (Modus für min. Warteschlangen) oder die Gesamtanzahl der für alle Teams verfügbaren Warteschlangen. Member (Sum-of-Queues-Modus).  

Wenn sich das Team im switchunabhängigen Team Vorgang-Modus befindet und Sie die Lastenverteilung auf den Hyper-V-Port Modus oder den dynamischen Modus festlegen, wird die Anzahl der gemeldeten Warteschlangen als Summe aller Warteschlangen der Teammitglieder (Sum-of-Queue-Modus) zurückgegeben. Andernfalls ist die Anzahl der gemeldeten Warteschlangen die kleinste Anzahl von Warteschlangen, die von einem Teammitglied unterstützt werden (Modus für min. Warteschlangen).

Dies ist der Grund:  
  
-   Wenn sich das switchunabhängige Team im Hyper-v-Porttyp oder im dynamischen Modus befindet, kommt der eingehende Datenverkehr für einen Hyper-v-Switchport (VM) immer auf demselben Teammitglied an. Der Host kann vorhersagen/steuern, welches Mitglied den Datenverkehr für einen bestimmten virtuellen Computer empfängt, sodass der NIC-Team Vorgang besser durchdacht werden kann, welche VMQ-Warteschlangen einem bestimmten Teammitglied zugeordnet werden sollen. Beim NIC-Team Vorgang, der mit dem Hyper-V-Switch arbeitet, wird VMQ für eine VM auf genau einem Teammitglied festgelegt, und es wird festgestellt, dass eingehender Datenverkehr diese Warteschlange erreicht  
  
-   Wenn sich das Team in einem Switch-abhängigen Modus befindet (statischer Team Vorgang oder LACP-Team Vorgang), steuert der Switch, mit dem das Team verbunden ist, die Verteilung des eingehenden Datenverkehrs. Die NIC-Team Vorgangs Software des Hosts kann nicht vorhersagen, welches Teammitglied den eingehenden Datenverkehr für einen virtuellen Computer erhält. der Switch verteilt den Datenverkehr für eine VM auf alle Teammitglieder. Das Ergebnis der NIC-Team Vorgangs Software, die mit dem Hyper-V-Switch arbeitet, programmiert eine Warteschlange für den virtuellen Computer auf jedem Teammitglied, nicht nur ein Teammitglied.  
  
-   Wenn sich das Team im Schalter unabhängigen Modus befindet und den Adress Hash-Lastenausgleich verwendet, kommt der eingehende Datenverkehr immer an eine NIC (das primäre Teammitglied), die alle auf nur einem Teammitglied ist. Da andere Teammitglieder nicht mit eingehendem Datenverkehr arbeiten, werden Sie mit denselben Warteschlangen wie der primäre Member programmiert, sodass bei einem Ausfall des primären Mitglieds alle anderen Teammitglieder verwendet werden können, um den eingehenden Datenverkehr zu übernehmen, und die Warteschlangen bereits vorhanden sind.  

- Die meisten NICs haben Warteschlangen für die Empfangs seitige Skalierung (RSS) oder VMQ, aber nicht gleichzeitig. Einige VMQ-Einstellungen scheinen Einstellungen für RSS-Warteschlangen zu sein, sind jedoch Einstellungen in den generischen Warteschlangen, die sowohl von RSS als auch von VMQ abhängig davon verwendet werden, welches Feature aktuell verwendet wird. Jede NIC verfügt in ihren erweiterten Eigenschaften über Werte für * rssbaseprocnumber und \*maxrssprocoren. Im folgenden finden Sie einige VMQ-Einstellungen, die eine bessere Systemleistung bereitstellen.  
  
-   Im Idealfall sollte für jede NIC die * rssbaseprocnumber auf eine gerade Zahl größer oder gleich zwei (2) festgelegt sein. Der erste physische Prozessor (Core 0 (logische Prozessoren 0 und 1) übernimmt in der Regel den größten Teil der Systemverarbeitung, sodass die Netzwerk Verarbeitung von diesem physischen Prozessor entfernt werden soll. Einige Computerarchitekturen verfügen nicht über zwei logische Prozessoren pro physischem Prozessor. Daher sollte der Basis Prozessor für solche Computer größer oder gleich 1 sein. Wenn Sie zweifelhaft sind, nehmen Sie an, dass Ihr Host einen 2 logischen Prozessor pro physischer Prozessorarchitektur verwendet.  
  
-   Wenn sich das Team im Warteschlangen Modus befindet, sollten die Prozessoren der Teammitglieder sich nicht überlappen. Beispielsweise können Sie in einem 4-Kern-Host (8 logische Prozessoren) mit einem Team von 2 10Gbit/s-NICs das erste so festlegen, dass der Basis Prozessor 2 verwendet und vier Kerne verwendet werden. der zweite Wert wird so festgelegt, dass er den Basis Prozessor 6 verwendet und 2 Kerne verwendet.  
  
-   Wenn sich das Team im Modus für minimale Warteschlangen befindet, müssen die von den Teammitgliedern verwendeten Prozessor Sätze identisch sein.  

  
## <a name="hyper-v-network-virtualization-hnv"></a>Hyper-V-Netzwerkvirtualisierung (HNV)  
Der NIC-Team Vorgang ist vollständig kompatibel mit der Hyper-v-Netzwerkvirtualisierung (HNV).  Das HNV-Verwaltungssystem stellt Informationen für den NIC-Team Vorgangs Treiber bereit, mit dem NIC-Team Vorgänge die Last auf eine Weise verteilen können, die den HNV-Datenverkehr optimiert.  
  
## <a name="live-migration"></a>Livemigration  
Der NIC-Team Vorgang auf VMS wirkt sich nicht auf Livemigration aus. Die gleichen Regeln gelten für Livemigration, ob der NIC-Team Vorgang auf dem virtuellen Computer konfiguriert wird.  


## <a name="virtual-local-area-networks-vlans"></a>Virtuelle lokale Netzwerke (VLANs)
Wenn Sie den NIC-Team Vorgang verwenden, ermöglicht die Erstellung mehrerer Team Schnittstellen, dass ein Host gleichzeitig eine Verbindung mit verschiedenen VLANs herstellt. Konfigurieren Sie Ihre Umgebung mit den folgenden Richtlinien:
  
- Bevor Sie den NIC-Team Vorgang aktivieren, konfigurieren Sie die physischen Switchports, die mit dem Team Vorgang-Host verbunden sind, um den trunk Modus (Promiscuous) zu verwenden. Der physische Switch sollte den gesamten Datenverkehr zum Filtern an den Host übergeben, ohne den Datenverkehr zu ändern.  

- Konfigurieren Sie keine VLAN-Filter für die NICs mithilfe der erweiterten NIC-Eigenschaften Einstellungen. Lassen Sie die NIC-Team Vorgangs Software oder den virtuellen Hyper-V-Switch (falls vorhanden) VLAN-Filterung durchführen.  
  
### <a name="use-vlans-with-nic-teaming-in-a-vm"></a>Verwenden von VLANs mit NIC-Team Vorgang auf einem virtuellen Computer  
Wenn ein Team eine Verbindung mit einem virtuellen Hyper-v-Switch herstellt, müssen alle VLAN-Trennungen im virtuellen Hyper-v-Switch statt im NIC-Team Vorgang durchgeführt werden.  

Planen Sie die Verwendung von VLANs auf einem mit einem NIC-Team konfigurierten virtuellen Computer mithilfe der folgenden Richtlinien:
  
-   Die bevorzugte Methode zur Unterstützung mehrerer VLANs auf einem virtuellen Computer besteht darin, die VM mit mehreren Ports auf dem virtuellen Hyper-V-Switch zu konfigurieren und jeden Port einem VLAN zuzuordnen. Diese Ports werden nie auf dem virtuellen Computer ausgeführt, da dadurch Netzwerk Kommunikationsprobleme verursacht werden.  

-   Wenn der virtuelle Computer über mehrere virtuelle SR-IOV-Funktionen (VFS) verfügt, müssen Sie sicherstellen, dass Sie sich im gleichen VLAN befinden, bevor Sie Sie auf dem virtuellen Computer ausführen. Es ist problemlos möglich, die verschiedenen VFS so zu konfigurieren, dass Sie sich auf unterschiedlichen VLANs befinden. Dies bewirkt Probleme bei der Netzwerkkommunikation.  
 
  
### <a name="manage-network-interfaces-and-vlans"></a>Verwalten von Netzwerkschnittstellen und VLANs 
Wenn Sie mehr als ein VLAN in einem Gast Betriebssystem verfügbar machen müssen, sollten Sie die Ethernet-Schnittstellen umbenennen, um VLAN zu verdeutlichen, die der Schnittstelle zugewiesen sind. Wenn Sie z. b. **Ethernet** -Schnittstelle mit VLAN 12 und der **Ethernet 2** -Schnittstelle mit VLAN 48 verknüpfen, benennen Sie die Schnittstelle Ethernet in **EthernetVLAN12** und die andere in **EthernetVLAN48**um. 

Benennen Sie Schnittstellen mit dem Windows PowerShell **-Befehl Rename-netadapter** um, oder führen Sie die folgenden Schritte aus:
  
1.  Klicken Sie in Server-Manager in den **Eigenschaften** für den Netzwerkadapter, den Sie umbenennen möchten, auf den Link rechts neben dem Namen des Netzwerkadapters. 
  
2.  Klicken Sie mit der rechten Maustaste auf den Netzwerkadapter, den Sie umbenennen möchten, und wählen Sie **Umbenennen**.  
  
3.  Geben Sie den neuen Namen für den Netzwerkadapter ein, und drücken Sie die EINGABETASTE.  


## <a name="virtual-machines-vms"></a>Virtual Machines (VMS)

Wenn Sie den NIC-Team Vorgang auf einem virtuellen Computer verwenden möchten, müssen Sie die virtuellen Netzwerkadapter in der VM nur mit externen virtuellen Hyper-V-Switches verbinden. Dies ermöglicht es dem virtuellen Computer, die Netzwerk Konnektivität auch dann aufrechtzuerhalten, wenn einer der physischen Netzwerkadapter, die mit einem virtuellen Switch verbunden sind, fehlschlägt oder getrennt wird. Virtuelle Netzwerkadapter, die mit internen oder privaten virtuellen Hyper-V-Switches verbunden sind, können keine Verbindung mit dem Switch herstellen, wenn Sie sich in einem Team befinden, und die Netzwerkverbindung für den virtuellen Computer schlägt fehl.  
  
Der NIC-Team Vorgang in Windows Server 2016 unterstützt Teams mit zwei Mitgliedern auf virtuellen Computern. Sie können größere Teams erstellen, aber es gibt keine Unterstützung für größere Teams. Jedes Teammitglied muss eine Verbindung mit einem anderen externen virtuellen Hyper-V-Switch herstellen, und die Netzwerkschnittstellen der VM müssen so konfiguriert werden, dass Team Vorgänge zulässig sind.

  
Wenn Sie ein NIC-Team in einem virtuellen Computer konfigurieren, müssen Sie einen **Teaming-Modus** von _Switch Independent_ und den **Lasten Ausgleichs Modus** _Address Hash_auswählen.   
  
  
## <a name="sr-iov-capable-network-adapters"></a>SR-IOV-fähige Netzwerkadapter  
Ein NIC-Team in oder auf dem Hyper-v-Host kann SR-IOV-Datenverkehr nicht schützen, da er nicht über den Hyper-V-Switch läuft.  Mit der Option VM-NIC-Team Vorgang können Sie zwei externe virtuelle Hyper-v-Switches konfigurieren, die jeweils mit einer eigenen SR-IOV-fähigen NIC verbunden sind.  
  
![Nic-Team Vorgang mit SR-IOV-fähigen Netzwerkadaptern](../../media/NIC-Teaming-in-Virtual-Machines--VMs-/nict_in_vm.jpg)  
  
Jeder virtuelle Computer kann über eine virtuelle Funktion (VF) aus einem oder beiden SR-IOV-NICs verfügen und ein Failover von der primären VF zum Sicherungs Adapter (VF), wenn eine NIC getrennt ist. Alternativ kann die VM über eine VF von einer NIC und eine nicht-VF-Vmnic verfügen, die mit einem anderen virtuellen Switch verbunden ist. Wenn die der VF zugeordnete NIC getrennt wird, kann der Datenverkehr ohne Verbindungsverlust ein Failover auf den anderen Switch durchführen.  
  
Da ein Failover zwischen NICs auf einem virtuellen Computer dazu führen kann, dass Datenverkehr mit der Mac-Adresse der anderen Vmnic gesendet wird, muss jeder virtuelle Hyper-V-Switchport, der einem virtuellen Computer mithilfe des NIC-Team Vorgangs zugeordnet ist, so festgelegt werden, dass er 


## <a name="related-topics"></a>Verwandte Themen

- [NIC-Team Vorgang MAC-Adress Verwendung und-Verwaltung](NIC-Teaming-MAC-Address-Use-and-Management.md): Wenn Sie ein NIC-Team mit dem Switch-unabhängigen Modus und entweder Address Hash oder Dynamic Load Distribution konfigurieren, verwendet das Team die Media Access Control (Mac)-Adresse des primären NIC-Teammitglieds für ausgehenden Datenverkehr. Das primäre NIC-Team Mitglied ist ein Netzwerkadapter, der vom Betriebssystem aus der anfänglichen Gruppe von Team Mitgliedern ausgewählt wird.

- [NIC](nic-teaming-settings.md)-Team Vorgangs Einstellungen: in diesem Thema erhalten Sie eine Übersicht über die NIC-Team Eigenschaften, z. b. Team-und Lasten ausgleichsmodi. Außerdem erhalten Sie Informationen über die standbyadaptereinstellung und die Eigenschaft "primäre Team Schnittstelle". Wenn Sie über mindestens zwei Netzwerkadapter in einem NIC-Team verfügen, müssen Sie keinen Standby-Adapter für die Fehlertoleranz festlegen.
  
- [Erstellen eines neuen NIC-Teams auf einem Host Computer oder einer VM](Create-a-New-NIC-Team-on-a-Host-Computer-or-VM.md): in diesem Thema erstellen Sie ein neues NIC-Team auf einem Host Computer oder auf einem virtuellen Hyper-V-Computer (VM), auf dem Windows Server 2016 ausgeführt wird.

- [Problem](Troubleshooting-NIC-Teaming.md)Behandlung beim NIC-Team Vorgang: in diesem Thema wird erläutert, wie Sie Probleme mit dem NIC-Team Vorgang beheben, wie z. b. Hardware, physische switchwertgeräte und das Deaktivieren oder Aktivieren von Netzwerkadaptern mithilfe von Windows PowerShell. 
 
