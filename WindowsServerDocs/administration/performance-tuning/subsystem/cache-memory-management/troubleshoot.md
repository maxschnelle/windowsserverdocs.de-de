---
title: Problembehandlung bei Cache und Speicher-Manager-Leistungsprobleme
description: Problembehandlung bei Cache und Speicher-Manager-Leistungsproblemen unter WindowsServer 16
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Pavel; ATales
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 66c7e2a6b264a837c65df927b271fadd2672fa24
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835791"
---
# <a name="troubleshoot-cache-and-memory-manager-performance-issues"></a>Problembehandlung bei Cache und Speicher-Manager-Leistungsprobleme

Vor Windows Server 2012 verursacht zwei primäre Probleme Systemdateicache zu wachsen, bis der verfügbare Arbeitsspeicher unter bestimmten Arbeitsbedingungen nahezu erschöpft war. Wenn können diese Situation ergibt das System langsam, Sie bestimmen, ob der Server ist eines der folgenden Probleme mit Internetzugriff.


## <a name="counters-to-monitor"></a>Indikatoren zum Überwachen

-   Arbeitsspeicher\\Long-term durchschnittliche Standby Cachelebensdauer (s) &lt; 1800 Sekunden

-   Arbeitsspeicher\\"Verfügbare MB" ist niedrig

-   Arbeitsspeicher\\Systemcache: Residente Bytes

Wenn Arbeitsspeicher\\"Verfügbare MB" ist niedrig und zur gleichen Zeit Arbeitsspeicher\\Systemcache: Residente Bytes belegt erheblichen Teil des physischen Speichers, können Sie mit [RAMMAP](https://technet.microsoft.com/sysinternals/ff700229.aspx) herausfinden, welche der Cache verwendet wird für.

## <a name="system-file-cache-contains-ntfs-metafile-data-structures"></a>Systemdateicache enthält NTFS-Metadatei Datenstrukturen


Dieses Problem wird durch eine sehr hohe Anzahl von aktiven Metadatei-Seiten im RAMMAP, die für die Ausgabe angegeben, wie in der folgenden Abbildung dargestellt. Dieses Problem möglicherweise beobachtet wurde auf ausgelasteten Servern mit Millionen von Dateien, die auf die zugegriffen wird, wodurch und Zwischenspeichern von NTFS-Metadatei Daten nicht aus dem Cache freigegeben werden.

![Rammap anzeigen](../../media/perftune-guide-rammap.png)

Das Problem verringert werden, indem Sie mit der *DynCache* Tool. In Windows Server 2012 und höher, die Architektur wurde überarbeitet und dieses Problem sollte nicht mehr vorhanden sind.

## <a name="system-file-cache-contains-memory-mapped-files"></a>Systemdateicache enthält, im Speicher abgebildete Dateien


Dieses Problem wird durch sehr hohe Anzahl von aktiven zugeordnete Datei-Seiten im RAMMAP Ausgabe angezeigt. Dies wird in der Regel gibt an, dass es sich bei eine Anwendung auf dem Server viele große Dateien, die mit geöffnet wird [CreateFile](https://msdn.microsoft.com/library/windows/desktop/aa363858.aspx) -API mit Datei\_FLAG\_RANDOM\_ACCESS Flag festgelegt.

Dieses Problem ist ausführlich im KB-Artikel [2549369](https://support.microsoft.com/default.aspx?scid=kb;en-US;2549369). Datei\_FLAG\_RANDOM\_Zugriffsflag ist ein Hinweis für die Cache-Manager zugeordnete Ansichten der Datei im Arbeitsspeicher, die so lange wie möglich zu halten, (bis der Speicher-Manager nicht genügend Arbeitsspeicher verfügbar signalisieren nicht). Dieses Kennzeichen wird zur gleichen Zeit Cache-Manager, deaktivieren die an Dateidaten Vorabruf angewiesen.

Dies hat zu einem gewissen Grad durch die Zusammenarbeit Satz verkürzen Verbesserungen in Windows Server 2012 und höher behoben, aber das Problem selbst muss sich in erster Linie vom Hersteller Anwendung behoben werden, nicht mit der Datei\_FLAG\_RANDOM\_Zugriff. Eine alternative Lösung für die app-Anbieter möglicherweise mit niedriger Priorität verwendet werden, wenn Sie die Dateien zugreifen. Dies erfolgt über die [SetThreadInformation](https://msdn.microsoft.com/library/windows/desktop/hh448390.aspx) API. Seiten, die mit nicht genügend arbeitsspeicherpriorität zugegriffen werden, werden in aggressivere Arbeitssatz entfernt.

Cache-Manager ab Windows Server 2016 Weitere Dies verringert FILE_FLAG_RANDOM_ACCESS ignorieren, wenn verkürzen Entscheidungen, zu treffen, damit es, genau wie jede andere Datei, die geöffnet werden, ohne das FILE_FLAG_RANDOM_ACCESS-Flag behandelt wird (Cache-Manager berücksichtigt noch dadurch Flag zum Deaktivieren der Vorabruf von Dateidaten). Sie können weiterhin System Cache Überfrachtung veranlassen, wenn Sie große Anzahl von Dateien, die mit diesem Flag geöffnet und im Zufallsprinzip zugegriffen haben. Es wird dringend empfohlen, dass FILE_FLAG_RANDOM_ACCESS nicht von Anwendungen verwendet werden.
