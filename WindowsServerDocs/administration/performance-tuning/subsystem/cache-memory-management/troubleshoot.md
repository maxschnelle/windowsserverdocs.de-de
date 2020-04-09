---
title: Beheben von Leistungsproblemen zwischen Cache und Speicher-Manager
description: Beheben von Leistungsproblemen zwischen Cache und Speicher-Manager unter Windows Server 16
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: pavel; atales
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 0b01808564cfaf1eaedf30a66c774e2228205847
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851653"
---
# <a name="troubleshoot-cache-and-memory-manager-performance-issues"></a>Beheben von Leistungsproblemen zwischen Cache und Speicher-Manager

Vor Windows Server 2012 haben zwei primäre potenzielle Probleme bewirkt, dass der Systemdatei Cache vergrößert wurde, bis der verfügbare Arbeitsspeicher unter bestimmten Arbeits Auslastungen fast erschöpft war. Wenn diese Situation dazu führt, dass das System langsam ist, können Sie bestimmen, ob der Server einem dieser Probleme ausgesetzt ist.


## <a name="counters-to-monitor"></a>Zu überwachende Zähler

-   Arbeitsspeicher\\langfristige Dauer der standbycache-Lebensdauer &lt; 1800 Sekunden

-   Der Arbeitsspeicher\\verfügbare MB ist niedrig.

-   Speicher\\System Cache Residente Bytes

Wenn Arbeitsspeicher\\verfügbare MB niedrig ist und gleichzeitig Speicher\\System Cache Residente Bytes einen erheblichen Teil des physischen Speichers beanspruchen, können Sie [rammap](https://technet.microsoft.com/sysinternals/ff700229.aspx) verwenden, um herauszufinden, wofür der Cache verwendet wird.

## <a name="system-file-cache-contains-ntfs-metafile-data-structures"></a>Der System Dateicache enthält NTFS-Metadatei-Datenstrukturen.


Dieses Problem wird durch eine sehr hohe Anzahl aktiver metadatendateiseiten in der rammap-Ausgabe angegeben, wie in der folgenden Abbildung dargestellt. Dieses Problem wurde möglicherweise auf stark ausgelasteten Servern erkannt, auf die Millionen von Dateien zugegriffen wurde, was dazu führte, dass die NTFS-Metadatendateien nicht aus dem Cache freigegeben werden.

![rammap-Ansicht](../../media/perftune-guide-rammap.png)

Das Problem, das durch das *dyncache* -Tool behoben werden muss. In Windows Server 2012 und höher wurde die Architektur neu gestaltet, und dieses Problem sollte nicht mehr bestehen.

## <a name="system-file-cache-contains-memory-mapped-files"></a>Der System Dateicache enthält Speicher Abbild Dateien.


Dieses Problem wird durch eine sehr hohe Anzahl aktiver zugeordneter Datei Seiten in der rammap-Ausgabe angegeben. Dies weist normalerweise darauf hin, dass einige Anwendungen auf dem Server viele große Dateien öffnen [, indem Sie](https://msdn.microsoft.com/library/windows/desktop/aa363858.aspx) die-API mit der Datei\_Flag\_Random\_Access-Flag festgelegt haben.

Dieses Problem wird im KB-Artikel [2549369](https://support.microsoft.com/default.aspx?scid=kb;en-US;2549369)ausführlich beschrieben. Datei\_Flag\_Random\_Access-Flag ist ein Hinweis für den Cache-Manager, dass die zugeordneten Sichten der Datei so lange wie möglich im Arbeitsspeicher aufbewahrt werden (bis der Speicher-Manager nicht zu wenig Arbeitsspeicher-Bedingungen signalisiert). Gleichzeitig weist dieses Flag den Cache-Manager an, das Vorabrufen von Datei Daten zu deaktivieren.

Diese Situation wurde in gewissem Maße durch das Arbeiten mit den Verbesserungen in Windows Server 2012 und höher behoben, aber das Problem selbst muss hauptsächlich vom Anwendungshersteller adressiert werden, indem kein Datei\_Flag\_Zufalls\_Zugriff verwendet wird. Eine alternative Lösung für den Hersteller der APP ist möglicherweise, beim Zugriff auf die Dateien eine niedrige Speicher Priorität zu verwenden. Dies kann mithilfe der [setthreadinformation](https://msdn.microsoft.com/library/windows/desktop/hh448390.aspx) -API erreicht werden. Seiten, auf die mit niedriger Arbeitsspeicher Priorität zugegriffen wird, werden aggressiver aus dem Workingset entfernt.

Der Cache-Manager, beginnend mit Windows Server 2016, verringert dies durch das Ignorieren von FILE_FLAG_RANDOM_ACCESS, wenn Kürzungs Entscheidungen getroffen werden. er wird daher wie jede andere Datei behandelt, die ohne das FILE_FLAG_RANDOM_ACCESS-Flag geöffnet wurde (der Cache-Manager berücksichtigt dieses Flag weiterhin, um das Vorabruf von Datei Daten zu deaktivieren). Sie können weiterhin System Cache Überlastung verursachen, wenn Sie über eine große Anzahl von Dateien verfügen, die mit diesem Flag geöffnet sind und auf eine ganz zufällige Weise aufgerufen werden. Es wird dringend empfohlen, FILE_FLAG_RANDOM_ACCESS von Anwendungen nicht verwendet zu werden.
