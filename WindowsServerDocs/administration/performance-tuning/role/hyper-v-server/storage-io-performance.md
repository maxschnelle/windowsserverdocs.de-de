---
title: Hyper-V-Speicher-e/a-Leistung
description: Überlegungen zur Speicher-e/a-Leistung bei der Hyper-V-Leistungsoptimierung
ms.topic: article
ms.author: asmahi; sandysp; jopoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: d19790a6a86c7538ee3a062b3f08bbbdbc8b9d92
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87992088"
---
# <a name="hyper-v-storage-io-performance"></a>Hyper-V-Speicher-e/a-Leistung

In diesem Abschnitt werden die verschiedenen Optionen und Überlegungen zum Optimieren der Speicher-e/a-Leistung auf einem virtuellen Computer beschrieben. Der Speicher-e/a-Pfad erstreckt sich vom Gast Speicher Stapel, über die hostvirtualisierungsebene, auf den Host Speicher Stapel und dann auf den physischen Datenträger. Im folgenden finden Sie Erläuterungen dazu, wie Optimierungen in jeder dieser Phasen möglich sind.

## <a name="virtual-controllers"></a>Virtuelle Controller

Hyper-V bietet drei Arten von virtuellen Controllern: IDE, SCSI und virtuelle Hostbus Adapter (HBAs).

## <a name="ide"></a>IDE

IDE-Controller machen IDE-Datenträger für den virtuellen Computer verfügbar. Der IDE-Controller wird emuliert, und er ist der einzige Controller, der für Gast-VMS verfügbar ist, auf denen eine ältere Version von Windows ausgeführt wird, ohne dass der virtuelle Computer Integration Services. Datenträger-e/a, die mit dem IDE-Filtertreiber ausgeführt werden, der mit dem virtuellen Computer Integration Services bereitgestellt wird, ist erheblich besser als die Datenträger-e/a-Leistung, die mit dem emulierten IDE-Controller bereitgestellt wird. Es wird empfohlen, IDE-Datenträger nur für die Betriebssystem Datenträger zu verwenden, da Sie aufgrund der maximalen e/a-Größe, die für diese Geräte ausgegeben werden kann, Leistungseinschränkungen aufweisen.

## <a name="scsi-sas-controller"></a>SCSI (SAS-Controller)

SCSI-Controller machen SCSI-Datenträger für den virtuellen Computer verfügbar, und jeder virtuelle SCSI-Controller kann bis zu 64 Geräte unterstützen. Für eine optimale Leistung empfiehlt es sich, mehrere Datenträger an einen einzelnen virtuellen SCSI-Controller anzufügen und zusätzliche Controller nur dann zu erstellen, wenn Sie die Anzahl der Datenträger, die mit dem virtuellen Computer verbunden sind, Skalieren müssen. Der SCSI-Pfad wird nicht emuliert und macht ihn als bevorzugten Controller für jeden anderen Datenträger als den Betriebssystem Datenträger fest. Tatsächlich ist es bei VMS der Generation 2 die einzige Art von Controller. Dieser Controller wurde in Windows Server 2012 R2 eingeführt und wird als SAS gemeldet, um freigegebene vhdx zu unterstützen.

## <a name="virtual-fibre-channel-hbas"></a>Virtuelle Fibre Channel HBAs

Virtuelle Fibre Channel HBAs können so konfiguriert werden, dass Sie den direkten Zugriff auf virtuelle Computer Fibre Channel und Fibre Channel over Ethernet (FCoE) LUNs ermöglichen. Virtuelle Fibre Channel Datenträger umgehen das NTFS-Dateisystem in der Stamm Partition, wodurch die CPU-Auslastung der Speicher-e/a reduziert wird.

Große Daten Laufwerke und Laufwerke, die von mehreren virtuellen Computern gemeinsam genutzt werden (für Gastclustering-Szenarien), sind die wichtigsten Kandidaten für virtuelle Fibre Channel-Datenträger.

Für virtuelle Fibre Channel Datenträger muss mindestens ein Fibre Channel Hostbus Adapter (HBAs) auf dem Host installiert sein. Jeder Host-HBA ist erforderlich, um einen HBA-Treiber zu verwenden, der die virtuellen Fibre Channel/NPIV-Funktionen von Windows Server 2016 unterstützt. Das SAN-Fabric sollte NPIV unterstützen, und die HBA-Ports, die für die virtuelle Fibre Channel verwendet werden, sollten in einer Fibre Channel Topologie eingerichtet werden, die NPIV unterstützt.

Zum Maximieren des Durchsatzes auf Hosts, die mit mehr als einem HBA installiert werden, empfiehlt es sich, mehrere virtuelle HBAs innerhalb des virtuellen Hyper-V-Computers zu konfigurieren (bis zu vier HBAs können für jeden virtuellen Computer konfiguriert werden). Mit Hyper-V wird automatisch ein ausgewogenes Verhältnis zwischen virtuellen HBAs und Host-HBAs unternommen, die auf dasselbe virtuelle SAN zugreifen.

## <a name="virtual-disks"></a>Virtuelle Datenträger

Datenträger können für die virtuellen Computer über die virtuellen Controller verfügbar gemacht werden. Diese Datenträger können virtuelle Festplatten sein, bei denen es sich um Datei Abstraktionen eines Datenträgers oder einen Pass-Through-Datenträger auf dem Host handelt.

## <a name="virtual-hard-disks"></a>Virtuelle Festplatten

Es gibt zwei virtuelle Festplattenformate: VHD und vhdx. Jedes dieser Formate unterstützt drei Arten von virtuellen Festplatten Dateien.

## <a name="vhd-format"></a>VHD-Format

Das VHD-Format war das einzige Format der virtuellen Festplatte, das in früheren Versionen von Hyper-V unterstützt wurde. Das VHD-Format wurde in Windows Server 2012 eingeführt, um eine bessere Ausrichtung zu ermöglichen. Dies führt zu einer deutlich besseren Leistung bei neuen Datenträgern mit großen Sektoren.

Jede neue virtuelle Festplatte, die auf einem Windows Server 2012 oder neuer erstellt wird, weist die optimale Ausrichtung von 4 KB auf. Dieses ausgerichtete Format ist vollständig mit früheren Windows Server-Betriebssystemen kompatibel. Allerdings wird die Alignment-Eigenschaft bei neuen Zuordnungen von Parsern, die nicht 4-KB-Ausrichtungs fähig sind (z. b. ein VHD-Parser aus einer früheren Version von Windows Server oder einem nicht-Microsoft-Parser), nicht unterstützt.

Alle virtuellen Festplatten, die von einer vorherigen Version verschoben werden, werden nicht automatisch in dieses neue, verbesserte VHD-Format konvertiert.

Führen Sie den folgenden Windows PowerShell-Befehl aus, um in das neue VHD-Format zu konvertieren:

``` syntax
Convert-VHD –Path E:\vms\testvhd\test.vhd –DestinationPath E:\vms\testvhd\test-converted.vhd
```

Sie können die Alignment-Eigenschaft für alle VHDs im System überprüfen, und Sie sollte in die optimale Ausrichtung von 4 KB konvertiert werden. Sie erstellen eine neue virtuelle Festplatte mit den Daten aus der ursprünglichen VHD mithilfe der Option " **Create-from-Source** ".

Um die Ausrichtung mithilfe von Windows PowerShell zu überprüfen, überprüfen Sie die Ausrichtungslinie, wie unten dargestellt:

``` syntax
Get-VHD –Path E:\vms\testvhd\test.vhd

Path                    : E:\vms\testvhd\test.vhd
VhdFormat               : VHD
VhdType                 : Dynamic
FileSize                : 69245440
Size                    : 10737418240
MinimumSize             : 10735321088
LogicalSectorSize       : 512
PhysicalSectorSize      : 512
BlockSize               : 2097152
ParentPath              :
FragmentationPercentage : 10
Alignment               : 0
Attached                : False
DiskNumber              :
IsDeleted               : False
Number                  :
```

Um die Ausrichtung mithilfe von Windows PowerShell zu überprüfen, überprüfen Sie die Ausrichtungslinie, wie unten dargestellt:

``` syntax
Get-VHD –Path E:\vms\testvhd\test-converted.vhd

Path                    : E:\vms\testvhd\test-converted.vhd
VhdFormat               : VHD
VhdType                 : Dynamic
FileSize                : 69369856
Size                    : 10737418240
MinimumSize             : 10735321088
LogicalSectorSize       : 512
PhysicalSectorSize      : 512
BlockSize               : 2097152
ParentPath              :
FragmentationPercentage : 0
Alignment               : 1
Attached                : False
DiskNumber              :
IsDeleted               : False
Number                  :
```

## <a name="vhdx-format"></a>VHDX-Format

Vhdx ist ein neues Format der virtuellen Festplatte, das in Windows Server 2012 eingeführt wurde, mit dem Sie robuste hochleistungsfähige virtuelle Festplatten mit bis zu 64 Terabytes erstellen können. Zu den Vorteilen dieses Formats gehören:

-   Unterstützung für die Speicherkapazität virtueller Festplatten mit bis zu 64 Terabyte.

-   Schutz gegen Datenbeschädigung durch Stromausfälle durch Protokollieren der Aktualisierungen an den VHDX-Metadatenstrukturen.

-   Die Möglichkeit, benutzerdefinierte Metadaten zu einer Datei zu speichern, die ein Benutzer möglicherweise aufzeichnen möchte, z. b. die Betriebssystemversion oder die angewendeten Patches.

Das vhdx-Format bietet außerdem die folgenden Leistungsvorteile:

-   Verbesserte Ausrichtung des virtuellen Festplattenformats zur Unterstützung von Festplatten mit großen Sektoren.

-   Größere Blockgrößen für dynamische und differenzielle Datenträger, sodass diese Datenträger den Anforderungen der Arbeitsauslastung gerecht werden können.

-   virtueller Datenträger mit einer Größe von 4 KB, der eine bessere Leistung ermöglicht, wenn Sie von Anwendungen und Workloads verwendet wird, die für 4-KB-Sektoren entwickelt wurden

-   Effizienz bei der Darstellung von Daten, was zu einer geringeren Dateigröße führt und es dem zugrunde liegenden physischen Speichergerät ermöglicht, nicht verwendeten Speicherplatz freizugeben. (Für Trim sind Pass-Through-oder SCSI-Datenträger und Trim-kompatible Hardware erforderlich.)

Wenn Sie ein Upgrade auf Windows Server 2016 durchführen, empfiehlt es sich, dass Sie alle VHD-Dateien in das vhdx-Format konvertieren. Das einzige Szenario, in dem es sinnvoll wäre, die Dateien im VHD-Format beizubehalten, ist, wenn ein virtueller Computer in eine frühere Version von Hyper-V verschoben werden kann, die das vhdx-Format nicht unterstützt.

## <a name="types-of-virtual-hard-disk-files"></a>Typen von virtuellen Festplatten Dateien

Es gibt drei Arten von VHD-Dateien. In den folgenden Abschnitten werden die Leistungsmerkmale und Kompromisse zwischen den-Typen beschrieben.

Die folgenden Empfehlungen sollten hinsichtlich der Auswahl eines VHD-Dateityps berücksichtigt werden:

-   Wenn Sie das VHD-Format verwenden, empfiehlt es sich, den Fixed-Typ zu verwenden, da er im Vergleich zu den anderen VHD-Dateitypen eine bessere Resilienz und Leistungsmerkmale aufweist.

-   Wenn Sie das vhdx-Format verwenden, empfiehlt es sich, den dynamischen Typ zu verwenden, da er zusätzlich zu den Speicherplatz Einsparungen, die mit der Zuweisung von Speicherplatz verbunden sind, auch bei Bedarf zu Speicherplatz Einsparungen führen kann.

-   Der Typ "Fixed" wird auch unabhängig vom Format empfohlen, wenn der Speicher auf dem hostingvolume nicht aktiv überwacht wird, um sicherzustellen, dass ausreichend Speicherplatz vorhanden ist, wenn die VHD-Datei zur Laufzeit erweitert wird.

-   Mit Momentaufnahmen eines virtuellen Computers wird eine differenzierende VHD erstellt, um Schreibvorgänge auf den Datenträgern zu speichern. Wenn nur einige Momentaufnahmen vorhanden sind, kann die CPU-Auslastung von Speicher-e/a-Vorgängen erhöht werden, aber die Leistung wird möglicherweise nicht merklich beeinträchtigt, außer in hochgradig e/a-intensiven Server Arbeitslasten Eine große Anzahl von Momentaufnahmen kann sich jedoch deutlich auf die Leistung auswirken, da das Lesen der virtuellen Festplatte die Überprüfung der angeforderten Blöcke in vielen differenzierenden VHDs erfordern kann. Die Beibehaltung von Momentaufnahme Ketten ist wichtig, um eine gute e/a-Leistung zu gewährleisten.

## <a name="fixed-virtual-hard-disk-type"></a>Typ der virtuellen Festplatte mit fester Größe

Der Speicherplatz für die virtuelle Festplatte wird zuerst zugewiesen, wenn die VHD-Datei erstellt wird. Diese Art von VHD-Datei wird weniger wahrscheinlich fragmentieren. Dadurch wird der e/a-Durchsatz reduziert, wenn eine einzelne e/a in mehrere e/a-Vorgänge aufgeteilt wird. Sie hat den geringsten CPU-Aufwand der drei VHD-Dateitypen, da Lese-und Schreibvorgänge nicht die Zuordnung des Blocks nachschlagen müssen.

## <a name="dynamic-virtual-hard-disk-type"></a>Typ der dynamischen virtuellen Festplatte

Der Speicherplatz für die virtuelle Festplatte wird bei Bedarf zugewiesen. Die Blöcke im Datenträger beginnen als nicht zugeordnete Blöcke und werden nicht von einem tatsächlichen Speicherplatz in der Datei unterstützt. Beim ersten Schreiben eines Blocks in muss der Virtualisierungsstapel Platz in der VHD-Datei für den Block zuordnen und dann die Metadaten aktualisieren. Dies erhöht die Anzahl der erforderlichen Datenträger-e/a-Vorgänge für den Schreibvorgang und steigert die CPU-Auslastung. Lese-und Schreibvorgänge für vorhandene Blöcke verursachen Datenträger Zugriff und CPU-Overhead beim Suchen der Blockierung in den Metadaten.

## <a name="differencing-virtual-hard-disk-type"></a>Typ der differenzierenden virtuellen Festplatte

Die VHD verweist auf eine übergeordnete VHD-Datei. Alle Schreibvorgänge in Blöcke, die nicht so geschrieben wurden, dass in der VHD-Dateispeicher Platz zugeordnet wird, wie bei einer dynamisch erweiterbaren virtuellen Festplatte. Lesevorgänge werden von der VHD-Datei aus verarbeitet, wenn auf den Block geschrieben wurde. Andernfalls werden Sie von der übergeordneten VHD-Datei gewartet. In beiden Fällen werden die Metadaten gelesen, um die Zuordnung des Blocks zu ermitteln. Lese-und Schreibvorgänge für diese VHD können mehr CPU verbrauchen und zu mehr e/a-Vorgängen führen als eine VHD-Datei mit fester Größe.

## <a name="block-size-considerations"></a>Überlegungen zur Block Größe

Die Block Größe kann sich erheblich auf die Leistung auswirken. Es ist optimal, die Blockgröße mit den Zuordnungs Mustern der Arbeitsauslastung zu vergleichen, die den Datenträger verwendet. Wenn eine Anwendung z. b. in Blöcken von 16 MB zugeordnet ist, wäre es optimal, eine virtuelle Festplatten Blockgröße von 16 MB zu haben. Eine Blockgröße von &gt; 2 MB ist nur auf virtuellen Festplatten im vhdx-Format möglich. Wenn eine größere Blockgröße als das Zuordnungs Muster für eine zufällige e/a-Arbeitsauslastung vorhanden ist, erhöht sich die Speicherauslastung auf dem Host erheblich.

## <a name="sector-size-implications"></a>Auswirkungen auf Sektorgröße

Der größte Teil der Softwarebranche ist von den Datenträger Sektoren von 512 Bytes abhängig, aber der Standardwert für Datenträger Sektoren mit 4 KB. Um Kompatibilitätsprobleme zu vermeiden, die durch eine Änderung der Sektorgröße entstehen können, stellen Hersteller von Festplattenherstellern eine Übergangs Größe mit 512-Emulations Laufwerken (512 e) dar.

Diese Emulations Laufwerke bieten einige der Vorteile, die in nativen Laufwerken mit 4-KB-Datenträger Sektoren angeboten werden, z. b. eine verbesserte Format Effizienz und ein verbessertes Schema für Fehlerkorrekturcodes. Es treten weniger Kompatibilitätsprobleme auf, die durch die Bereitstellung einer Sektorgröße von 4 KB an der Datenträger Schnittstelle auftreten würden.

## <a name="support-for-512e-disks"></a>Unterstützung für 512 e-Festplatten

Ein 512 e-Datenträger kann Schreibvorgänge nur im Hinblick auf einen physischen Sektor ausführen – das heißt, er kann nicht direkt einen für ihn ausgegebenen 512-Byte-Sektor schreiben. Der interne Prozess auf dem Datenträger, der diese Schreibvorgänge ermöglicht, folgt den folgenden Schritten:

-   Der Datenträger liest den physischen Sektor mit 4 KB in seinen internen Cache, der den logischen 512-Byte-Sektor enthält, auf den der Schreibvorgang verweist.

-   Die Daten im 4-KB-Puffer werden geändert, sodass sie den aktualisierten 512-Byte-Sektor einschließen.

-   Das Laufwerk schreibt den Inhalt des aktualisierten 4-KB-Puffers zurück auf den physischen Sektor auf dem Laufwerk.

Dieser Vorgang wird als "Read-Modify-Write" (RMW) bezeichnet. Die Auswirkungen auf die Gesamtleistung des RMW-Prozesses sind abhängig von den Arbeits Auslastungen. Der RMW-Prozess verursacht aus folgenden Gründen eine Leistungsminderung bei virtuellen Festplatten:

-   Dynamische und differenzierende virtuelle Festplatten verfügen über eine 512-Byte-sektorbitmap vor Ihrer Daten Nutzlast. Außerdem werden Fußzeilen-, Header-und übergeordnete Locators an einem 512-Byte-Sektor ausgerichtet. Es kommt häufig vor, dass der virtuelle Festplattentreiber 512-Byte-Schreib Befehle ausgibt, um diese Strukturen zu aktualisieren, was zu dem zuvor beschriebenen RMW-Prozess führt.

-   Anwendungen geben häufig Lese-und Schreibvorgänge in Vielfachen von 4-KB-Größen aus (die Standard Clustergröße von NTFS). Da sich vor dem Daten Nutz Last Block dynamischer und differenzierender virtueller Festplatten eine 512-Byte-sektorbitmap befindet, sind die 4-KB-Blöcke nicht an der physischen 4-KB-Grenze ausgerichtet. Die folgende Abbildung zeigt einen VHD-Block mit 4 KB (hervorgehoben), der nicht an der physischen Grenze von 4 KB ausgerichtet ist.

![VHD 4 KB-Block](../../media/perftune-guide-vhd-4kb-block.png)

Jeder 4-KB-Schreibbefehl, der vom aktuellen Parser zum Aktualisieren der Nutzlastdaten ausgegeben wird, führt zu zwei Lesevorgängen für zwei Blöcke auf dem Datenträger, die dann aktualisiert und anschließend auf die beiden Datenträger Blöcke zurückgeschrieben werden. Hyper-V in Windows Server 2016 reduziert einige Leistungs Effekte auf 512 e-Datenträgern im VHD-Stapel, indem die zuvor erwähnten Strukturen für die Ausrichtung auf 4-KB-Begrenzungen im VHD-Format vorbereitet werden. Dies vermeidet den RMW-Effekt beim Zugriff auf die Daten in der virtuellen Festplatten Datei und beim Aktualisieren der Metadatenstrukturen der virtuellen Festplatten.

Wie bereits erwähnt, werden VHDs, die aus früheren Versionen von Windows Server kopiert wurden, nicht automatisch auf 4 KB ausgerichtet. Sie können Sie manuell konvertieren, indem Sie die Option **aus Quell** Datenträger kopieren verwenden, die in den VHD-Schnittstellen verfügbar ist.

VHDs werden standardmäßig mit einer physischen Sektorgröße von 512 Bytes verfügbar gemacht. Dadurch wird sichergestellt, dass abhängige Anwendungen von physischer Sektorgröße nicht beeinträchtigt werden, wenn die Anwendung und die VHDs aus einer früheren Version von Windows Server verschoben werden.

Standardmäßig werden Datenträger mit dem vhdx-Format mit der physischen Sektorgröße 4 KB erstellt, um Ihre Leistungsprofile für reguläre Datenträger und große sektordatenträger zu optimieren. Zum vollständigen Einsatz von 4-KB-Sektoren empfiehlt es sich, das vhdx-Format zu verwenden.

## <a name="support-for-native-4kb-disks"></a>Unterstützung für Native 4-KB-Datenträger

Hyper-V in Windows Server 2012 R2 und darüber hinaus unterstützt native Datenträger mit 4 KB. Es ist jedoch weiterhin möglich, VHD-Datenträger auf einem nativen 4-KB-Datenträger zu speichern Zu diesem Zweck wird ein RMW-Software Algorithmus in der virtuellen Speicher Stapel Ebene implementiert, der den 512-Byte-Zugriff und Update Anforderungen in entsprechende 4-KB-Zugriffe und-Updates konvertiert.

Da sich die VHD-Datei nur als Datenträger mit einer Größe von 512 Byte-logischen Sektoren verfügbar machen kann, ist es sehr wahrscheinlich, dass Anwendungen, die e/a-Anforderungen mit 512 Bytes ausgeben, vorhanden sind. In diesen Fällen erfüllt die RMW-Schicht diese Anforderungen und führt zu Leistungseinbußen. Dies gilt auch für einen Datenträger, der mit der vhdx-Datei mit einer logischen Sektorgröße von 512 Bytes formatiert ist.

Es ist möglich, eine vhdx-Datei so zu konfigurieren, dass Sie als Datenträger mit einer logischen Sektorgröße von 4 KB verfügbar gemacht wird. Dies ist eine optimale Konfiguration für die Leistung, wenn der Datenträger auf einem nativen physischen Gerät mit 4 KB gehostet wird. Es muss darauf geachtet werden, dass der Gast und die Anwendung, die den virtuellen Datenträger verwendet, durch die logische Sektorgröße von 4 KB gestützt werden. Die vhdx-Formatierung funktioniert ordnungsgemäß auf einem Gerät mit einer Größe von 4 KB.

## <a name="pass-through-disks"></a>Pass-Through-Datenträger

Die virtuelle Festplatte auf einem virtuellen Computer kann direkt einem physischen Datenträger oder einer logischen Gerätenummer (Logical Unit Number, LUN) anstelle einer VHD-Datei zugeordnet werden. Der Vorteil ist, dass diese Konfiguration das NTFS-Dateisystem in der Stamm Partition umgeht, wodurch die CPU-Auslastung der Speicher-e/a reduziert wird. Das Risiko besteht darin, dass physische Datenträger oder LUNs schwieriger zwischen Computern verschoben werden können als VHD-Dateien.

Pass-Through-Datenträger sollten aufgrund der Einschränkungen bei der Migration virtueller Computer vermieden werden.

## <a name="advanced-storage-features"></a>Erweiterte Speicher Features

### <a name="storage-quality-of-service-qos"></a>Quality of Service (QoS) für Speicher

Ab Windows Server 2012 R2 bietet Hyper-V die Möglichkeit, bestimmte QoS-Parameter (Quality of Service) für den Speicher auf den virtuellen Computern festzulegen. Quality of Service für Speicher stellt eine Speicherleistungsisolierung in einer mehrinstanzenfähigen Umgebung und Mechanismen bereit, um Sie zu benachrichtigen, wenn die Speicher-E/A-Leistung den definierten Schwellenwert nicht erfüllt, der erforderlich ist, damit die Arbeitsauslastungen Ihres virtuellen Computers effizient ausgeführt werden.

Mit Quality of Service für Speicher kann ein maximaler IOPS-Wert (Input/Output Operations per Second, Eingabe-/Ausgabevorgänge pro Sekunde) für Ihre virtuelle Festplatte festgelegt werden. Ein Administrator kann den Speicher-E/A drosseln, um einen Mandanten daran zu hindern, sehr umfangreiche Speicherressourcen zu beanspruchen, wenn dadurch ein anderer Mandant beeinflusst wird.

Sie können auch einen minimalen IOPS-Wert festlegen. Er wird benachrichtigt, wenn der IOPS-Wert für eine angegebene virtuelle Festplatte unter einem Schwellenwert liegt, der für die optimale Leistung erforderlich ist.

Die Infrastruktur der Metriken des virtuellen Computers wird auch mit speicherbezogenen Parametern aktualisiert, damit der Administrator die Leistung überwachen und zugehörige Parameter rückbelasten kann.

Maximale und minimale Werte werden in Bezug auf normalisierte IOPS-Werte angegeben, wobei alle 8 KB Daten als e/a gezählt werden.

Folgende Einschränkungen sind zu beachten:

-   Nur für virtuelle Festplatten

-   Differenzierender Datenträger darf keinen übergeordneten virtuellen Datenträger auf einem anderen Volume aufweisen

-   Replikat-QoS für Replikat Standort, separat vom primären Standort konfiguriert

-   Freigegebene vhdx wird nicht unterstützt.

Weitere Informationen zu Speicher Quality of Service finden Sie unter [Storage Quality of Service für Hyper-V](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn282281(v=ws.11)).

### <a name="numa-io"></a>NUMA-e/a

Windows Server 2012 und darüber hinaus unterstützen große virtuelle Computer, und jede große VM-Konfiguration (z. b. eine Konfiguration mit Microsoft SQL Server mit 64 virtuellen Prozessoren) benötigt auch Skalierbarkeit im Hinblick auf den e/a-Durchsatz.

Die folgenden wichtigen Verbesserungen, die zuerst in den Windows Server 2012-Speicher Stapel und Hyper-V eingeführt wurden, stellen die e/a-Skalierbarkeits Anforderungen großer virtueller Computer dar:

-   Eine Erhöhung der Anzahl der zwischen den Gast Geräten und dem Host Speicher Stapel erstellten Kommunikationskanäle.

-   Ein effizienterer e/a-Abschlussmechanismus zur Unterbrechung der Verteilung zwischen den virtuellen Prozessoren, um teure interprozessorunterbrechungen zu vermeiden.

In Windows Server 2012 wurden einige Registrierungseinträge in der Datei "HKLM \\ System \\ CurrentControlSet \\ Enum \\ VMBus \\ {Device ID} \\ {instance ID}" gespeichert, mit \\ denen die Anzahl der Kanäle angepasst werden kann. Außerdem richten Sie die virtuellen Prozessoren, die die e/a-Vervollständigung verarbeiten, an die virtuellen CPUs aus, die von der Anwendung als e/a-Prozessoren zugewiesen werden. Die Registrierungs Einstellungen werden auf Adapter Basis mit dem Hardwareschlüssel des Geräts konfiguriert.

-   **ChannelCount (DWORD)** Die Gesamtanzahl der zu verwendenden Kanäle mit maximal 16. Standardmäßig wird eine Obergrenze verwendet. Dies ist die Anzahl der virtuellen Prozessoren/16.

-   **Channelmask (QWORD)** Die Prozessor Affinität für die Kanäle. Wenn Sie nicht festgelegt oder auf 0 festgelegt ist, wird standardmäßig der vorhandene Kanal Verteilungs Algorithmus verwendet, den Sie für den normalen Speicher oder für Netzwerk Kanäle verwenden. Dadurch wird sichergestellt, dass Ihre Speicherkanäle nicht mit Ihren Netzwerk Kanälen in Konflikt stehen.

### <a name="offloaded-data-transfer-integration"></a>Offloaded Datenübertragung Integration

Wichtige Wartungsaufgaben für virtuelle Festplatten (z. b. zusammenführen, verschieben und komprimieren) hängen von dem Kopieren großer Datenmengen ab. Die aktuelle Methode zum Kopieren von Daten erfordert, dass die Daten an unterschiedlichen Standorten eingelesen und geschrieben werden, was sehr zeitaufwändig sein kann. Außerdem werden CPU-und Arbeitsspeicher Ressourcen auf dem Host verwendet, die möglicherweise zum Bedienen virtueller Maschinen verwendet wurden.

SAN-Hersteller (Storage Area Network) arbeiten daran, Kopiervorgänge für große Datenmengen nahezu in Echtzeit zu ermöglichen. Dieser Speicher ist so konzipiert, dass dem System oberhalb der Festplatten das Verschieben eines bestimmten Datasets von einem Speicherort zu einem anderen ermöglicht wird. Diese Hardware Funktion wird als offloaded Datenübertragung bezeichnet.

Hyper-V in Windows Server 2012 und höher unterstützt die Offload-Datenübertragung (ODX), sodass diese Vorgänge vom Gast Betriebssystem an die Host Hardware übermittelt werden können. Dadurch wird sichergestellt, dass die Arbeitsauslastung ODX-fähigen Speicher verwenden kann, wie dies bei der Ausführung in einer nicht virtualisierten Umgebung der Fall wäre. Der Hyper-V-Speicher Stapel gibt auch ODX-Vorgänge bei Wartungs Vorgängen für virtuelle Festplatten aus, z. b. zum Zusammenführen von Datenträgern und Speicher Migrationen, bei denen große Datenmengen verschoben werden.

### <a name="unmap-integration"></a>Zuordnung der Zuordnung aufheben

Dateien für virtuelle Festplatten sind als Dateien auf einem Speicher Volume vorhanden, und Sie geben verfügbaren Speicherplatz für andere Dateien frei. Da die Größe dieser Dateien tendenziell groß ist, kann der von Ihnen belegte Speicherplatz schnell zunehmen. Der Bedarf an physischem Speicher wirkt sich auf das IT-Hardware Budget aus. Es ist wichtig, die Verwendung von physischem Speicher so weit wie möglich zu optimieren.

Vor Windows Server 2012 hatte der Windows-Speicher Stapel im Gast Betriebssystem und auf dem Hyper-V-Host Einschränkungen, wenn Anwendungen Inhalt auf einer virtuellen Festplatte löschen, wodurch der Speicherplatz des Inhalts tatsächlich abgebrochen wurde. Dies hat zur Folge, dass diese Informationen nicht an die virtuelle Festplatte und das physische Speichergerät übermittelt werden konnten. Dies verhindert, dass der Hyper-V-Speicher Stapel die Speicherplatz Auslastung durch die VHD-basierten virtuellen Festplatten Dateien optimiert. Außerdem wurde das zugrunde liegende Speichergerät daran gehindert, den Speicherplatz freizugeben, der zuvor durch die gelöschten Daten belegt war.

Ab Windows Server 2012 unterstützt Hyper-V das Aufheben der Zuordnung von Benachrichtigungen, die es ermöglichen, dass vhdx-Dateien bei der Darstellung der darin enthaltenen Daten effizienter sind. Dies führt zu einer geringeren Größe von Dateien und ermöglicht dem zugrunde liegenden physischen Speichergerät, nicht verwendeten Speicherplatz freizugeben.

Nur Hyper-V-spezifische SCSI-, aktivierte IDE-und virtuelle Fibre Channel Controller ermöglichen dem Befehl zum Aufheben der Zuordnung vom Gast, den virtuellen Speicher Stapel des Hosts zu erreichen. Auf den virtuellen Festplatten unterstützen nur virtuelle Datenträger, die als vhdx formatiert sind, die Zuordnung von Befehlen des Gasts.

Aus diesen Gründen wird empfohlen, dass Sie vhdx-Dateien verwenden, die an einen SCSI-Controller angeschlossen sind, wenn keine virtuellen Fibre Channel-Datenträger verwendet werden.

## <a name="additional-references"></a>Weitere Verweise

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Serverkonfiguration](configuration.md)

-   [Hyper-V-Prozessorleistung](processor-performance.md)

-   [Hyper-V-Arbeitsspeicherleistung](memory-performance.md)

-   [E/A-Leistung für Hyper-V-Netzwerk](network-io-performance.md)

-   [Erkennen von Engpässen in einer virtualisierten Umgebung](detecting-virtualized-environment-bottlenecks.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)