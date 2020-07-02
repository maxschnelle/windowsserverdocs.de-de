---
ms.assetid: 1368bc83-9121-477a-af09-4ae73ac16789
title: Auswählen von Laufwerken für direkte Speicherplätze
ms.prod: windows-server
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 07/01/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2ffe34097971f4477f0f536637b49b704678c93e
ms.sourcegitcommit: c40c29683d25ed75b439451d7fa8eda9d8d9e441
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/01/2020
ms.locfileid: "85833364"
---
# <a name="choosing-drives-for-storage-spaces-direct"></a>Auswählen von Laufwerken für direkte Speicherplätze

>Gilt für: Windows Server 2019, Windows Server 2016

Dieses Thema enthält Anleitungen zum Auswählen von Laufwerken für [direkte Speicherplätze](storage-spaces-direct-overview.md) , um Ihre Leistungs-und Kapazitätsanforderungen zu erfüllen.

## <a name="drive-types"></a>Laufwerkstypen

Direkte Speicherplätze funktioniert derzeit mit vier Arten von Laufwerken:

<table>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/pmem-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>PMem</b> bezieht sich auf den dauerhaften Speicher, einen neuen Typ von niedriger Latenz und Hochleistungsspeicher.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/NVMe-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>Nvme</b> (Non-volatile-Speicher Express) bezieht sich auf Solid State Drives, die sich direkt auf dem PCIe-Bus befinden. Allgemeine Formfaktoren sind 2,5 Zoll U.2 PCI-Add-In-Karte (AIC) und M.2. Nvme bietet einen höheren IOPS-und e/a-Durchsatz mit geringerer Latenz als alle anderen von uns unterstützten Laufwerke mit Ausnahme des permanenten Speichers.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px" >
            <img src="media/understand-the-cache/SSD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>SSD</b> bezieht sich auf Solid State Drives, die eine Verbindung über herkömmliches SATA oder SAS herstellen.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/HDD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>HDD</b> bezieht sich auf rotierende, Magnet Festplattenlaufwerke, die eine große Speicherkapazität bieten.
        </td>
    </tr>
</table>

## <a name="built-in-cache"></a>Integrierter Cache

Direkte Speicherplätze verfügt über einen integrierten serverseitigen Cache. Es handelt sich um einen großen, persistenten Echtzeit-Cache für Lese- und Schreibvorgänge. Bei bereit Stellungen mit mehreren Laufwerkstypen wird diese automatisch für die Verwendung aller Laufwerke des Typs "schnellste" konfiguriert. Alle weiteren Datenträger werden zur Bereitstellung der Kapazität verwendet.

Weitere Informationen finden Sie Untergrund Legendes [zum Cache in direkte Speicherplätze](understand-the-cache.md).

## <a name="option-1--maximizing-performance"></a>Option 1 – Maximieren der Leistung

Um eine vorhersagbare und einheitliche Latenz von unter Millisekunden über zufällige Lese-und Schreibvorgänge an Daten zu erzielen oder um extrem hohe IOPS (was [über 6 Millionen](https://www.youtube.com/watch?v=0LviCzsudGY&t=28m)!) oder einen e/a-Durchsatz erreicht werden soll (wir haben [mehr als 1 TB/s](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=16m50s)!), sollten Sie "alles-Flash" durchlaufen.

Es gibt derzeit drei Möglichkeiten:

![All-Flash-Deployment-Possibilities](media/choosing-drives-and-resiliency-types/All-Flash-Deployment-Possibilities.png)

1. **Alle nvme.** Die ausschließliche Verwendung von NVMe bietet unübertroffene Leistung, inklusive der vorhersagbar niedrigsten Latenz. Wenn das Modell all Ihrer Laufwerke identisch ist, gibt es keinen Cache. Sie können NVMe-Modelle für höhere und niedrigere Belastungen miteinander verwenden und das erste Modell zum Speichern von Schreibvorgängen auf das Cache des zweiten Modells konfigurieren ([Installation erforderlich](understand-the-cache.md#manual-configuration)).

2. **Nvme und SSD.** Bei der Verwendung von NVMe- mit SSDs-Laufwerken speichert das NVMe-Laufwerk automatisch Schreibvorgänge im Cache des SSDs-Laufwerks. Dadurch können Schreibvorgänge im Cache zusammengefügt und nur bei Bedarf zur Reduzierung der Abnutzung des SSDs-Laufwerks aufgehoben werden. Dies ermöglicht NVMe-ähnliche Merkmale der Schreibvorgänge, während Lesevorgänge ebenfalls direkt von den ebenfalls schnellen SSDs-Laufwerken bereitgestellt wird.

3. **Nur SSD.** Wie bei allen NVMe-Laufwerken ist kein Cache vorhanden, wenn das Modell all Ihrer Laufwerke identisch ist. Wenn Sie NVMe-Modelle für höhere und niedrigere Belastungen miteinander verwenden, können Sie das erste Modell zum Speichern von Schreibvorgängen auf das Cache des zweiten Modells konfigurieren ([Installation erforderlich](understand-the-cache.md#manual-configuration)).

   >[!NOTE]
   > Der Vorteil bei der ausschließlichen Verwendung von NVMe oder von SSD ohne Cache ist, dass Sie jederzeit auf die verwendbare Speicherkapazität jedes Laufwerks zugreifen können. Es gibt keine „überschüssige” Kapazität beim Zwischenspeichern, was bei einer Skalierung von kleineren Laufwerken von Vorteil sein kann.

## <a name="option-2--balancing-performance-and-capacity"></a>Option 2 – Ausgleich von Leistung und Kapazität

Für Umgebungen mit einer Vielzahl von Anwendungen und Arbeits Auslastungen, bei denen es sich um strenge Leistungsanforderungen handelt und andere eine beträchtliche Speicherkapazität benötigen, sollten Sie mit nvme oder SSDs Caching für größere HDDs "Hybrid" machen.

![Hybrid-Deployment-Possibilities](media/choosing-drives-and-resiliency-types/Hybrid-Deployment-Possibilities.png)

1. **NVMe + HDD**. NVMe-Laufwerke beschleunigen sowohl Lese- als auch Schreibvorgänge durch ein Zwischenspeichern beider Vorgänge. Lesevorgänge ermöglichen dem HDDs, sich auf Schreibvorgänge zu konzentrieren. Schreibvorgänge im Cache übernehmen Datenverkehrsspitzen. Dadurch können Schreibvorgänge im Cache zusammengefügt und nur bei Bedarf durch künstliches Serialisieren zur Optimierung des HDD IOPS und E/A-Durchsatzes aufgehoben werden. Dies ermöglicht NVMe-ähnliche Merkmale der Schreib- und Lesevorgänge für häufig oder kürzlich gelesene Daten.

2. **SSD + HDD**. Ähnlich wie die oben genannten Vorgänge, beschleunigt SSDs Lese- und Schreibvorgänge durch deren Zwischenspeichern. Dies ermöglicht SSD-ähnliche Merkmale der Schreib- und Lesevorgänge für häufig oder kürzlich gelesene Daten.

    Es gibt eine zusätzliche, etwas „exotische” Option: Laufwerke mit *allen drei* Typen.

3. **Nvme + SSD + HDD.** Bei Laufwerken aller drei Typen werden die nvme-Laufwerke für SSDs und HDDs zwischengespeichert. Der Anreiz dabei ist, dass Sie parallel im gleichen Cluster Volumes auf SSDs und HDDs erstellen können, die alle von NVMe beschleunigt werden. Die erste Option gleicht einer Bereitstellung, die ausschließlich Flash verwendet, während letztere Option einer oben beschriebenen hybriden Bereitstellung gleicht. Konzeptuell gleicht es einem System mit zwei Pools, dessen Kapazitätsmanagement, Fehler- und Reparaturzyklus usw. überwiegend unabhängig ist.

   >[!IMPORTANT]
   > Es wird empfohlen, die SSD-Ebene zu verwenden, um die Leistungs sensitiven Workloads bei allen Flash-Vorgängen zu platzieren.

## <a name="option-3--maximizing-capacity"></a>Option 3 – Maximieren der Kapazität

Für Arbeits Auslastungen, die eine umfangreiche Kapazität erfordern und nur selten schreiben, wie z. b. Archivierung, Sicherungs Ziele, Data Warehouse oder "kalte" Speicherung, sollten Sie einige SSDs für die Zwischenspeicherung mit vielen größeren HDDs für die Kapazität kombinieren.

![Bereitstellungsoptionen für das Maximieren der Kapazität-](media/choosing-drives-and-resiliency-types/maximizing-capacity.png)

1. **SSD + HDD**. SSDs speichern Lese- und Schreibvorgänge, um Datenverkehrsspitzen aufzufangen und eine SSD-ähnliche Leistung der Schreibvorgänge mit einer späteren optimierten Bereitstellung im HDD anzubieten.

>[!IMPORTANT]
>Nur die Konfiguration mit HDDs wird unterstützt. Hohe Ausdauer-SSDs-Zwischenspeicherung und SSDs mit niedriger Ausdauer ist nicht empfehlenswert.

## <a name="sizing-considerations"></a>Überlegungen zur Größe

### <a name="cache"></a>Cache

Jeder Server muss über mindestens zwei Cache-Laufwerke verfügen (die Mindestanforderungen für Redundanz). Wir empfehlen, dass die Anzahl der Kapazitätslaufwerke um ein Vielfaches der Anzahl der Cache-Laufwerke entspricht. Wenn Sie z. b. über 4 Cache Laufwerke verfügen, kommt es zu einer konsistenten Leistung mit 8 Kapazitäts Laufwerken (1:2-Verhältnis) als 7 oder 9.

Der Cache sollte die Größe des Arbeits Satzes Ihrer Anwendungen und Arbeits Auslastungen abdecken, d. h. alle Daten, die Sie zu einem beliebigen Zeitpunkt aktiv Lesen und schreiben. Darüber hinaus gibt es keine Cachegrößenanforderung. Bei bereit Stellungen mit HDDs besteht ein guter Ausgangspunkt aus 10% der Kapazität – beispielsweise, wenn jeder Server 4 x 4 TB HDD = 16 TB Kapazität hat, dann 2 x 800 GB SSD = 1,6 TB Cache pro Server. Für alle Flash Bereitstellungen, insbesondere bei sehr [hohen Belastungs](https://blogs.technet.microsoft.com/filecab/2017/08/11/understanding-dwpd-tbw/) -SSDs, ist es möglicherweise sehr wichtig, sich mit 5% der Kapazität zu beginnen – beispielsweise, wenn jeder Server über 24 x 1,2 TB SSD = 28,8 TB Kapazität verfügt, dann 2 x 750 GB nvme = 1,5 TB Cache pro Server. Sie können zu einem späteren Zeitpunkt immer noch Cache-Laufwerke hinzufügen oder entfernen.

### <a name="general"></a>Allgemein

Es wird empfohlen, die gesamte Speicherkapazität pro Server auf ungefähr 400 Terabyte (TB) zu begrenzen. Je mehr Speicherkapazität pro Server existiert, desto länger dauert die Neusynchronisierung der Daten nach dem Herunterfahren des Systems oder nach einem Neustart wie z. B. beim Aktualisieren von Software. Die aktuelle maximale Größe pro Speicherpool beträgt 4 Petabytebereich (PB) (4.000 TB) für Windows Server 2019 oder 1 Petabytebereich für Windows Server 2016.

## <a name="additional-references"></a>Weitere Verweise

- [Übersicht über direkte Speicherplätze](storage-spaces-direct-overview.md)
- [Verstehen des Caches in direkten Speicherplätzen](understand-the-cache.md)
- [Direkte Speicherplätze Hardwareanforderungen](storage-spaces-direct-hardware-requirements.md)
- [Planen von Volumes in direkte Speicherplätze](plan-volumes.md)
- [Fehlertoleranz und Speichereffizienz](storage-spaces-fault-tolerance.md)
