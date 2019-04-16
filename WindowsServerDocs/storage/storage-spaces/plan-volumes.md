---
ms.assetid: 342173ca-4e10-44f4-b2c9-02a6c26f7a4a
title: Planen von Volumes in Direkte Speicherplätze
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 01/10/2019
ms.localizationpriority: medium
ms.openlocfilehash: e2d9e6828584f4027aa32cec26572c2290098ab6
ms.sourcegitcommit: 6f5bd789e165baf2b399033dae3eb958d16bc988
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/10/2019
ms.locfileid: "9000232"
---
# Planen von Volumes in Direkte Speicherplätze

> Gilt für: WindowsServer 2016, WindowsServer 2019

Dieses Thema enthält Informationen zum Planen von Volumes in Direkte Speicherplätze, um die Leistungs- und Kapazitätsanforderungen Ihrer Workloads zu erfüllen, einschließlich der Auswahl des Dateisystems, Resilienztyps und der Größe.

## Lesen Sie: Was sind Volumes?

Volumes sind die Datenspeicher, in denen Sie die von Ihren Workloads benötigten Dateien ablegen, z.B. VHD- oder VHDX-Dateien für virtuelle Hyper-V-Computer. Volumes kombinieren die Laufwerke im Speicherpool, um die Fehlertoleranz, Skalierbarkeit und Leistungsvorteile von Direkte Speicherplätze einzuführen.

   >[!NOTE]
   > In der gesamten Dokumentation für Direkte Speicherplätze verwenden wir Begriff "Volume" als Bezeichnung für das Volume und den virtuellen Datenträger darunter, einschließlich der Funktionen, die von anderen integrierten Windows-Features bereitgestellt werden, z.B. freigegebenen Clustervolumes (Cluster Shared Volumes, CSV) und ReFS. Es ist nicht erforderlich, diese Unterschiede auf Implementierungsebene zu verstehen, um Direkte Speicherplätze erfolgreich zu planen und bereitzustellen.

![what-are-volumes](media/plan-volumes/what-are-volumes.png)

Alle Volumes sind für alle Server im Cluster gleichzeitig zugänglich. Sobald sie erstellt wurden, werden sie unter **C:\ClusterStorage\** auf allen Servern angezeigt.

![csv-folder-screenshot](media/plan-volumes/csv-folder-screenshot.png)

## Auswählen, wie viele Volumes erstellt werden

Es wird empfohlen, der Anzahl der Volumes auf ein Vielfaches der Anzahl von Servern im Cluster festzulegen. Wenn Sie 4 Server haben, werden Sie z. B. mit 4 insgesamt Volumes mit 3 oder 5 als eine konsistentere Leistung auftreten. Dies ermöglicht dem Cluster das gleichmäßige Verteilen des Volume-"Besitzes" (ein Server übernimmt die Metadatenorchestrierung pro Volume) auf Server.

Es wird empfohlen, beschränken die Gesamtanzahl der Volumes auf:

| Windows Server 2016          | Windows Server 2019          |
|------------------------------|------------------------------|
| Bis zu 32 Volumes pro cluster | Bis zu 64 Volumes pro cluster |

## Auswahl des Dateisystems

Wir empfehlen die Verwendung des neuen [robusten Dateisystems (Resilient File System, ReFS)](../refs/refs-overview.md) für Direkte Speicherplätze. ReFS ist das wichtigste Dateisystem, das speziell für die Virtualisierung entwickelt wurde und viele Vorteile bietet, z.B. stark beschleunigte Leistung und integrierten Schutz vor Datenbeschädigung. Fast alle Schlüssel NTFS-Funktionen, einschließlich der Datendeduplizierung in Windows Server, Version 1709 und höher unterstützt. Finden Sie in der ReFS [Vergleich](../refs/refs-overview.md#feature-comparison) Details.

Wenn Ihre Workload ein Feature erfordert, das von ReFS noch nicht unterstützt wird, können Sie stattdessen NTFS verwenden.

   >[!TIP]
   > Volumes mit verschiedenen Dateisystemen können im selben Cluster vorhanden sein.

## Auswählen des Resilienztyps

Volumes in Direkte Speicherplätze bieten Resilienz zum Schutz vor Hardwareproblemen, z.B. Laufwerks- oder Serverausfällen, und zum Aktivieren von kontinuierlicher Verfügbarkeit während der gesamten Serverwartung der Server, z.B. bei Softwareupdates.

   >[!NOTE]
   > Die auswählbaren Resilienztypen hängen nicht von der Art der Laufwerke ab, die Sie verwenden.

### Bei zwei Servern

Die einzige Option für Cluster mit zwei Servern ist die Zweiwegespiegelung. Dabei werden zwei Kopien aller Daten beibehalten, eine Kopie auf den Laufwerken auf jedem Server. Die Speichereffizienz ist 50% – zum Schreiben von 1TB an Daten benötigen Sie mindestens 2TB physische Speicherkapazität im Speicherpool. Die Zweiwegespiegelung kann jeweils einen Hardwarefehler (Laufwerk oder Server) sicher tolerieren.

![two-way-mirror](media/plan-volumes/two-way-mirror.png)

Wenn Sie mehr als zwei Server haben, wird empfohlen, stattdessen einen der folgenden Resilienztypen zu verwenden.

### Bei drei-Servern

Bei drei Servern sollten Sie die Dreiwegespiegelung für eine bessere Fehlertoleranz und Leistung verwenden. Bei der Dreiwegespiegelung werden drei Kopien aller Daten beibehalten, eine Kopie auf den Laufwerken auf jedem Server. Die Speichereffizienz ist 33,3% – zum Schreiben von 1TB an Daten benötigen Sie mindestens 3TB physische Speicherkapazität im Speicherpool. Die Dreiwegespiegelung kann [mindestens zwei gleichzeitige Hardwareprobleme (Laufwerk oder Server) sicher tolerieren](storage-spaces-fault-tolerance.md#examples). Wenn 2 Knoten nicht mehr verfügbar wird Speicherpool Quorum, verlieren, da 2/3 der Datenträger nicht verfügbar sind, und die virtueller Datenträger nicht erreichbar. Allerdings kann ein Knoten nach unten und einen oder mehrere Datenträger auf einem anderen Knoten können fehlschlagen, und bleibt die virtueller Datenträger online. Beispiel: Wenn Sie einen Server neu starten und plötzlich ein anderes Laufwerk oder ein anderer Server ausfällt, bleiben alle Daten sicher und kontinuierlich zugänglich.

![three-way-mirror](media/plan-volumes/three-way-mirror.png)

### Bei vier oder mehr Servern

Bei vier oder mehr Servern können Sie für jedes Volume auswählen, ob Dreiwegespiegelung, duale Parität (häufig als "Erasure Coding" bezeichnet) oder eine Kombination aus beidem verwendet wird.

Die duale Parität bietet die gleiche Fehlertoleranz wie die Drei-Wege-Spiegelung, allerdings mit einer verbesserten Speichereffizienz. Bei vier Servern ist die Speichereffizienz 50,0% – zum Speichern von 2TB an Daten benötigen Sie 4TB physische Kapazität im Speicherpool. Dies erhöht sich bei sieben Servern auf 66,7% Speichereffizienz und kann auf eine Speichereffizienz von 80,0% gesteigert werden. Der Nachteil besteht darin, dass Paritätscodierung rechenintensiver ist, was die Leistung einschränken kann.

![dual-parity](media/plan-volumes/dual-parity.png)

Welcher Resilienztyp verwendet werden sollte, hängt von den Anforderungen Ihrer Workload ab. Hier sehen Sie eine Tabelle, die zusammengefasst, welche Workloads für jeden resilienztyp sowie die Leistung und die Speichereffizienz der einzelnen resilienztypen geeignet sind.

| **Resilienztyp**| **Effizienz der Kapazität**| **Geschwindigkeit**| **Workloads**
|--------------------|--------------------------------|--------------------------------|--------------------------
| **Spiegel**         | ![Speichereffizienz mit 33 %](media\plan-volumes\3-way-mirror-storage-efficiency.png)<br>Drei-Wege-Spiegelung: 33 % <br>Zwei-Wege-Spiegelung: 50 %     |![Leistung mit 100 %](media\plan-volumes\three-way-mirror-perf.png)<br> Höchste Leistung  | Virtualisierte workloads<br> Datenbanken<br>Andere Workloads mit hoher Leistung |
| **Durch Spiegelung beschleunigte Parität** |![Mit etwa 50 % Speichereffizienz](media\plan-volumes\mirror-accelerated-parity-storage-efficiency.png)<br> Richtet sich nach Anteil der Spiegelung und Parität | ![Leistung ca. 20 % anzeigen](media\plan-volumes\mirror-accelerated-parity-perf.png)<br>Deutlich langsamer übereinstimmen, aber oben auf zweimal so schnell wie Dual-Parität<br> Am besten für große sequenzielle Schreibvorgänge und Lesevorgänge | Archivierung und Sicherung<br> Virtualisierten Desktopinfrastruktur     |
| **Dual-Parität**               | ![Mit ca. 80 % Speichereffizienz](media\plan-volumes\dual-parity-storage-efficiency.png)<br>4 Server: 50 % <br>16 Server: bis zu 80 % | ![Leistung ca. 10 % anzeigen](media\plan-volumes\dual-parity-perf.png)<br>Höchste e/a-Latenz und CPU-Auslastung auf Schreibvorgänge<br> Am besten für große sequenzielle Schreibvorgänge und Lesevorgänge | Archivierung und Sicherung<br> Virtualisierten Desktopinfrastruktur  |

#### Wenn Leistung am wichtigsten ist

Workloads, die strikte Latenzanforderungen haben oder viele gemischte zufällige Random-IOPS benötigen, z.B. SQL Server-Datenbanken oder leistungsabhängige virtuelle Hyper-V-Computer, sollten auf Volumes ausgeführt werden, die Spiegelung verwenden, um die Leistung zu maximieren.

   >[!TIP]
   > Die Spiegelung ist schneller als jeder andere Resilienztyp. Wir verwenden die Spiegelung für fast alle unsere Beispiele.

#### Wenn die Kapazität am wichtigsten ist

Workloads, die nur selten schreiben, z.B. Data Warehouses oder "kalte" Speicher, sollten auf Volumes ausgeführt werden, die duale Parität verwenden, um die Speichereffizienz zu maximieren. Bestimmte andere Workloads wie herkömmliche Dateiserver oder virtuelle Desktopinfrastrukturen (VDI), die nicht viel zufälligen E/A-Datenverkehr in schneller Bewegung erstellen und/oder keine optimale Leistung erfordern, können nach Ihrem Ermessen auch duale Parität verwenden. Parität erhöht im Vergleich mit Spiegelung zwangsläufig die CPU-Auslastung und E/A-Latenz, insbesondere bei Schreibvorgängen.

#### Wenn in Massenvorgängen geschrieben werden

Workloads, die in großen, sequenziellen Phasen schreiben, z.B. Archivierungs- oder Sicherungsziele, haben eine weitere Option, die in Windows Server2016 neu ist: ein Volume kann Spiegelung und duale Parität kombinieren. Schreibvorgänge werden zuerst im gespiegelten Bereich platziert und später schrittweise in den Paritätsbereich verschoben. Dies beschleunigt die Erfassung und reduziert die Ressourcenbelegung beim Eingang großer Schreibvorgänge, indem zugelassen wird, dass die rechenintensive Paritätscodierung über einen längeren Zeitraum erfolgt. Berücksichtigen Sie beim Festlegen der Größe der Teile, dass die Menge der gleichzeitigen Schreibvorgänge (z.B. eine tägliche Sicherung) problemlos in den Spiegelungsteil passen sollte. Beispiel: Wenn Sie einmal täglich 100GB erfassen, erwägen Sie die Verwendung von Spiegelung für 150GB bis 200GB und der dualen Parität für den Rest.

Die resultierende Speichereffizienz hängt von den ausgewählten Proportionen ab. In [dieser Demo](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=36m55s) finden Sie einige Beispiele.

   >[!TIP]
   > Wenn Sie einer abrupten Verschlechterung der Leistung der Schreibvorgänge Rechnungszyklus über Daten Injestion beobachten, kann dies bedeuten, dass der Spiegelung Teil nicht groß genug ist, oder durch Spiegelung beschleunigte Parität eignet sich gut für Ihren Zweck nicht. Beispiel: Wenn Leistungseinbußen von 400 MB/s zu 40 MB/s schreiben, sollten Sie den Teil Spiegelung erweitern oder wechseln Sie zu drei-Wege-Spiegelung.

### Informationen zu Bereitstellungen mit NVMe, SSD und HDD

Bei Bereitstellungen mit zwei Arten von Laufwerken bieten die schnellere Laufwerke Zwischenspeicherung, während die langsameren Laufwerke Kapazität bieten. Dies geschieht automatisch – weitere Informationen finden Sie unter [Grundlegendes zum Cache in Direkte Speicherplätze](understand-the-cache.md). In solchen Bereitstellungen befinden sich alle Datenträger letztendlich auf der gleichen Art von Laufwerken – den Kapazitätslaufwerken.

Bei Bereitstellungen mit allen drei Arten von Laufwerken bieten nur die schnellsten Laufwerke (NVMe) Zwischenspeicherung, die zwei verbleibenden Laufwerkarten (SSD und HDD) stellen die Kapazität bereit. Für jedes Volume können Sie auswählen, ob es sich vollständig auf SSD-Ebene, vollständig auf der HDD-Ebene befindet oder sich über beide erstreckt.

   >[!IMPORTANT]
   > Wir empfehlen die Verwendung der SSD-Ebene, um für Ihre leistungsabhängigsten Workloads eine reine Flash-Bereitstellung zu nutzen.

## Auswählen der Volumegröße

Es wird empfohlen, die Größe der einzelnen Volumes zu beschränken:

| Windows Server 2016 | Windows Server 2019 |
|---------------------|---------------------|
| Bis zu 32 TB         | Bis zu 64 TB         |

   >[!TIP]
   > Wenn Sie eine Sicherungslösung verwenden, die auf dem Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) und dem Softwareanbieter Volsnap basiert – wie es für Dateiserver-Workloads üblich ist – verbessert das Beschränken die Volumegröße 10TB die Leistung und Zuverlässigkeit. Sicherungslösungen, die die neuere Hyper-V RCT-API und/oder Block-Clone-Vorgänge auf ReFS und/oder die systemeigenen SQL-Sicherungs-APIs verwenden, bieten bei einer Größe von bis zu 32 TB und mehr eine gute Leistung.

### Speicherbedarf

Die Größe eines Volumes bezieht sich auf die nutzbare Kapazität, d. h. die Menge an Daten, die es speichern kann. Diese Information wird vom Parameter **-Size** des Cmdlets **New-Volume** bereitgestellt und dann in der Eigenschaft **Größe** angezeigt, wenn Sie das Cmdlet **Get-Volume** ausführen.

Die Größe unterscheidet sich vom *Speicherbedarf* des Volumes, der gesamten physischen Speicherkapazität, die es im Speicherpool belegt. Der Speicherbedarf hängt vom Resilienztyp ab. Beispiel: Der Speicherbedarf von Volumes, die Dreiwegespiegelung verwenden, ist das Dreifache ihrer Größe.

Der Speicherbedarf Ihrer Volumes muss vom Speicherpool erfüllt werden können.

![size-versus-footprint](media/plan-volumes/size-versus-footprint.png)

### Reservekapazität

Wenn etwas Kapazität im Speicherpool nicht zugeteilt wird, haben Volumes genügend Speicherplatz für "direktes" Reparieren, nachdem Laufwerke ausgefallen sind. Dies verbessert die Datensicherheit und Leistung. Wenn ausreichend Kapazität vorhanden ist, kann eine sofortige, direkte, parallele Reparatur die vollständige Resilienz von Volumes wiederherstellen, noch bevor die ausgefallenen Laufwerke ersetzt werden. Dies erfolgt automatisch.

Es wird empfohlen, das Äquivalent eines Kapazitätslaufwerks pro Server auf bis zu 4 Laufwerken zu reservieren. Sie können nach eigenem Ermessen mehr reservieren, aber dieses empfohlene Minimum gewährleistet, dass eine sofortige, direkte, parallele Reparatur nach dem Ausfall eines beliebigen Laufwerks erfolgreich ist.

![Reservieren](media/plan-volumes/reserve.png)

Beispiel: Wenn Sie 2 Server haben und Kapazitätslaufwerke mit 1TB verwenden, reservieren Sie 2 x 1 = 2 TB des Pools. Wenn Sie 3 Server haben und Kapazitätslaufwerke mit 1TB verwenden, reservieren Sie 3 x 1 = 3 TB. Wenn Sie 4 oder mehr Server haben und Kapazitätslaufwerke mit 1TB verwenden, reservieren Sie 4 x 1 = 4 TB.

   >[!NOTE]
   > Bei Clustern mit Laufwerken aller drei Arten (NVMe + SSD + HDD) wird empfohlen, das Äquivalent einer SSD plus einer HDD pro Server, jeweils bis zu 4 Laufwerke, zu reservieren.

## Beispiel: Kapazitätsplanung

Gehen Sie von einem Vier-Server-Cluster aus. Jeder Server verfügt über einige Cachelaufwerke plus sechzehn 2-TB-Laufwerke für Kapazität.

```
4 servers x 16 drives each x 2 TB each = 128 TB
```

Von diesen 128TB im Speicherpool reservieren wir vier Laufwerke oder 8 TB, sodass direkte Reparaturen ausgeführt werden können und beim Ersetzen ausgefallener Laufwerke keine Eile besteht. Dadurch verbleiben 120 TB physische Speicherkapazität im Pool, mit der wir Volumes erstellen können.

```
128 TB – (4 x 2 TB) = 120 TB
```

Angenommen, unsere Bereitstellung muss einige sehr aktive virtuelle Hyper-V-Computer hosten, aber wir haben auch viel kalten Speicher – alte Dateien und Sicherungen müssen wir behalten. Da wir vier Server haben, erstellen wir vier Volumes.

Wir platzieren die virtuellen Computer in die ersten beiden Volumes, *Volume1* und *Volume2*. Wir wählen ReFS als Dateisystem (für die schnellere Erstellung und Prüfpunkte) und Dreiwegespiegelung für Resilienz, um die Leistung zu maximieren. Den kalten Speicher platzieren wir in den anderen zwei Volumes *Volume 3* und *Volume 4*. Wir wählen NTFS als Dateisystem (für Datendeduplizierung) und duale Parität für Resilienz, um die Leistung zu maximieren.

Es ist nicht erforderlich, dass wir alle Datenträger gleich groß machen, aber der Einfachheit halber machen wir es – beispielsweise können wie für alle eine Größe von 12 TB festlegen.

*Volume1* und *Volume2* belegen jeweils 12 TB x 33,3% Effizienz = 36 TB physische Speicherkapazität.

*Volume3* und *Volume4* belegen jeweils 12 TB x 50,0% Effizienz = 24 TB physische Speicherkapazität.

```
36 TB + 36 TB + 24 TB + 24 TB = 120 TB
```

Die vier Volumes passen genau für die in unserem Pool verfügbare physische Speicherkapazität. Perfekt!

![Beispiel](media/plan-volumes/example.png)

   >[!TIP]
   > Sie müssen nicht alle Volumes sofort erstellen. Sie können jederzeit Volumes erweitern oder später neue Volumes erstellen.

Der Einfachheit halber werden in diesem Beispiel durchgehend Dezimaleinheiten (Basis 10) verwendet, d.h. 1 TB = 1,000,000,000,000 Bytes. Speichermengen in Windows werden jedoch in Binäreinheiten (Basis 2) angezeigt. Beispiel: Alle 2-TB-Laufwerke werden in Windows als 1,82 TiB angezeigt. Ebenso wird der 128-TB-Speicherpool als 116.41 TiB angezeigt. Dies ist so vorgesehen.

## Nutzung

Siehe [Erstellen von Volumes in Direkte Speicherplätze](create-volumes.md).

### Weitere Informationen

- [Direkte Speicherplätze – Übersicht](storage-spaces-direct-overview.md)
- [Auswählen von Laufwerken für Direkte Speicherplätze](choosing-drives.md)
- [Fehlertoleranz und Speichereffizienz](storage-spaces-fault-tolerance.md)
