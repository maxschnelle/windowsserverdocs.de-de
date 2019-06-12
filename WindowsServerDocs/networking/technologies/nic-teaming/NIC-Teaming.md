---
title: NIC-Teamvorgang
description: In diesem Thema stellen wir Ihnen in Windows Server 2016 einen Überblick über die Windows-Verwaltungsinstrumentation (Network Interface Card, NIC)-Teamvorgang. NIC-Teamvorgang ermöglicht Ihnen, zwischen 1 und 32 gruppieren, physische Ethernet-Netzwerkadapter in ein oder mehrere softwarebasierte virtuelle Netzwerkadapter. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-nict
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abded6f3-5708-4e35-9a9e-890e81924fec
ms.author: pashort
author: shortpatti
ms.date: 09/10/2018
ms.openlocfilehash: cf58956ead8e8a47b8ec6d189bf23e5c576d5f15
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812184"
---
# <a name="nic-teaming"></a>NIC-Teamvorgang

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema stellen wir Ihnen in Windows Server 2016 einen Überblick über die Windows-Verwaltungsinstrumentation (Network Interface Card, NIC)-Teamvorgang. NIC-Teamvorgang ermöglicht Ihnen, zwischen 1 und 32 gruppieren, physische Ethernet-Netzwerkadapter in ein oder mehrere softwarebasierte virtuelle Netzwerkadapter. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.  
  
> [!IMPORTANT]
> Sie müssen den NIC-Team Member-Netzwerkadapter in demselben physischen Hostcomputer installieren. 

> [!TIP]  
> Ein NIC-Team, das nur einen Netzwerkadapter enthält, kann keine beim Lastenausgleich und Failover bereitstellen. Allerdings mit einem Netzwerkadapter können Sie NIC-Teamvorgang für die Trennung des Netzwerkdatenverkehrs, wenn Sie auch virtuelle lokale Netzwerke (VLANs) verwenden.  
  
Wenn Sie den Netzwerkadapter in einem NIC-Team konfigurieren, verbinden sie in der NIC teaming Lösung gemeinsamen Kern, der dann eine oder mehrere virtuelle Adapter (auch als Team NICs [tNICs] oder teamschnittstellen) für das Betriebssystem bietet. 

Da Windows Server 2016 bis zu 32 teamschnittstellen pro Team unterstützt, gibt es verschiedene Algorithmen, die ausgehenden Datenverkehr (laden) zwischen den NICs zu verteilen.  Die folgende Abbildung zeigt ein NIC-Team mit mehreren tNICs.  
  
![NIC-Teams mit mehreren tNICs](../../media/NIC-Teaming/nict_overview.jpg)  
  
Darüber hinaus können Sie Ihre Teaming-fähigen Netzwerkkarten mit demselben Switch oder verschiedenen Switches verbinden. Wenn Sie Netzwerkkarten mit verschiedenen Switches verbunden sind, müssen beide Schalter im gleichen Subnetz sein.  
  
## <a name="availability"></a>Verfügbarkeit  
NIC-Teamvorgang ist in allen Versionen von Windows Server 2016 verfügbar. Sie können eine Vielzahl von Tools zum Verwalten von Clientcomputern, die mit Client-Betriebssystem, wie z. B. NIC-Teamvorgang: • Windows PowerShell-Cmdlets • Remotedesktop • Remoteserver-Verwaltungstools  
  
## <a name="supported-and-unsupported-nics"></a>Unterstützte und nicht unterstützten Netzwerkkarten   
Alle Ethernet-Netzwerkkarte können, die die Qualifikation für Windows-Hardware und das Logo-Test (WHQL-Tests) in einem NIC-Team in Windows Server 2016 vergangen ist.  
  
Sie können die folgenden NICs nicht in einem NIC-Team platzieren:
  
-   Hyper-V virtuelle Netzwerkadapter, die von virtuellen Hyper-V-Switch-Ports, die in der Hostpartition als Netzwerkkarten verfügbar gemacht werden.  
  
    > [!IMPORTANT]  
    > Platzieren Sie virtuelle Hyper-V-NICs verfügbar gemacht werden, in der Hostpartition (vNICs) in einem Team nicht. Gastteamvorgang vNICs in die Hostpartition wird in jeder Konfiguration nicht unterstützt. Versucht, Team-vNICs dazu vollständigen Verlust der Kommunikation, treten Netzwerkfehler auf.  
  
-   Kerneldebugger-Netzwerkadapter (KDNIC).  
  
-   Netzwerkkarten, die für den Netzwerkstart verwendet werden.  
  
-   Netzwerkkarten, die Technologien als Ethernet, z. B. WWAN, WLAN/Wi-Fi, Bluetooth und Infiniband, einschließlich Internet Protocol über NICs mit Infiniband (IPoIB) verwenden.  
  
## <a name="compatibility"></a>Kompatibilität  
NIC-Teamvorgang ist kompatibel mit allen netzwerktechnologien in Windows Server 2016 mit den folgenden Ausnahmen.  
  
-   **Single-Root i/o-Virtualisierung (SR-IOV)** . Bei SR-IOV werden Daten direkt an die NIC übermittelt, ohne Umweg über den Netzwerkstapel (im Betriebssystem Hosts, bei der Virtualisierung). Aus diesem Grund ist es nicht möglich, für das NIC-Team, um zu überprüfen oder die Daten an einen anderen Pfad im Team umleiten.  
  
-   **Nativer Host Quality of Service (QoS)** . Wenn Sie QoS-Richtlinien auf ein systemeigenes oder Host-System, und diese Richtlinien aufrufen Mindestbandbreite Einschränkungen, müssen der Gesamtdurchsatz für eine NIC-Team ist kleiner als die ohne den Bandbreitenrichtlinien vorhanden wäre.  
  
-   **TCP Chimney**. TCP-Chimney wird nicht unterstützt, mit NIC-Teamvorgang, da TCP-Chimney entlasten Sie den gesamten Netzwerkstapel direkt auf die NIC.  
  
-   **802.1 x Authentifizierung**. Sie sollten nicht 802.1X-Authentifizierung mit NIC-Teamvorgang verwenden, da einige Switches nicht die Konfiguration von 802.1 X Authentifizierung und NIC-Teamvorgang auf demselben Port zulassen.  
  
Weitere Informationen zur NIC-Teamvorgang auf virtuellen Computern (VMs), die auf einem Hyper-V-Host ausgeführt werden, finden Sie unter [Erstellen eines neuen NIC-Teams auf einem Host oder virtuellen Computer](Create-a-New-NIC-Team-on-a-Host-Computer-or-VM.md).
  
## <a name="virtual-machine-queues-vmqs"></a>Warteschlangen für virtuelle Computer (Vmq)  

Vmq wird eine NIC-Funktion, die eine Warteschlange für jeden virtuellen Computer reserviert.  Jedes Mal, wenn Sie Hyper-V aktiviert haben. VMQ muss ebenfalls aktiviert werden. In Windows Server 2016 verwenden Vmq NIC Switch vPorts mit einer einzigen Warteschlange zugewiesen wird, um die vPort aus, um die gleiche Funktionalität bereitzustellen. 

Je nach der Switch-Konfigurationsmodus und die Load-Verteilungsalgorithmus können stellt entweder die kleinste Anzahl von verfügbaren und unterstützten Warteschlangen über den alle Netzwerkadapter im Team (Min-Warteschlangen-Modus) oder die Gesamtanzahl von Warteschlangen zur Verfügung NIC-Teamvorgang, alle Teams Elemente (Summe der Warteschlangen Modus).  

Wenn das Team in Switchunabhängige teamvorgangsmodus ist, und die lastverteilung auf Hyper-V-Port-Modus oder im dynamischen Modus festlegen, ist die Anzahl der gemeldeten Warteschlangen die Summe aller Warteschlangen, die von den Teammitgliedern (Summe der Warteschlangen Modus) verfügbar. Die Anzahl der Warteschlangen, die gemeldet wird, andernfalls die kleinste Anzahl von Warteschlangen, die von jedem Mitglied des Teams (Min-Warteschlangen-Modus) unterstützt.

Hier ist die Antwort:  
  
-   Wenn das Team switchunabhängige in Hyper-V-Port-Modus oder im dynamischen Modus den eingehenden Datenverkehr für einen Hyper-V-Switchport (VM) immer ist trifft auf demselben Teammitglied. Der Host kann Vorhersagen/Kontrolle welches Element empfängt den Datenverkehr für einen bestimmten virtuellen Computer, sodass NIC-Teamvorgang eingehenden zu der VMQ-Warteschlangen auf einem bestimmten Teammitglied zugewiesen werden können. NIC-Teamvorgang, arbeiten mit dem Hyper-V-Switch, legt die VMQ für einen virtuellen Computer, auf genau ein Teammitglied und wissen, dass eingehender Datenverkehr trifft an diese Warteschlange.  
  
-   Wenn das Team alle abhängigen Modus wechseln (statischer Teamvorgang oder LACP-teaming), wird der Switch, der das Team verbunden ist, steuert die Verteilung des eingehenden Datenverkehrs. Host NIC-Teamvorgang Software kann nicht vorhersagen, welche Team Member eingehenden Datenverkehr für einen virtuellen Computer ruft ab, und es kann sein, dass es sich bei der Switch den Datenverkehr für einen virtuellen Computer auf alle Teammitglieder verteilt. Als Ergebnis der NIC-Teamvorgang Software, arbeiten mit dem Hyper-V-Switch eine Warteschlange für den virtuellen Computer für jedes Teammitglied-Programmen die, nicht nur eine-Teammitglied.  
  
-   Wenn das Team wird switchunabhängige-Modus und verwendet adresshash des Lastenausgleichs, der eingehende Datenverkehr ist immer in einer NIC (die primäre Teammitglied) - alle Daten auf nur einem Teammitglied. Da andere Teammitglieder Umgang mit eingehenden Datenverkehr sind nicht erhalten sie mit der gleichen Warteschlange als dem primären Mitglied so programmiert, dass wenn das primäre Mitglied ein Fehler auftritt, andere Teammitglieder kann verwendet werden, um eingehenden Datenverkehr übernehmen und die Warteschlangen bereits vorhanden sind.  

- Die meisten Netzwerkkarten haben Warteschlangen für entweder empfangen empfangsseitige Skalierung (RSS) oder VMQ, jedoch nicht zur gleichen Zeit. Einige Einstellungen VMQ Einstellungen für die RSS-Warteschlangen zu sein scheinen, aber sind Einstellungen für die generische Warteschlangen, die sowohl RSS als auch VMQ-verwendet abhängig von der Funktion aktuell verwendet wird. Jede NIC verfügt, in der erweiterten Eigenschaften, Werte für * RssBaseProcNumber und \*MaxRssProcessors. Im folgenden werden einige VMQ-Einstellungen, die eine bessere Systemleistung bereitstellen.  
  
-   Im Idealfall jede NIC aufweisen sollte die * RssBaseProcNumber legen Sie auf eine gerade Zahl größer als oder gleich zwei (2). Der ersten physischen Prozessor Kern 0 (logische Prozessoren 0 und 1), in der Regel führt das System verarbeitet, damit die netzwerkverarbeitung von diesen physischen Prozessor nach steuern, sollten die meisten. Einige Feld Computerarchitekturen. keine zwei logische Prozessoren pro physischen Prozessor, sodass für solche Computer, der Basis-Prozessor größer als oder gleich 1 sein sollte. Wenn Sie im Zweifelsfall davon ausgegangen, dass Ihr Host ist ein Prozessor mit 2 logischen pro physischen Prozessor-Architektur.  
  
-   In der Summe der Warteschlangen Modus ist das Team sollte die Teammitglieder Prozessoren nicht überlappende sein. In einem 4-Core-Host (8 logische Prozessoren) mit einem Team von 2 NICs von 10 Gbit/s, konnte Sie z. B. die erste Bedingung, verwenden den Basis-Prozessor 2 und 4 Kerne nutzt, festlegen; Basis 6-Prozessor verwenden, und Verwenden von 2 Kerne, würde das zweite festgelegt werden.  
  
-   Die Prozessor-Sätze ein, die die Mitglieder des Teams müssen identisch sein, wenn das Team im Min-Warteschlangen-Modus befindet.  

  
## <a name="hyper-v-network-virtualization-hnv"></a>Hyper-V-Netzwerkvirtualisierung (HNV)  
NIC-Teamvorgang ist vollständig kompatibel mit Hyper-V-Netzwerkvirtualisierung (HNV).  Das HNV-Management-System bietet Informationen zum NIC-Teamvorgang Treiber, der ermöglicht, um die Last auf eine Weise zu verteilen, das hnv-Datenverkehr optimiert die NIC-Teamvorgang.  
  
## <a name="live-migration"></a>Livemigration  
NIC-Teamvorgang auf virtuellen Computern, hat dies keine Auswirkungen auf Livemigration. Die gleichen Regeln vorhanden für Livemigration, und zwar unabhängig davon, ob der NIC-Teamvorgang auf dem virtuellen Computer konfigurieren.  


## <a name="virtual-local-area-networks-vlans"></a>Virtuelle lokale Netzwerke (VLANs)
Wenn Sie NIC-Teamvorgang verwenden, ermöglicht das Erstellen von mehreren teamschnittstellen einen Host gleichzeitig eine Verbindung zu verschiedenen VLANs aus. Konfigurieren Sie Ihre Umgebung die folgenden Richtlinien beachten:
  
- Bevor Sie NIC-Teamvorgang aktivieren, konfigurieren Sie den physischen Switchports, die Verbindung mit dem Teamvorgang Host trunkmodus (gemischten) verwenden. Physische Switch sollten sämtlichen Datenverkehr an dem Host übergeben, für die Filterung, ohne den Datenverkehr zu ändern.  

- Konfigurieren Sie die VLAN-Filter nicht auf den Netzwerkkarten, indem Sie mit der Netzwerkkarte, die erweiterten Einstellungen für die Eigenschaften. Lassen Sie die NIC-Teamvorgang-Software oder den Hyper-V-Switch (falls vorhanden) VLAN gefiltert werden.  
  
### <a name="use-vlans-with-nic-teaming-in-a-vm"></a>Verwenden von VLANs mit NIC-Teamvorgang auf einem virtuellen Computer  
Wenn ein Team mit einem virtuellen Hyper-V-Switch verbunden ist, muss alle VLAN-Segregation in den virtuellen Hyper-V-Switch nicht am NIC-Teamvorgang ausgeführt wird.  

Planen der Verwendung von VLANs auf einem virtuellen Computer konfiguriert, die mit einem NIC-Team die folgenden Richtlinien beachten:
  
-   Die bevorzugte Methode für die Unterstützung von mehrere VLANs auf einem virtuellen Computer wird zum Konfigurieren des virtuellen Computers mit mehreren Ports auf dem virtuellen Hyper-V-Switch und ordnen Sie jeden Port mit einem VLAN. Nie team diese Ports auf dem virtuellen Computer auf, weil dies also Problem mit der Netzwerkverbindung verursacht.  

-   Wenn der virtuelle Computer über mehrere virtuelle SR-IOV-Funktionen (VFs) verfügt, stellen Sie sicher, dass sie sich in demselben VLAN sind, bevor sie auf der VM-Teamvorgang. Es ist ganz einfach möglich ist, so konfigurieren Sie die verschiedenen VFs werden in unterschiedlichen VLANs und diesem Fall kommt es Problem mit der Netzwerkverbindung.  
 
  
### <a name="manage-network-interfaces-and-vlans"></a>Verwalten von Netzwerkschnittstellen und VLANs 
Wenn Sie mehr als ein VLAN in einem Gastbetriebssystem verfügbar gemacht haben müssen, sollten Sie die Umbenennen der Ethernet-Schnittstellen, um auf die Schnittstelle zugewiesenen VLAN zu verdeutlichen. Angenommen, Sie verknüpfen **Ethernet** Schnittstelle mit der VLAN-12 und **Ethernet 2** eine Verbindung mit der VLAN-48, benennen Sie die Ethernet-Schnittstelle auf **EthernetVLAN12** und andere, **EthernetVLAN48**. 

Benennen Sie die Schnittstellen mithilfe des Windows PowerShell-Befehls **Rename-NetAdapter** oder durch Ausführen des folgenden Verfahrens:
  
1.  Im Server-Manager in **Eigenschaften** für den Netzwerkadapter, die Sie umbenennen möchten, klicken Sie auf den Link, um rechts neben den Namen des Netzwerkadapters. 
  
2.  Mit der rechten Maustaste in des Netzwerkadapters, die Sie verwenden möchten, benennen Sie ein, und wählen Sie **umbenennen**.  
  
3.  Geben Sie den neuen Namen für den Netzwerkadapter aus, und drücken Sie die EINGABETASTE.  


## <a name="virtual-machines-vms"></a>Virtuelle Computer (VMs)

Wenn Sie NIC-Teamvorgang auf einem virtuellen Computer verwenden möchten, müssen Sie die virtuellen Netzwerkadapter auf dem virtuellen Computer auf externe Hyper-V virtuelle Switches nur verbinden. Auf diese Weise können den virtuellen Computer Netzwerkkonnektivität sogar im Fall aufrechterhalten, wenn eines der physischen Netzwerkadapter, um einen virtuellen Switch ein Fehler auftritt verbunden, oder ruft getrennt. Virtuelle Netzwerkadapter mit internen oder privaten virtuellen Hyper-V-Switches verbunden sind, sind nicht mit dem Switch herstellen, wenn sie in einem Team sind, und Netzwerke ein Fehler, für den virtuellen Computer auftritt.  
  
NIC-Teamvorgang in Windows Server 2016 unterstützen Teams, die mit zwei Membern auf virtuellen Computern. Sie können größere Teams erstellen, aber es gibt keine Unterstützung für größere Teams. Jedes Teammitglied muss eine Verbindung mit einem anderen, externen, virtuelle Hyper-V-Switch herstellen, und die Netzwerkschnittstellen des virtuellen Computers müssen so konfiguriert werden, dass der Teamvorgang zulässig.

  
Wenn Sie einen NIC-Teams auf einem virtuellen Computer konfigurieren, müssen Sie auswählen einer **teammodus** von _Switchunabhängig_ und ein **Lastenausgleichsmodus** von _Adresshash_.   
  
  
## <a name="sr-iov-capable-network-adapters"></a>SR-IOV-fähige Netzwerkadapter  
SR-IOV-Datenverkehr kann von einem NIC-Team im oder unter der Hyper-V-Host kann nicht geschützt werden, da es über den Hyper-V-Switch geleitet nicht.  Klicken Sie mit der Option VM NIC-Teamvorgang können Sie zwei externer virtueller Hyper-V-Switches konfigurieren, jeweils einen eigenen SR-IOV-fähige NIC verbunden sind  
  
![NIC-Teaming mit SR-IOV-fähige Netzwerkadapter](../../media/NIC-Teaming-in-Virtual-Machines--VMs-/nict_in_vm.jpg)  
  
Jeder virtuelle Computer kann es sich um eine virtuelle Funktion (VF) von einem oder beiden SR-IOV-NICs und im Falle einer NIC trennen, Failover von der primären VF zum Sicherungsadapter (VF) verfügen. Alternativ können Sie der virtuellen Computer ein VF aus einer möglicherweise NIC und eine nicht-VF VmNIC mit einem anderen virtuellen Switch verbunden. Wenn die NIC, die die VF zugeordneten getrennt wird, der Datenverkehr können ein Failover auf den anderen Switch erfolgen, ohne Verlust der Verbindung.  
  
Da Failover zwischen NICs in einem virtuellen Computer Datenverkehr gesendet wird, mit der MAC-Adresse von den anderen VmNIC führen kann, muss jeder virtuelle Hyper-V-Switch Port eines virtuellen Computers mit NIC-Teamvorgang zugeordnet festgelegt werden, um Teamvorgang zu ermöglichen. 


## <a name="related-topics"></a>Verwandte Themen

- [NIC-Teamvorgang-MAC-Adresse und -Verwaltung](NIC-Teaming-MAC-Address-Use-and-Management.md): Beim Konfigurieren eines NIC-Teams mit unabhängigen Modus wechseln und adresshash oder dynamische lastverteilung steuern das Team verwendet, die die MAC-Adresse (MAC) des primären Mitglieds-NIC-Team für ausgehenden Datenverkehr. Dem primären NIC-Team-Mitglied ist, einen Netzwerkadapter, die vom Betriebssystem aus den anfänglichen Satz von Team-Mitglieder ausgewählt wird.

- [Einstellungen für die NIC-Teamvorgang](nic-teaming-settings.md): In diesem Thema haben wir bieten Ihnen einen Überblick über den NIC-Team-Eigenschaften, z. B. Teamvorgang und Lastenausgleich Modi zu laden. Sie haben zudem Details über die Standby-adaptereinstellung und die Eigenschaft des primären Team-Schnittstelle. Wenn Sie in einem NIC-Team über mindestens zwei Netzwerkadapter verfügen, müssen Sie keinen Standby-Adapter für die Fehlertoleranz zu bestimmen.
  
- [Erstellen eines neuen NIC-Teams auf einem Host oder virtuellen Computer](Create-a-New-NIC-Team-on-a-Host-Computer-or-VM.md): In diesem Thema erstellen Sie einen neuen NIC-Teams auf einem Hostcomputer oder in einer Hyper-V-Computer (VM) unter Windows Server 2016.

- [Problembehandlung bei der NIC-Teamvorgang](Troubleshooting-NIC-Teaming.md): In diesem Thema werden Möglichkeiten zum Beheben von NIC-Teamvorgang, z. B. Hardware, Wertpapiere der physische Switch und das Deaktivieren oder aktivieren Netzwerkadapter, die mithilfe von Windows PowerShell beschrieben. 
 
