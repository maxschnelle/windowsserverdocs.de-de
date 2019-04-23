---
title: Fehlertoleranz und Speichereffizienz in Direkte Speicherplätze
ms.prod: windows-server-threshold
ms.author: cosmosdarwin
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 10/11/2017
ms.assetid: 5e1d7ecc-e22e-467f-8142-bad6d82fc5d0
description: Eine Erläuterung der Resilienzoptionen in Direkte Speicherplätze, einschließlich Spiegelung und Parität.
ms.localizationpriority: medium
ms.openlocfilehash: 4e6a29e82a85ec9570cda827060dfe1cdf192c53
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849571"
---
# <a name="fault-tolerance-and-storage-efficiency-in-storage-spaces-direct"></a>Fehlertoleranz und Speichereffizienz in Direkte Speicherplätze

>Gilt für: Windows Server 2016

In diesem Thema werden die in [Direkte Speicherplätze](storage-spaces-direct-overview.md) verfügbaren Resilienzoptionen vorgestellt und die Skalierungsanforderungen, Speichereffizienz sowie allgemeine Vorteile und Nachteile der einzelnen Optionen beschrieben. Außerdem finden Sie einige Anweisungen zur Verwendung, um Ihnen den Einstieg erleichtern, sowie Verweise auf einige hilfreiche Dokumente, Blogs und weitere Inhalte, mit denen Sie sich informieren können.

Falls Sie bereits mit Speicherplätzen vertraut sind, können Sie mit dem Abschnitt [Zusammenfassung](#summary) fortfahren.

## <a name="overview"></a>Übersicht

Im Wesentlichen dienen Speicherplätze zur Bereitstellung von Fehlertoleranz – häufig als „Resilienz“ bezeichnet – für Ihre Daten. Die Implementierung erfolgt ähnlich wie bei RAID, allerdings verteilt über mehrere Server und in Software implementiert.

Wie bei RAID gibt es auch für Speicherplätze verschiedene Implementierungsmethoden, bei denen jeweils unterschiedliche Kompromisse zwischen Fehlertoleranz, Speichereffizienz und rechnerischer Komplexität gelten. Diese lassen sich grob in zwei Kategorien unterteilen: „Spiegelung“ und „Parität“. Die zweite Option wird auch als „Erasure Coding“ bezeichnet.

## <a name="mirroring"></a>Spiegelung

Die Spiegelung erzielt Fehlertoleranz durch das Beibehalten mehrerer Kopien aller Daten. Diese Methode ist am ehesten mit RAID-1 vergleichbar. Die Aufteilung in Stripesets und Platzierung von Daten ist nicht trivial (siehe Informationen in [diesem Blog](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/)), grundsätzlich gilt jedoch, dass alle gespeicherten Daten, für die Spiegelung verwendet wird, mehrmals vollständig geschrieben werden. Jede Kopie wird auf eine andere physische Hardwarekomponente (unterschiedliche Laufwerke auf unterschiedlichen Servern) geschrieben, bei denen davon ausgegangen wird, dass sie unabhängig voneinander ausfallen.

Unter Windows Server 2016 bieten Speicherplätze zwei Arten von Spiegelung: „Zwei-Wege“ und „Drei-Wege“.

### <a name="two-way-mirror"></a>Zwei-Wege-Spiegelung

Die Zwei-Wege-Spiegelung schreibt zwei Kopien aller Elemente. Die Speichereffizienz ist 50 % – zum Schreiben von 1 TB an Daten benötigen Sie mindestens 2 TB physische Speicherkapazität. Ebenso benötigen Sie mindestens zwei [Hardware-„Fehlerdomänen“](../../failover-clustering/fault-domains.md) – bei Direkte Speicherplätze bedeutet das zwei Server.

![Zwei-Wege-Spiegelung](media/Storage-Spaces-Fault-Tolerance/two-way-mirror-180px.png)

   >[!WARNING]
   > Wenn Sie mehr als zwei Server haben, empfehlen wir stattdessen die Drei-Wege-Spiegelung.

### <a name="three-way-mirror"></a>Drei-Wege-Spiegelung

Die Drei-Wege-Spiegelung schreibt drei Kopien aller Elemente. Die Speichereffizienz ist 33.3 % – zum Schreiben von 1 TB an Daten benötigen Sie mindestens 3 TB physische Speicherkapazität. Ebenso benötigen Sie mindestens drei Hardware-Fehlerdomänen – bei Direkte Speicherplätze bedeutet das drei Server.

Die Dreiwegespiegelung kann [mindestens zwei gleichzeitige Hardwareprobleme (Laufwerk oder Server) sicher tolerieren](#examples). Beispiel: Wenn Sie einen Server neu starten und plötzlich ein anderes Laufwerk oder ein anderer Server ausfällt, bleiben alle Daten sicher und kontinuierlich zugänglich.

![Drei-Wege-Spiegelung](media/Storage-Spaces-Fault-Tolerance/three-way-mirror-180px.png)

## <a name="parity"></a>Parität

Die Paritätscodierung, häufig auch als „Erasure Coding“ bezeichnet, erzielt Fehlertoleranz durch bitweise arithmetische Operationen, die [außerordentlich kompliziert](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/LRC12-cheng20webpage.pdf) sein können. Die Funktionsweise ist weniger offensichtlich als bei der Spiegelung, und es gibt viele hilfreiche Onlineressourcen (z. B. das Dokument [Dummies Guide to Erasure Coding](http://smahesh.com/blog/2012/07/01/dummies-guide-to-erasure-coding/) eines Drittanbieter), die Ihnen einen Eindruck davon vermitteln. Hervorzuheben ist lediglich, dass diese Methode eine bessere Speichereffizienz bietet, ohne die Fehlertoleranz zu beeinträchtigen.

In Windows Server 2016 bieten Speicherplätze zwei Arten von Parität – „Einzelparität“ und „duale Parität“. Die zweite Option verwendet bei umfangreicheren Vorgängen ein fortgeschrittenes Verfahren, das als „Code für die lokale Wiederherstellung“ bezeichnet wird.

> [!IMPORTANT]
> Es wird empfohlen, für die meisten leistungsabhängigen Arbeitslasten eine Spiegelung zu verwenden. Weitere Informationen zum Ausgleich der Leistung und Kapazität je nach Ihrer Workload finden Sie unter [Volumes planen](plan-volumes.md#choosing-the-resiliency-type).

### <a name="single-parity"></a>Einzelparität
Die Einzelparität behält nur ein bitweises Paritätssymbol bei, das nur Fehlertoleranz für jeweils einen Ausfall bereitstellt. Diese Methode ist am ehesten mit RAID-5 vergleichbar. Zur Verwendung der Einzelparität benötigen Sie mindestens drei Hardware-Fehlerdomänen – bei Direkte Speicherplätze bedeutet das drei Server. Da die Drei-Wege-Spiegelung mehr Fehlertoleranz im selben Maßstab bereitstellt, wird von der Verwendung einer Einzelparität abgeraten. Falls Sie diese Option dennoch verwenden möchten, ist sie verfügbar und wird vollständig unterstützt.

   >[!WARNING]
   > Es wird davon abgeraten, einzelne Parität zu verwenden, da sie nur jeweils einen Hardwarefehler sicher tolerieren kann: Wenn Sie einen Server neu starten und plötzlich ein anderes Laufwerk oder ein anderer Server ausfällt, werden Ausfallzeiten auftreten. Wenn Sie nur über drei Server verfügen, wird die Drei-Wege-Spiegelung empfohlen. Wenn Sie mindestens vier Server haben, lesen Sie im nächsten Abschnitt weiter.

### <a name="dual-parity"></a>Duale Parität

Die duale Parität implementiert Reed-Solomon-Codes zur Fehlerkorrektur, um zwei bitweise Paritätssymbole beizubehalten. So stellen Sie dieselbe Fehlertoleranz wie die Drei-Wege-Spiegelung (d. h. für bis zu zwei gleichzeitige Ausfälle), jedoch mit besserer Speichereffizienz bereit. Diese Methode ist am ehesten mit RAID-6 vergleichbar. Zur Verwendung der dualen Parität benötigen Sie mindestens vier Hardware-Fehlerdomänen – bei Direkte Speicherplätze bedeutet das vier Server. In diesem Umfange beträgt die Speichereffizienz 50 % – zum Speichern von 2 TB an Daten benötigen Sie mindestens 4 TB physische Speicherkapazität.

![dual-parity](media/Storage-Spaces-Fault-Tolerance/dual-parity-180px.png)

Die Speichereffizienz der dualen Parität steigt mit der Anzahl vorhandener Hardware-Fehlerdomänen von 50 % auf bis zu 80 %. Bei sieben Domänen (d. h. sieben Servern bei Direkte Speicherplätze) steigt die Effizienz auf 66,7 % – zum Speichern von 4 TB an Daten benötigen Sie nur 6 TB physische Speicherkapazität.

![dual-parity-wide](media/Storage-Spaces-Fault-Tolerance/dual-parity-wide-180px.png)

Im Abschnitt [Zusammenfassung](#summary) finden Sie Informationen zur Effizienz der dualen Parität und von Codes für die lokale Wiederherstellung in jeder Größenordnung.

### <a name="local-reconstruction-codes"></a>Codes für die lokale Wiederherstellung

Für Speicherplätze unter Windows Server 2016 wird eine fortgeschrittene Technik eingeführt, die von Microsoft Research entwickelt wurde und als „Codes für die lokale Wiederherstellung“ bzw. LRC (Local Reconstruction Codes) bezeichnet wird. Bei umfangreichen Vorgängen verwendet die duale Parität LRC, um ihre Codierung/Decodierung in einige kleinere Gruppen aufzuteilen, sodass der Aufwand für Schreibvorgänge oder Wiederherstellungen nach Ausfällen reduziert wird.

Bei Festplattenlaufwerken (HDDs) umfasst eine Gruppe vier Symbole, und bei Festkörperlaufwerken (SSDs) umfasst eine Gruppe sechs Symbole. Beispiel: Hier sehen Sie das Layout bei Festplattenlaufwerken und 12 Hardware-Fehlerdomänen (also 12 Server). Es sind zwei Gruppen mit je vier Datensymbolen vorhanden. Es wird eine Speichereffizienz von 72,7 % erzielt.

![local-reconstruction-codes](media/Storage-Spaces-Fault-Tolerance/local-reconstruction-codes-180px.png)

Wir empfehlen diese detaillierte aber sehr gut lesbare exemplarische Vorgehensweise zur[Handhabung verschiedener Fehlerszenarien durch Codes für die lokale Wiederherstellung und deren Vorteile](https://blogs.technet.microsoft.com/filecab/2016/09/06/volume-resiliency-and-efficiency-in-storage-spaces-direct/) unseres Mitarbeiters [Claus Joergensen](https://twitter.com/clausjor).

## <a name="mirror-accelerated-parity"></a>Durch Spiegelung beschleunigte Parität

Ab Windows Server 2016 kann für ein Direkte Speicherplätze-Volume sowohl Spiegelung als auch Parität eingesetzt werden. Schreibvorgänge werden zuerst im gespiegelten Bereich platziert und später schrittweise in den Paritätsbereich verschoben. Im Grunde ist dies [die Verwendung der Spiegelung zum Beschleunigen von Erasure Coding](https://blogs.technet.microsoft.com/filecab/2016/09/06/volume-resiliency-and-efficiency-in-storage-spaces-direct/).

Für die Kombination aus Drei-Wege-Spiegelung und dualer Parität benötigen Sie mindestens vier Fehlerdomänen, d. h. vier Server.

Die Speichereffizienz einer durch Spiegelung beschleunigten Parität liegt zwischen den Ergebnissen, die Sie nur mit Spiegelung oder nur mit Parität erzielen würden, und hängt von den gewählten Proportionen ab. Die Demo in Minute 37 dieser Präsentation zeigt z. B. [verschiedene Kombinationen, die eine Effizienz von 46 %, 54 % und 65 % Effizienz](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=36m55s) mit 12 Servern erzielen.

> [!IMPORTANT]
> Es wird empfohlen, für die meisten leistungsabhängigen Arbeitslasten eine Spiegelung zu verwenden. Weitere Informationen zum Ausgleich der Leistung und Kapazität je nach Ihrer Workload finden Sie unter [Volumes planen](plan-volumes.md#choosing-the-resiliency-type).

## <a name="summary"></a>Zusammenfassung

Dieser Abschnitt enthält die in „Direkte Speicherplätze“ verfügbaren Resilienztypen, die Mindestanforderungen für die Skalierung bei Verwendung der einzelnen Typen, die Anzahl von tolerierbaren Fehlern pro Typ und die entsprechende Speichereffizienz.

### <a name="resiliency-types"></a>Resilienztypen

|    Resilienz          |    Fehlertoleranz       |    Speichereffizienz      |
|------------------------|----------------------------|----------------------------|
|    Zwei-Wege-Spiegelung      |    1                       |    50,0 %                   |
|    Drei-Wege-Spiegelung    |    2                       |    33,3 %                   |
|    Duale Parität         |    2                       |    50,0 % - 80,0 %           |
|    Gemischt               |    2                       |    33,3 % - 80,0 %           |

### <a name="minimum-scale-requirements"></a>Mindestanforderungen für Skalierung

|    Resilienz          |    Mindestens erforderliche Fehlerdomänen   |
|------------------------|-------------------------------------|
|    Zwei-Wege-Spiegelung      |    2                                |
|    Drei-Wege-Spiegelung    |    3                                |
|    Duale Parität         |    4                                |
|    Gemischt               |    4                                |

   >[!TIP]
   > Sofern Sie nicht die [Gehäuse- oder Rackfehlertoleranz](../../failover-clustering/fault-domains.md) verwenden, bezieht sich die Anzahl von Fehlerdomänen auf die Anzahl von Servern. Die Anzahl von Laufwerken auf jedem Server hat keine Auswirkung darauf, welche Resilienztypen Sie verwenden können, solange Sie die Mindestanforderungen für „Direkte Speicherplätze“ erfüllen. 

### <a name="dual-parity-efficiency-for-hybrid-deployments"></a>Effizienz der dualen Parität für Hybridbereitstellungen

In dieser Tabelle sind die Speichereffizienz der dualen Parität und die Codes für die lokale Wiederherstellung in jeder Größenordnung für Hybridbereitstellungen mit Festplattenlaufwerken (HDDs) und Festkörperlaufwerken (SSDs) angegeben.

|    Fehlerdomänen      |    Layout           |    Effizienz   |
|-----------------------|---------------------|-----------------|
|    2                  |    –                |    –            |
|    3                  |    –                |    –            |
|    4                  |    RS 2+2           |    50,0 %        |
|    5                  |    RS 2+2           |    50,0 %        |
|    6                  |    RS 2+2           |    50,0 %        |
|    7                  |    RS 4+2           |    66,7 %        |
|    8                  |    RS 4+2           |    66,7 %        |
|    9                  |    RS 4+2           |    66,7 %        |
|    10                 |    RS 4+2           |    66,7 %        |
|    11                 |    RS 4+2           |    66,7 %        |
|    12                 |    LRC (8, 2, 1)    |    72,7 %        |
|    13                 |    LRC (8, 2, 1)    |    72,7 %        |
|    14                 |    LRC (8, 2, 1)    |    72,7 %        |
|    15                 |    LRC (8, 2, 1)    |    72,7 %        |
|    16                 |    LRC (8, 2, 1)    |    72,7 %        |

### <a name="dual-parity-efficiency-for-all-flash-deployments"></a>Effizienz der dualen Parität für reine Flash-Bereitstellungen

In dieser Tabelle sind die Speichereffizienz der dualen Parität und die Codes für die lokale Wiederherstellung in jeder Größenordnung für reine Flash-Bereitstellungen mit Festkörperlaufwerken (SSDs) angegeben. Für das Paritätslayout können höhere Gruppengrößen verwendet werden, und für eine reine Flash-Konfiguration kann eine bessere Speichereffizienz erzielt werden.

|    Fehlerdomänen      |    Layout           |    Effizienz   |
|-----------------------|---------------------|-----------------|
|    2                  |    –                |    –            |
|    3                  |    –                |    –            |
|    4                  |    RS 2+2           |    50,0 %        |
|    5                  |    RS 2+2           |    50,0 %        |
|    6                  |    RS 2+2           |    50,0 %        |
|    7                  |    RS 4+2           |    66,7 %        |
|    8                  |    RS 4+2           |    66,7 %        |
|    9                  |    RS 6+2           |    75,0 %        |
|    10                 |    RS 6+2           |    75,0 %        |
|    11                 |    RS 6+2           |    75,0 %        |
|    12                 |    RS 6+2           |    75,0 %        |
|    13                 |    RS 6+2           |    75,0 %        |
|    14                 |    RS 6+2           |    75,0 %        |
|    15                 |    RS 6+2           |    75,0 %        |
|    16                 |    LRC (12, 2, 1)   |    80,0 %        |

## <a name="examples"></a>Beispiele für

Sofern Sie nicht nur zwei Server verwenden, empfehlen wir Ihnen die Nutzung der Drei-Wege-Spiegelung bzw. der dualen Parität, weil dies eine bessere Fehlertoleranz ermöglicht. Es wird sichergestellt, dass alle Daten auch dann sicher und ständig verfügbar sind, wenn zwei Fehlerdomänen – bei „Direkte Speicherplätze“ also zwei Server – von gleichzeitigen Ausfällen betroffen sind.

### <a name="examples-where-everything-stays-online"></a>Beispiele für Fälle, in denen alle Komponenten online bleiben

Diese sechs Beispiele verdeutlichen, was bei der Drei-Wege-Spiegelung bzw. der dualen Parität toleriert werden **kann**.

- **1.**    Ein Laufwerk verloren geht (einschließlich Cachelaufwerken)
- **2.**    Ein Server, die verloren gehen

![fault-tolerance-examples-1-and-2](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-12.png)

- **3.**    Ein Server und ein Laufwerk verloren.
- **4.**    Zwei Laufwerke verloren gehen in unterschiedlichen-Servern

![fault-tolerance-examples-3-and-4](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-34.png)

- **5.**    Mehr als zwei Laufwerke verloren, sofern höchstens zwei Server betroffen sind
- **6.**    Zwei Server, die verloren gehen

![fault-tolerance-examples-5-and-6](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-56.png)

In all diesen Fällen bleiben alle Volumes online. (Stellen Sie sicher, dass für Ihren Cluster das Quorum beibehalten wird.)

### <a name="examples-where-everything-goes-offline"></a>Beispiele, in denen alles offline geschaltet wird

Während ihrer gesamten Lebensdauer können Speicherplätze eine beliebige Anzahl von Ausfällen tolerieren, da die Resilienz nach jedem Ausfall vollständig wiederhergestellt wird, sofern genügend Zeit ist. Es können aber jeweils nur maximal zwei Fehlerdomänen von einem Fehler betroffen sein, ohne dass es zu Problemen kommt. Daher sind hier Beispiele dafür angegeben, was bei der Drei-Wege-Spiegelung bzw. der dualen Parität toleriert werden **kann**.

- **7.** Laufwerke gleichzeitig in drei oder mehr Servern verloren
- **8.** Drei oder mehr Servern auf einmal verloren.

![fault-tolerance-examples-7-and-8](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-78.png)

## <a name="usage"></a>Verwendung

Sehen Sie sich [Erstellen von Volumes in direkten Speicherplätzen](create-volumes.md) an.

## <a name="see-also"></a>Siehe auch

Alle folgenden Links sind inline im Text dieses Themas vorhanden.

- ["Direkte Speicherplätze" unter WindowsServer 2016](storage-spaces-direct-overview.md)
- [Fehlerdomänenunterstützung in WindowsServer 2016](../../failover-clustering/fault-domains.md)
- [Erasure Coding in Azure von Microsoft Research](https://www.microsoft.com/en-us/research/publication/erasure-coding-in-windows-azure-storage/)
- [Lokale Code und schnellere Paritätsvolumes](https://blogs.technet.microsoft.com/filecab/2016/09/06/volume-resiliency-and-efficiency-in-storage-spaces-direct/)
- [Volumes in der Speicherverwaltungs-API](https://blogs.technet.microsoft.com/filecab/2016/08/29/deep-dive-volumes-in-spaces-direct/)
- [Storage Effizienz Demo bei Microsoft Ignite 2016](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=36m55s)
- [Capacity-Rechner-Vorschau für den Speicher "direkte Speicherplätze"](http://aka.ms/s2dcalc)
