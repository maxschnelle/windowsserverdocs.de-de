---
title: Planen der Hyper-V-Skalierbarkeit in Windows Server 2016 und Windows Server 2019
description: Listet die maximal unterstützte Anzahl von Komponenten auf, die Sie zu Hyper-V und virtuellen Computern hinzufügen bzw. daraus entfernen können, wie viel Arbeitsspeicher und wie viele virtuelle Prozessoren.
manager: dongill
ms.topic: article
author: kbdazure
ms.author: kathydav
ms.date: 09/28/2016
ms.openlocfilehash: bf7ad4e90f5303041153bb4f651d2f09c613da84
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996061"
---
# <a name="plan-for-hyper-v-scalability-in-windows-server-2016-and-windows-server-2019"></a>Planen der Hyper-V-Skalierbarkeit in Windows Server 2016 und Windows Server 2019

> Gilt für: Windows Server 2016, Windows Server 2019

Dieser Artikel enthält Details zur maximalen Konfiguration für Komponenten, die Sie auf einem Hyper-V-Host oder seinen virtuellen Maschinen hinzufügen und entfernen können, z. b. virtuelle Prozessoren oder Prüfpunkte. Berücksichtigen Sie beim Planen der Bereitstellung die Höchstwerte, die für die einzelnen virtuellen Computer gelten, sowie die für den Hyper-V-Host geltenden Höchstwerte.

Maximums für Arbeitsspeicher und logische Prozessoren sind die größten Steigerungen von Windows Server 2012 als Reaktion auf Anforderungen zur Unterstützung von neueren Szenarien wie Machine Learning und Datenanalyse. Der Windows Server-Blog veröffentlichte vor kurzem die Leistungsergebnisse eines virtuellen Computers mit 5,5 Terabyte Arbeitsspeicher und 128 virtuellen Prozessoren mit einer in-Memory Database von 4 TB. Die Leistung war größer als 95% der Leistung eines physischen Servers. Weitere Informationen finden Sie unter [Windows Server 2016 Hyper-V-VM-Leistung in großem Maßstab für die Verarbeitung im Arbeitsspeicher](https://blogs.technet.microsoft.com/windowsserver/2016/09/28/windows-server-2016-hyper-v-large-scale-vm-performance-for-in-memory-transaction-processing/). Andere Zahlen ähneln denen für Windows Server 2012. \(Maximums für Windows Server 2012 R2 waren identisch mit Windows Server 2012.\)

> [!NOTE]
> Informationen zu System Center Virtual Machine Manager (VMM) finden Sie unter [Virtual Machine Manager](/system-center/vmm/overview?view=sc-vmm-2019). VMM ist ein Microsoft-Produkt zur Verwaltung virtualisierter Datencenter, das separat verkauft wird.

## <a name="maximums-for-virtual-machines"></a>Maximums für virtuelle Maschinen
Diese Höchstwerte gelten für jeden virtuellen Computer. Nicht alle Komponenten sind in beiden Generationen virtueller Computer verfügbar. Einen Vergleich der Generationen finden Sie unter [sollte ich einen virtuellen Computer der Generation 1 oder 2 in Hyper-V erstellen?](should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md)

|Komponente|Maximum|Hinweise|
|-------------|-----------|---------|
|Prüfpunkte|50|Der tatsächliche Wert kann in Abhängigkeit vom verfügbaren Speicher niedriger sein. Jeder Prüfpunkt wird als AVHD-Datei gespeichert, die physischen Speicher verwendet.|
|Arbeitsspeicher|12 TB für Generation 2; <br>1 TB für Generation 1|Überprüfen Sie die Anforderungen für das jeweilige Betriebssystem, um den Mindestwert und den empfohlenen Wert zu bestimmen.|
|Serielle (COM-) Anschlüsse|2|Keine.|
|Größe von direkt an einen virtuellen Computer angeschlossenen physischen Datenträgern|Varies|Die maximale Größe hängt vom Gastbetriebssystem ab.|
|Virtuelle Fibre Channel-Adapter|4|Es empfiehlt sich, jeden Fibre Channel-Adapter mit einem unterschiedlichen virtuellen SAN zu verbinden.|
|Virtuelle Diskettenlaufwerke|1 virtuelles Diskettenlaufwerk|Keine.|
|Kapazität virtueller Festplatten|64 TB für vhdx-Format;<br>2040 GB für VHD-Format|Jede virtuelle Festplatte wird auf physischen Medien in Abhängigkeit des durch die virtuelle Festplatte verwendeten Formats als VHDX- oder VHD-Datei unterstützt.|
|Virtuelle IDE-Datenträger|4|Der Start Datenträger (manchmal als Start Datenträger bezeichnet) muss an eines der IDE-Geräte angeschlossen werden. Beim Startdatenträger kann es sich entweder um eine virtuelle Festplatte oder um einen physischen Datenträger, der an einen virtuellen Computer angeschlossen ist, handeln.|
|Virtuelle Prozessoren|240 für Generation 2;<br>64 für Generation 1;<br>320 verfügbar für das Host Betriebssystem (Stamm Partition)|Die Anzahl der von einem Gastbetriebssystem unterstützten virtuellen Prozessoren kann niedriger sein. Weitere Informationen finden Sie in den Informationen, die für das jeweilige Betriebssystem veröffentlicht wurden.|
|Virtuelle SCSI-Controller|4|Die Verwendung von virtuellen SCSI-Geräten erfordert Integration Services, die für unterstützte Gast Betriebssysteme verfügbar sind. Ausführliche Informationen dazu, welche Betriebssysteme unterstützt werden, finden Sie [unter Unterstützte virtuelle Linux-und FreeBSD](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md) -Computer und [unterstützte Windows-Gast Betriebssysteme](../supported-windows-guest-operating-systems-for-hyper-v-on-windows.md).|
|Virtuelle SCSI-Datenträger|256|Jeder SCSI-Controller unterstützt maximal 64 Datenträger. Das heißt, für jeden virtuellen Computer können bis zu 256 virtuelle SCSI-Datenträger konfiguriert werden. (4 Controller x 64 Datenträger pro Controller)|
|Virtuelle Netzwerkkarten|Windows Server 2016 unterstützt 12 gesamt:<br> -8 Hyper-V-spezifische Netzwerkadapter<br>-4 Legacy-Netzwerkadapter <br> Windows Server 2019 unterstützt 68 gesamt: <br> -64 Hyper-V-spezifische Netzwerkadapter<br>-4 Legacy-Netzwerkadapter  |Der Hyper-V-spezifische Netzwerkadapter bietet eine bessere Leistung und erfordert einen Treiber, der in Integration Services enthalten ist. Weitere Informationen finden Sie unter [Planen von Hyper-V-Netzwerken in Windows Server](plan-hyper-v-networking-in-windows-server.md).|

## <a name="maximums-for-hyper-v-hosts"></a>Maximums für Hyper-V-Hosts
Diese Höchstwerte gelten für jeden Hyper-V-Host.

|Komponente|Maximum|Hinweise|
|-------------|-----------|---------|
|Logische Prozessoren|512|Beide müssen in der Firmware aktiviert werden:<p>-Hardware gestützte Virtualisierung<br />-Hardware erzwungene Daten Ausführungs Verhinderung (Data Execution Prevention, DEP)<p>Für das Host Betriebssystem (Stamm Partition) werden nur die maximalen 320 logischen Prozessoren angezeigt.|  
|Arbeitsspeicher|24 TB|Keine.|
|Netzwerkkartenbegriffe (NIC-Teamvorgang)|Keine Begrenzung durch Hyper-V.|Weitere Informationen finden Sie unter [NIC](../../../networking/technologies/nic-teaming/NIC-Teaming.md)-Team Vorgang.|
|Physische Netzwerkkarten|Keine Begrenzung durch Hyper-V.|Keine.|
|Virtuelle Computer pro Server|1024|Keine.|
|Storage|Begrenzt durch das, was vom Host Betriebssystem unterstützt wird. Keine Begrenzung durch Hyper-V.|**Hinweis:** Bei Verwendung von SMB 3,0 unterstützt Microsoft Network Attached Storage (NAS). Die NFS-basierte Speicherung wird nicht unterstützt.|
|Virtuelle Netzwerk-Switchports pro Server|Unterschiedlich; keine Begrenzung durch Hyper-V.|Der Grenzwert hängt in der Praxis von den verfügbaren Computerressourcen ab.|
|Virtuelle Prozessoren pro logischem Prozessor|Kein Verhältnis durch Hyper-V vorgegeben.|Keine.|
|Virtuelle Prozessoren pro Server|2048|Keine.|
|Virtuelle SANs (Storage Area Networks).|Keine Begrenzung durch Hyper-V.|Keine.|
|Virtuelle Switches|Unterschiedlich; keine Begrenzung durch Hyper-V.|Der Grenzwert hängt in der Praxis von den verfügbaren Computerressourcen ab.|

## <a name="failover-clusters-and-hyper-v"></a>Failovercluster und Hyper-V
In dieser Tabelle werden die Höchstwerte aufgelistet, die bei der Verwendung von Hyper-V und Failoverclustering gelten. Es ist wichtig, dass Sie eine Kapazitätsplanung durchführen, um sicherzustellen, dass ausreichend Hardware Ressourcen vorhanden sind, um alle virtuellen Computer in einer Cluster Umgebung auszuführen.

Weitere Informationen zu Updates für das Failoverclustering, einschließlich neuer Features für virtuelle Computer, finden Sie unter [Neues beim Failoverclustering unter Windows Server 2016](../../../failover-clustering/whats-new-in-failover-clustering.md).

|Komponente|Maximum|Hinweise|
|-------------|-----------|---------|
|Knoten pro Cluster|64|Berücksichtigen Sie die Anzahl von Knoten, die Sie für das Failover reservieren möchten, sowie Wartungsaufgaben wie etwa das Anwenden von Updates. Es wird empfohlen, ausreichend Ressourcen einzuplanen, damit 1 Knoten für das Failover reserviert werden kann. Dies bedeutet, dass dieser Knoten sich so lange im Leerlauf befindet, bis das Failover zu einem anderen Knoten erfolgt ist. (Dies wird mitunter auch als passiver Knoten bezeichnet.) Sie können diese Anzahl erhöhen, wenn Sie zusätzliche Knoten reservieren möchten. Es gibt kein empfohlenes Verhältnis oder einen Multiplikator reservierter Knoten für aktive Knoten. die einzige Voraussetzung besteht darin, dass die Gesamtanzahl der Knoten in einem Cluster nicht den maximalen Wert von 64 überschreiten kann.|
|Ausführen virtueller Computer pro Cluster und pro Knoten|8.000 pro Cluster|Mehrere Faktoren können sich auf die tatsächliche Anzahl von virtuellen Computern auswirken, die Sie gleichzeitig auf einem Knoten ausführen können, wie z. b.:<br />-Menge des physischen Speichers, der von den einzelnen virtuellen Computern verwendet wird.<br />-Netzwerk-und Speicherbandbreite.<br />-Anzahl der Datenträger Spindeln, die sich auf die Datenträger-e/a-Leistung auswirken.|