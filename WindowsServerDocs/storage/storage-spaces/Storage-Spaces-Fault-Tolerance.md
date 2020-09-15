---
title: Fehlertoleranz und Speichereffizienz in Direkte Speicherplätze
manager: eldenc
ms.topic: article
author: cosmosdarwin
ms.author: cosdar
ms.date: 10/11/2017
ms.assetid: 5e1d7ecc-e22e-467f-8142-bad6d82fc5d0
description: Enthält eine Beschreibung der Resilienzoptionen in „Direkte Speicherplätze“, einschließlich Spiegelung und Parität.
ms.localizationpriority: medium
ms.openlocfilehash: c6ef53927a1c6ed4e5275bc2412faa97510c024e
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90078507"
---
# <a name="fault-tolerance-and-storage-efficiency-in-storage-spaces-direct"></a>Fehlertoleranz und Speichereffizienz in Direkte Speicherplätze

>Gilt für: Windows Server 2016

In diesem Thema werden die in [direkte Speicherplätze](storage-spaces-direct-overview.md) verfügbaren resilienzoptionen vorgestellt und die Skalierungs Anforderungen, die Speichereffizienz sowie allgemeine Vorteile und Nachteile der einzelnen beschrieben. Darüber hinaus werden einige Nutzungshinweise gegeben, um Ihnen den Einstieg zu erleichtern, und es wird auf hilfreiche Dokumente, Blogs und Ressourcen mit weiteren Informationen verwiesen.

Falls Sie mit „Direkte Speicherplätze“ bereits vertraut sind, können Sie ggf. direkt mit dem Abschnitt [Zusammenfassung](#summary) fortfahren.

## <a name="overview"></a>Übersicht

Im Grunde geht es bei Speicherplätzen um die Bereitstellung von Fehlertoleranz, die häufig als "Resilienz" bezeichnet wird, für Ihre Daten. Die Implementierung ähnelt RAID, aber sie ist auf Server verteilt und wird per Software implementiert.

Wie auch bei RAID gibt es für „Direkte Speicherplätze“ verschiedene Möglichkeiten, dies zu erreichen. Es handelt sich jeweils um unterschiedliche Kompromisse in Bezug auf Fehlertoleranz, Speichereffizienz und Computekomplexität. Diese werden im Wesentlichen in zwei Kategorien unterteilt: "Spiegelung" und "Parität", letztere wird manchmal als "Erasure Coding" bezeichnet.

## <a name="mirroring"></a>Spiegelung

Die Spiegelung ermöglicht Fehlertoleranz, indem mehrere Kopien aller Daten aufbewahrt werden. Dies ähnelt am ehesten RAID-1. Das Striping und die Anordnung dieser Daten ist nicht trivial (weitere Informationen in [diesem Blog](https://techcommunity.microsoft.com/t5/storage-at-microsoft/deep-dive-the-storage-pool-in-storage-spaces-direct/ba-p/425959)), aber es lässt sich festhalten, dass alle per Spiegelung gespeicherten Daten vollständig mehrfach geschrieben werden. Jede Kopie wird auf andere physische Hardware (unterschiedliche Laufwerke von nicht identischen Servern) geschrieben, für die angenommen wird, dass sie nicht gemeinsam ausfallen.

In Windows Server 2016 bieten Speicherplätze zwei Arten von Spiegelung – "bidirektional" und "drei-Wege".

### <a name="two-way-mirror"></a>Zwei-Wege-Spiegelung

Bei der Zwei-Wege-Spiegelung werden jeweils zwei Kopien aller Daten geschrieben. Die Speichereffizienz ist 50 % – zum Schreiben von 1 TB an Daten benötigen Sie mindestens 2 TB physische Speicherkapazität. Darüber hinaus benötigen Sie mindestens zwei [Hardwarefehlerdomänen](../../failover-clustering/fault-domains.md). Bei „Direkte Speicherplätze“ bedeutet dies, dass zwei Server verwendet werden.

![Zwei-Wege-Spiegelung](media/Storage-Spaces-Fault-Tolerance/two-way-mirror-180px.png)

   >[!WARNING]
   > Wenn Sie über mehr als zwei Server verfügen, empfiehlt es sich, stattdessen den drei-Wege-Spiegelungen zu verwenden.

### <a name="three-way-mirror"></a>Drei-Wege-Spiegelung

Bei der Drei-Wege-Spiegelung werden jeweils drei Kopien aller Daten geschrieben. Die Speichereffizienz ist 33.3 % – zum Schreiben von 1 TB an Daten benötigen Sie mindestens 3 TB physische Speicherkapazität. Darüber hinaus benötigen Sie mindestens drei Hardwarefehlerdomänen. Bei „Direkte Speicherplätze“ bedeutet dies, dass drei Server verwendet werden.

Bei der Drei-Wege-Spiegelung können mindestens [zwei gleichzeitige Hardwareprobleme (Laufwerk oder Server)](#examples) problemlos toleriert werden. Wenn Sie beispielsweise einen Server neu starten und plötzlich ein anderes Laufwerk bzw. ein Server ausfällt, bleiben alle Daten geschützt und sind ohne Unterbrechung zugänglich.

![Drei-Wege-Spiegelung](media/Storage-Spaces-Fault-Tolerance/three-way-mirror-180px.png)

## <a name="parity"></a>Parität

Die Paritäts Codierung, oft als "Erasure Coding" bezeichnet, bietet Fehlertoleranz mithilfe bitweiser Arithmetik, die [erheblich kompliziert](https://www.microsoft.com/research/wp-content/uploads/2016/02/LRC12-cheng20webpage.pdf)werden kann. Die Funktionsweise ist hierbei weniger offensichtlich als bei der Spiegelung. Es sind viele hervorragende Onlineressourcen verfügbar (z. B. die [„Erasure Coding“-Anleitung für Anfänger](http://smahesh.com/blog/2012/07/01/dummies-guide-to-erasure-coding/) eines Drittanbieters), in denen die Grundlagen vermittelt werden. Kurz gesagt: Hierbei wird eine höhere Speichereffizienz ermöglicht, ohne dass dies zu Lasten der Fehlertoleranz geht.

In Windows Server 2016 bieten Speicherplätze zwei Arten von Parität – die Parität "Single" und "Dual", letztere verwendet ein erweitertes Verfahren mit dem Namen "local Reconstruction Codes" in größerem Maßstab.

> [!IMPORTANT]
> Wir empfehlen Ihnen für die meisten leistungsempfindlichen Workloads die Nutzung der Spiegelung. Weitere Informationen zum Abwägen zwischen Leistung und Kapazität je nach Workload finden Sie unter [Planen von Volumes](plan-volumes.md#choosing-the-resiliency-type).

### <a name="single-parity"></a>Einzelparität
Bei Einzelparität wird nur ein Symbol für bitweise Parität beibehalten, sodass nur Fehlertoleranz für jeweils einen Fehler vorhanden ist. Dies ähnelt am ehesten RAID-5. Für die Nutzung der Einzelparität benötigen Sie mindestens drei Hardwarefehlerdomänen. Bei „Direkte Speicherplätze“ bedeutet dies, dass drei Server verwendet werden. Da die Drei-Wege-Spiegelung bei gleichem Umfang eine höhere Fehlertoleranz ermöglicht, raten wir von der Nutzung der Einzelparität ab. Diese Option steht Ihnen aber offen, falls Sie dies möchten, und die Nutzung wird vollständig unterstützt.

   >[!WARNING]
   > Wir raten von der Einzelparität ab, da nur jeweils ein Hardwarefehler problemlos toleriert werden kann: Wenn Sie einen Server neu starten und plötzlich ein anderes Laufwerk oder ein anderer Server ausfällt, kommt es zu Ausfallzeit. Falls Sie nur drei Server haben, empfehlen wir Ihnen, die Drei-Wege-Spiegelung zu verwenden. Bei vier oder mehr helfen Ihnen die Informationen im nächsten Abschnitt weiter.

### <a name="dual-parity"></a>Duale Parität

Bei der dualen Parität werden Reed-Solomon-Fehlerkorrekturcodes implementiert, um zwei Symbole für bitweise Parität beizubehalten. So wird die gleiche Fehlertoleranz wie bei der Drei-Wege-Spiegelung ermöglicht (also bis zu zwei Fehler auf einmal), aber es wird eine höhere Speichereffizienz erzielt. Dies ähnelt am ehesten RAID-6. Für die Nutzung der dualen Parität benötigen Sie mindestens vier Hardwarefehlerdomänen. Bei „Direkte Speicherplätze“ bedeutet dies, dass vier Server verwendet werden. Auf dieser Ebene beträgt die Speichereffizienz 50 %. Zum Speichern von 2 TB an Daten benötigen Sie 4 TB an physischer Speicherkapazität.

![Duale Parität](media/Storage-Spaces-Fault-Tolerance/dual-parity-180px.png)

Die Speichereffizienz der dualen Parität steigt mit der Anzahl vorhandener Hardware-Fehlerdomänen von 50 % auf bis zu 80 %. Bei sieben Domänen (d. h. sieben Servern bei Direkte Speicherplätze) steigt die Effizienz auf 66,7 % – zum Speichern von 4 TB an Daten benötigen Sie nur 6 TB physische Speicherkapazität.

![Duale Parität (breit)](media/Storage-Spaces-Fault-Tolerance/dual-parity-wide-180px.png)

Informationen zur Effizienz von dualer Parität und „Local Reconstruction Codes“ für jeden Umfang finden Sie im Abschnitt [Zusammenfassung](#summary).

### <a name="local-reconstruction-codes"></a>Local Reconstruction Codes

Mithilfe von Speicherplätzen in Windows Server 2016 wird ein erweitertes Verfahren eingeführt, das von Microsoft Research entwickelt wurde, das als "local Reconstruction Codes" oder LRC bezeichnet wird. Bei größerem Umfang wird LRC für die duale Parität genutzt, um die Codierung bzw. Decodierung in kleinere Gruppen zu unterteilen. So soll der Mehraufwand reduziert werden, der mit Schreibvorgängen oder der Wiederherstellung nach Fehlern verbunden ist.

Bei Festplattenlaufwerken (HDDs) beträgt die Gruppengröße vier Symbole, und bei Solid State Drives (SSDs) sind es sechs Symbole. Hier ist beispielsweise angegeben, wie das Layout mit Festplattenlaufwerken und zwölf Hardwarefehlerdomänen (zwölf Server) aussieht. Es sind zwei Gruppen mit vier Datensymbolen vorhanden. Es wird eine Speichereffizienz von 72,7 % erzielt.

![Local Reconstruction Codes](media/Storage-Spaces-Fault-Tolerance/local-reconstruction-codes-180px.png)

Wir empfehlen Ihnen diese eingehende und dennoch gut lesbare Beschreibung zum [Umgang von Local Reconstruction Codes mit unterschiedlichen Fehlerszenarien und den Gründen für ihre Attraktivität](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) von unserem Mitarbeiter [Claus Joergensen](https://twitter.com/clausjor).

## <a name="mirror-accelerated-parity"></a>Parität mit Beschleunigung per Spiegelung

Ab Windows Server 2016 kann ein direkte Speicherplätze Volume Teil Spiegelung und Teil Parität sein. Schreibvorgänge landen zuerst im gespiegelten Teil und werden später dann allmählich in den Paritätsteil verschoben. Hierbei wird praktisch die [Spiegelung genutzt, um das Erasure Coding zu beschleunigen](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB).

Zum Mischen von Drei-Wege-Spiegelung und dualer Parität benötigen Sie mindestens vier Fehlerdomänen (also vier Server).

Die Speichereffizienz der Parität mit Beschleunigung per Spiegelung liegt zwischen den Ergebnissen, die Sie bei reiner Spiegelung und bei reiner Parität erzielen, und hängt von den gewählten Proportionen ab. Die Demo in Minute 37 dieser Präsentation zeigt z. B. [verschiedene Kombinationen, die eine Effizienz von 46 %, 54 % und 65 % Effizienz](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=36m55s) mit 12 Servern erzielen.

> [!IMPORTANT]
> Wir empfehlen Ihnen für die meisten leistungsempfindlichen Workloads die Nutzung der Spiegelung. Weitere Informationen zum Abwägen zwischen Leistung und Kapazität je nach Workload finden Sie unter [Planen von Volumes](plan-volumes.md#choosing-the-resiliency-type).

## <a name="summary"></a><a name="summary"></a>Zusammenfassung

In diesem Abschnitt sind die in „Direkte Speicherplätze“ verfügbaren Resilienztypen, die minimalen Skalierungsanforderungen der einzelnen Typen, die tolerierte Anzahl von Ausfällen pro Typ und die entsprechende Speichereffizienz zusammengefasst.

### <a name="resiliency-types"></a>Resilienztypen

|    Resilienz          |    Fehlertoleranz       |    Speichereffizienz      |
|------------------------|----------------------------|----------------------------|
|    Zwei-Wege-Spiegelung      |    1                       |    50,0 %                   |
|    Drei-Wege-Spiegelung    |    2                       |    33,3 %                   |
|    Duale Parität         |    2                       |    50,0 % bis 80,0 %           |
|    Mixed               |    2                       |    33,3 % bis 80,0 %           |

### <a name="minimum-scale-requirements"></a>Mindestanforderungen für die Skalierung

|    Resilienz          |    Mindestens erforderliche Fehlerdomänen   |
|------------------------|-------------------------------------|
|    Zwei-Wege-Spiegelung      |    2                                |
|    Drei-Wege-Spiegelung    |    3                                |
|    Duale Parität         |    4                                |
|    Mixed               |    4                                |

   >[!TIP]
   > Wenn Sie keine [Chassis- oder Rack-Fehlertoleranz](../../failover-clustering/fault-domains.md) verwenden, bezieht sich die Anzahl von Fehlerdomänen auf die Anzahl von Servern. Die Anzahl von Laufwerken auf jedem Server wirkt sich nicht darauf aus, welche Resilienztypen Sie verwenden können, solange Sie die Mindestanforderungen für „Direkte Speicherplätze“ erfüllen.

### <a name="dual-parity-efficiency-for-hybrid-deployments"></a>Effizienz der dualen Parität für Hybridbereitstellungen

In dieser Tabelle ist die Speichereffizienz der dualen Parität und Local Reconstruction Codes für verschiedene Umfänge von Hybridbereitstellungen angegeben, die sowohl Festplattenlaufwerke (HDDs) als auch Solid State Drives (SSDs) enthalten.

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

In dieser Tabelle ist die Speichereffizienz der dualen Parität und Local Reconstruction Codes für verschiedene Umfänge von reinen Flash-Bereitstellungen angegeben, die nur Solid State Drives (SSDs) enthalten. Für das Paritätslayout können größere Gruppen verwendet werden, und es kann eine bessere Speichereffizienz für eine reine Flash-Konfiguration erzielt werden.

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

## <a name="examples"></a><a name="examples"></a>Beispiele

Sofern Sie nicht nur über zwei Server verfügen, empfehlen wir Ihnen die Nutzung der Drei-Wege-Spiegelung bzw. der dualen Parität, weil diese Verfahren eine bessere Fehlertoleranz bieten. Vor allem wird dabei sichergestellt, dass alle Daten auch dann sicher und dauerhaft zugänglich bleiben, wenn zwei Fehlerdomänen – bei „Direkte Speicherplätze“ also zwei Server – von gleichzeitigen Ausfällen betroffen sind.

### <a name="examples-where-everything-stays-online"></a>Beispiele für den allgemeinen Erhalt des Onlinezustands

In diesen sechs Beispielen ist dargestellt, was bei der Drei-Wege-Spiegelung bzw. bei dualer Parität toleriert werden **kann**.

- **1.**    Ein Laufwerk ist ausgefallen (einschließlich der Cachelaufwerke)
- **2.**    Ein Server ist ausgefallen

![fault-tolerance-examples-1-and-2](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-12.png)

- **3.**    Ein Server und ein Laufwerk sind ausgefallen
- **4.**    Zwei Laufwerke auf unterschiedlichen Servern sind ausgefallen

![fault-tolerance-examples-3-and-4](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-34.png)

- **5.**    Mehr als zwei Laufwerke sind ausgefallen, sofern höchstens zwei Server betroffen sind
- **6.**    Zwei Server sind ausgefallen

![fault-tolerance-examples-5-and-6](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-56.png)

...in allen Fällen bleiben alle Volumes im Onlinezustand. (Stellen Sie sicher, dass das Quorum für Ihren Cluster erhalten bleibt.)

### <a name="examples-where-everything-goes-offline"></a>Beispiele für einen allgemeinen Wechsel in den Offlinezustand

Während der Lebensdauer von „Speicherplätze“ kann das Feature eine beliebige Anzahl von Ausfällen tolerieren, weil nach jedem Ausfall die vollständige Resilienz wiederhergestellt wird – sofern dafür genügend Zeit ist. Es dürfen aber jeweils nur maximal zwei Fehlerdomänen von Ausfällen betroffen sein. Unten sind also Beispiele dafür aufgeführt, was bei der Drei-Wege-Spiegelung bzw. der dualen Parität **nicht** tolerierbar ist.

- **7.** Ausfall von Laufwerken auf drei oder mehr Servern gleichzeitig
- **8.** Ausfall von drei oder mehr Servern gleichzeitig

![fault-tolerance-examples-7-and-8](media/Storage-Spaces-Fault-Tolerance/Fault-Tolerance-Example-78.png)

## <a name="usage"></a>Verwendung

Weitere Informationen finden Sie [unter Erstellen von Volumes in direkte Speicherplätze](create-volumes.md).

## <a name="additional-references"></a>Weitere Verweise

Alle folgenden Links sind inline im Text dieses Themas vorhanden.

- [Direkte Speicherplätze in Windows Server 2016](storage-spaces-direct-overview.md)
- [Fehler Domänen Bewusstsein in Windows Server 2016](../../failover-clustering/fault-domains.md)
- [Erasure Coding in Azure von Microsoft Research](https://www.microsoft.com/research/publication/erasure-coding-in-windows-azure-storage/)
- [Local Reconstruction Codes und Beschleunigung von Paritätsvolumes](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)
- [Volumes in der Speicherverwaltungs-API](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)
- [Demo zur Speichereffizienz bei der Microsoft Ignite 2016](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=36m55s)
- [Capacity Calculator (Vorschau) für „Direkte Speicherplätze“](https://aka.ms/s2dcalc)
