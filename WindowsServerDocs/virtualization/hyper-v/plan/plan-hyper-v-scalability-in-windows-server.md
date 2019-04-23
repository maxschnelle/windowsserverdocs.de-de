---
title: Planen der Hyper-V-Skalierbarkeit unter Windows Server 2016
description: Listen, die die maximal unterstützte Anzahl für Komponenten, die Sie hinzufügen oder Entfernen von Hyper-V und Virtual Machines können z. B., wie viel Arbeitsspeicher und wie viele virtuelle Prozessoren.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: KBDAzure
ms.author: kathydav
ms.date: 09/28/2016
ms.openlocfilehash: 03a464269c8aea29c226dee776f0dfacfe48743a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850261"
---
# <a name="plan-for-hyper-v-scalability-in-windows-server-2016"></a>Planen der Hyper-V-Skalierbarkeit unter Windows Server 2016

> Gilt für: Windows Server 2016
  
Dieser Artikel bietet Details zu die maximale Konfiguration für Komponenten, die Sie hinzufügen und entfernen, die auf einem Hyper-V-Host oder der virtuelle Computer, z. B. virtuelle Prozessoren oder Prüfpunkte. Bei der Planung Ihrer Bereitstellung sollten Sie die Höchstwerte für jeden virtuellen Computer als auch diejenigen, die für den Hyper-V-Host gelten. 

Höchstwerte für Speicher und die logischen Prozessoren sind die größten Zunahme von Windows Server 2012 als Antwort auf Anforderungen zur Unterstützung neuer Szenarien wie z. B. Machine Learning- und Data-Analysen. Windows Server-Blog veröffentlicht vor kurzem die Leistungsergebnisse eines virtuellen Computers mit Exchange 5.5 Terabyte Arbeitsspeicher und 128 virtuelle Prozessoren, 4-TB-in-Memory-Datenbank ausgeführt wird. Leistung war größer als 95 % der Leistung eines physischen Servers. Weitere Informationen finden Sie unter [Leistung für umfangreiche virtueller Computer in Windows Server 2016 Hyper-V für die in-Memory-transaktionsverarbeitung](https://blogs.technet.microsoft.com/windowsserver/2016/09/28/windows-server-2016-hyper-v-large-scale-vm-performance-for-in-memory-transaction-processing/). Andere Versionsnummern sind vergleichbar mit denen, die für Windows Server 2012 gelten. \(Maximalwerte für Windows Server 2012 R2 sind identisch mit Windows Server 2012.\) 
  
> [!NOTE]  
> Weitere Informationen zu System Center Virtual Machine Manager (VMM) finden Sie unter [Virtual Machine Manager-](https://technet.microsoft.com/system-center-docs/vmm/vmm). VMM ist ein Microsoft-Produkt zur Verwaltung virtualisierter Datencenter, das separat verkauft wird.  
  
## <a name="maximums-for-virtual-machines"></a>Höchstwerte für virtuelle Computer  
Diese Maximalwerte gelten für jeden virtuellen Computer. Nicht alle Komponenten sind in beiden Generationen virtueller Computer verfügbar. Einen Vergleich der aufzulistenden Generationen finden Sie unter [sollten virtuelle Maschine der Generation 1 oder 2 in Hyper-V erstellen?](should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md) 
  
|Component|Maximal|Hinweise|  
|-------------|-----------|---------|  
|Prüfpunkte|50|Der tatsächliche Wert kann in Abhängigkeit vom verfügbaren Speicher niedriger sein. Jedem Prüfpunkt wird als AVHD-Datei gespeichert, der physische Speicher verwendet.|  
|Arbeitsspeicher|12 TB für Generation 2; <br>1 TB für Generation 1|Überprüfen Sie die Anforderungen für das jeweilige Betriebssystem, um den Mindestwert und den empfohlenen Wert zu bestimmen.|  
|Serielle (COM-) Anschlüsse|2|Keine|  
|Größe von direkt an einen virtuellen Computer angeschlossenen physischen Datenträgern|Variiert|Die maximale Größe hängt vom Gastbetriebssystem ab.|  
|Virtuelle Fibre Channel-Adapter|4|Es empfiehlt sich, jeden Fibre Channel-Adapter mit einem unterschiedlichen virtuellen SAN zu verbinden.|  
|Virtuelle Diskettenlaufwerke|1 virtuelles Diskettenlaufwerk|Keine|
|Kapazität virtueller Festplatten|64 TB für VHDX-Format;<br>Größe von 2040 GB für VHD-format|Jede virtuelle Festplatte wird auf physischen Medien in Abhängigkeit des durch die virtuelle Festplatte verwendeten Formats als VHDX- oder VHD-Datei unterstützt.|  
|Virtuelle IDE-Datenträger|4|(Manchmal auch als Datenträger als Startdatenträger bezeichnet) Startdatenträger muss an eines der IDE-Geräte angefügt werden. Beim Startdatenträger kann es sich entweder um eine virtuelle Festplatte oder um einen physischen Datenträger, der an einen virtuellen Computer angeschlossen ist, handeln.|  
|Virtuelle Prozessoren|240 für Generation 2;<br>64 für die Generation 1;<br>320, die auf das Hostbetriebssystem (Root-Partition) zur Verfügung.|Die Anzahl der von einem Gastbetriebssystem unterstützten virtuellen Prozessoren kann niedriger sein. Weitere Informationen finden Sie die Informationen, die für das jeweilige Betriebssystem veröffentlicht.|
|Virtuelle SCSI-Controller|4|Verwendung von virtuellen SCSI-Geräte muss es sich um Integrationsservices, die für unterstützte Gastbetriebssysteme verfügbar sind. Details für die Betriebssysteme werden unterstützt, finden Sie unter [unterstützt Linux- und FreeBSD-Computer](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md) und [unterstützt Windows-Gastbetriebssysteme](../supported-windows-guest-operating-systems-for-hyper-v-on-windows.md).|  
|Virtuelle SCSI-Datenträger|256|Jeder SCSI-Controller unterstützt maximal 64 Datenträger. Das heißt, für jeden virtuellen Computer können bis zu 256 virtuelle SCSI-Datenträger konfiguriert werden. (4 Controller x 64 Datenträger pro Controller)|  
|Virtuelle Netzwerkkarten|insgesamt 12:<br> – 8 bestimmte Hyper-V-Netzwerkadapter<br>-4 legacy-Netzwerkadapter|Die bestimmten Hyper-V-Netzwerkadapter bietet eine bessere Leistung und erfordert einen Treiber in Integrationsservices enthalten. Weitere Informationen finden Sie unter [Planen des Hyper-V-Netzwerks in Windows Server](plan-hyper-v-networking-in-windows-server.md).|  
  
## <a name="maximums-for-hyper-v-hosts"></a>Maximalwerte für Hyper-V-hosts  
Diese Maximalwerte gelten für jeden Hyper-V-Host.  
  
|Component|Maximal|Hinweise|  
|-------------|-----------|---------|  
|Logische Prozessoren|512|Beide müssen in der Firmware aktiviert sein:<br /><br />-Die hardwareunterstützte Virtualisierung<br />– Von der Hardware erzwungene Datenausführungsverhinderung (DEP)<br /><br />Das Hostbetriebssystem (Root-Partition) wird nur maximale 320 logische Prozessoren angezeigt.|  
|Arbeitsspeicher|24 TB|Keine|  
|Netzwerkkartenbegriffe (NIC-Teamvorgang)|Keine Begrenzung durch Hyper-V.|Weitere Informationen finden Sie unter [NIC-Teamvorgang](../../../networking/technologies/nic-teaming/NIC-Teaming.md).|  
|Physische Netzwerkkarten|Keine Begrenzung durch Hyper-V.|Keine|  
|Virtuelle Computer pro Server|1024|Keine|  
|Speicher|Begrenzt durch den wird vom Betriebssystem Hosts unterstützt. Keine Begrenzung durch Hyper-V.|**Hinweis**: Microsoft unterstützt Network attached Storage (NAS), wenn SMB 3.0 verwendet wird. Die NFS-basierte Speicherung wird nicht unterstützt.|
|Virtuelle Netzwerk-Switchports pro Server|Unterschiedlich; keine Begrenzung durch Hyper-V.|Der Grenzwert hängt in der Praxis von den verfügbaren Computerressourcen ab.|  
|Virtuelle Prozessoren pro logischem Prozessor|Kein Verhältnis durch Hyper-V vorgegeben.|Keine|  
|Virtuelle Prozessoren pro Server|2.048|Keine|  
|Virtuelle SANs (Storage Area Networks).|Keine Begrenzung durch Hyper-V.|Keine|  
|Virtuelle Switches|Unterschiedlich; keine Begrenzung durch Hyper-V.|Der Grenzwert hängt in der Praxis von den verfügbaren Computerressourcen ab.|  
 
## <a name="failover-clusters-and-hyper-v"></a>Failovercluster und Hyper-V  
Diese Tabelle enthält die Höchstwerte bei Verwendung von Hyper-V und Failover-Clusterunterstützung. Es ist wichtig, kapazitätsplanung, um sicherzustellen, dass ausreichend Hardwareressourcen zum Ausführen aller virtuellen Computer in einer Clusterumgebung nutzen.  

Informationen zu Updates für die Failover-Clusterunterstützung, einschließlich neuer Funktionen für virtuelle Computer finden Sie unter [neues beim Failoverclustering unter Windows Server 2016](../../../failover-clustering/whats-new-in-failover-clustering.md).

|Component|Maximal|Hinweise|  
|-------------|-----------|---------|  
|Knoten pro Cluster|64|Berücksichtigen Sie die Anzahl von Knoten, die Sie für das Failover reservieren möchten, sowie Wartungsaufgaben wie etwa das Anwenden von Updates. Es wird empfohlen, ausreichend Ressourcen einzuplanen, damit 1 Knoten für das Failover reserviert werden kann. Dies bedeutet, dass dieser Knoten sich so lange im Leerlauf befindet, bis das Failover zu einem anderen Knoten erfolgt ist. (Dies wird manchmal als passiver Knoten bezeichnet.) Sie können diesen Wert erhöhen, wenn Sie zusätzliche Knoten reservieren möchten. Ist keine empfohlene Verhältnis oder Multiplikator von reservierten Knoten zum aktiven Knoten; die einzige Voraussetzung ist, dass die Gesamtzahl der Knoten in einem Cluster darf nicht das Maximum von 64 überschreiten.|  
|Ausführen virtueller Computer pro Cluster und pro Knoten|8.000 pro Cluster|Die tatsächliche Anzahl von virtuellen Computern, die Sie zur gleichen Zeit auf einem Knoten, wie z. B. ausführen können, können von verschiedenen Faktoren beeinflusst:<br />– Menge des physischen Arbeitsspeichers, die von jedem virtuellen Computer verwendet wird.<br />-Netzwerk und Speicherbandbreite.<br />-Anzahl der Festplattenspindles, e/a-Leistung auswirkt.|  
  

