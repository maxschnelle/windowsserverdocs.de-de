---
title: Zu verstehen Sie und das Speicherkonto neu synchronisiert
description: Ausführliche Informationen zu geschieht, wenn Speicher neu synchronisiert und in Windows Server-2019 angezeigt.
keywords: "\"Direkte Speicherplätze\", Speicher eine neusynchronisierung, resync, S2D-Speicher"
ms.prod: windows-server-threshold
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 01/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 81b1136a4b6a5cf8423a99e898b482a9b2849b5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813461"
---
# <a name="understand-and-monitor-storage-resync"></a>Grundlagen und Überwachung der Neusynchronisierung des Speichers

>Gilt für: Windows Server 2019

Neusynchronisierung Datenbankspeicher-Warnungen sind eine neue Funktion des ["direkte Speicherplätze"](storage-spaces-direct-overview.md) in Windows Server-2019, die den Health-Dienst einen Fehler auslöst, wenn es sich bei Ihrem Speicher werden neu synchronisiert werden können. Die Warnung eignet sich für benachrichtigt, wenn erneute Synchronisierung erfolgt, sodass Sie weitere Server versehentlich ergreifen nicht nach unten (das mehrere Fehlerdomänen betroffen sind, was in Ihrem Cluster sinkt führen könnte). 

Dieses Thema enthält Hintergrundinformationen und Schritte, um zu verstehen und neusynchronisierung von Speicher in einem Windows Server Failovercluster "direkte Speicherplätze".

## <a name="understanding-resync"></a>Grundlegendes zur neusynchronisierung

Beginnen wir mit einem einfachen Beispiel, um zu verstehen, wie der Speicher nicht synchronisiert wird. Bedenken Sie, dass jede shared-Nothing (nur lokale Laufwerke) verteilte speicherlösung weist dieses Verhalten. Wie Sie unten sehen werden, wenn ein Serverknoten ausfällt und dann deren Laufwerke wird nicht aktualisiert werden, bis sie wieder online - ist, ist dies "true" für jede hyper-konvergiert-Architektur. 

Nehmen wir an, dass die Zeichenfolge "HELLO" gespeichert werden soll. 

![-ASCII-Zeichenfolge "Hello"](media/understand-storage-resync/hello.png)

Asssuming haben wir drei-Wege-Spiegelung, haben wir drei Kopien dieser Zeichenfolge. Nun, wenn wir Server #1 (für Maintanence) vorübergehend unten verwenden, können wir kopieren #1 nicht zugreifen.

![Kopieren Sie #1 kann nicht zugegriffen werden.](media/understand-storage-resync/copy1.png)

Nehmen wir an, dass wir unsere Zeichenfolge von "HELLO" Aktualisieren auf "Hilfe". zu diesem Zeitpunkt.

![-ASCII-Zeichenfolge "Help".](media/understand-storage-resync/help.png)

Nachdem wir die Zeichenfolge zu aktualisieren, werden Kopie #2 und #3 erfolgreich aktualisiert. Allerdings kann nicht #1-Kopie weiterhin zugegriffen werden, weil Server #1 vorübergehend nicht verfügbar (für Maintanence) ist. 

![GIF-Datei beim Schreiben in #2 und #2 kopieren "](media/understand-storage-resync/write.gif)

Jetzt haben wir die Kopie #1, die Daten enthält, die nicht mehr synchron ist. Das Betriebssystem verwendet präzise dirty Region tracking zum Nachverfolgen der Bits, die nicht mehr synchron sind. Auf diese Weise beim Server #1 wieder online ist, können wir die Änderungen synchronisieren, durch Lesen von Daten aus der Kopie #2 "oder" #3, und überschreiben die Daten in der Kopie #1. Die Vorteile dieses Ansatzes sind, müssen wir nur die Daten kopiert, die veraltete, statt alle Daten vom Server #2 oder #3-Server werden neu synchronisiert ist.

![GIF-Datei überschrieben, kopieren Sie #1 "](media/understand-storage-resync/overwrite.gif)

Daher wird dies erläutert, wie die Daten nicht synchronisiert werden. Aber wie sieht diese aus auf hoher Ebene? In diesem Beispiel haben wir einen drei hyperkonvergenten Cluster wird angenommen. Wenn der Server #1 im Wartungsmodus befindet, wird es als ausgefallen angezeigt werden. Wenn Sie Server #1 wieder öffnen, startet er alle von der Speicher das präzise dirty Region Tracking (siehe oben) werden neu synchronisiert. Sobald die Daten alle synchronisiert sind, werden alle Server angezeigt werden als aktiv.

![GIF der administratoransicht des Resync"](media/understand-storage-resync/admin.gif)

## <a name="how-to-monitor-storage-resync-in-windows-server-2019"></a>Überwachen von Speicher erneute Synchronisierung in Windows Server-2019

Nun, da Sie die Funktionsweise von Speicher-Resync verstehen, sehen wir uns, wie dies in Windows Server-2019 wird angezeigt. Wir haben einen neuen Fehler um hinzugefügt der [Integritätsdienst](../../failover-clustering/health-service-overview.md) , die angezeigt, wenn Sie Ihren Speicher neu synchronisiert wird.

Um diesen Fehler in PowerShell anzuzeigen, führen Sie Folgendes aus:

``` PowerShell
Get-HealthFault
```

Dies ist ein neuer Fehler im Windows Server-2019 und erscheint in PowerShell, in den Bericht der clustervalidierung, und an anderer Stelle, die auf den Integritätsdienst Fehler erstellt. 

Um einen tieferen Einblick zu erhalten, können Sie die Zeitreihen-Datenbank in PowerShell wie folgt Abfragen:

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

Vor allem verwendet Windows Admin Center-Health-Fehler, um den Status und die Farbe der Clusterknoten festzulegen. Daher wird dieser neue Fehler Clusterknoten zugreifen, um den Übergang von Rot (unten) in (Neusynchronisieren) auf Grün (nach oben), anstatt direkt von Rot, Grün, Gelb auf dem Dashboard HCI verursachen.

![Bild der 2016 Vs 2019-Ansicht des Resync"](media/understand-storage-resync/compare.png)

Zeigen Sie den Gesamtstatus der neusynchronisierung von Speicher, können Sie genau wissen, wie viele Daten synchron sind, und gibt an, ob Ihr System Fortschritte macht. Wenn Sie Windows Admin Center zu öffnen, und wechseln Sie zu der *Dashboard*, die neue Warnung wird wie folgt angezeigt:

![Image von Windows Admin Center-Warnungen"](media/understand-storage-resync/alert.png)

Die Warnung eignet sich für benachrichtigt, wenn erneute Synchronisierung erfolgt, sodass Sie weitere Server versehentlich ergreifen nicht nach unten (das mehrere Fehlerdomänen betroffen sind, was in Ihrem Cluster sinkt führen könnte). 

Wenn Sie zum Navigieren der *Server* Windows Admin Center auf der Seite, klicken Sie auf *Inventur*, und wählen Sie dann auf einen bestimmten Server, erhalten Sie eine detailliertere Ansicht der Darstellung von diesem Speicher Resync auf pro Server aggregiert. Wenn Sie mit dem Server navigieren, und sehen Sie sich die *Storage* Diagramm sehen Sie die Menge der Daten, die in repariert werden müssen eine *lila* Zeile mit der genauen Anzahl direkt über. Dieser Betrag wird zu erhöhen, wenn der Server ausgefallen (Weitere Daten muss resynced werden) ist, und allmählich verringert wird, wenn der Server wieder online ist (Daten synchronisiert wird). Wenn die Menge der Daten, die Reparatur ist 0, der Speicher ist fertig Neusynchronisieren - Sie können jetzt einen Server Herunterfahren, wenn Sie möchten. Ein Screenshot aus dieser Erfahrung in der Windows Admin Center wird unten gezeigt:

![Abbildung des Serveransicht in Windows Admin Center "](media/understand-storage-resync/server.png)

## <a name="how-to-see-storage-resync-in-windows-server-2016"></a>Wie Sie die neusynchronisierung von Speicher in Windows Server 2016 finden Sie unter

Wie Sie sehen können, ist diese Warnung besonders hilfreich, in einen ganzheitlichen Überblick über die Abläufe in der Speicherschicht zur abrufen. Es werden effektiv zusammengefasst, die Informationen, die Sie über das Cmdlet Get-StorageJob abrufen können, die Informationen zu lang andauernden speichermodulaufträgen mit, wie z. B. einen Reparaturvorgang auf einem Speicherplatz zurückgibt. Ein Beispiel ist unten dargestellt:

```PowerShell
Get-StorageJob
```

Hier ist Beispiel der Ausgabe:

```
Name                  ElapsedTime           JobState              PercentComplete       IsBackgroundTask
----                  -----------           --------              ---------------       ----------------
Regeneration          00:01:19              Running               50                    True

```

In dieser Ansicht ist sehr viel präziser, da die speicheraufträge, die aufgelistet, pro Volume werden, sehen Sie die Liste der Aufträge, die ausgeführt werden und Sie können die einzelnen Status nachverfolgen. Dieses Cmdlet funktioniert sowohl für Windows Server 2016 2019.

## <a name="see-also"></a>Siehe auch

- [Ein Server zur Wartung offline geschaltet](maintain-servers.md)
- [Übersicht über Storage "direkte Speicherplätze"](storage-spaces-direct-overview.md)