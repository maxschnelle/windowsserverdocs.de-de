---
ms.assetid: 1368bc83-9121-477a-af09-4ae73ac16789
title: Auswählen von Laufwerken für „Direkte Speicherplätze“
ms.prod: windows-server
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 07/01/2020
ms.localizationpriority: medium
ms.openlocfilehash: aae554c87b8a4ac6005ad359bc474026f5f1ed9e
ms.sourcegitcommit: acfdb7b2ad283d74f526972b47c371de903d2a3d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87769408"
---
# <a name="choosing-drives-for-storage-spaces-direct"></a>Auswählen von Laufwerken für „Direkte Speicherplätze“

>Gilt für: Windows Server 2019, Windows Server 2016

Dieses Thema enthält Anleitungen zum Auswählen von Laufwerken für [direkte Speicherplätze](storage-spaces-direct-overview.md) , um Ihre Leistungs-und Kapazitätsanforderungen zu erfüllen.

## <a name="drive-types"></a>Laufwerkstypen

Für „Direkte Speicherplätze“ können derzeit vier Arten von Laufwerken verwendet werden:

<table>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/pmem-100px.png" alt="Image of PMem (persistent memory)">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>PMem</b> bezieht sich auf persistenten Speicher. Dabei handelt es sich um eine neue Art von Hochleistungsspeicher mit geringen Wartezeiten.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/NVMe-100px.png" alt="Image of NVMe (Non-Volatile Memory Express)">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>NVMe</b>-Laufwerke (Non-Volatile Memory Express) sind Solid State Drives, die direkt auf dem PCIe-Bus angeordnet sind. Häufig verwendete Formfaktoren sind 2,5" U.2, PCIe Add-In-Card (AIC) und M.2. Nvme bietet einen höheren IOPS-und e/a-Durchsatz mit geringerer Latenz als alle anderen von uns unterstützten Laufwerke mit Ausnahme des permanenten Speichers.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px" >
            <img src="media/understand-the-cache/SSD-100px.png" alt="Image of SSD drive">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>SSD</b> bezieht sich auf Solid State Drives, die eine Verbindung über herkömmliches SATA oder SAS herstellen.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/HDD-100px.png" alt="Image of HDD">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>HDD</b> bezieht sich auf rotierende, Magnet Festplattenlaufwerke, die eine große Speicherkapazität bieten.
        </td>
    </tr>
</table>

## <a name="built-in-cache"></a>Integrierter Cache

„Direkte Speicherplätze“ verfügt über einen integrierten serverseitigen Cache. Es handelt sich um einen großen, persistenten Echtzeitcache für Lese- und Schreibvorgänge. Bei Bereitstellungen mit mehreren Arten von Laufwerken wird er automatisch so konfiguriert, dass alle „schnellsten“ Laufwerke verwendet werden. Alle weiteren Datenträger werden zur Bereitstellung der Kapazität verwendet.

Weitere Informationen finden Sie unter [Grundlegendes zum Cache in „Direkte Speicherplätze“](understand-the-cache.md).

## <a name="option-1--maximizing-performance"></a>Option 1: Maximieren der Leistung

Um eine vorhersagbare und einheitliche Latenz von unter Millisekunden über zufällige Lese-und Schreibvorgänge an Daten zu erzielen oder um extrem hohe IOPS (was [über 6 Millionen](https://www.youtube.com/watch?v=0LviCzsudGY&t=28m)!) oder einen e/a-Durchsatz erreicht werden soll (wir haben [mehr als 1 TB/s](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=16m50s)!), sollten Sie "alles-Flash" durchlaufen.

Hierfür gibt es derzeit drei Möglichkeiten:

![Optionen bei Nur-Flash-Bereitstellungen](media/choosing-drives-and-resiliency-types/All-Flash-Deployment-Possibilities.png)

1. **Nur NVMe:** Die Verwendung einer reinen NVMe-Bereitstellung ermöglicht eine unvergleichlich hohe Leistung und eine geringe Latenz mit bestmöglicher Vorhersagbarkeit. Wenn Sie für Ihre gesamten Laufwerke das gleiche Modell nutzen, ist kein Cache vorhanden. Sie können auch NVMe-Modelle mit längerer und kürzerer Lebensdauer mischen und festlegen, dass Erstere die Schreibvorgänge für Letztere zwischenspeichern ([Einrichtung erforderlich](understand-the-cache.md#manual-configuration)).

2. **NVMe und SSD:** Wenn NVMe-Laufwerke zusammen mit SSDs verwendet werden, werden vom NVMe-Laufwerk automatisch Schreibvorgänge für die SSDs zwischengespeichert. Auf diese Weise können Schreibvorgänge im Cache zusammengefasst werden. Das De-Staging wird hierfür dann nur bei Bedarf durchgeführt, um die Belastung für die SSDs zu verringern. Dies ermöglicht NVMe-ähnliche Schreibeigenschaften, während Lesevorgänge direkt über die ebenfalls schnellen SSDs bereitgestellt werden.

3. **Nur SSDs:** Wie auch bei einer reinen Bereitstellung mit NVMe-Laufwerken ist kein Cache vorhanden, wenn für alle Laufwerke das gleiche Modell verwendet wird. Wenn Sie Modelle mit längerer und kürzerer Lebensdauer mischen, können Sie festlegen, dass Erstere die Schreibvorgänge für Letztere zwischenspeichern ([Einrichtung erforderlich](understand-the-cache.md#manual-configuration)).

   >[!NOTE]
   > Ein Vorteil bei der Verwendung von reinen NVMe- oder SSD-Bereitstellungen ohne Cache ist, dass Sie für jedes Laufwerk über nutzbare Speicherkapazität verfügen. Es geht keine Kapazität für die Zwischenspeicherung verloren. Dies kann bei kleineren Bereitstellungen ratsam sein.

## <a name="option-2--balancing-performance-and-capacity"></a>Option 2: Abstimmen von Leistung und Kapazität

Für Umgebungen mit einer Vielzahl von Anwendungen und Workloads, für die teilweise strenge Leistungsanforderungen gelten und teilweise beträchtliche Speicherkapazität benötigt wird, sollten Sie einen Hybridansatz wählen, bei dem entweder mit NVMe-Laufwerken oder SSDs die Zwischenspeicherung für größere HDDs durchgeführt wird.

![Optionen bei Hybridbereitstellungen](media/choosing-drives-and-resiliency-types/Hybrid-Deployment-Possibilities.png)

1. **NVMe und HDDs:** Mit den NVMe-Laufwerken werden Lese- und Schreibvorgänge beschleunigt, indem beide zwischengespeichert werden. Die Zwischenspeicherung von Lesevorgängen ermöglicht den HDDs die Konzentration auf Schreibvorgänge. Mit der Zwischenspeicherung von Schreibvorgängen werden Bursts absorbiert, und Schreibvorgänge können zusammengefasst werden, bis bei Bedarf das De-Staging durchgeführt wird. Dies erfolgt auf künstlich serialisierte Weise, um den IOPS- und E/A-Durchsatz für HDDs zu maximieren. So können NVMe-ähnliche Schreibeigenschaften und – für häufig oder kürzlich gelesene Daten – auch NVMe-ähnliche Leseeigenschaften erzielt werden.

2. **SSDs und HDDs:** Ähnlich wie im obigen Fall werden Lese- und Schreibvorgänge mit SSDs beschleunigt, indem beide zwischengespeichert werden. Dies ermöglicht SSD-ähnliche Schreibeigenschaften und für häufig oder kürzlich gelesene Daten auch SSD-ähnliche Leseeigenschaften.

    Es gibt noch eine weitere Option, die eher ungewöhnlich ist: die Nutzung von Laufwerken *aller drei* Typen.

3. **NVMe, SSDs und HDDs:** Bei Verwendung von Laufwerken aller drei Typen übernehmen die NVMe-Laufwerke die Zwischenspeicherung für die SSDs und HDDs. Der Vorteil besteht darin, dass Sie Volumes auf den SSDs und den HDDs parallel in demselben Cluster erstellen können, die alle per NVMe beschleunigt werden. Erstere verhalten sich genauso wie bei einer reinen Flash-Bereitstellung, und Letztere verhalten sich genauso wie bei den oben beschriebenen Hybridbereitstellungen. Vom Konzept her entspricht dies der Nutzung von zwei Pools mit größtenteils unabhängiger Kapazitätsverwaltung, Ausfall- und Reparaturzyklen usw.

   >[!IMPORTANT]
   > Wir empfehlen Ihnen, die SSD-Ebene zu verwenden, um Ihre leistungsempfindlichsten Workloads als reine Flash-Bereitstellung anzuordnen.

## <a name="option-3--maximizing-capacity"></a>Option 3: Maximieren der Kapazität

Für Arbeits Auslastungen, die eine umfangreiche Kapazität erfordern und nur selten schreiben, wie z. b. Archivierung, Sicherungs Ziele, Data Warehouse oder "kalte" Speicherung, sollten Sie einige SSDs für die Zwischenspeicherung mit vielen größeren HDDs für die Kapazität kombinieren.

![Bereitstellungsoptionen zur Maximierung der Kapazität](media/choosing-drives-and-resiliency-types/maximizing-capacity.png)

1. **SSDs und HDDs:** Die SSDs übernehmen die Zwischenspeicherung der Lese- und Schreibvorgänge, um Bursts zu absorbieren und eine SSD-ähnliche Schreibleistung zu erzielen. Später wird dann das optimierte De-Staging für die HDDs durchgeführt.

>[!IMPORTANT]
>Konfigurationen nur mit HDDs werden nicht unterstützt. Es ist nicht ratsam, dass SSDs mit längerer Lebensdauer die Zwischenspeicherung für SSDs mit kürzerer Lebensdauer übernehmen.

## <a name="sizing-considerations"></a>Überlegungen zur Größenanpassung

### <a name="cache"></a>Cache

Jeder Server muss mindestens über zwei Cachelaufwerke verfügen (Mindestanforderung zur Erzielung von Redundanz). Wir empfehlen Ihnen, als Anzahl von Kapazitätslaufwerken ein Vielfaches der Anzahl von Cachelaufwerken zu wählen. Wenn Sie beispielsweise vier Cachelaufwerke verwenden, erhalten Sie eine einheitlichere Leistung, wenn Sie acht Kapazitätslaufwerke (Verhältnis 1:2) nutzen, und nicht sieben oder neun.

Der Cache sollte die Größe des Arbeits Satzes Ihrer Anwendungen und Arbeits Auslastungen abdecken, d. h. alle Daten, die Sie zu einem beliebigen Zeitpunkt aktiv Lesen und schreiben. Darüber hinaus besteht für die Cachegröße keine weitere Anforderung. Bei bereit Stellungen mit HDDs besteht ein guter Ausgangspunkt aus 10% der Kapazität – beispielsweise, wenn jeder Server 4 x 4 TB HDD = 16 TB Kapazität hat, dann 2 x 800 GB SSD = 1,6 TB Cache pro Server. Für alle Flash Bereitstellungen, insbesondere bei sehr [hohen Belastungs](https://techcommunity.microsoft.com/t5/storage-at-microsoft/understanding-ssd-endurance-drive-writes-per-day-dwpd-terabytes/ba-p/426024) -SSDs, ist es möglicherweise sehr wichtig, sich mit 5% der Kapazität zu beginnen – beispielsweise, wenn jeder Server über 24 x 1,2 TB SSD = 28,8 TB Kapazität verfügt, dann 2 x 750 GB nvme = 1,5 TB Cache pro Server. Sie können später jederzeit Cachelaufwerke hinzufügen oder entfernen, um dies anzupassen.

### <a name="general"></a>Allgemein

Wir empfehlen Ihnen, die Gesamtspeicherkapazität pro Server auf ca. 400 TB (Terabyte) zu begrenzen. Je mehr Speicherkapazität pro Server vorhanden ist, desto mehr Zeit wird nach einem Ausfall oder Neustart für die erneute Synchronisierung der Daten benötigt, z. B. beim Anwenden von Softwareupdates. Die aktuelle maximale Größe pro Speicherpool beträgt 4 Petabytebereich (PB) (4.000 TB) für Windows Server 2019 oder 1 Petabytebereich für Windows Server 2016.

## <a name="additional-references"></a>Weitere Verweise

- [Direkte Speicherplätze – Übersicht](storage-spaces-direct-overview.md)
- [Verstehen des Caches in direkten Speicherplätzen](understand-the-cache.md)
- [Hardwareanforderungen für „Direkte Speicherplätze“](storage-spaces-direct-hardware-requirements.md)
- [Planen von Volumes in direkte Speicherplätze](plan-volumes.md)
- [Fehlertoleranz und Speichereffizienz](storage-spaces-fault-tolerance.md)
