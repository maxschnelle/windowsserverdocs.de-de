---
title: Beheben von Leistungsproblemen zwischen Cache und Speicher-Manager
description: Beheben von Leistungsproblemen zwischen Cache und Speicher-Manager unter Windows Server 16
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Pavel; ATales
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: d55ad122048a8b180c9d12abe03666b796c3e9b5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370013"
---
# <a name="troubleshoot-cache-and-memory-manager-performance-issues"></a>Beheben von Leistungsproblemen zwischen Cache und Speicher-Manager

Vor Windows Server 2012 haben zwei primäre potenzielle Probleme bewirkt, dass der Systemdatei Cache vergrößert wurde, bis der verfügbare Arbeitsspeicher unter bestimmten Arbeits Auslastungen fast erschöpft war. Wenn diese Situation dazu führt, dass das System langsam ist, können Sie bestimmen, ob der Server einem dieser Probleme ausgesetzt ist.


## <a name="counters-to-monitor"></a>Zu überwachende Zähler

-   Lange\\Dauer des Arbeitsspeichers für den standbycache im &lt; standbycache 1800 Sekunden

-   Verfüg\\barer Arbeitsspeicher (MB) ist niedrig

-   Speicher\\System-Cache Residente Bytes

Wenn der\\verfügbare Arbeitsspeicher (MB) gering ist und gleich\\zeitig in den Speicher System Cache Residente Bytes einen erheblichen Teil des physischen Speichers beanspruchen, können Sie [rammap](https://technet.microsoft.com/sysinternals/ff700229.aspx) verwenden, um herauszufinden, wofür der Cache verwendet wird.

## <a name="system-file-cache-contains-ntfs-metafile-data-structures"></a>Der System Dateicache enthält NTFS-Metadatei-Datenstrukturen.


Dieses Problem wird durch eine sehr hohe Anzahl aktiver metadatendateiseiten in der rammap-Ausgabe angegeben, wie in der folgenden Abbildung dargestellt. Dieses Problem wurde möglicherweise auf stark ausgelasteten Servern erkannt, auf die Millionen von Dateien zugegriffen wurde, was dazu führte, dass die NTFS-Metadatendateien nicht aus dem Cache freigegeben werden.

![rammap-Ansicht](../../media/perftune-guide-rammap.png)

Das Problem, das durch das *dyncache* -Tool behoben werden muss. In Windows Server 2012 und höher wurde die Architektur neu gestaltet, und dieses Problem sollte nicht mehr bestehen.

## <a name="system-file-cache-contains-memory-mapped-files"></a>Der System Dateicache enthält Speicher Abbild Dateien.


Dieses Problem wird durch eine sehr hohe Anzahl aktiver zugeordneter Datei Seiten in der rammap-Ausgabe angegeben. Dies weist normalerweise darauf hin, dass einige Anwendungen auf dem Server viele große Dateien öffnen [, indem Sie](https://msdn.microsoft.com/library/windows/desktop/aa363858.aspx) die API "\_-\_API\_" mit dem Dateiflag "Random Access" festlegen.

Dieses Problem wird im KB-Artikel [2549369](https://support.microsoft.com/default.aspx?scid=kb;en-US;2549369)ausführlich beschrieben. Das\_Flag\_"\_Dateiflag für Zufalls Zugriff" ist ein Hinweis für den Cache-Manager, um die zugeordneten Sichten der Datei so lange wie möglich im Arbeitsspeicher beizubehalten Gleichzeitig weist dieses Flag den Cache-Manager an, das Vorabrufen von Datei Daten zu deaktivieren.

Diese Situation wurde in gewissem Maße durch das Arbeiten mit den Verbesserungen in Windows Server 2012 und höher behoben, aber das Problem selbst muss hauptsächlich vom Anwendungshersteller behandelt werden, indem kein\_Dateiflag\_zufällig\_verwendetwird.Zugriff. Eine alternative Lösung für den Hersteller der APP ist möglicherweise, beim Zugriff auf die Dateien eine niedrige Speicher Priorität zu verwenden. Dies kann mithilfe der [setthreadinformation](https://msdn.microsoft.com/library/windows/desktop/hh448390.aspx) -API erreicht werden. Seiten, auf die mit niedriger Arbeitsspeicher Priorität zugegriffen wird, werden aggressiver aus dem Workingset entfernt.

Der Cache-Manager, beginnend mit Windows Server 2016, verringert dies durch das Ignorieren von FILE_FLAG_RANDOM_ACCESS, wenn Kürzungs Entscheidungen getroffen werden. Daher wird er wie jede andere Datei behandelt, die ohne das FILE_FLAG_RANDOM_ACCESS-Flag geöffnet wurde (der Cache-Manager berücksichtigt dies weiterhin Flag, das das Vorabrufen von Datei Daten deaktiviert. Sie können weiterhin System Cache Überlastung verursachen, wenn Sie über eine große Anzahl von Dateien verfügen, die mit diesem Flag geöffnet sind und auf eine ganz zufällige Weise aufgerufen werden. Es wird dringend empfohlen, FILE_FLAG_RANDOM_ACCESS nicht von Anwendungen zu verwenden.
