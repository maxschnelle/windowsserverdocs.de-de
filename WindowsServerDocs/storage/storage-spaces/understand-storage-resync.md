---
title: Verstehen und Anzeigen der erneuten Synchronisierung von Speicher
description: Ausführliche Informationen darüber, wann die erneute Synchronisierung des Speichers stattfindet und wie Sie in Windows Server 2019 angezeigt wird.
ms.prod: windows-server
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 01/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1209a3e08922a380ef46d3be6d28ce489b748f22
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820933"
---
# <a name="understand-and-monitor-storage-resync"></a>Grundlagen und Überwachung der Neusynchronisierung des Speichers

>Gilt für: Windows Server 2019

Warnungen zum erneuten Synchronisieren von Speicher stellen eine neue Funktion von [direkte Speicherplätze](storage-spaces-direct-overview.md) in Windows Server 2019 dar, die es dem Integritätsdienst ermöglicht, bei der erneuten Synchronisierung des Speichers einen Fehler auszulösen. Die Warnung ist hilfreich, wenn Sie benachrichtigt werden, wenn eine erneute Synchronisierung durchgeführt wird, sodass Sie nicht versehentlich weitere Server herunterfahren (was dazu führen kann, dass mehrere Fehler Domänen beeinträchtigt werden, was dazu führt, dass Ihr Cluster ausfällt). 

Dieses Thema enthält Hintergrundinformationen und Schritte, um die erneute Synchronisierung von Speicher in einem Windows Server-Failovercluster mit direkte Speicherplätze zu verstehen und zu lesen.

## <a name="understanding-resync"></a>Grundlegendes zum erneuten Synchronisieren

Beginnen wir mit einem einfachen Beispiel, um zu verstehen, wie der Speicher nicht synchronisiert wird. Beachten Sie, dass die verteilte Speicherlösung "Shared-Nothing" (nur lokale Laufwerke) dieses Verhalten aufweist. Wie Sie unten sehen werden, werden die Laufwerke, wenn ein Server Knoten ausfällt, erst dann aktualisiert, wenn Sie wieder online geschaltet werden. Dies gilt für jede hyperkonvergierte Architektur. 

Angenommen, Sie möchten die Zeichenfolge "Hello" speichern. 

![ASCII-Zeichenfolge "Hello"](media/understand-storage-resync/hello.png)

Wenn wir die drei-Wege-Spiegelungs Resilienz haben, haben wir drei Kopien dieser Zeichenfolge. Wenn wir jetzt den Server #1 vorübergehend (für die maintangente) nutzen, können wir nicht auf Kopier #1 zugreifen.

![Zugriff auf Kopier #1 nicht möglich](media/understand-storage-resync/copy1.png)

Angenommen, wir aktualisieren die Zeichenfolge von "Hello" in "Help!" zu diesem Zeitpunkt.

![ASCII-Zeichenfolge "Help!"](media/understand-storage-resync/help.png)

Wenn Sie die Zeichenfolge aktualisieren, werden die Kopier #2 und #3 erfolgreich aktualisiert. Es ist jedoch nicht möglich, auf den Kopiervorgang #1 zuzugreifen, da der Server #1 vorübergehend ausfällt (für die Wartung). 

![GIF von Schreibvorgang zum Kopieren #2 und #2 "](media/understand-storage-resync/write.gif)

Nun verfügen wir über eine Kopie #1, die Daten enthält, die nicht synchronisiert sind. Das Betriebssystem verwendet eine differenzierte Änderungs Regions Überwachung, um die Bits zu verfolgen, die nicht synchron sind. Auf diese Weise können die Änderungen synchronisiert werden, wenn die Server #1 wieder online geschaltet werden, indem Sie die Daten aus der Kopier #2 lesen oder #3 und die Daten in der Kopier #1 überschreiben. Der Vorteil dieses Ansatzes besteht darin, dass wir nur die veralteten Daten kopieren müssen, anstatt alle Daten von Server #2 oder Server #3 neu zu synchronisieren.

![GIF der Überschreibung zum Kopieren #1 "](media/understand-storage-resync/overwrite.gif)

Dadurch wird die Synchronisierung der Daten erläutert. Aber wie sieht das auf einer hohen Ebene aus? Nehmen wir an, dass in diesem Beispiel ein drei Server mit hyperkonvergiertem Cluster vorhanden ist. Wenn sich der Server #1 im Wartungsmodus befindet, wird er als nicht herunterladen angezeigt. Wenn Sie Server #1 wiederherstellen, wird der gesamte Speicher mithilfe der Granularität der Nachverfolgung von Änderungs Regionen neu synchronisiert (oben erläutert). Sobald die Daten synchron sind, werden alle Server als aufwärts angezeigt.

![GIF der admin-Ansicht von Resync "](media/understand-storage-resync/admin.gif)

## <a name="how-to-monitor-storage-resync-in-windows-server-2019"></a>Überwachen der erneuten Synchronisierung von Speicher in Windows Server 2019

Nachdem Sie nun wissen, wie die Speicher Neusynchronisierung funktioniert, sehen wir uns an, wie dies in Windows Server 2019 angezeigt wird. Wir haben dem [Integritätsdienst](../../failover-clustering/health-service-overview.md) einen neuen Fehler hinzugefügt, der angezeigt wird, wenn der Speicher neu synchronisiert wird.

Führen Sie folgenden Befehl aus, um diesen Fehler in PowerShell anzuzeigen:

``` PowerShell
Get-HealthFault
```

Dabei handelt es sich um einen neuen Fehler in Windows Server 2019, der in PowerShell, im Cluster Validierungsbericht und an allen anderen Orten angezeigt wird, die auf Integritäts Fehlern aufbauen. 

Um eine tiefere Ansicht zu erhalten, können Sie die Zeitreihen Datenbank in PowerShell wie folgt Abfragen:

```PowerShell
Get-ClusterNode | Get-ClusterPerf -ClusterNodeSeriesName ClusterNode.Storage.Degraded
```
Ausgabebeispiel:

```
Object Description: ClusterNode Server1

Series                       Time                Value Unit
------                       ----                ----- ----
ClusterNode.Storage.Degraded 01/11/2019 16:26:48     214 GB
```

Insbesondere verwendet Windows Admin Center Integritäts Fehler, um den Status und die Farbe von Cluster Knoten festzulegen. Dieser neue Fehler bewirkt also, dass Cluster Knoten von rot (nach unten) zu gelb (Neusynchronisierung) auf grün (nach oben) anstatt direkt von rot nach grün im HCI-Dashboard wechseln.

![Abbildung von 2016 vs 2019 Ansicht der erneuten Synchronisierung "](media/understand-storage-resync/compare.png)

Wenn Sie den Gesamtstatus der erneuten Synchronisierung des Speichers anzeigen, können Sie genau wissen, wie viele Daten nicht synchronisiert sind und ob Ihr System den Fortschritt vornimmt. Wenn Sie das Windows Admin Center öffnen und zum *Dashboard*navigieren, wird die neue Warnung wie folgt angezeigt:

![Abbildung der Warnung im Windows Admin Center "](media/understand-storage-resync/alert.png)

Die Warnung ist hilfreich, wenn Sie benachrichtigt werden, wenn eine erneute Synchronisierung durchgeführt wird, sodass Sie nicht versehentlich weitere Server herunterfahren (was dazu führen kann, dass mehrere Fehler Domänen beeinträchtigt werden, was dazu führt, dass Ihr Cluster ausfällt). 

Wenn Sie im Windows Admin Center zur Seite " *Server* " navigieren, auf "Inventory" ( *Inventur*) klicken und dann einen bestimmten Server auswählen, erhalten Sie eine ausführlichere Übersicht darüber, wie diese Speicher Neusynchronisierung auf Server Basis durchsucht wird. Wenn Sie zu Ihrem Server navigieren und sich das *Speicher* Diagramm ansehen, sehen Sie, dass die Menge der zu reparierenden Daten in einer *lila* Linie mit der exakten Zahl rechts oben repariert werden muss. Diese Menge erhöht sich, wenn der Server heruntergefahren wird (mehr Daten müssen neu synchronisiert werden müssen) und sich allmählich verringern, wenn der Server wieder online geschaltet wird (die Daten werden synchronisiert). Wenn die Menge der zu reparierenden Daten 0 beträgt, ist die erneute Synchronisierung des Speichers abgeschlossen. bei Bedarf können Sie einen Server herunterladen. Im folgenden finden Sie einen Screenshot dieses Erlebnisses in Windows Admin Center:

![Abbildung der Serveransicht im Windows Admin Center "](media/understand-storage-resync/server.png)

## <a name="how-to-see-storage-resync-in-windows-server-2016"></a>Anzeigen der erneuten Synchronisierung von Speicher in Windows Server 2016

Wie Sie sehen können, ist diese Warnung besonders hilfreich, um eine ganzheitliche Ansicht der Vorgänge auf der Speicher Ebene zu erhalten. Sie fasst die Informationen zusammen, die Sie aus dem Cmdlet "Get-storagejob" abrufen können, das Informationen zu Aufträgen für Speichermodule mit langer Ausführungszeit zurückgibt, wie z. b. einen Reparaturvorgang auf einem Speicherplatz. Unten ist ein Beispiel angegeben:

```PowerShell
Get-StorageJob
```

Beispielausgabe:

```
Name                  ElapsedTime           JobState              PercentComplete       IsBackgroundTask
----                  -----------           --------              ---------------       ----------------
Regeneration          00:01:19              Running               50                    True

```

Diese Ansicht ist weitaus präziser, da die aufgeführten Speicher Aufträge pro Volume angezeigt werden. Sie können die Liste der ausgeführten Aufträge anzeigen und Ihren individuellen Fortschritt nachverfolgen. Dieses Cmdlet funktioniert sowohl auf Windows Server 2016 als auch auf 2019.

## <a name="see-also"></a>Siehe auch

- [Offlineschalten eines „Direkte Speicherplätze“-Servers zu Wartungszwecken](maintain-servers.md)
- [Übersicht über direkte Speicherplätze](storage-spaces-direct-overview.md)