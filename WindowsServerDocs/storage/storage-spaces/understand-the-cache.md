---
title: Grundlegendes zum Cache in direkten Speicherplätzen
ms.assetid: 69b1adc0-ee64-4eed-9732-0fb216777992
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 07/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0050a8931162e37408895ef664293be2349d1bde
ms.sourcegitcommit: 1bc3c229e9688ac741838005ec4b88e8f9533e8a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68314999"
---
# <a name="understanding-the-cache-in-storage-spaces-direct"></a>Grundlegendes zum Cache in direkten Speicherplätzen

>Gilt für: Windows Server 2019, Windows Server 2016

[Direkte Speicherplätze](storage-spaces-direct-overview.md) verfügt über einen integrierten serverseitigen Cache zum Steigern der Speicherleistung. Es handelt sich um einen großen, persistenten Echtzeit-Cache für Lese- *und* Schreibvorgänge. Der Cache wird automatisch konfiguriert, wenn „Direkte Speicherplätze“ aktiviert wird. In den meisten Fällen sind keine manuellen Verwaltungsschritte erforderlich.
Die Funktionsweise des Caches richtet sich nach den vorhandenen Laufwerktypen.

Das folgende Video zeigt im Detail die Funktionsweise des Zwischenspeicherns für direkte Speicherplätze sowie andere Entwurfsüberlegungen.

<strong>Überlegungen zum direkte Speicherplätze Entwurf</strong><br>(20 Minuten)<br>
<iframe src="https://channel9.msdn.com/Blogs/windowsserver/Design-Considerations-for-Storage-Spaces-Direct/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

## <a name="drive-types-and-deployment-options"></a>Laufwerktypen und Bereitstellungsoptionen

Direkte Speicherplätze funktionieren derzeit mit drei Arten von Speichergeräten:

<table>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/NVMe-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            NVMe (Non-Volatile Memory Express) – nicht flüchtiger Express-Speicher
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/SSD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            SATA/SAS SSD (Solid-State Drive) – Festkörperlaufwerk
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/HDD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            HDD (Hard Disk Drive) – Festplattenlaufwerk
        </td>
    </tr>
</table>

Diese Komponenten können auf sechs verschiedene Arten kombiniert werden, die wir in zwei Kategorien unterteilen: „reine Flash-Bereitstellung“ und „Hybridbereitstellung“.

### <a name="all-flash-deployment-possibilities"></a>Möglichkeiten bei der reinen Flash-Bereitstellung

Das Ziel bei reinen Flash-Bereitstellungen besteht darin, die Speicherleistung zu steigern und keine Festplatten (HDDs) mit rotierenden Speichermedien zu verwenden.

![All-Flash-Deployment-Possibilities](media/understand-the-cache/All-Flash-Deployment-Possibilities.png)

### <a name="hybrid-deployment-possibilities"></a>Möglichkeiten der Hybridbereitstellung

Bei Hybridbereitstellungen besteht das Ziel darin, eine gute Balance zwischen Leistung und Kapazität zu erzielen oder die Kapazität zu erhöhen und Festplatten (HDDs) mit rotierenden Speichermedien einzubinden.

![Hybrid-Deployment-Possibilities](media/understand-the-cache/Hybrid-Deployment-Possibilities.png)

## <a name="cache-drives-are-selected-automatically"></a>Automatische Auswahl von Cachelaufwerken

Bei Bereitstellungen mit mehreren Arten von Laufwerken werden für „Direkte Speicherplätze“ automatisch alle schnellsten Laufwerke für die Zwischenspeicherung verwendet. Die restlichen Laufwerke werden für Kapazitätszwecke genutzt.

Welche Art von Laufwerk am „schnellsten“ ist, wird anhand der folgenden Hierarchie ermittelt.

![Drive-Type-Hierarchy](media/understand-the-cache/Drive-Type-Hierarchy.png)

Wenn Sie beispielsweise über NVMe und SSDs verfügen, fungiert NVMe als Cache für die SSDs.

Wenn Sie SSDs und HDDs verwenden, dienen die SSDs als Cache für die HDDs.

   >[!NOTE]
   > Cachelaufwerke leisten keinen Beitrag zur nutzbaren Speicherkapazität. Alle im Cache gespeicherten Daten werden auch an einem anderen Ort gespeichert (spätestens nach Aufhebung der Bereitstellung). Dies bedeutet, dass die gesamte reine Speicherkapazität Ihrer Bereitstellung nur die Summe Ihrer Kapazitätslaufwerke ist.

Wenn alle Laufwerke den gleichen Typ haben, wird nicht automatisch ein Cache konfiguriert. Sie können manuell konfigurieren, dass Laufwerke mit höherer Belastbarkeit als Cache für Laufwerke desselben Typs dienen, die für geringere Belastungen ausgelegt sind. Informationen hierzu finden Sie im Abschnitt [Manuelle Konfiguration](#manual-configuration).

   >[!TIP]
   > Bei reinen NVMe- oder SSD-Bereitstellungen (vor allem in kleinerem Umfang) kann die Speichereffizienz deutlich verbessert werden, wenn keine Laufwerke für den Cache reserviert werden.

## <a name="cache-behavior-is-set-automatically"></a>Automatisches Festlegen des Cacheverhaltens

Das Verhalten des Caches wird automatisch anhand der Typen von Laufwerken bestimmt, für die die Zwischenspeicherung durchgeführt wird. Bei der Zwischenspeicherung für Festkörperlaufwerke (z. B. NVMe als Cache für SSDs) werden nur Schreibvorgänge zwischengespeichert. Beim Zwischenspeichern für Festplattenlaufwerke (z. B. SSDs als Cache für HDDs) werden sowohl Lese- als auch Schreibvorgänge zwischengespeichert.

![Cache-Read-Write-Behavior](media/understand-the-cache/Cache-Read-Write-Behavior.png)

### <a name="write-only-caching-for-all-flash-deployments"></a>Ausschließliche Zwischenspeicherung von Schreibvorgängen für reine Flash-Bereitstellungen

Beim Zwischenspeichern für Festkörperlaufwerke (NVMe oder SSDs) werden nur Schreibvorgänge zwischengespeichert. Hierdurch wird die Belastung von Kapazitätslaufwerken reduziert, weil viele Schreibvorgänge und erneute Schreibvorgänge im Cache zusammengefügt werden können und die Aufhebung der Bereitstellung nur bei Bedarf durchgeführt wird. So wird der Gesamtdatenverkehr für die Kapazitätslaufwerke verringert und deren Lebensdauer erhöht. Aus diesem Grund empfehlen wir die Verwendung von Laufwerken, [die für höhere Belastung ausgelegt und für Schreibvorgänge optimiert sind](http://whatis.techtarget.com/definition/DWPD-device-drive-writes-per-day), als Cache. Als Kapazitätslaufwerke können Laufwerke genutzt werden, die für geringere Belastungen ausgelegt sind.

Da Lesevorgänge keine signifikante Auswirkung auf die Flash-Lebensdauer haben und Festkörperlaufwerke eine niedrige Leselatenz haben, werden Lesevorgänge nicht zwischengespeichert. Diese Daten werden direkt von den Kapazitätslaufwerken bereitgestellt (es sei denn, die Daten wurden erst vor so kurzer Zeit geschrieben, dass die Bereitstellung noch nicht aufgehoben wurde). So kann der Cache vollständig für Schreibvorgänge genutzt werden, um seine Effektivität zu erhöhen.

Dies führt dazu, dass Merkmale von Schreibvorgängen, z. B. die Schreiblatenz, von den Cachelaufwerken diktiert werden, während die Merkmale von Lesevorgängen von den Kapazitätslaufwerken vorgegeben werden. Beide sind konsistent, vorhersehbar und einheitlich.

### <a name="readwrite-caching-for-hybrid-deployments"></a>Zwischenspeichern von Lese-/Schreibvorgängen für Hybridbereitstellungen

Beim Zwischenspeichern für Festplattenlaufwerke (HDDs) werden sowohl Lese- *als auch* Schreibvorgänge zwischengespeichert, um für beide Vorgänge eine Latenz wie bei Flash zu erzielen (häufig um den Faktor 10 schneller). Im Lesecache werden kürzlich und häufig gelesene Daten zwischengespeichert, um den schnellen Zugriff zu ermöglichen und zufälligen Datenverkehr für die HDDs zu verringern. (Aufgrund von Such-und Rotations Verzögerungen ist die Latenz und die verlorene Zeit, die durch den zufälligen Zugriff auf eine HDD entstehen, von großer Bedeutung.) Schreibvorgänge werden zwischengespeichert, um Spitzen zu absorbieren, und, wie zuvor, die zusammen Fügung von Schreib-und Schreibvorgängen sowie das Minimieren des kumulativen Datenverkehrs an die Kapazitäts Laufwerke.

Für „Direkte Speicherplätze“ wird ein Algorithmus implementiert, mit dem die Zufälligkeit von Schreibvorgängen beseitigt wird, bevor deren Bereitstellung aufgehoben wird. So soll ein E/A-Muster für das Laufwerk emuliert werden, das auch dann noch sequenziell erscheint, wenn die tatsächliche Eingabe/Ausgabe von der Workload (z. B. virtuelle Computer) zufälliger Art ist. Auf diese Weise werden der IOPS-Wert und der Durchsatz für die HDDs maximiert.

### <a name="caching-in-deployments-with-drives-of-all-three-types"></a>Zwischenspeicherung bei Bereitstellungen mit Laufwerken aller drei Typen

Wenn alle drei Laufwerkstypen vorhanden sind, übernehmen die NVMe-Laufwerke die Zwischenspeicherung für die SSDs und die HDDs. Das Verhalten ist wie oben beschrieben: Für die SSDs werden nur Schreibvorgänge zwischengespeichert, und für die HDDs werden sowohl Lese- als auch Schreibvorgänge zwischengespeichert. Die Last der Zwischenspeicherung für die HDDs wird gleichmäßig auf die Cachelaufwerke verteilt. 

## <a name="summary"></a>Zusammenfassung

In der folgenden Tabelle ist angegeben, welche Laufwerke zum Zwischenspeichern verwendet werden, welche als Kapazitätslaufwerke eingesetzt werden und welches Cacheverhalten für jede Bereitstellungsmöglichkeit gilt.

| Bereitstellung     | Cachelaufwerke                        | Kapazitätslaufwerke | Cacheverhalten (Standard)  |
| -------------- | ----------------------------------- | --------------- | ------------------------- |
| Nur NVMe         | Keine (Optional: manuelle Konfiguration) | NVMe            | Nur Schreibvorgänge (falls konfiguriert)  |
| Nur SSDs          | Keine (Optional: manuelle Konfiguration) | SSD             | Nur Schreibvorgänge (falls konfiguriert)  |
| NVMe und SSD       | NVMe                                | SSD             | Nur Schreibvorgänge                  |
| NVMe und HDD       | NVMe                                | HDD             | Lese- und Schreibvorgänge                |
| SSD und HDD        | SSD                                 | HDD             | Lese- und Schreibvorgänge                |
| NVMe und SSD und HDD | NVMe                                | SSD und HDD       | Lese- und Schreibvorgänge für HDD, nur Schreibvorgänge für SSD  |

## <a name="server-side-architecture"></a>Serverseitige Architektur

Der Cache wird auf Laufwerksebene implementiert: Einzelne Cachelaufwerke innerhalb eines Servers sind an mindestens ein Kapazitätslaufwerk auf demselben Server gebunden.

Da sich der Cache unterhalb der restlichen Elemente des per Software definierten Speicherstapels von Windows befindet, verfügt er über keinerlei Informationen zu vorhandenen Konzepten wie Speicherplätzen oder Fehlertoleranz (und dies ist auch nicht erforderlich). Sie können sich dies wie die Erstellung von „Hybridlaufwerken“ (teils Flash, teils Festplatte) vorstellen, die dann für Windows zur Verfügung gestellt werden. Wie bei einem richtigen Hybridlaufwerk auch, ist die Echtzeitverschiebung von heißen und kalten Daten zwischen den schnelleren und langsameren Teilen der physischen Medien von außen nahezu unsichtbar.

Wenn sichergestellt ist, dass die Resilienz in Direkte Speicherplätze mindestens auf Serverebene angeordnet ist (Datenkopien also immer auf unterschiedliche Server geschrieben werden und maximal eine Kopie pro Server vorliegt), profitieren die Daten im Cache von der gleichen Resilienz wie für Daten außerhalb des Cache.

![Cache-Server-Side-Architecture](media/understand-the-cache/Cache-Server-Side-Architecture.png)

Bei Verwendung der Drei-Wege-Spiegelung werden beispielsweise drei Kopien aller Daten auf unterschiedliche Server geschrieben, wo sie im Cache abgelegt werden. Unabhängig davon, ob dafür später die Aufhebung der Bereitstellung durchgeführt wird, sind immer drei Kopien vorhanden.

## <a name="drive-bindings-are-dynamic"></a>Laufwerksbindungen sind dynamisch

Für die Bindung zwischen Cache- und Kapazitätslaufwerken kann ein beliebiges Verhältnis gelten, also von 1:1 bis zu 1:12 und mehr. Es wird jeweils dynamisch angepasst, wenn Laufwerke hinzugefügt oder entfernt werden, z. B. beim zentralen Hochskalieren oder nach Ausfällen. Dies bedeutet, dass Sie Cache- oder Kapazitätslaufwerke jederzeit unabhängig voneinander hinzufügen können.

![Dynamic-Binding](media/understand-the-cache/Dynamic-Binding.gif)

Wir empfehlen, dass die Anzahl von Kapazitätslaufwerken aus Gründen der Symmetrie einem Vielfachen der Anzahl von Cachelaufwerken entspricht. Wenn Sie beispielsweise über vier Cachelaufwerke verfügen, ist die Leistung bei Verwendung von acht Kapazitätslaufwerken ausgeglichener (Verhältnis 1:2) als bei Verwendung von sieben oder neun Laufwerken.

## <a name="handling-cache-drive-failures"></a>Behandeln von Ausfällen von Cachelaufwerken

Wenn ein Cachelaufwerk ausfällt, gehen alle Schreibvorgänge, für die die Bereitstellung noch nicht aufgehoben wurde, *auf dem lokalen Server* verloren. Dies bedeutet, dass nur noch die anderen Kopien (auf anderen Servern) vorliegen. Wie auch für alle anderen Laufwerksausfälle gilt Folgendes: Für Speicherplätze kann und wird eine automatische Wiederherstellung durchgeführt, indem die noch vorhandenen Kopien genutzt werden.

Für einen kurzen Zeitraum werden die Kapazitätslaufwerke, die an das verloren gegangene Cachelaufwerk gebunden waren, als fehlerhaft angezeigt. Nachdem die Neueinbindung für den Cache (automatisch) durchgeführt und die Reparatur der Daten (automatisch) abgeschlossen wurde, werden sie wieder als fehlerfrei angezeigt.

Dies verdeutlicht, warum mindestens zwei Cachelaufwerke pro Server benötigt werden, um die Leistung aufrechtzuerhalten.

![Handling-Failure](media/understand-the-cache/Handling-Failure.gif)

Sie können das Cachelaufwerk dann wie jedes andere Laufwerk auch normal austauschen.

   >[!NOTE]
   > Es kann erforderlich sein, das Gerät von der Stromversorgung zu trennen, damit Sie die NVMe-Komponente auf sichere Weise austauschen können, wenn es sich um den Formfaktor Erweiterungskarte (AIC) oder M.2 handelt.

## <a name="relationship-to-other-caches"></a>Beziehung zu anderen Caches

Der per Software definierte Speicherstapel von Windows enthält mehrere andere Caches, die nicht miteinander in Beziehung stehen. Beispiele hierfür sind der Zurückschreibcache von Direkte Speicherplätze und der speicherinterne Lesecache vom Typ „Freigegebenes Clustervolume“ (Cluster Shared Volume, CSV).

Bei Direkte Speicherplätze sollte das Standardverhalten für den Zurückschreibcache von Direkte Speicherplätze nicht geändert werden. Vermeiden Sie es beispielsweise, Parameter wie **-WriteCacheSize** für das **New-Volume**-Cmdlet zu verwenden.

Sie können frei entscheiden, ob Sie den CSV-Cache verwenden möchten. Er ist in Direkte Speicherplätze standardmäßig deaktiviert, steht aber in keinerlei Konflikt mit dem neuen Cache, der in diesem Thema beschrieben wird. In bestimmten Szenarien können hiermit wertvolle Leistungssteigerungen erzielt werden. Weitere Informationen finden Sie unter [How to Enable CSV Cache](../../failover-clustering/failover-cluster-csvs.md#enable-the-csv-cache-for-read-intensive-workloads-optional) (Aktivieren des CSV-Caches).

## <a name="manual-configuration"></a>Manuelle Konfiguration

Bei den meisten Bereitstellungen ist keine manuelle Konfiguration erforderlich. Falls Sie ihn benötigen, finden Sie weitere Informationen in den folgenden Abschnitten. 

Wenn Sie nach der Installation Änderungen am Cache Gerätemodell vornehmen müssen, bearbeiten Sie das Dokument mit den unterstützten Komponenten der Integritätsdienst, wie in [Integritätsdienst Übersicht](../../failover-clustering/health-service-overview.md#supported-components-document)beschrieben.

### <a name="specify-cache-drive-model"></a>Angeben des Cachelaufwerkmodells

Bei Bereitstellungen, bei denen alle Laufwerke den gleichen Typ haben, z. B. Bereitstellungen nur mit NVMe- oder SSD-Komponenten, wird kein Cache konfiguriert, da Windows für Laufwerke des gleichen Typs nicht automatisch zwischen Merkmalen wie der Schreibbelastbarkeit unterscheiden kann.

Wenn Sie Laufwerke mit höherer Belastbarkeit als Cache für Laufwerke des gleichen Typs mit geringerer Belastbarkeit verwenden möchten, können Sie angeben, welches Laufwerksmodell mit dem Parameter **-CacheDeviceModel** des **Enable-ClusterS2D**-Cmdlets verwendet werden soll. Nachdem Direkte Speicherplätze aktiviert wurde, werden alle Laufwerke dieses Modells für die Zwischenspeicherung verwendet.

   >[!TIP]
   > Achten Sie darauf, dass die Modellzeichenfolge genau wie in der Ausgabe von **Get-PhysicalDisk** angegeben ist.

####  <a name="example"></a>Beispiel

Holen Sie zunächst eine Liste der physischen Datenträger:

```PowerShell
Get-PhysicalDisk | Group Model -NoElement
```

Ausgabebeispiel:

```
Count Name
----- ----
    8 FABRIKAM NVME-1710
   16 CONTOSO NVME-1520
```

Geben Sie dann den folgenden Befehl ein, wobei Sie das Cache Gerätemodell angeben:

```PowerShell
Enable-ClusterS2D -CacheDeviceModel "FABRIKAM NVME-1710"
```

Sie können überprüfen, ob die gewünschten Laufwerke für die Zwischenspeicherung verwendet werden, indem Sie **Get-PhysicalDisk** in PowerShell ausführen und sicherstellen, dass für die **Usage**-Eigenschaft der Wert **"Journal"** angegeben ist.

### <a name="manual-deployment-possibilities"></a>Möglichkeiten der manuellen Bereitstellung

Bei der manuellen Konfiguration haben Sie die folgenden Bereitstellungsmöglichkeiten:

![Exotic-Deployment-Possibilities](media/understand-the-cache/Exotic-Deployment-Possibilities.png)

### <a name="set-cache-behavior"></a>Festlegen des Cacheverhaltens

Es ist möglich, das Standardverhalten des Caches außer Kraft zu setzen. Beispielsweise können Sie auch für eine reine Flash-Bereitstellung festlegen, dass Lesevorgänge zwischengespeichert werden sollen. Es ist nicht ratsam, das Verhalten zu ändern (es sei denn, Sie sind sich sicher, dass die Standardeinstellungen für Ihre Workloads nicht geeignet sind).

Um das Verhalten zu überschreiben, verwenden Sie das Cmdlet " **Set-clusterstoragespacesdirect** " und die Parameter " **-cachemodessd** " und " **-cachemodehdd** ". Mit dem Parameter **CacheModeSSD** wird das Cacheverhalten für die Zwischenspeicherung für Festkörperlaufwerke festgelegt. Mit dem Parameter **CacheModeHDD** wird das Cacheverhalten für die Zwischenspeicherung für Festplattenlaufwerke festgelegt. Dies ist jederzeit nach dem Aktivieren von Direkte Speicherplätze möglich.

Sie können **Get-clusterstoragespacesdirect** verwenden, um zu überprüfen, ob das Verhalten festgelegt ist.

#### <a name="example"></a>Beispiel

Holen Sie sich zunächst die direkte Speicherplätze Einstellungen:

```PowerShell
Get-ClusterStorageSpacesDirect
```

Ausgabebeispiel:

```
CacheModeHDD : ReadWrite
CacheModeSSD : WriteOnly
```

Gehen Sie dann wie folgt vor:

```PowerShell
Set-ClusterStorageSpacesDirect -CacheModeSSD ReadWrite

Get-ClusterS2D
```

Ausgabebeispiel:

```
CacheModeHDD : ReadWrite
CacheModeSSD : ReadWrite
```

## <a name="sizing-the-cache"></a>Festlegen der Größe des Caches

Die Größe des Caches sollte so gewählt werden, dass sie für den Arbeitssatz (die Daten, die aktiv gelesen oder geschrieben werden) Ihrer Anwendungen und Workloads ausreicht.

Dies ist besonders bei Hybridbereitstellungen mit Festplattenlaufwerken wichtig. Wenn der aktive Arbeitssatz die Größe des Caches übersteigt oder sich zu schnell verändert, kommt es vermehrt zu Lesecachefehlern, und die Aufhebung der Bereitstellung von Schreibvorgängen muss aggressiver erfolgen, wodurch die Gesamtleistung beeinträchtigt wird.

Sie können das integrierte Hilfsprogramm „Systemmonitor“ (PerfMon.exe) unter Windows verwenden, um die Cachefehlerrate zu überprüfen. Genauer gesagt: Sie können den Wert **Cache Miss Reads/sec** des Indikatorsatzes **Cluster Storage Hybrid Disk** mit dem IOPS-Gesamtwert für Lesevorgänge Ihrer Bereitstellung vergleichen. Jedes Hybridlaufwerk („Hybrid Disk“) entspricht einem Kapazitätslaufwerk.

Wenn beispielsweise zwei Cachelaufwerke an vier Kapazitätslaufwerke gebunden sind, ergibt dies vier „Hybrid Disk“-Objektinstanzen pro Server.

![Performance-Monitor](media/understand-the-cache/PerfMon.png)

Es gibt keine allgemeingültige Regel, aber wenn es für zu viele Lesevorgänge zu Cachefehlern kommt, reicht die Größe ggf. nicht aus, und Sie sollten erwägen, zur Erweiterung des Caches mehr Cachelaufwerke hinzuzufügen. Sie können Cache- oder Kapazitätslaufwerke jederzeit unabhängig voneinander hinzufügen.

## <a name="see-also"></a>Siehe auch

- [Auswählen von Laufwerken und resilienztypen](choosing-drives.md)
- [Fehlertoleranz und Speichereffizienz](storage-spaces-fault-tolerance.md)
- [Direkte Speicherplätze Hardwareanforderungen](storage-spaces-direct-hardware-requirements.md)
