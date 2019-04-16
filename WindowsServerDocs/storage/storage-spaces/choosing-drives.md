---
ms.assetid: 1368bc83-9121-477a-af09-4ae73ac16789
title: Auswählen von Laufwerken für Direkte Speicherplätze
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 10/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 227906685d77c31587c66d1c292f20ca94775058
ms.sourcegitcommit: bb626d8626ef47426b781925ea588755dbe2e403
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/28/2018
ms.locfileid: "7871593"
---
# Auswählen von Laufwerken für Direkte Speicherplätze

>Gilt für: Windows Server2016

Dieses Thema enthält Informationen zum Auswählen von Laufwerken für [Direkte Speicherplätze](storage-spaces-direct-overview.md), um Ihre Leistungs- und Kapazitätsanforderungen zu erfüllen.

## Laufwerkstypen

Direkte Speicherplätze funktioniert derzeit mit drei Arten von Laufwerken:

<table>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/NVMe-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>Als NVMe</b> (Non-Volatile Memory Express) werden Solid State Drives bezeichnet, die sich direkt auf dem PCIe-Bus befinden. Allgemeine Formfaktoren sind 2,5 Zoll U.2 PCI-Add-In-Karte (AIC) und M.2. NVMe bietet einen höheren IOPS-Wert und E/A-Durchsatz mit geringerer Latenz als jedes andere Laufwerk, das wir heute unterstützen.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px" >
            <img src="media/understand-the-cache/SSD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>Als SSD</b> werden Solid State Drives bezeichnet, die eine Verbindung über herkömmliche SATA oder SAS ermöglichen.
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/HDD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>Als HDD</b> werden herkömmliche, magnetische Festplattenlaufwerke bezeichnet, die eine große Speicherkapazität bieten.
        </td>
    </tr>
</table>

## Integrierter Cache

Direkte Speicherplätze verfügt über einen integrierten serverseitigen Cache. Es handelt sich um einen großen, persistenten Echtzeit-Cache für Lese- und Schreibvorgänge. In Bereitstellungen mit mehreren Arten von Laufwerken wird er automatisch für die Verwendung aller Laufwerke vom Typ "schnellste" konfiguriert. Die restlichen Laufwerke werden für Kapazitätszwecke genutzt.

Weitere Informationen finden Sie unter [Grundlegendes zum Cache in Direkte Speicherplätze](understand-the-cache.md).

## Option 1 – Maximieren der Leistung

Wenn Ihr Ziel eine vorhersehbare und einheitliche Latenz unter Millisekunden für hohe Geschwindigkeiten von direkten Lese-/Schreibvorgängen auf alle Daten oder ein besonders hoher IOPS (wir erreichten über [6 Millionen](https://www.youtube.com/watch?v=0LviCzsudGY&t=28m)!) oder ein E/A-Durchsatz ist (wir erreichten [mehr als 1 Tb/s](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=16m50s)!), sollten Sie reine Flash-Bereitstellungen verwenden.

Es gibt zur Zeit drei Möglichkeiten dafür:

![All-Flash-Deployment-Possibilities](media/choosing-drives-and-resiliency-types/All-Flash-Deployment-Possibilities.png)

1. **Nur NVMe.** Die ausschließliche Verwendung von NVMe bietet unübertroffene Leistung, inklusive der vorhersagbar niedrigsten Latenz. Wenn das Modell all Ihrer Laufwerke identisch ist, gibt es keinen Cache. Sie können NVMe-Modelle für höhere und niedrigere Belastungen miteinander verwenden und das erste Modell zum Speichern von Schreibvorgängen auf das Cache des zweiten Modells konfigurieren ([Installation erforderlich](understand-the-cache.md#manual)).

2. **NVMe + SSD.** Bei der Verwendung von NVMe- mit SSDs-Laufwerken speichert das NVMe-Laufwerk automatisch Schreibvorgänge im Cache des SSDs-Laufwerks. Dadurch können Schreibvorgänge im Cache zusammengefügt und nur bei Bedarf zur Reduzierung der Abnutzung des SSDs-Laufwerks aufgehoben werden. Dies ermöglicht NVMe-ähnliche Merkmale der Schreibvorgänge, während Lesevorgänge ebenfalls direkt von den ebenfalls schnellen SSDs-Laufwerken bereitgestellt wird.

3. **Nur SSD.** Wie bei allen NVMe-Laufwerken ist kein Cache vorhanden, wenn das Modell all Ihrer Laufwerke identisch ist. Wenn Sie NVMe-Modelle für höhere und niedrigere Belastungen miteinander verwenden, können Sie das erste Modell zum Speichern von Schreibvorgängen auf das Cache des zweiten Modells konfigurieren ([Installation erforderlich](understand-the-cache.md#manual)).

   >[!NOTE]
   > Der Vorteil bei der ausschließlichen Verwendung von NVMe oder von SSD ohne Cache ist, dass Sie jederzeit auf die verwendbare Speicherkapazität jedes Laufwerks zugreifen können. Es gibt keine „überschüssige” Kapazität beim Zwischenspeichern, was bei einer Skalierung von kleineren Laufwerken von Vorteil sein kann.

## Option 2 – Ausgleich von Leistung und Kapazität

Für Umgebungen mit einer Vielzahl von Anwendungen und Workloads – einige davon mit strengen Leistungsanforderungen und andere, die eine beträchtliche Speicherkapazität erfordern – sollten Sie eine Hybrid-Bereitstellung mit NVMe oder SSDs-Zwischenspeicherung für größere HDDs verwenden.

![Hybrid-Bereitstellungsmöglichkeiten](media/choosing-drives-and-resiliency-types/Hybrid-Deployment-Possibilities.png)

1. **NVMe + HDD**. NVMe-Laufwerke beschleunigen sowohl Lese- als auch Schreibvorgänge durch ein Zwischenspeichern beider Vorgänge. Lesevorgänge ermöglichen dem HDDs, sich auf Schreibvorgänge zu konzentrieren. Schreibvorgänge im Cache übernehmen Datenverkehrsspitzen. Dadurch können Schreibvorgänge im Cache zusammengefügt und nur bei Bedarf durch künstliches Serialisieren zur Optimierung des HDD IOPS und E/A-Durchsatzes aufgehoben werden. Dies ermöglicht NVMe-ähnliche Merkmale der Schreib- und Lesevorgänge für häufig oder kürzlich gelesene Daten.

2. **SSD + HDD**. Ähnlich wie die oben genannten Vorgänge, beschleunigt SSDs Lese- und Schreibvorgänge durch deren Zwischenspeichern. Dies ermöglicht SSD-ähnliche Merkmale der Schreib- und Lesevorgänge für häufig oder kürzlich gelesene Daten.

    Es gibt eine zusätzliche, etwas „exotische” Option: Laufwerke mit *allen drei* Typen.

3. **NVMe + SSD + HDD.** Bei der Verwendung von Laufwerken aller drei Typen übernimmt der NVME-Speicher das Zwischenspeichern die SSDs und HDDs. Der Anreiz dabei ist, dass Sie parallel im gleichen Cluster Volumes auf SSDs und HDDs erstellen können, die alle von NVMe beschleunigt werden. Die erste Option gleicht einer Bereitstellung, die ausschließlich Flash verwendet, während letztere Option einer oben beschriebenen hybriden Bereitstellung gleicht. Konzeptuell gleicht es einem System mit zwei Pools, dessen Kapazitätsmanagement, Fehler- und Reparaturzyklus usw. überwiegend unabhängig ist.

   >[!IMPORTANT]
   > Wir empfehlen die Verwendung der SSD-Ebene, um für Ihre leistungsabhängigsten Workloads eine reine Flash-Bereitstellung zu nutzen.

## Option 3 – Maximieren der Kapazität

Für Workloads, die eine große Kapazität erfordern und unregelmäßig schreiben, z.B. Archivierung, Sicherungsziele, Data Warehouses oder "kalter" Speicher, sollten Sie einige SSDs für die Zwischenspeicherung mit mehreren größeren HDDs kombinieren, um die Kapazität zu erhöhen.

![Bereitstellungsoptionen für das Maximieren der Kapazität-](media/choosing-drives-and-resiliency-types/maximizing-capacity.png)

1. **SSD + HDD**. SSDs speichern Lese- und Schreibvorgänge, um Datenverkehrsspitzen aufzufangen und eine SSD-ähnliche Leistung der Schreibvorgänge mit einer späteren optimierten Bereitstellung im HDD anzubieten.

>[!IMPORTANT]
>Konfiguration mit HDDs wird nur nicht unterstützt. Hohe Belastung SSDs-Zwischenspeicherung zu niedrig Belastung SSDs wird nicht empfohlen.

## Überlegungen zur Größe

### Cache

Jeder Server muss über mindestens zwei Cache-Laufwerke verfügen (die Mindestanforderungen für Redundanz). Wir empfehlen, dass die Anzahl der Kapazitätslaufwerke um ein Vielfaches der Anzahl der Cache-Laufwerke entspricht. Wenn Sie beispielsweise über vier Cachelaufwerke verfügen, ist die Leistung bei Verwendung von acht Kapazitätslaufwerken konsistenter (Verhältnis 1:2) als bei Verwendung von sieben oder neun Laufwerken.

Die Größe des Caches muss dem Arbeitssatz Ihrer Anwendungen und Workloads, d. h. alle Daten sie aktiv lesen und schreiben zu einem bestimmten Zeitpunkt entsprechend. Darüber hinaus gibt es keine Cachegrößenanforderung. Bei Bereitstellungen mit HDDs ein fairer Ausgangspunkt ist 10 % der Kapazität – z. B. verfügt jeder Server über 4 x 4 TB HDD = 16 TB Kapazität, 2 x 800 GB SSD = 1,6 TB Cache pro Server. Für reine Flash-Bereitstellungen, insbesondere bei sehr [hohe Belastung](https://blogs.technet.microsoft.com/filecab/2017/08/11/understanding-dwpd-tbw/) SSDs, kann es fair näher auf 5 % der Kapazität – z. B. gestartet werden, wenn jeder Server 24 x 1.2 TB SSD verfügt = 28,8 TB Kapazität, dann 2 x 750 GB NVMe = 1,5 TB Cache pro Server. Sie können zu einem späteren Zeitpunkt immer noch Cache-Laufwerke hinzufügen oder entfernen.

### Allgemein

Es wird empfohlen, die gesamte Speicherkapazität pro Server auf etwa 100 Terabytes (TB) zu beschränken. Je mehr Speicherkapazität pro Server existiert, desto länger dauert die Neusynchronisierung der Daten nach dem Herunterfahren des Systems oder nach einem Neustart wie z.B. beim Aktualisieren von Software.

Die aktuelle maximale Größe pro Speicherpool beträgt 1 Petabyte (PB) oder 1000 TB.

## Weitere Informationen

- [Direkte Speicherplätze – Übersicht](storage-spaces-direct-overview.md)
- [Verstehen des Caches in Direkte Speicherplätze](understand-the-cache.md)
- [Hardwareanforderungen für „Direkte Speicherplätze“](storage-spaces-direct-hardware-requirements.md)
- [Planen von Volumes in Direkte Speicherplätze](plan-volumes.md)
- [Fehlertoleranz und Speichereffizienz](storage-spaces-fault-tolerance.md)
