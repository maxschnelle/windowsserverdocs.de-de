---
title: 'Robustes Dateisystem (ReFS) : Übersicht'
ms.prod: windows-server-threshold
ms.author: gawatu
ms.manager: mchad
ms.technology: storage-file-systems
ms.topic: article
author: gawatu
ms.date: 06/07/2019
ms.openlocfilehash: fed23c999c67ba81b3bbb821170a748ed5eaa7b8
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812018"
---
# <a name="resilient-file-system-refs-overview"></a>Robustes Dateisystem (ReFS) : Übersicht

>Gilt für: WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, WindowsServer (Halbjährlicher Kanal)

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

- **[Mirror-beschleunigte Parität](./mirror-accelerated-parity.md)**  -Mirror-beschleunigte Parität bietet hohe Leistung und auch Kapazität effiziente Speicherung Ihrer Daten. 

    - Um eine hohe Leistung und effiziente Speicherkapazität zu übermitteln, teilt ReFS ein Volume in zwei logische Speichergruppen ein, die als Ebenen bezeichnet werden. Diese Ebenen können ihre eigenen Laufwerke und Resilienztypen haben, die jeder Ebene die Optimierung von Kapazität oder Leistung ermöglicht. Zu den Beispielkonfigurationen gehören: 
    
      | Leistungsebene | Kapazitätsebene |
      | ---------------- | ----------------- |
      | Gespiegelte SSD | Gespiegelte HDD |
      | Gespiegelte SSD | Paritäts-SSD: |
      | Gespiegelte SSD | Paritäts-HDD |
            
    - Nachdem diese Ebenen konfiguriert wurden, verwendet ReFS diese, um schnell Speicherplatz für „Hot Data” anzubieten und effizient Speicherkapazität für „Cold Data” bereitzustellen:
        - Alle Schreibvorgänge werden in der Leistungsebene ausgeführt und große Teile der Daten, die in der Leistungsebene verbleiben, werden in Echtzeit auf die Kapazitätsebene verschoben.
        - Wenn Sie eine hybridbereitstellung (das Kombinieren von Flash und HDD-Laufwerke), verwenden [den "direkte Speicherplätze"-Cache](../storage-spaces/understand-the-cache.md) hilft Ihnen, schneller Lesevorgänge, verringert die Auswirkungen von Daten von Fragmentierung virtualisierte arbeitsauslastungen sind. Andernfalls auftreten, wenn eine All-Flash-Bereitstellung verwenden zu können, Lesevorgänge auch in die Leistungsstufe.

> [!NOTE]
> Für Serverbereitstellungen wird die durch Spiegelung beschleunigte Parität nur auf [direkten Speicherplätzen](../storage-spaces/storage-spaces-direct-overview.md) unterstützt. Es wird empfohlen, Archivierung und Sicherung-Workloads mit Parität Mirror-Beschleunigung. Für virtualisierte und andere zufällige Hochleistungsworkloads empfehlen wir drei-Wege-Spiegel für eine bessere Leistung.

- **Beschleunigte VM-Vorgänge** - ReFS führt neue Funktionen ein, die speziell die Leistung virtualisierter Workloads verbessern:
    - [Block-Clone-Vorgänge](./block-cloning.md) - Block-Clone-Vorgänge beschleunigen Kopiervorgänge und ermöglichen schnelle und ressourcensparende VM-Prüfpunkt-Mergevorgänge.
    - Platzsparende VDL - Mit platzsparenden VDLs können ReFS Dateien in „null“ umwandeln und so die erforderliche Zeit für feste VHDs von duzenden Minuten auf Sekunden reduzieren.

- **Variable Clustergrößen** -ReFS unterstützt Clustergrößen von sowohl 4-KB als auch 64 KB. 4K ist die empfohlene Clustergröße für die meisten Bereitstellungen, doch 64 KB Cluster sind für große, aufeinander folgende E/A-Workloads am geeignetsten.

### <a name="scalability"></a>Skalierbarkeit

ReFS unterstützt besonders große Datensätze--Millionen Terabytes-- ohne sich negativ auf die Leistung auszuwirken und erzielt eine größere Skalierung als vorherige Dateisysteme.

## <a name="supported-deployments"></a>Unterstützte Bereitstellungen

Microsoft hat NTFS speziell für die allgemeine Verwendung mit einer Vielzahl von Konfigurationen und Workloads entwickelt, jedoch für Kunden, die speziell erfordern die Verfügbarkeit, resilienz, und/oder Skala an, ReFS bietet, Microsoft für die Verwendung unter ReFS unterstützt die folgenden Konfigurationen und Szenarien. 

> [!NOTE]
> ReFS unterstützt Konfigurationen müssen, verwenden alle [Windows Server-Katalog](https://www.WindowsServerCatalog.com) certified Anforderungen für Hardware- und erfüllen.

### <a name="storage-spaces-direct"></a>Direkte Speicherplätze

Das Bereitstellen von ReFS auf direkte Speicherplätze ist für virtualisierte Workloads oder Network Attached Storage empfohlen: 
- Durch Spiegelung beschleunigte Parität und [der Cache im direkten Speicherplatz](../storage-spaces/understand-the-cache.md) bieten eine hohe Leistung und effizient Speicherkapazität. 
- Die Einführung von Block-Clone-Vorgängen und platzsparende VDLs beschleunigt .vhdx-Dateivorgänge wie das Erstellen, Zusammenführen und Erweitern ganz erheblich.
- Integritätsdatenströme – online reparieren und alternativen Datenkopien aktivieren ReFS und Storage Spaces Direct gemeinsam zum Erkennen und Beheben der Speichercontroller und die Speicher-Media-Beschädigungen in Metadaten und Daten. 
- ReFS bietet die Funktionalität zur Skalierung und unterstützt große Datasets. 

### <a name="storage-spaces"></a>Speicherplätze

- Integritätsdatenströme – online reparieren und alternativen Datenkopien aktivieren ReFS und [Speicherplätze](../storage-spaces/overview.md) , gemeinsam an der Speichercontroller und Speicher Media Beschädigungen in Metadaten und Daten erkennen und korrigieren.
- Die Bereitstellungen von Speicherplätzen unterstützt ebenfalls Block-Clone-Vorgänge und eine in ReFS angebotene Skalierbarkeit.
- Bereitstellen von ReFS auf Speicherplätzen mit freigegebenen SAS-Gehäuse ist für Archivdaten hosting und Speicherung von Benutzerdokumenten geeignet.

> [!NOTE]
> Storage Spaces unterstützt lokale nicht austauschbare direkt angeschlossener über BusTypes SATA, SAS und NVME oder per HBA (auch bekannt als RAID-Controller im Pass-Through-Modus) angefügt.

### <a name="basic-disks"></a>Basisfestplatten

Bereitstellen von ReFS auf Basisdatenträgern eignet sich optimal für Anwendungen, die ihre eigenen softwarelösungen für resilienz und Verfügbarkeit zu implementieren. 
- Anwendungen, die ihre eigenen Software-Resilienz- und Verfügbarkeitslösungen aufweisen, können Integrity Streams, Block-Clone-Vorgänge und die Möglichkeit, Skalierung und große Mengen von Daten nutzen. 

> [!NOTE]
> Basisdatenträger enthalten nicht austauschbare über BusTypes SATA, SAS, NVME oder RAID direkt angeschlossenen lokalen. 

### <a name="backup-target"></a>Sicherungsziel

Bereitstellen von ReFS als Sicherungsziel am besten geeignet ist geeignet für Anwendungen und Hardware, die ihre eigenen Lösungen für resilienz und Verfügbarkeit zu implementieren.
- Anwendungen, die ihre eigenen Software-Resilienz- und Verfügbarkeitslösungen aufweisen, können Integrity Streams, Block-Clone-Vorgänge und die Möglichkeit, Skalierung und große Mengen von Daten nutzen.

> [!NOTE]
> Sicherungsziele, enthalten die oben genannten unterstützten Konfigurationen. Wenden Sie Anwendung und Speicher-Array-Anbieter aus, um Informationen zur Unterstützung für Fiber-Channel und iSCSI-SANs. Für muss SANs, wenn Sie z. B. die schlanke Bereitstellung, TRIM/UNMAP oder Offloaded Data Transfer (ODX) erforderlich ist, werden NTFS verwendet werden.   

## <a name="feature-comparison"></a>Vergleichbare Funktionen

### <a name="limits"></a>Limits

| Feature       | ReFS                                        | NTFS |
|----------------|------------------------------------------------|-----------------------|
| Maximale Dateinamenslänge | 255 Unicode-Zeichen  | 255 Unicode-Zeichen               |
| Maximale Pfadnamenslänge |32.000 Unicode-Zeichen | 32.000 Unicode-Zeichen                |
| Maximale Dateigröße | 35 PB (im Petabyte-Bereich)  | 256 TB               |
| Maximale Volumegröße | 35 PB                           | 256 TB                |

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
| Trim/Unmap | Ja<sup>3</sup> | Ja |
1. Unter Windows Server, Version 1709 und höher verfügbar.
2. Unter Windows Server 2012 R2 und höher verfügbar.
3. Nur die Speicherplätze

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
| Offloaded Data Transfer (ODX) | Nein | Ja |
| Kurznamen | Nein | Ja |
| Erweiterte Attribute | Nein | Ja |
| Datenträgerkontingente | Nein | Ja |
| Startbar | Nein | Ja |
| Seite-dateiunterstützung | Nein | Ja |
| Auf Wechselmedien unterstützt | Nein | Ja |

## <a name="see-also"></a>Siehe auch

-   [Übersicht über Storage "direkte Speicherplätze"](../storage-spaces/storage-spaces-direct-overview.md)
-   [Klonen von ReFS-block](block-cloning.md)
-   [ReFS integritätsdatenströme](integrity-streams.md)