---
title: Hyper-V-Speicher-e/a-Leistung
description: Speicher-e/a-Leistungsaspekte in Hyper-V zur leistungsoptimierung
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: fedc23083914bcf97a8cde12b78c0b174143de25
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831311"
---
# <a name="hyper-v-storage-io-performance"></a>Hyper-V-Speicher-e/a-Leistung

Dieser Abschnitt beschreibt die verschiedenen Optionen und Überlegungen für die Optimierung von Speicher-e/a-Leistung auf einem virtuellen Computer. Der Speicher-e/a-Pfad erstreckt sich von den Gast-Speicherstapel, bis der Host-Virtualisierungsschicht, für den Host-Speicherstapel, und klicken Sie dann auf den physischen Datenträger. Es folgen Erklärungen dazu, wie Optimierungen an jede dieser Phasen möglich sind.

## <a name="virtual-controllers"></a>Virtuelle Controller

Hyper-V bietet drei Arten von virtuellen Domänencontrollern: IDE, SCSI und virtuellen Hostbusadapter (HBAs).

## <a name="ide"></a>IDE

IDE-Controller verfügbar machen, IDE-Datenträger an den virtuellen Computer. Der IDE-Controller wird emuliert, und es ist der einzige Domänencontroller, die für die Gast-VMs, die mit der älteren Version von Windows ohne die Integrationsdienste der virtuellen Computer verfügbar ist. Datenträger-e/a, die mit der IDE-Filtertreiber, der bereitgestellt wird, die die VM-Integrationsdienste ausgeführt wird, ist wesentlich höher als der Datenträger-e/a-Leistung, die mit den emulierten IDE-Controller bereitgestellt wird. Es wird empfohlen, dass die IDE-Datenträger nur für Betriebssystem-Datenträger verwendet werden, da sie leistungseinschränkungen aufgrund der maximalen e/a-Größe aufweisen, die für diese Geräte ausgestellt werden können.

## <a name="scsi-sas-controller"></a>SCSI (SAS-Controller)

SCSI-Controller verfügbar machen, SCSI-Datenträger an den virtuellen Computer aus, und jeder virtuelle SCSI-Controller kann bis zu 64 Geräte unterstützen. Um eine optimale Leistung empfehlen wir, fügen Sie mehrere Datenträger an einen einzelnen virtuellen SCSI-Controller und zusätzliche Controller zu erstellen, nur bei Bedarf skalieren Sie die Anzahl von Datenträgern, die mit dem virtuellen Computer verbunden sind. SCSI-Pfad wird nicht emuliert werden die bevorzugten Domänencontroller für Datenträger als Betriebssystem-Datenträger. Mit VMs der 2. Generation ist es in der Tat die einzige Art von Domänencontroller möglich. In Windows Server 2012 R2 eingeführt wurde, ist dieser Controller als SAS gemeldet zur Unterstützung von freigegebenen VHDX.

## <a name="virtual-fibre-channel-hbas"></a>Virtuelle Fibre Channel-HBAs

Virtuelle Fibre Channel-HBAs können für den um Direktzugriff für virtuelle Computer mit Fibre Channel- und Fibre Channel über Ethernet (FCoE)-LUNs zu ermöglichen konfiguriert werden. Virtuelle Fibre Channel-Datenträger, umgehen die NTFS-Dateisystem in der Stammpartition, die wodurch die CPU-Auslastung von Speicher-e/a reduziert wird.

Umfangreiche Daten und Laufwerke, die freigegeben werden mehrere virtuelle Computer (für Gast-clustering-Szenarien) sind ideale Kandidaten für virtuelle Fibre Channel-Datenträger.

Virtueller Fibre Channel-Datenträger ist erforderlich, eine oder mehrere Fibre Channel Hostbusadapter (HBAs), auf dem Host installiert werden. Jeder Host-HBA ist erforderlich, um einen HBA-Treiber verwenden, der die Funktionen von Windows Server 2016 Virtual Fibre Channel/NPIV unterstützt. Die SAN-Fabric sollte die NPIV unterstützt, und die HBA-Ports, die für den virtuellen Fibre Channel verwendet werden, in einer Fibre Channel-Topologie, die NPIV unterstützt eingerichtet werden soll.

Um Durchsatz auf den Hosts zu maximieren, die mit mehr als einen HBA installiert sind, wird empfohlen, mehrere virtuellen HBAs auf dem virtuellen Hyper-V-Computer zu konfigurieren (bis zu vier HBAs kann für jeden virtuellen Computer konfiguriert werden). Hyper-V wird automatisch versucht, den virtuellen HBAs auf Host-HBAs zu verteilen, die Zugriff auf das gleiche virtuelle SAN stellen.

## <a name="virtual-disks"></a>Virtuelle Datenträger

Datenträger können auf die virtuellen Computer über das virtuelle Controller verfügbar gemacht werden. Dieser Datenträger ist möglicherweise virtuelle Festplatten, der Datei Abstraktionen von einem Datenträger oder einen Pass-Through-Datenträger auf dem Host sind.

## <a name="virtual-hard-disks"></a>Virtuelle Festplatten

Es gibt zwei virtuelle Festplattenformate VHD und VHDX. Jede der folgenden Formate unterstützt drei Arten von Dateien virtueller Festplatten.

## <a name="vhd-format"></a>VHD-format

Das VHD-Format war die einzige virtuelle Festplatte-Format, das in früheren Versionen von Hyper-V unterstützt wurde. In Windows Server 2012 eingeführt wurde, hat das VHD-Format geändert, um eine bessere Ausrichtung zu ermöglichen, die erheblich bessere auf neuen Datenträger mit großen Sektoren Leistung.

Jeder neue virtuelle Festplatte, die auf einem Windows Server 2012 oder höher erstellt wird, hat die optimale 4-KB-Ausrichtung. Diese ausgerichteten Format ist vollständig kompatibel mit früheren Windows Server-Betriebssystemen. Allerdings werden die Ausrichtungseigenschaft für neue Zuordnungen vom Parser unterbrochen, die Ausrichtung-fähig, z. B. (eine VHD-Parser von einer früheren Version von Windows Server) oder einen nicht-Microsoft-Parser als 4 KB sind.

Eine VHD, die von einer früheren Version verschoben werden, ist nicht automatisch in dieses neue, verbesserte VHD-Format konvertiert abrufen.

Führen Sie den folgenden Windows PowerShell-Befehl, um in der neuen VHD-Format zu konvertieren:

``` syntax
Convert-VHD –Path E:\vms\testvhd\test.vhd –DestinationPath E:\vms\testvhd\test-converted.vhd
```

Sehen Sie sich die Ausrichtungseigenschaft für alle virtuellen Festplatten auf dem System, und es um die optimale 4-KB-Ausrichtung konvertiert werden sollen. Erstellen Sie eine neue virtuelle Festplatte mit den Daten aus der ursprünglichen virtuellen Festplatte mithilfe der **erstellen-aus-Source-** Option.

Überprüfen Sie zum Überprüfen mithilfe von Windows Powershell für die Ausrichtung der Zeile Ausrichtung, wie unten dargestellt:

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

Überprüfen Sie die Ausrichtung-Zeile, um Ausrichtung mithilfe von Windows PowerShell zu überprüfen, wie unten dargestellt:

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

## <a name="vhdx-format"></a>VHDX-format

VHDX wird ein neues VHD-Format, eingeführt in Windows Server 2012, in dem Sie robuste virtueller Datenträger mit hoher Leistung bis zu 64 Terabyte erstellen können. Dieses Formats bietet folgende Vorteile:

-   Unterstützung für die virtuelle Festplatte Speicherkapazität von bis zu 64 Terabyte.

-   Schutz gegen Datenbeschädigung durch Stromausfälle durch Protokollieren der Aktualisierungen an den VHDX-Metadatenstrukturen.

-   Fähigkeit zum Speichern von benutzerdefinierten Metadaten zu einer Datei, die ein Benutzer, z. B. die Betriebssystemversion oder ein angewendetes aufzeichnen möchten.

Das VHDX-Format bietet außerdem die folgenden Leistungsvorteile:

-   Verbesserte Ausrichtung des virtuellen Festplattenformats zur Unterstützung von Festplatten mit großen Sektoren.

-   Größere Blöcke für dynamische und differenzielle Datenträger, wodurch dieser Datenträger an, an die Anforderungen der Workload abzustimmen.

-   4 KB logische Sektorgröße virtueller Datenträger, der es höhere Leistung ermöglicht bei Verwendung von Anwendungen und Workloads, die entwickelt wurden, für die 4-KB-Sektoren.

-   Die Effizienz beim Darstellen von Daten, wodurch kleinere Dateigrößen führt und die zugrunde liegende physische Speichergerät nicht verwendeten Speicherplatz freigeben. (Die Trim erfordert Pass-Through oder SCSI-Datenträger und Trim-kompatibler Hardware).

Wenn Sie auf Windows Server 2016 aktualisieren, empfehlen wir, dass Sie alle VHD-Dateien in das VHDX-Format aufgrund dieser Vorteile konvertieren. Das einzige Szenario, in dem die Dateien in das VHD-Format beibehalten sinnvoll wäre, ist, wenn es sich bei ein virtuellen Computer hat das Potenzial, die in einer früheren Version von Hyper-V verschoben werden, die das VHDX-Format nicht unterstützt.

## <a name="types-of-virtual-hard-disk-files"></a>Typen von Dateien virtueller Festplatten

Es gibt drei Arten von VHD-Dateien. In den folgenden Abschnitten sind die Leistungsmerkmale und die vor-und Nachteile zwischen den Typen.

Die folgenden Empfehlungen sollen im Hinblick auf das Auswählen eines Typs der VHD-Datei berücksichtigt werden:

-   Wenn Sie das VHD-Format zu verwenden, empfehlen wir, dass Sie den festen Typ verwenden, da sie eine höhere Flexibilität und Leistungsmerkmale, die im Vergleich zu anderen VHD-Dateitypen hat.

-   Wenn Sie das VHDX-Format zu verwenden, empfehlen wir, dass den dynamischen Typ verwenden, da er Stabilität Garantien zusätzlich zur Einsparung von Speicherplatz, die bietet mit datenträgerzuweisung nur, wenn ein entsprechender Bedarf vorhanden ist.

-   Der feste Typ wird auch unabhängig von dem Format, empfohlen, wenn der Speicher auf dem hostingvolume nicht aktiv überwacht wird, stellen Sie sicher, dass genügend Speicherplatz vorhanden, wenn die VHD-Datei zur Laufzeit erweitert ist.

-   Nach dem Erstellen von Momentaufnahmen einer virtuellen Maschine eine differenzierende virtuelle Festplatte zum Speichern von Schreibvorgänge auf den Datenträgern. Müssen nur ein paar Momentaufnahmen die CPU-Auslastung von Speicher-e/as, jedoch möglicherweise nicht deutlich erhöhen können beeinträchtigt außer bei hoher e/A-Intensive serverarbeitsauslastungen. Allerdings kann eine großen Kette von Momentaufnahmen erheblich Leistung beeinträchtigen, da beim Lesen von der virtuellen Festplatte erforderlich sein kann, Überprüfen der angeforderten Blöcke auf vielen differenzierenden VHDs. Momentaufnahme Ketten kurz zu halten, ist wichtig, für die Verwaltung von guten Datenträger-e/a-Leistung.

## <a name="fixed-virtual-hard-disk-type"></a>Feste virtuelle Festplatte-Typ

Zunächst wird Speicherplatz für die virtuelle Festplatte zugeordnet, wenn die VHD-Datei erstellt wird. Diese Art von VHD-Datei ist weniger wahrscheinlich, fragment ist, dass dadurch verringern sich die e/a-Durchsatz bei einer einzelnen e/a in mehrere e/as aufgeteilt wird. Sie hat die niedrigste CPU-Auslastung der drei Typen der VHD-Datei, da Lese- und Schreibvorgänge nicht benötigen, um die Zuordnung des Blocks suchen.

## <a name="dynamic-virtual-hard-disk-type"></a>Typ der dynamischen virtuellen Festplatte

Speicherplatz für die virtuelle Festplatte wird bei Bedarf zugeordnet. Die Blöcke auf dem Datenträger als nicht zugeordneten Blöcken gestartet werden und verfügen nicht über alle tatsächlich Speicherplatz in der Datei. Wenn der erste eines Blocks ist muss geschrieben, die virtualisierungsstapels Speicherplatz innerhalb der VHD-Datei für das der Block belegt und klicken Sie dann die Metadaten aktualisiert werden. Dies erhöht die Anzahl der erforderlichen Datenträger-e/a für das Schreiben und CPU-Auslastung. Liest und schreibt auf vorhandene Blöcke Zugriff auf die Festplatte und CPU-Auslastung verursachen, bei der Suche nach Blöcke-Zuordnung in den Metadaten.

## <a name="differencing-virtual-hard-disk-type"></a>Typ der differenzierenden virtuellen Festplatte

Die virtuelle Festplatte verweist auf eine übergeordnete VHD-Datei. Alle Schreibvorgänge an Blöcken, die nicht zu einer Speicherplatz in der VHD-Datei, wie bei einer dynamisch erweiterbaren virtuellen Festplatte geschrieben werden soll. Lesevorgänge werden aus der VHD-Datei bearbeitet werden, wenn der Block geschrieben wurde. Andernfalls werden sie von der übergeordneten VHD-Datei abgewickelt. In beiden Fällen wird die Metadaten lesen, um die Zuordnung des Blocks zu bestimmen. Liest und schreibt in diese virtuelle Festplatte mehr CPU-Leistung nutzen können, und führen mehr e/as als eine feste VHD-Datei.

## <a name="block-size-considerations"></a>Überlegungen zu Block-Größen

Blockgröße kann die Leistung deutlich beeinträchtigen. Es ist am besten mit die Blockgröße zu den zuordnungsmustern der arbeitsauslastung zu entsprechen, die den Datenträger verwendet. Z. B. wenn eine Anwendung in Blöcken von 16 MB zugewiesen wird, wäre am besten mit eine virtuellen Festplatte Blockgröße von 16 MB haben es. Eine Blockgröße von &gt;2 MB kann nur auf virtuellen Festplatten im VHDX-Format. Mit einer größeren Blockgröße als das Zuweisungsmuster für eine zufällige e/a-arbeitsauslastung erhöht sich erheblich auf die Verwendung von Speicherplatz auf dem Host aus.

## <a name="sector-size-implications"></a>Auswirkungen auf die Sektor-Größe

Die meisten der Softwarebranche hat auf Sektoren von 512 Byte abhing, aber der Standard auf 4-KB-Sektoren verschoben wurde. Um Probleme mit der Anwendungskompatibilität zu reduzieren, die aus einer Änderung der Sektorengröße auftreten können, führen Festplatte Anbieter eine Übergangsphase Größe als 512-Emulation-Laufwerke (512e) bezeichnet.

Diese Emulation Festplatten bieten einige der Vorteile, die von 4 KB-Sektor native Laufwerke, wie z. B. verbesserte formateffizienz und ein verbessertes Schema für die Korrektur des Fehlercodes (ECC) angeboten werden. Sie verfügen über weniger Kompatibilitätsprobleme, die durch das Verfügbarmachen einer Sektorgröße von 4 KB auf Ebene der Festplattenschnittstelle auftreten würden.

## <a name="support-for-512e-disks"></a>Unterstützung für 512e-Laufwerken

Ein 512e-Datenträger kann Schreibvorgänge nur bezogen auf physische Sektoren ausführen – d. h. es kann nicht direkt zu schreiben einen 512-Byte-Sektor, die für sie ausgestellt wird. Der interne Prozess auf dem Datenträger, der diese Schreibvorgänge kann: Diese Schritte aus

-   Das Laufwerk liest den physischen 4-KB-Sektor auf den internen Cache ein, der der logischen Sektor von 512 Byte gemäß den Schreibvorgang enthält.

-   Die Daten im 4-KB-Puffer werden geändert, sodass sie den aktualisierten 512-Byte-Sektor einschließen.

-   Der Datenträger führt einen Schreibvorgang des aktualisierten 4-KB-Puffers zurück auf den physischen Sektor auf dem Datenträger.

Dieser Vorgang wird die Lese-Änderungs-Schreib (RMW) bezeichnet. Die Beeinträchtigung der gesamtleistung des RMW-Prozesses hängt von den Workloads ab. Der RMW-Prozess führt dazu, dass eine Verringerung der Leistung in virtuelle Festplatten aus den folgenden Gründen:

-   Dynamischen und differenzierenden virtuellen Festplatten müssen vor der Datennutzlast eine 512-Byte-sektorbitmap. Darüber hinaus Footer, Header und übergeordnete Locators an einer 512-Byte-Sektor ausgerichtet werden. Es ist üblich, für die virtuelle Festplatte-Treiber zum Schreiben von 512-Byte-Befehle an diese Strukturen, die den oben beschriebenen RMW-Prozess zu aktualisieren.

-   Anwendungen im allgemeinen Problem liest und schreibt in Vielfachen von 4 KB ausgegeben (der Standardclustergröße von NTFS). Da gibt es eine 512-Byte-sektorbitmap vor dem Block mit der Datennutzlast der dynamischen und differenzierenden virtuellen Festplatten, die 4-KB-Blöcke nicht an der physischen 4-KB-Begrenzung ausgerichtet. Die folgende Abbildung zeigt einen VHD-4-KB-Block (hervorgehoben), nicht mit der physischen 4-KB-Begrenzung ausgerichtet.

![VHD-4-kb-block](../../media/perftune-guide-vhd-4kb-block.png)

Jeder 4-KB-schreiben-Befehl, das vom aktuellen Parser zum Aktualisieren der Nutzlastdaten ausgegeben wird, führt zu zwei Lesevorgängen für zwei Blöcke auf dem Datenträger, die dann aktualisiert und anschließend auf die zwei Blöcke geschrieben werden. Hyper-V unter Windows Server 2016 werden einige der der leistungsauswirkungen auf 512e-Laufwerken im VHD-Stapel mit dem die zuvor genannten Strukturen für die Ausrichtung auf 4-KB-Begrenzungen im VHD-Format vorbereiten. Dadurch werden die Auswirkungen des RMW vermieden, wenn Zugriff auf die Daten in der VHD-Datei und der VHD-Metadatenstrukturen.

Wie bereits erwähnt, werden virtuelle Festplatten, die von früheren Versionen von Windows Server kopiert werden nicht automatisch auf 4 KB ausgerichtet werden. Sie können manuell konvertieren sie optimal mit Ausrichten der **Datenkopiervorgang von der Quelle** Datenträger die Option aus, in das VHD-Schnittstellen verfügbar ist.

Standardmäßig werden virtuelle Festplatten mit einer physischen Sektorgröße von 512 Byte verfügbar gemacht. Dies erfolgt, um sicherzustellen, dass die physischen Sektor abhängige Anwendungen nicht beeinträchtigt werden, wenn die Anwendung und die VHDs von einer früheren Version von Windows Server verschoben werden.

Standardmäßig werden Festplatten im VHDX-Format mit die physische Sektorgröße von 4 KB optimieren Sie ihre Leistung regulärer Benutzerprofil-Datenträger und Datenträger mit großen Sektoren erstellt. Um 4-KB-Sektoren vollständige nutzen hat es empfohlen, die VHDX-Format verwendet werden soll.

## <a name="support-for-native-4kb-disks"></a>Unterstützung für systemeigenen 4-KB-Datenträgern

Hyper-V in Windows Server 2012 R2 und darüber hinaus unterstützt 4 KB systemeigene Datenträger. Aber es ist weiterhin möglich, die VHD-Datenträger auf systemeigenen 4-KB-Datenträger zu speichern. Dies erfolgt durch die Implementierung einer Software RMW-Algorithmus in der die Ebene der virtuellen Storage-Stack, die konvertiert von 512-Byte-Zugriff und aktualisierungsanforderungen in entsprechende 4-KB-Zugriffe und-Aktualisierungen.

Da die VHD-Datei nur sich selbst als logische Sektorgröße von 512-Byte-Datenträger bereitstellen kann, ist es sehr wahrscheinlich, dass Anwendungen, die 512-Byte-e/a-Anforderungen genutzt werden. In diesen Fällen wird die RMW-Ebene diese Anforderungen zu erfüllen und Leistungseinbußen führen. Dies gilt auch für einen Datenträger, der mit VHDX formatiert sind, die eine logischen Sektorgröße von 512 Byte.

Es ist möglich, konfigurieren Sie eine VHDX-Datei als Datenträger Größe logische Sektorgröße 4-KB verfügbar gemacht werden, und dies wäre eine optimale Konfiguration für die Leistung auf, wenn der Datenträger auf einem physischen Gerät mit 4 KB native gehostet wird. Vorsichtig sollte vorgenommen werden, um sicherzustellen, dass der Gast und die Anwendung, die den virtuellen Datenträger verwendet wird, durch die logische Sektorgröße von 4 KB gesichert sind. Die Formatierung VHDX funktionieren ordnungsgemäß auf einem 4-KB logische Sektorgröße Größe-Gerät.

## <a name="pass-through-disks"></a>Pass-Through-Datenträger

Die virtuelle Festplatte auf einem virtuellen Computer kann direkt an einen physischen Datenträger oder logische Gerätenummer (LUN), anstelle von einer VHD-Datei zugeordnet werden. Der Vorteil ist, dass diese Konfiguration NTFS-Dateisystem in der Stammpartition, umgeht, wodurch die CPU-Auslastung von Speicher-e/a reduziert wird. Es besteht die Gefahr, dass physische Datenträger oder LUNs schwieriger zwischen Computern als VHD-Dateien verschoben werden können.

Pass-Through-Datenträger sollte vermieden werden, aufgrund der Beschränkungen, die mit VM-Migrationsszenarien eingeführt wurde.

## <a name="advanced-storage-features"></a>Erweiterte Speicherfunktionen

### <a name="storage-quality-of-service-qos"></a>Quality of Service (QoS) für Speicher

Ab Windows Server 2012 R2-Hyper-V enthält die Möglichkeit, bestimmte Quality of Service (QoS)-Parameter für Speicher auf den virtuellen Computern festzulegen. Quality of Service für Speicher stellt eine Speicherleistungsisolierung in einer mehrinstanzenfähigen Umgebung und Mechanismen bereit, um Sie zu benachrichtigen, wenn die Speicher-E/A-Leistung den definierten Schwellenwert nicht erfüllt, der erforderlich ist, damit die Arbeitsauslastungen Ihres virtuellen Computers effizient ausgeführt werden.

Mit Quality of Service für Speicher kann ein maximaler IOPS-Wert (Input/Output Operations per Second, Eingabe-/Ausgabevorgänge pro Sekunde) für Ihre virtuelle Festplatte festgelegt werden. Ein Administrator kann den Speicher-E/A drosseln, um einen Mandanten daran zu hindern, sehr umfangreiche Speicherressourcen zu beanspruchen, wenn dadurch ein anderer Mandant beeinflusst wird.

Sie können auch einen minimalen IOPS-Wert festlegen. Er wird benachrichtigt, wenn der IOPS-Wert für eine angegebene virtuelle Festplatte unter einem Schwellenwert liegt, der für die optimale Leistung erforderlich ist.

Die Infrastruktur der Metriken des virtuellen Computers wird auch mit speicherbezogenen Parametern aktualisiert, damit der Administrator die Leistung überwachen und zugehörige Parameter rückbelasten kann.

Maximale und minimale Werte werden in Bezug auf normalisierte IOPS-Werte angegeben, in dem jede 8 KB Daten als e/a gezählt wird.

Einige der Einschränkungen lauten wie folgt:

-   Nur für virtuelle Datenträger

-   Differenzierender Datenträger keine übergeordnete virtuelle Festplatte auf einem anderen volume

-   Replikat - QoS für Replikat-Site, die unabhängig vom primären Standort konfiguriert

-   Freigegebener VHDX wird nicht unterstützt.

Weitere Informationen zu Storage Quality of Service, finden Sie unter [Quality of Service für Speicher für Hyper-V](https://technet.microsoft.com/library/dn282281.aspx).

### <a name="numa-io"></a>NUMA I/O

WindowsServer 2012, und es wird darüber hinaus unterstützt große virtuelle Computer und alle großen VM-Konfiguration (z. B. eine Konfiguration mit Microsoft SQL Server mit 64 virtuellen Prozessoren) benötigen auch die Skalierbarkeit im Hinblick auf e/a-Durchsatz.

Die folgenden wichtigen Verbesserungen eingeführt wurden und in der Speicherstapel von Windows Server 2012 und Hyper-V bereitstellen, die e/a-Anforderungen an die Skalierbarkeit großer virtueller Computer:

-   Eine Zunahme der Anzahl der Kommunikationskanäle zwischen Geräten von Gast und Host-Speicherstapel erstellt.

-   Eine effizientere e/a-Abschlussmechanismus im Zusammenhang mit Interrupt-Verteilung für die virtuellen Prozessoren um teure interprocessor Unterbrechungen zu vermeiden.

In Windows Server 2012 eingeführt wurde, es gibt ein paar Registrierungseinträge, die am HKLM\\System\\CurrentControlSet\\Enum\\VMBUS\\{Geräte-Id}\\{Instanz-Id}\\StorChannel, mit denen die Anzahl von Kanälen angepasst werden können. Sie richten Sie auch virtuellen Prozessoren, die die e/a-vervollständigungen für das virtuelle CPUs zu verarbeiten, die von der Anwendung für die e/a-Prozessoren zugewiesen sind. Die registrierungseinstellungen werden pro pro-Adapter für den Schlüssel des Geräts Hardware konfiguriert.

-   **ChannelCount (DWORD)** die Gesamtzahl der Kanäle mit maximal 16 verwendet. Wird standardmäßig eine Obergrenze, die die Anzahl der virtuellen Prozessoren/16 ist.

-   **ChannelMask (QWORD)** die Prozessoraffinität für die Kanäle. Wenn es nicht festgelegt oder auf 0 festgelegt ist, wird standardmäßig die vorhandenen Kanal Verteilungsalgorithmus, die Sie für den normalen Speicher oder Netzwerkkanäle verwenden. Dadurch wird sichergestellt, dass die Speicher-Kanäle mit Ihrem Netzwerk-Kanälen in Konflikt steht.

### <a name="offloaded-data-transfer-integration"></a>Offloaded Data Transfer-integration

Wichtige Wartungsaufgaben für virtuelle Festplatten verwenden, beispielsweise das Zusammenführen, verschieben und komprimieren, kopieren große Datenmengen abhängen. Die aktuelle Methode zum Kopieren von Daten erfordert, dass die Daten an unterschiedlichen Standorten eingelesen und geschrieben werden, was sehr zeitaufwändig sein kann. Er verwendet auch die CPU-und Arbeitsspeicherressourcen auf dem Host, der auf virtuelle dienstmaschinen verwendet werden können hätte.

SAN-Hersteller (Storage Area Network) arbeiten daran, Kopiervorgänge für große Datenmengen nahezu in Echtzeit zu ermöglichen. Dieser Speicher soll es das System oberhalb der Festplatten an die Verschiebung eines bestimmten Datasets von einem Speicherort zu einem anderen ermöglicht. Diese Funktion "Hardware" wird als ein Offloaded Data Transfer bezeichnet.

Hyper-V in Windows Server 2012 und darüber hinaus unterstützt Offload Data Transfer (ODX)-Vorgänge, sodass diese Vorgänge vom Gastbetriebssystem, das an die Hosthardware übergeben werden können. Dadurch wird sichergestellt, dass die arbeitsauslastung ODX aktivierten Speicher verwenden kann, als wäre er in einer nicht virtualisierten Umgebung ausgeführt wurden. Der Hyper-V-Speicherstapel gibt ODX-Vorgänge auch bei Wartungsvorgängen für virtuelle Festplatten, beispielsweise beim Zusammenführen von Datenträgern und Speicher-Vorgänge, in denen große Mengen an Daten verschoben werden.

### <a name="unmap-integration"></a>Aufheben der integration

Virtuelle Festplattendateien, die als Dateien auf einem Speichervolume vorhanden sein, und andere Dateien Speicherplatz freigegeben. Da die Größe dieser Dateien umfangreich tendenziell, kann der Speicherplatz, den sie nutzen schnell wachsen. Bei Bedarf für mehr physischen Speicher wirkt sich auf die IT-Hardwarebudget. Es ist wichtig, die die Verwendung von physischem Speicher so weit wie möglich zu optimieren.

Vor Windows Server 2012 als Anwendungen Inhalte in einer virtuellen Festplatte,, die effektive Speicherplatz des Inhalts abgebrochen löschen, hatte der Windows-Speicherstapel im Gast-Betriebssystems und der Hyper-V-Host Einschränkungen, die dies verhindert Informationen aus der virtuellen Festplatte und das physische Medium mitgeteilt wird. Dadurch wird verhindert, dass den Hyper-V-Speicherstapel Optimieren der Speicherplatzverwendung durch die VHD-basierte virtuelle Datenträgerdateien. Es wird auch verhindert, dass die zugrunde liegenden Speichergerät Freigeben der Speicherplatz, der zuvor von den gelöschten Daten belegt wurde.

Beginnend mit Windows Server 2012, aufheben Hyper-V unterstützt Benachrichtigungen, VHDX-Dateien, die darstellt, die darin enthaltenen Daten effizienter sein können. Dies führt zu kleineren Größe, und es ermöglicht, dass die zugrunde liegende physische Speichergerät nicht verwendeten Speicherplatz freigeben.

Nur Hyper-V-spezifischer SCSI, aktivierte IDE und der virtuelle Fibre Channel Controller ermöglicht es dem Unmap-Befehl des Gasts erreichen den virtuellen Speicherstapel Host. Auf der virtuellen Festplatten die Zuordnung nur virtuelle Laufwerke, die entsprechend der Unterstützung von VHDX formatiert Befehle zwischen dem Gast aufheben.

Aus diesen Gründen empfehlen wir die Verwendung von VHDX-Dateien, die an einen SCSI-Controller angefügt wird, wenn keine virtuellen Fibre Channel-Datenträger verwenden.

## <a name="see-also"></a>Siehe auch

-   [Hyper-V-Terminologie](terminology.md)

-   [Hyper-V-Architektur](architecture.md)

-   [Hyper-V-Server-Konfiguration](configuration.md)

-   [Hyper-V, prozessorbezogene Leistungsdaten](processor-performance.md)

-   [Hyper-V-Memory-Leistung](memory-performance.md)

-   [Hyper-V-Netzwerk-e/a-Leistung](network-io-performance.md)

-   [Erkennen von Engpässen in einer virtualisierten Umgebung](detecting-virtualized-environment-bottlenecks.md)

-   [Virtuelle Linux-Computer](linux-virtual-machine-considerations.md)
