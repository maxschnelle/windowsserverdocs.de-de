---
title: Verstehen Sie und finden Sie unter Speicher neu synchronisierten
description: Ausführliche Informationen zum Speicher neu synchronisierten wann erfolgt und wie Sie in Windows Server 2019 angezeigt.
keywords: Direkte Speicherplätze, Speicher neu synchronisierten, neusynchronisierung, Speicher, S2D
ms.prod: windows-server-threshold
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 01/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 81b1136a4b6a5cf8423a99e898b482a9b2849b5f
ms.sourcegitcommit: 748eccd10fc0c3c962d6e64ff6ead08017ac1947
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/15/2019
ms.locfileid: "9009623"
---
# Verstehen und Überwachen von Speicher neu synchronisierten

>Gilt für: WindowsServer 2019

Speicher neu synchronisierten Warnungen sind eine neue Funktion von [Direkte Speicherplätze](storage-spaces-direct-overview.md) in Windows Server 2019, mit dem der Zustandsdienst einen Fehler ausgelöst wird, wenn Sie Ihren Speicher neu synchronisiert wird. Die Warnung eignet sich Hinweis darauf, dass neu synchronisierten ausgeführt wird, damit Sie versehentlich weitere Server nutzen nicht nach unten (wodurch mehrere Fehlerdomänen betroffen sein, könnte sich ergebenden im Cluster gelangen). 

Dieses Thema enthält Hintergrundinformationen und Schritte zu verstehen und zu finden Sie unter Speicher neu synchronisierten in einem Windows Server-Failovercluster mit "direkte Speicherplätze".

## Grundlegendes zu neu synchronisierten

Beginnen wir mit einem einfachen Beispiel zu verstehen, wie die Speicher synchron abruft. Denken Sie daran, die von allen shared-Nothing (lokale Laufwerke) verteilten speicherlösung dieses Verhalten dargestellt. Wie Sie weiter unten sehen können, wenn ein Serverknoten nach unten, geht, und klicken Sie dann die Laufwerke wird nicht aktualisiert werden, bis es wieder online - ist gilt dies für alle hyperkonvergente Architektur. 

Nehmen wir an, dass wir die Zeichenfolge "HELLO" speichern möchten. 

![-ASCII-Zeichenfolge "Hello"](media/understand-storage-resync/hello.png)

Asssuming haben wir die drei-Wege-spiegelungsresilienz, haben wir drei Kopien dieser Zeichenfolge. Nun, wenn wir Server #1 nach unten vorübergehend (für Maintanence) verwenden, können wir Kopie #1 nicht zugreifen.

![Kopie #1 kann nicht zugegriffen werden.](media/understand-storage-resync/copy1.png)

Nehmen wir an, dass wir unsere Zeichenfolge aus "HELLO" Aktualisieren "Hilfe!" zu diesem Zeitpunkt.

![-ASCII-Zeichenfolge "Hilfe!"](media/understand-storage-resync/help.png)

Nachdem wir die Zeichenfolge aktualisieren, werden Kopie #2 und #3 erfolgreich aktualisiert. Jedoch kann nicht kopieren #1 weiterhin zugegriffen werden, da Server #1 vorübergehend nach unten (für Maintanence) ist. 

![GIF-Datei zum Schreiben in #2 und #2 kopieren "](media/understand-storage-resync/write.gif)

Jetzt haben wir Kopie #1, die Daten enthält, die synchron sind. Das Betriebssystem verwendet die präzise veralteten Bereich nachverfolgen, um zu verfolgen die Bits, die nicht mehr synchron sind. Auf diese Weise, wenn der Server #1 wieder online ist, können wir die Änderungen durch Lesen der Daten von Kopie #2 oder #3 und überschreiben die Daten in Kopie #1 synchronisieren. Die Vorteile dieses Ansatzes sind, müssen wir nur über die Daten zu kopieren, veraltet, anstatt neu synchronisiert alle Daten vom Server #2 oder Server #3.

![GIF zu überschreiben, kopieren Sie #1 "](media/understand-storage-resync/overwrite.gif)

Ja, wird dies erläutert, wie Daten synchron abruft. Aber was diese sieht aus auf hoher Ebene? Gehen davon aus, in diesem Beispiel haben wir einen drei Server zusammengeführte Cluster. Wenn Server #1 in Wartung ist, wird es als nicht verfügbar angezeigt werden. Wenn Sie Server #1 wieder verfügbar zu machen, starten wird neu synchronisiert alle von der Speicher die präzise veralteten Bereich Tracking (siehe oben). Nachdem die Daten alle synchron sind, auf allen Servern angezeigt werden als verfügbar.

![GIF-Datei der Admin-Ansicht des neu synchronisierten"](media/understand-storage-resync/admin.gif)

## Wie Sie Speicher neu synchronisierten in Windows Server 2019 überwachen

Nun, da Sie Verständnis der Funktionsweise von Speicher-RE, sehen wir uns wie dies in Windows Server 2019 wird angezeigt. Wir haben einen neuen Fehler an den [Dienst zum](../../failover-clustering/health-service-overview.md) hinzugefügt, die angezeigt wird, wenn Sie Ihren Speicher neu synchronisiert wird.

Um diesen Fehler in PowerShell anzuzeigen, führen Sie:

``` PowerShell
Get-HealthFault
```

Dies ist eine neue Fehler in Windows Server 2019 und in PowerShell, in der Prüfbericht Cluster und an anderer Stelle, die builds zu Health-Fehlern angezeigt. 

Um eine genauere Ansicht zu erhalten, können Sie die Zeit Reihe-Datenbank in PowerShell wie folgt Abfragen:

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

Insbesondere verwendet Windows Admin Center Health-Fehler, um den Status und die Farbe der Clusterknoten festzulegen. Daher bewirkt diese neue Fehlertoleranz Clusterknoten für den Übergang von Rot (unten) (neu synchronisiert) in Grün (oben), statt direkt von Rot in Grün, Gelb im Dashboard HCI, dass.

![Abbildung der 2016 Vs 2019 Ansicht der neu synchronisierten"](media/understand-storage-resync/compare.png)

Indem Sie mit dem Fortschritt der gesamten Speicher neu synchronisierten, können Sie genau feststellen, wie viele Daten synchron sind, und gibt an, ob das System Fortschritt macht. Wenn Sie Windows Admin Center und Sie das *Dashboard öffnen*, sehen Sie die neue Benachrichtigung wie folgt:

![Abbildung der Warnung in Windows Admin Center"](media/understand-storage-resync/alert.png)

Die Warnung eignet sich Hinweis darauf, dass neu synchronisierten ausgeführt wird, damit Sie versehentlich weitere Server nutzen nicht nach unten (wodurch mehrere Fehlerdomänen betroffen sein, könnte sich ergebenden im Cluster gelangen). 

Wenn Sie auf die *Server* -Seite im Windows Admin Center navigieren, klicken Sie auf *Inventar*und wählen Sie dann einen bestimmten Server, erhalten Sie eine weitere detaillierte Ansicht der Darstellung von diesem Speicher neu synchronisierten auf pro Server. Wenn Sie an den Server zu navigieren und sehen Sie sich das Diagramm *Speicher* , sehen Sie die Menge an Daten, die in eine *violette* Linie genaue Anzahl repariert werden nach rechts oben. Dieser Betrag wird vergrößern, wenn der Server nach unten (Weitere Daten muss neu synchronisiert muss, wenn werden) ist, und schrittweise, verringern, wenn der Server wieder online ist (es ist Daten synchronisiert wird). Wenn die Menge der Daten, die Reparatur ist 0 sein müssen, Ihren Speicher ist fertig neu synchronisiert - Sie können jetzt einen Server offline schalten, wenn notwendig. Ein Bildschirmfoto des diese Erfahrung im Windows Admin Center ist unten dargestellt:

![Abbildung der Serveransicht in Windows Admin Center"](media/understand-storage-resync/server.png)

## Wie Sie Speicher neu synchronisierten in Windows Server 2016

Wie Sie sehen können, ist diese Warnung besonders hilfreich, eine umfassende Ansicht, was passiert Ebene Speicher abrufen. Es sind effektiv die Informationen, die Sie aus dem Cmdlet Get-StorageJob erhalten können, die Informationen über die Speicher-Modul Aufträge mit langer Ausführung, z. B. einen Reparaturvorgang an einem Speicherplatz zurückgibt zusammengefasst. Ein Beispiel ist unten dargestellt:

```PowerShell
Get-StorageJob
```

Hier ist der Ausgabe:

```
Name                  ElapsedTime           JobState              PercentComplete       IsBackgroundTask
----                  -----------           --------              ---------------       ----------------
Regeneration          00:01:19              Running               50                    True

```

Diese Ansicht ist viel genauere, da die Speicher-Aufträge aufgeführt, pro Volume sind, sehen Sie die Liste der Aufträge, die ausgeführt werden und Sie können den einzelnen Fortschritt nachverfolgen. Dieses Cmdlet kann unter Windows Server 2016 und 2019.

## Weitere Informationen:

- [Server zu Wartungszwecken offline schalten](maintain-servers.md)
- [Direkte Speicherplätze – Übersicht](storage-spaces-direct-overview.md)