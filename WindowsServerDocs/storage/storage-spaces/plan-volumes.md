---
ms.assetid: 342173ca-4e10-44f4-b2c9-02a6c26f7a4a
title: Planen von Volumes in direkte Speicherplätze
ms.prod: windows-server
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 06/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: d5c45b68f18fe3126867a9b6608b0911bb3f63b2
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474757"
---
# <a name="planning-volumes-in-storage-spaces-direct"></a>Planen von Volumes in direkte Speicherplätze

> Gilt für: Windows Server 2019, Windows Server 2016

Dieses Thema enthält Anleitungen zum Planen von Volumes in direkte Speicherplätze, um die Leistungs-und Kapazitätsanforderungen ihrer Arbeits Auslastungen zu erfüllen, einschließlich der Auswahl des Dateisystems, des resilienztyps und der Größe.

## <a name="review-what-are-volumes"></a>Review: Was sind Volumes?

In Volumes platzieren Sie die Dateien, die ihre Workloads benötigen, z. b. VHD-oder vhdx-Dateien für virtuelle Hyper-V-Computer. Für Volumes werden die Laufwerke im Speicherpool kombiniert, um die Fehlertoleranz, Skalierbarkeit und Leistungsvorteile von „Direkte Speicherplätze“ zu erhalten.

   >[!NOTE]
   > In der Dokumentation für direkte Speicherplätze wird der Begriff "Volume" verwendet, um gemeinsam auf das Volume und den virtuellen Datenträger zu verweisen, einschließlich der Funktionen, die von anderen integrierten Windows-Features wie freigegebenen Clustervolumes (CSV) und Refs bereitgestellt werden. Das Verständnis dieser Unterschiede in der Implementierungs Ebene ist nicht erforderlich, um direkte Speicherplätze erfolgreich zu planen und bereitzustellen.

![Was sind Volumes?](media/plan-volumes/what-are-volumes.png)

Alle Server im Cluster können gleichzeitig auf alle Volumes zugreifen. Nach der Erstellung werden Sie auf allen Servern unter " **c:\ClusterStorage \\ ** " angezeigt.

![CSV-Folder-Bildschirmfoto](media/plan-volumes/csv-folder-screenshot.png)

## <a name="choosing-how-many-volumes-to-create"></a>Auswählen, wie viele Volumes erstellt werden sollen

Es wird empfohlen, die Anzahl der Volumes um ein Vielfaches der Anzahl der Server in Ihrem Cluster zu übernehmen. Wenn Sie z. b. über vier Server verfügen, kommt es zu einer konsistenten Leistung mit vier Gesamt Volumes als 3 oder 5. Dadurch kann der Cluster das Volume "Ownership" verteilen (ein Server verarbeitet die metadatenorchestrierung für jedes Volume) gleichmäßig zwischen den Servern.

Es wird empfohlen, die Gesamtanzahl der Volumes auf Folgendes zu beschränken:

| Windows Server 2016          | Windows Server 2019          |
|------------------------------|------------------------------|
| Bis zu 32 Volumes pro Cluster | Bis zu 64 Volumes pro Cluster |

## <a name="choosing-the-filesystem"></a>Auswählen des Dateisystems

Wir empfehlen die Verwendung des neuen [robusten Dateisystems (Refs)](../refs/refs-overview.md) für direkte Speicherplätze. Refs ist das wichtigste Dateisystem, das für die Virtualisierung entwickelt wurde und viele Vorteile bietet, einschließlich dramatischer Leistungs Beschleunigung und integrierter Schutz vor Daten Beschädigung. Es unterstützt fast alle wichtigen NTFS-Features, einschließlich der Datendeduplizierung in Windows Server, Version 1709 und höher. Weitere Informationen finden Sie in der [Vergleichstabelle](../refs/refs-overview.md#feature-comparison) zu Refs-Features.

Wenn für ihre Arbeitsauslastung ein Feature erforderlich ist, das von refs noch nicht unterstützt wird, können Sie stattdessen NTFS verwenden.

   > [!TIP]
   > Volumes mit unterschiedlichen Dateisystemen können im gleichen Cluster nebeneinander vorhanden sein.

## <a name="choosing-the-resiliency-type"></a>Auswählen des resilienztyps

Volumes unter „Direkte Speicherplätze“ bieten Resilienz als Schutz vor Hardwareproblemen, z. B. Laufwerks- oder Serverfehler, und ermöglichen eine ununterbrochene Verfügbarkeit bei der Serverwartung, z. B. Softwareupdates.

   > [!NOTE]
   > Welche resilienztypen Sie auswählen können, ist unabhängig davon, welche Arten von Laufwerken Sie haben.

### <a name="with-two-servers"></a>Mit zwei Servern

Mit zwei Servern im Cluster können Sie die bidirektionale Spiegelung verwenden. Wenn Sie Windows Server 2019 ausführen, können Sie auch die Möglichkeit zur Ausfallsicherheit verwenden.

Die bidirektionale Spiegelung speichert zwei Kopien aller Daten, eine Kopie auf den Laufwerken auf den einzelnen Servern. Die Speichereffizienz beträgt 50% – um 1 TB Daten zu schreiben, benötigen Sie mindestens 2 TB physische Speicherkapazität im Speicherpool. Die bidirektionale Spiegelung kann einen Hardwarefehler auf sichere Weise tolerieren (ein Server oder Laufwerk).

![Zwei-Wege-Spiegelung](media/plan-volumes/two-way-mirror.png)

Geschachtelte Resilienz (nur unter Windows Server 2019 verfügbar) bietet datenresilienz zwischen Servern mit bidirektionaler Spiegelung und erhöht dann die Resilienz innerhalb eines Servers mit bidirektionaler Spiegelung oder einer Spiegel beschleunigten Parität. Die Schachtelung bietet Daten Resilienz, selbst wenn ein Server neu gestartet oder nicht verfügbar ist. Die Speichereffizienz beträgt 25% mit einer gedugten bidirektionalen Spiegelung und ca. 35-40% für eine gespiegelte, in der Spiegelung beschleunigte Parität. Die geschlagene Resilienz kann zwei Hardwarefehler auf sichere Weise tolerieren (zwei Laufwerke oder ein Server und ein Laufwerk auf dem verbleibenden Server). Aufgrund dieser zusätzlichen Daten Resilienz wird empfohlen, dass Sie bei der Bereitstellung von zwei Servern, wenn Sie Windows Server 2019 ausführen, die Sicherheit bei der Bereitstellung von Daten in der Produktionsumgebung in der Produktionsumgebung verwenden. Weitere Informationen finden Sie unter in der [nsted Resilienz](nested-resiliency.md).

![Gespiegelte gespiegelte Spiegelung](media/nested-resiliency/nested-mirror-accelerated-parity.png)

### <a name="with-three-servers"></a>Mit drei Servern

Mit drei Servern sollten Sie eine drei-Wege-Spiegelung verwenden, um die Fehlertoleranz und die Leistung zu verbessern. Die drei-Wege-Spiegelung speichert drei Kopien aller Daten, eine Kopie auf den Laufwerken auf den einzelnen Servern. Die Speichereffizienz beträgt 33,3% – um 1 TB Daten zu schreiben, benötigen Sie im Speicherpool mindestens 3 TB physischer Speicherkapazität. Die drei-Wege-Spiegelung kann [jeweils mindestens zwei Hardwareprobleme (Laufwerk oder Server)](storage-spaces-fault-tolerance.md#examples)sicher tolerieren. Wenn zwei Knoten nicht mehr verfügbar sind, verliert der Speicherpool das Quorum, da 2/3 der Datenträger nicht verfügbar sind und die virtuellen Datenträger nicht zugänglich sind. Ein Knoten kann jedoch Herunterfahren, und ein oder mehrere Datenträger auf einem anderen Knoten können fehlschlagen, und die virtuellen Datenträger bleiben online. Wenn Sie beispielsweise einen Server neu starten und plötzlich ein anderes Laufwerk bzw. ein Server ausfällt, bleiben alle Daten geschützt und sind ohne Unterbrechung zugänglich.

![Drei-Wege-Spiegelung](media/plan-volumes/three-way-mirror.png)

### <a name="with-four-or-more-servers"></a>Mit vier oder mehr Servern

Mit vier oder mehr Servern können Sie für jedes Volume auswählen, ob die drei-Wege-Spiegelung, die duale Parität (häufig "Lösch Programmierung" genannt) verwendet werden soll, oder Sie können die beiden mit der Spiegel beschleunigten Parität vermischen.

Die duale Parität bietet die gleiche Fehlertoleranz wie die drei-Wege-Spiegelung, aber mit besserer Speichereffizienz. Bei vier Servern beträgt die Speichereffizienz von 50,0% – um 2 TB Daten speichern zu können, benötigen Sie 4 TB physische Speicherkapazität im Speicherpool. Dies erhöht die Speichereffizienz von 66,7% mit sieben Servern und setzt bis zu 80,0% Speichereffizienz fort. Der Kompromiss besteht darin, dass die Parität-Codierung Rechen intensiver ist, was die Leistung begrenzen kann.

![dual-parity](media/plan-volumes/dual-parity.png)

Welcher resilienztyp zu verwenden ist, hängt von den Anforderungen der Arbeitsauslastung ab. Im folgenden finden Sie eine Tabelle, in der zusammengefasst ist, welche Arbeits Auslastungen für die einzelnen resilienztypen geeignet sind, sowie die Leistung und Speichereffizienz jedes resilienztyps.

| Resilienztyp | Kapazitäts Effizienz | Geschwindigkeit | Arbeitsauslastungen |
| ------------------- | ----------------------  | --------- | ------------- |
| **Spiegel**         | ![Speichereffizienz, die 33% anzeigt](media/plan-volumes/3-way-mirror-storage-efficiency.png)<br>Drei-Wege-Spiegelung: 33% <br>Zwei-Wege-Spiegelung: 50%     |![Leistungsanzeige 100%](media/plan-volumes/three-way-mirror-perf.png)<br> Höchste Leistung  | Virtualisierte Arbeits Auslastungen<br> Datenbanken<br>Andere hochleistungsfähige Workloads |
| **Durch Spiegelung beschleunigte Parität** |![Speichereffizienz mit ungefähr 50%](media/plan-volumes/mirror-accelerated-parity-storage-efficiency.png)<br> Hängt von einem Anteil von Spiegelung und Parität ab | ![Leistungsanzeige ungefähr 20%](media/plan-volumes/mirror-accelerated-parity-perf.png)<br>Viel langsamer als die Spiegelung, aber bis zu doppelt so schnell wie die duale Parität<br> Beste für große sequenzielle Schreib-und Lesevorgänge | Archivierung und Sicherung<br> Virtualisierte Desktop Infrastruktur     |
| **Duale Parität**               | ![Speichereffizienz mit ungefähr 80%](media/plan-volumes/dual-parity-storage-efficiency.png)<br>4 Server: 50% <br>16 Server: bis zu 80% | ![Leistungsanzeige ungefähr 10%](media/plan-volumes/dual-parity-perf.png)<br>Höchste e/a-Latenz & CPU-Auslastung bei Schreibvorgängen<br> Beste für große sequenzielle Schreib-und Lesevorgänge | Archivierung und Sicherung<br> Virtualisierte Desktop Infrastruktur  |

#### <a name="when-performance-matters-most"></a>Wenn die Leistung am meisten liegt

Workloads, die strenge Latenz Anforderungen aufweisen oder viele gemischte, zufällige IOPS benötigen, wie z. b. SQL Server-Datenbanken oder Leistungs relevante virtuelle Hyper-V-Computer, sollten auf Volumes ausgeführt werden, die die-Spiegelung zum Maximieren der Leistung verwenden.

   >[!TIP]
   > Die Spiegelung ist schneller als jeder andere Resilienztyp. Wir verwenden die Spiegelung für fast alle Leistungs Beispiele.

#### <a name="when-capacity-matters-most"></a>Wenn die Kapazität die größte Rolle spielt

Workloads, die selten schreiben, z. b. Data Warehouse-Daten oder "kalte" Speicher, sollten auf Volumes ausgeführt werden, die duale Parität verwenden, um die Speichereffizienz zu maximieren. Bestimmte andere Workloads, z. b. herkömmliche Dateiserver, virtuelle Desktop Infrastruktur (VDI) oder andere, die keinen großen schnellen drifteten e/a-Datenverkehr erstellen und/oder nicht die beste Leistung erfordern, können nach eigenem Ermessen auch duale Parität verwenden. Die Parität erhöht die CPU-Auslastung und die e/a-Latenz, insbesondere bei Schreibvorgängen, im Vergleich zur

#### <a name="when-data-is-written-in-bulk"></a>Wenn Daten in einem Massen Vorgang geschrieben werden

Workloads, die in großen, sequenziellen Durchläufen schreiben, wie z. b. Archivierungs-oder Sicherungs Ziele, haben eine weitere Option, die in Windows Server 2016 neu ist: ein Volume kann Spiegelung und duale Parität kombinieren Schreibt das Land zuerst in den gespiegelten Teil und wird später allmählich in den Paritäts Teil verschoben. Dadurch wird die Erfassung beschleunigt, und die Ressourcennutzung wird reduziert, wenn umfangreiche Schreibvorgänge eintreffen, indem die rechenintensive Paritäts Codierung über einen längeren Zeitraum ausgeführt wird. Berücksichtigen Sie bei der Größenanpassung der Teile, dass die Menge der Schreibvorgänge, die gleichzeitig ausgeführt werden (z. b. eine tägliche Sicherung), in den Spiegel Teil passt. Wenn Sie z. b. 100 GB einmal täglich erfassen, sollten Sie die Verwendung von Spiegelung für 150 GB bis 200 GB und die duale Parität für den Rest in Erwägung gezogen.

Die resultierende Speichereffizienz hängt von den Proportionen ab, die Sie auswählen. In [dieser Demo](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=36m55s) finden Sie einige Beispiele.

   > [!TIP]
   > Wenn Sie eine abrupte Abnahme der Schreibleistung bei der Datenerfassung beobachten, kann dies darauf hindeuten, dass der Spiegelungs Bereich nicht groß genug ist oder dass die Spiegelungs beschleunigte Parität für Ihren Anwendungsfall nicht gut geeignet ist. Wenn z. b. die Schreibleistung von 400 MB/s auf 40 MB/s sinkt, sollten Sie den Spiegel Teil erweitern oder zu einer drei-Wege-Spiegelung wechseln.

### <a name="about-deployments-with-nvme-ssd-and-hdd"></a>Informationen zu bereit Stellungen mit nvme, SSD und HDD

Bei bereit Stellungen mit zwei Arten von Laufwerken ermöglichen die schnelleren Laufwerke das Zwischenspeichern, während die langsameren Laufwerke Kapazität bereitstellen. Dies geschieht automatisch – weitere Informationen finden Sie Untergrund Legendes [zum Cache in direkte Speicherplätze](understand-the-cache.md). In solchen bereit Stellungen befinden sich alle Volumes letztendlich auf demselben Lauftyp – die Kapazitäts Laufwerke.

In bereit Stellungen mit allen drei Laufwerkstypen bieten nur die schnellsten Laufwerke (nvme) Zwischenspeicherung, sodass zwei Arten von Laufwerken (SSD und HDD) die Kapazität bereitstellen. Sie können für jedes Volume auswählen, ob es sich vollständig auf der SSD-Ebene befindet, vollständig auf der HDD-Ebene, oder ob es sich um die beiden Volumes handelt.

   > [!IMPORTANT]
   > Es wird empfohlen, die SSD-Ebene zu verwenden, um die Leistungs sensitiven Workloads bei allen Flash-Vorgängen zu platzieren.

## <a name="choosing-the-size-of-volumes"></a>Auswählen der Größe von Volumes

Es wird empfohlen, die Größe der einzelnen Volumes auf Folgendes zu beschränken:

| Windows Server 2016 | Windows Server 2019 |
| ------------------- | ------------------- |
| Bis zu 32 TB         | Bis zu 64 TB         |

   > [!TIP]
   > Wenn Sie eine Sicherungs Lösung verwenden, die auf dem Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) und dem Volsnap-Softwareanbieter basiert – wie bei Dateiserver-Arbeits Auslastungen üblich – wird die Leistung und Zuverlässigkeit durch die Beschränkung der Volumegröße auf 10 Sicherungslösungen, die die neuere Hyper-V-RCT-API und/oder das Klonen von refs-Blöcken und/oder die nativen SQL-Sicherungs-APIs verwenden, können bis zu 32 TB und darüber hinaus ausführen.

### <a name="footprint"></a>Bruch

Die Größe eines Volumes bezieht sich auf seine nutzbare Kapazität, die Menge der Daten, die gespeichert werden können. Dies wird durch den **-size-** Parameter des Cmdlets **New-Volume** bereitgestellt und dann in der **size** -Eigenschaft angezeigt, wenn Sie das **Get-Volume** -Cmdlet ausführen.

Die Größe unterscheidet sich vom Speicher *Bedarf*des Volumes, der gesamten physischen Speicherkapazität, die für den Speicherpool belegt ist. Der Speicherbedarf hängt vom resilienztyp ab. Beispielsweise verfügen Volumes, die die drei-Wege-Spiegelung verwenden, über einen dreidimensionalen Speicherbedarf.

Die Spuren Ihrer Volumes müssen in den Speicherpool passen.

![Größe und Speicherbedarf](media/plan-volumes/size-versus-footprint.png)

### <a name="reserve-capacity"></a>Kapazität reservieren

Wenn Sie einige Kapazität im Speicherpool nicht zuordnen lassen, werden Volumes Speicherplatz zur Reparatur von "direkt" nach einem Ausfall der Laufwerke bereitgestellt, wodurch die Datensicherheit und die Leistung verbessert werden. Wenn ausreichend Kapazität vorhanden ist, kann eine sofortige, direkte und parallele Reparatur Volumes wieder in vollständiger Resilienz wiederherstellen, auch wenn die fehlerhaften Laufwerke ersetzt wurden. Dies geschieht automatisch.

Es wird empfohlen, das Äquivalent eines Kapazitäts Laufwerks pro Server und bis zu 4 Laufwerken zu reservieren. Sie können sich nach eigenem Ermessen besser reservieren, aber durch diese minimale Empfehlung wird gewährleistet, dass eine sofortige, direkte und parallele Reparatur nach dem Ausfall eines beliebigen Laufwerks erfolgreich durchgeführt werden kann.

![reserve](media/plan-volumes/reserve.png)

Wenn Sie z. b. über zwei Server verfügen und 1 TB Kapazitäts Laufwerke verwenden, legen Sie 2 x 1 = 2 TB des Pools als Reserve fest. Wenn Sie über drei Server und 1 TB Kapazitäts Laufwerke verfügen, legen Sie 3 x 1 = 3 TB als Reserve fest. Wenn Sie über vier oder mehr Server und Kapazitäts Laufwerke von 1 TB verfügen, legen Sie 4 x 1 = 4 TB als Reserve fest.

   >[!NOTE]
   > In Clustern mit Laufwerken aller drei Typen (nvme + SSD + HDD) empfiehlt es sich, das Äquivalent von einem SSD plus einer HDD pro Server, jeweils bis zu 4 Laufwerke, zu reservieren.

## <a name="example-capacity-planning"></a>Beispiel: Kapazitätsplanung

Beachten Sie 1 4-Server Cluster. Jeder Server verfügt über einige Cache Laufwerke Plus sechzehn 2-TB-Laufwerke für die Kapazität.

```
4 servers x 16 drives each x 2 TB each = 128 TB
```

Aus diesen 128 TB im Speicherpool haben wir vier Laufwerke oder 8 TB eingestellt, sodass direkte Reparaturen erfolgen können, ohne dass die Laufwerke nach einem Ausfall ersetzt werden müssen. Dadurch bleiben in dem Pool, mit dem wir Volumes erstellen können, 120 TB physische Speicherkapazität erhalten.

```
128 TB – (4 x 2 TB) = 120 TB
```

Angenommen, wir benötigen unsere Bereitstellung, um einige hochaktive virtuelle Hyper-V-Computer zu hosten, aber wir verfügen auch über viele Cold Storage – alte Dateien und Sicherungen, die wir beibehalten müssen. Da wir vier Server haben, erstellen wir vier Volumes.

Fügen wir die virtuellen Computer auf die ersten beiden Volumes ein, *volume1* und *Volume2*. Wir wählen Refs als Dateisystem (für schnellere Erstellung und Prüfpunkte) und drei-Wege-Spiegelung für Resilienz, um die Leistung zu maximieren. Wir legen die Cold Storage auf den anderen beiden Volumes, *Volume 3* und *Volume 4*, ab. Wir wählen NTFS als Dateisystem (für die Datendeduplizierung) und duale Parität für Resilienz, um die Kapazität zu maximieren.

Es ist nicht erforderlich, dass alle Volumes die gleiche Größe haben, aber aus Gründen der Einfachheit ist es – beispielsweise, dass Sie alle 12 TB erreichen können.

*Volume1* und *Volume2* belegen jeweils 12 TB x 33,3% Effizienz = 36 TB physischer Speicherkapazität.

*Volume3* und *Volume4* belegen jeweils 12 TB x 50,0% Effizienz = 24 TB physischer Speicherkapazität.

```
36 TB + 36 TB + 24 TB + 24 TB = 120 TB
```

Die vier Volumes passen genau auf die physische Speicherkapazität, die in unserem Pool verfügbar ist. Ragend!

![Beispiel](media/plan-volumes/example.png)

   >[!TIP]
   > Sie müssen nicht alle Volumes sofort erstellen. Sie können Volumes jederzeit erweitern oder später neue Volumes erstellen.

Der Einfachheit halber werden in diesem Beispiel dezimale (Basis 10) Einheiten verwendet, d. h. 1 TB = 1 Billion Bytes. Allerdings werden Speichermengen in Windows in binären Einheiten (Basis 2) angezeigt. Beispielsweise würde jedes Laufwerk mit 2 TB in Windows als 1,82 tib angezeigt werden. Ebenso wird der Speicherpool mit 128 TB als 116,41 tib angezeigt. Dies entspricht dem erwarteten Verhalten.

## <a name="usage"></a>Zweck

Siehe [Erstellen von Volumes in direkte Speicherplätze](create-volumes.md).

### <a name="additional-references"></a>Zusätzliche Referenzen

- [Übersicht über direkte Speicherplätze](storage-spaces-direct-overview.md)
- [Auswählen von Laufwerken für direkte Speicherplätze](choosing-drives.md)
- [Fehlertoleranz und Speichereffizienz](storage-spaces-fault-tolerance.md)
