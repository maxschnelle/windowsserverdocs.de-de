---
title: 'Robustes Dateisystem (ReFS) : Übersicht'
ms.prod: windows-server
ms.author: gawatu
ms.manager: mchad
ms.technology: storage-file-systems
ms.topic: article
author: gawatu
ms.date: 06/17/2019
ms.openlocfilehash: 91fdd5aa696c170cacc8903a65e996beb71c4b8f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403020"
---
# <a name="resilient-file-system-refs-overview"></a>Robustes Dateisystem (ReFS) : Übersicht

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server (halbjährlicher Kanal)

Das ReFS (Resilient File System, Robustes Dateisystem) ist das neuste Dateisystem von Microsoft, das die Datenverfügbarkeit maximiert, große Datasets über diverse Arbeitslasten effektiv skaliert und Datenintegrität durch Resilienz gegenüber Beschädigungen von zentraler Bedeutung bereitstellt. Es versucht, die Erweiterung verschiedener Speicherszenarien zu behandeln und eine Grundlage für zukünftige Innovationen herzustellen.

## <a name="key-benefits"></a>Wichtige Vorteile

### <a name="resiliency"></a>Resilienz

ReFS führt neue Features ein, die präzise Schäden erkennen und diese auch Online beheben können und so eine verbesserte Integrität und Verfügbarkeit der Daten unterstützt. 

- **Integrity Streams** -ReFS verwendet Prüfsummen für Metadaten und optional für Dateidaten, wodurch ReFS Schäden zuverlässig erkennt. 
- **Integration in Speicherplätze** – Wenn dies zusammen mit einem Spiegelungs- oder Paritätsbereich verwendet wird, kann ReFS unter Verwendung der alternativen Kopie der in den Speicherplätzen bereitgestellten Daten die automatisch erkannten Schäden reparieren. Die Reparatur wird sowohl im beschädigten Bereich erkannt als auch Online ausgeführt, ohne Ausfallzeiten des Volume.
- **Rettung von Daten** - Wenn ein Volume beschädigt wurde und keine Kopie der beschädigten Daten vorhanden ist, entfernt ReFS die beschädigten Daten aus dem „Namespace”. ReFS behält das Volume Online, während es die meisten nicht behebbaren Schäden behandelt. In seltenen Fällen muss ReFS das Volume offline schalten.
- **Proaktive Fehlerkorrektur** - Zusätzlich zur Überprüfung von Daten vor Lese- und Schreibvorgänge führt ReFS einen Datenintegritätsscanner, auch <i>Bereinigung</i> genannt. Die Bereinigung durchsucht regelmäßig das Volume, erkennt dabei potenzielle Beschädigungen und löst dann proaktiv eine Reparatur dieser beschädigten Daten aus. 

### <a name="performance"></a>Leistung

Zusätzlich zur Verbesserungen der Resilienz führt ReFS neue Features für leistungsabhängige und virtualisierten Workloads ein. Ebenenoptimierung in Echtzeit, Block-Clone-Vorgänge und platzsparenden VDLs sind gute Beispiele für die neuen Funktionen von ReFS, die zur Unterstützung dynamischer und verschiedener Workloads konzipiert werden.

- **[Spiegel-beschleunigte Parität](./mirror-accelerated-parity.md)** : bei der Spiegelungs Beschleunigung wird sowohl eine hohe Leistung als auch ein Kapazitäts effizienter Speicher für Ihre Daten bereitstellt. 

    - Um eine hohe Leistung und effiziente Speicherkapazität zu übermitteln, teilt ReFS ein Volume in zwei logische Speichergruppen ein, die als Ebenen bezeichnet werden. Diese Ebenen können ihre eigenen Laufwerke und Resilienztypen haben, die jeder Ebene die Optimierung von Kapazität oder Leistung ermöglicht. Zu den Beispielkonfigurationen gehören: 
    
      | Leistungsebene | Kapazitätsebene |
      | ---------------- | ----------------- |
      | Gespiegelte SSD | Gespiegelte HDD |
      | Gespiegelte SSD | Paritäts-SSD: |
      | Gespiegelte SSD | Paritäts-HDD |
            
    - Nachdem diese Ebenen konfiguriert wurden, verwendet ReFS diese, um schnell Speicherplatz für „Hot Data” anzubieten und effizient Speicherkapazität für „Cold Data” bereitzustellen:
        - Alle Schreibvorgänge werden in der Leistungsebene ausgeführt und große Teile der Daten, die in der Leistungsebene verbleiben, werden in Echtzeit auf die Kapazitätsebene verschoben.
        - Bei Verwendung einer Hybrid Bereitstellung (mit einer Mischung aus Flash-und HDD-Laufwerken) hilft [der Cache in direkte Speicherplätze](../storage-spaces/understand-the-cache.md) bei der Beschleunigung von Lesevorgängen, wodurch die Auswirkungen der Daten Fragmentierung von virtualisierten Workloads verringert werden Andernfalls werden bei der Verwendung einer Bereitstellung mit einem beliebigen Flash-/Lesevorgänge auch in der Leistungsstufe ausgeführt.

> [!NOTE]
> Für Serverbereitstellungen wird die durch Spiegelung beschleunigte Parität nur auf [direkten Speicherplätzen](../storage-spaces/storage-spaces-direct-overview.md) unterstützt. Wir empfehlen die Verwendung der Spiegel beschleunigten Parität bei der Archivierung und bei sicherungsworkloads. Für virtualisierte und andere hochleistungsfähige zufällige Workloads empfiehlt es sich, drei-Wege-Spiegelungen zu verwenden, um die Leistung zu verbessern.

- **Beschleunigte VM-Vorgänge** - ReFS führt neue Funktionen ein, die speziell die Leistung virtualisierter Workloads verbessern:
    - [Block-Clone-Vorgänge](./block-cloning.md) - Block-Clone-Vorgänge beschleunigen Kopiervorgänge und ermöglichen schnelle und ressourcensparende VM-Prüfpunkt-Mergevorgänge.
    - Platzsparende VDL - Mit platzsparenden VDLs können ReFS Dateien in „null“ umwandeln und so die erforderliche Zeit für feste VHDs von duzenden Minuten auf Sekunden reduzieren.

- **Variable Clustergrößen** -ReFS unterstützt Clustergrößen von sowohl 4-KB als auch 64 KB. 4K ist die empfohlene Clustergröße für die meisten Bereitstellungen, doch 64 KB Cluster sind für große, aufeinander folgende E/A-Workloads am geeignetsten.

### <a name="scalability"></a>Skalierbarkeit

ReFS unterstützt besonders große Datensätze--Millionen Terabytes-- ohne sich negativ auf die Leistung auszuwirken und erzielt eine größere Skalierung als vorherige Dateisysteme.

## <a name="supported-deployments"></a>Unterstützte Bereitstellungen

Microsoft hat NTFS speziell für die allgemeine Verwendung mit einer Vielzahl von Konfigurationen und Arbeits Auslastungen entwickelt. für Kunden, die speziell die Verfügbarkeit, Resilienz und/oder Skalierung benötigen, die von refs bereitgestellt werden, unterstützt Microsoft jedoch Refs für die Verwendung unter die folgenden Konfigurationen und Szenarien. 

> [!NOTE]
> Alle von refs unterstützten Konfigurationen müssen die [Windows Server-Katalog](https://www.WindowsServerCatalog.com) zertifizierte Hardware verwenden und die Anwendungsanforderungen erfüllen.

### <a name="storage-spaces-direct"></a>Direkte Speicherplätze

Das Bereitstellen von ReFS auf direkte Speicherplätze ist für virtualisierte Workloads oder Network Attached Storage empfohlen: 
- Durch Spiegelung beschleunigte Parität und [der Cache im direkten Speicherplatz](../storage-spaces/understand-the-cache.md) bieten eine hohe Leistung und effizient Speicherkapazität. 
- Die Einführung von Block-Clone-Vorgängen und platzsparende VDLs beschleunigt .vhdx-Dateivorgänge wie das Erstellen, Zusammenführen und Erweitern ganz erheblich.
- Mit Integritäts Datenströmen, Online Reparatur und alternativen Datenkopien können Refs und direkte Speicherplätze gemeinsam die Beschädigungen von Speicher Controllern und Speichermedien innerhalb von Metadaten und Daten erkennen und korrigieren. 
- ReFS bietet die Funktionalität zur Skalierung und unterstützt große Datasets. 

### <a name="storage-spaces"></a>Speicherplätze

- Mit Integritäts Datenströmen, Online Reparatur und alternativen Datenkopien können Refs und [Speicherplätze](../storage-spaces/overview.md) gemeinsam zum erkennen und korrigieren von Speicher Controllern und Speichermedien in Metadaten und Daten auf die gleiche Weise erstellt werden.
- Die Bereitstellungen von Speicherplätzen unterstützt ebenfalls Block-Clone-Vorgänge und eine in ReFS angebotene Skalierbarkeit.
- Das Bereitstellen von refs für Speicherplätze mit freigegebenen SAS-Gehäusen eignet sich zum Hosting von Archivierungs Daten und Speichern von Benutzer

> [!NOTE]
> "Speicherplätze" unterstützt lokale, nicht austauschbare direkt mit "bustypes SATA", "SAS", "nvme" oder "Attached" über HBA (auch als RAID-Controller im Pass-Through-Modus bezeichnet)

### <a name="basic-disks"></a>Basisfestplatten

Das Bereitstellen von refs für Basis Datenträger eignet sich am besten für Anwendungen, die ihre eigenen Lösungen für Software Resilienz und Verfügbarkeit 
- Anwendungen, die ihre eigenen Software-Resilienz- und Verfügbarkeitslösungen aufweisen, können Integrity Streams, Block-Clone-Vorgänge und die Möglichkeit, Skalierung und große Mengen von Daten nutzen. 

> [!NOTE]
> Zu den Basis Datenträgern gehören lokale nicht austauschbare direkt Anfügung über bustypes SATA, SAS, nvme oder RAID. 

### <a name="backup-target"></a>Sicherungs Ziel

Das Bereitstellen von refs als Sicherungs Ziel eignet sich am besten für Anwendungen und Hardware, die ihre eigenen Lösungen für Resilienz und Verfügbarkeit implementieren.
- Anwendungen, die ihre eigenen Software-Resilienz- und Verfügbarkeitslösungen aufweisen, können Integrity Streams, Block-Clone-Vorgänge und die Möglichkeit, Skalierung und große Mengen von Daten nutzen.

> [!NOTE]
> Sicherungs Ziele enthalten die oben genannten unterstützten Konfigurationen. Wenden Sie sich an die Anbieter von Anwendungs-und Speicherarrays, um Support Details zu Fiber-Channel und iSCSI-SANs Für SANs müssen NTFS verwendet werden, wenn Features wie Thin Provisioning, Trim/unmap oder offloaded Datenübertragung (ODX) erforderlich sind.   

## <a name="feature-comparison"></a>Vergleichbare Funktionen

### <a name="limits"></a>Limits

| Feature       | ReFS                                        | NTFS |
|----------------|------------------------------------------------|-----------------------|
| Maximale Dateinamenslänge | 255 Unicode-Zeichen  | 255 Unicode-Zeichen               |
| Maximale Pfadnamenslänge |32.000 Unicode-Zeichen | 32.000 Unicode-Zeichen                |
| Maximale Dateigröße | 35 PB (Peer tabytes)  | 256 TB               |
| Maximale Volumegröße | 35-PB                           | 256 TB                |

### <a name="functionality"></a>Funktionalität

#### <a name="the-following-features-are-available-on-refs-and-ntfs"></a>Die folgenden Features sind in ReFS und NTFS verfügbar:

| Funktionalität       | ReFS                                        | NTFS |
|---------------------------|------------------|-----------------------|
| BitLocker-Verschlüsselung | Ja | Ja |
| Datendeduplizierung | Ja<sup>1</sup> | Ja |
| Volumes mit freigegebener Unterstützung (Cluster Shared Volume, CSV) | Ja<sup>2</sup> | Ja |
| Weiche Links | Ja | Ja |
| Failover-Clusterunterstützung | Ja | Ja |
| Zugriffssteuerungslisten | Ja | Ja |
| USN-Journal | Ja | Ja |
| Änderungsbenachrichtigungen | Ja | Ja |
| Abzweigungspunkte | Ja | Ja |
| Mount points (Bereitstellungspunkte) | Ja | Ja |
| Analysepunkte | Ja | Ja |
| Volumesnapshots | Ja | Ja |
| Datei-ID | Ja | Ja |
| OPLOCKs | Ja | Ja |
| Dateien mit geringer Datendichte | Ja | Ja |
| Benannte Datenströme | Ja | Ja |
| Schlanke Speicherzuweisung | Ja<sup>3</sup> | Ja |
| Trim/unmap | Ja<sup>3</sup> | Ja |
1. Verfügbar unter Windows Server, Version 1709 und höher.
2. Verfügbar unter Windows Server 2012 R2 und höher.
3. Nur Speicherplätze

#### <a name="the-following-features-are-only-available-on-refs"></a>Die folgenden Features sind nur in ReFS verfügbar:

| Funktionalität       | ReFS                                        | NTFS |
|---------------------------|------------------|-----------------------|
| Block-Clone-Vorgang | Ja | Nein |
| Platzsparende VDL | Ja | Nein |
| Durch Spiegelung beschleunigte Parität| Ja (auf direkten Speicherplätzen) | Nein |

#### <a name="the-following-features-are-unavailable-on-refs-at-this-time"></a>Folgende Features sind im Moment nicht auf ReFS verfügbar:

| Funktionalität       | ReFS                                        | NTFS |
|---------------------------|------------------|-----------------------|
| Komprimierung des Dateisystems | Nein | Ja |
| Verschlüsseln des Dateisystems | Nein | Ja |
| Transaktionen | Nein | Ja |
| Feste Links | Nein | Ja |
| Objekt-IDs | Nein | Ja |
| Offloaded Datenübertragung (ODX) | Nein | Ja |
| Kurznamen | Nein | Ja |
| Erweiterte Attribute | Nein | Ja |
| Datenträgerkontingente | Nein | Ja |
| Startbar | Nein | Ja |
| Unterstützung von Seiten Dateien | Nein | Ja |
| Auf Wechselmedien unterstützt | Nein | Ja |

## <a name="see-also"></a>Siehe auch

- [Empfehlungen für die Cluster Größe für Refs und NTFS](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/Cluster-size-recommendations-for-ReFS-and-NTFS/ba-p/425960)
- [Übersicht über direkte Speicherplätze](../storage-spaces/storage-spaces-direct-overview.md)
- [Neuklonen von refs-Blöcken](block-cloning.md)
- [Refs-Integritäts Datenströme](integrity-streams.md)