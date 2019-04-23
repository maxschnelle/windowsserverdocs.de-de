---
title: Cluster-AntiAffinity
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 03/07/2019
description: Dieser Artikel beschreibt die Failover-Cluster AntiAffinity Ebenen
ms.openlocfilehash: 0e7511aa4305e09a1e895a4f8f4ec120079733b7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857201"
---
# <a name="cluster-affinity"></a>Cluster-Affinität

> Gilt für: Windows Server 2019, Windows Server 2016

Ein Failovercluster kann zahlreiche Rollen enthalten, die zwischen den Knoten zu verschieben und ausführen können.  Es gibt Situationen, wann bestimmte Rollen (d. h. virtuelle Computer, Ressourcengruppen, usw.) nicht auf demselben Knoten ausgeführt werden soll.  Möglicherweise liegt Ressourcenverbrauch, arbeitsspeicherauslastung usw.  Beispielsweise stehen zwei virtuellen Maschinen, die Arbeitsspeicher- und CPU-intensiv sind, und wenn die beiden virtuellen Computer auf demselben Knoten ausgeführt werden, eine oder beide der virtuellen Computer möglicherweise Auswirkungen auf Leistungsprobleme.  In diesem Artikel wird erläutert, cluster antiaffinity Ebenen und wie Sie sie verwenden können.

## <a name="what-is-affinity-and-antiaffinity"></a>Was ist die Affinität und AntiAffinity?

Affinität ist eine Regel, die Sie eingerichtet werden, die eine Beziehung zwischen mindestens zwei Rollen (i, e, virtuelle Computer, Ressourcengruppen, usw.), werden zusammen aufzubewahren, herstellt.  AntiAffinity ist identisch, aber es wird verwendet, um das Testen und die angegebenen Rollen getrennt halten.  Failovercluster werden AntiAffinity für die Rollen verwenden.  Genauer gesagt die ["AntiAffinityClassNames"](https://docs.microsoft.com/previous-versions/windows/desktop/mscs/groups-antiaffinityclassnames) Parameter für die Rollen definiert wurden, sodass sie nicht auf demselben Knoten ausgeführt werden.  

## <a name="antiaffinityclassnames"></a>AntiAffinityClassnames

Wenn Sie die Eigenschaften einer Gruppe zu suchen, die Parameter "AntiAffinityClassNames" vorhanden ist, und es ist standardmäßig leer.  In den folgenden Beispielen müssen Gruppe1 und Gruppe2 getrennt werden, auf dem gleichen Knoten ausgeführt.  Um die Eigenschaft anzuzeigen, wäre die PowerShell-Befehl und das Ergebnis:

    PS> Get-ClusterGroup Group1 | fl AntiAffinityClassNames
    AntiAffinityClassNames : {}

    PS> Get-ClusterGroup Group2 | fl AntiAffinityClassNames
    AntiAffinityClassNames : {}

Da "AntiAffinityClassNames" können diese Rollen zusammen ausgeführt werden oder voneinander entfernt sind standardmäßig nicht definiert sind.  Ziel ist es, halten Sie sie getrennt werden.  Der Wert für "AntiAffinityClassNames" können sie beliebig sein, müssen sie nur identisch sein.  Angenommen Sie, dass Gruppe1 und Gruppe2 sind Domänencontroller, die auf virtuellen Computern ausgeführt, und sie am besten bereitgestellt werden würden, die auf verschiedenen Knoten ausgeführt.  Da dieser Domänencontroller sind, werde ich DC für den Namen der Klasse verwenden.  Um den Wert festzulegen, wäre die PowerShell-Befehl und die Ergebnisse:

    PS> $AntiAffinity = New-Object System.Collections.Specialized.StringCollection
    PS> $AntiAffinity.Add("DC")
    PS> (Get-ClusterGroup -Name "Group1").AntiAffinityClassNames = $AntiAffinity
    PS> (Get-ClusterGroup -Name "Group2").AntiAffinityClassNames = $AntiAffinity

    PS> Get-ClusterGroup "Group1" | fl AntiAffinityClassNames
    AntiAffinityClassNames : {DC}

    PS> Get-ClusterGroup "Group2" | fl AntiAffinityClassNames
    AntiAffinityClassNames : {DC}

Nun, da sie festgelegt wurden, versucht die Failover-Clusterunterstützung auseinander halten.  

Der AntiAffinityClassName-Parameter ist ein "soft" Block.  Dies bedeutet, es wird versucht, diese auseinander zu halten, aber nicht, sie können trotzdem auf demselben Knoten ausgeführt.  Beispielsweise werden die Gruppen auf einem Failovercluster mit zwei Knoten ausgeführt.  Wenn ein Knoten für die Wartung ausfallen muss, würde dies bedeuten, dass beide Gruppen auf demselben Knoten ausgeführt werden würde.  In diesem Fall wäre es kein Problem haben.  Er möglicherweise nicht in die ideale, aber beide Computer Virtial werden noch ausgeführt wird, innerhalb der Bereiche für eine akzeptable Leistung.

## <a name="i-need-more"></a>Ich benötige weitere

Wie bereits erwähnt, ist "AntiAffinityClassNames" ein soft Block.  Aber was geschieht, wenn ein hard Block wird benötigt?  Die virtuellen Computer kann nicht ausgeführt werden, auf die er denselben Knoten Auswirkungen auf die Leistung wird andernfalls auftreten und dazu führen, dass einige Dienste möglicherweise ausfällt.

Für diese Fälle ist eine zusätzliche Clustereigenschaft des ClusterEnforcedAntiAffinity vorhanden.  Derartige antiaffinity um jeden Preis eines dieselben Werte für "AntiAffinityClassNames" verhindert, dass auf dem gleichen Knoten ausgeführt wird.

Zum Anzeigen der Eigenschaft und Wert wäre die PowerShell-Befehl (und das Ergebnis):

    PS> Get-Cluster | fl ClusterEnforcedAntiAffinity
    ClusterEnforcedAntiAffinity : 0

Der Wert "0" bedeutet, dass er deaktiviert ist, und nicht erzwungen werden.  Der Wert "1" aktiviert und ist die feste.  Um diesen festen Block zu aktivieren, werden der Befehl (und Ergebnis):

    PS> (Get-Cluster).ClusterEnforcedAntiAffinity = 1
    ClusterEnforcedAntiAffinity : 1

Wenn beide Werte festgelegt sind, werden die Gruppe daran gehindert, neue online zusammen.  Wenn sie sich auf demselben Knoten befinden, ist dies an, was Sie im Failovercluster-Manager sehen würden.

![Cluster-Affinität](media\Cluster-Affinity\Cluster-Affinity-1.png)

In einer PowerShell-Auflistung der Gruppen, wird Folgendes angezeigt:

    PS> Get-ClusterGroup

    Name       State
    ----       -----
    Group1     Offline(Anti-Affinity Conflict)
    Group2     Online

## <a name="additional-comments"></a>Zusätzliche Kommentare

- Stellen Sie sicher, dass Sie die richtige AntiAffinity Einstellung je nach den Anforderungen verwenden.
- Beachten Sie, dass in einem Szenario zwei Knoten und ClusterEnforcedAntiAffinity, wenn ein Knoten nach unten, beide Gruppen wird nicht ausgeführt werden.  

- Die Verwendung der bevorzugten Besitzer für Gruppen kann in einem Cluster mit drei oder mehr Knoten mit AntiAffinity kombiniert werden.
- Die Einstellungen für "AntiAffinityClassNames" und ClusterEnforcedAntiAffinity nur, erfolgt nachdem eine Wiederverwendung von Ressourcen. D. H. Sie können sie festlegen, aber Sie sind, wenn beide Gruppen auf demselben Knoten online. Wenn festgelegt, sie beide weiterhin online bleiben.



