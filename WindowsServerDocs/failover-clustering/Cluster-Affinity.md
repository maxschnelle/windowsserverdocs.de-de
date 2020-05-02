---
title: Clusteraffinität
ms.prod: windows-server
manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.author: johnmar
ms.date: 03/07/2019
description: In diesem Artikel werden Failovercluster-Affinität und antiaffinitäts Stufen beschrieben
ms.openlocfilehash: b0c2209680f3c34ac8376d5662620595aff92c0b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720612"
---
# <a name="cluster-affinity"></a>Clusteraffinität

> Gilt für: Windows Server 2019, Windows Server 2016

Ein Failovercluster kann zahlreiche Rollen enthalten, die zwischen Knoten wechseln und ausgeführt werden können. Es gibt Zeiten, in denen bestimmte Rollen (z. b. virtuelle Computer, Ressourcengruppen usw.) nicht auf demselben Knoten ausgeführt werden dürfen.  Dies kann auf den Ressourcenverbrauch, die Arbeitsspeicher Auslastung usw. zurückzuführen sein.  Beispielsweise gibt es zwei virtuelle Computer, die Arbeitsspeicher und CPU-intensiv sind. wenn die beiden virtuellen Computer auf demselben Knoten ausgeführt werden, können sich auf einem oder beiden virtuellen Computern Probleme mit der Leistungs Beeinträchtigung ergeben.  In diesem Artikel werden die Cluster-antiaffinitäts Stufen und deren Verwendung erläutert.

## <a name="what-is-affinity-and-antiaffinity"></a>Was ist Affinität und antiaffinität?

Die Affinität ist eine Regel, die Sie einrichten, die eine Beziehung zwischen zwei oder mehr Rollen (i, e, Virtual Machines, Ressourcengruppen usw.) herstellt, um sie zusammenzuhalten.  Die antiaffinität ist identisch, wird jedoch verwendet, um zu versuchen, die angegebenen Rollen voneinander getrennt zu halten. Failovercluster verwenden die antiaffinität für Ihre Rollen.  Genauer gesagt, ist der [AntiAffinityClassNames](https://docs.microsoft.com/previous-versions/windows/desktop/mscs/groups-antiaffinityclassnames) -Parameter für die Rollen definiert, sodass Sie nicht auf demselben Knoten ausgeführt werden.  

## <a name="antiaffinityclassnames"></a>AntiAffinityClassnames

Wenn Sie sich die Eigenschaften einer Gruppe ansehen, gibt es den Parameter AntiAffinityClassNames, der Standardwert ist leer.  In den folgenden Beispielen sollten group1 und group2 von der Ausführung auf dem gleichen Knoten getrennt werden.  Zum Anzeigen der-Eigenschaft lauten der PowerShell-Befehl und das-Ergebnis wie folgt:

    PS> Get-ClusterGroup Group1 | fl AntiAffinityClassNames
    AntiAffinityClassNames : {}

    PS> Get-ClusterGroup Group2 | fl AntiAffinityClassNames
    AntiAffinityClassNames : {}

Da "AntiAffinityClassNames" nicht als Standard definiert ist, können diese Rollen gleichzeitig ausgeführt werden.  Das Ziel besteht darin, diese getrennt zu halten.  Der Wert für "AntiAffinityClassNames" kann der gewünschte Wert sein. Sie müssen lediglich identisch sein.  Das heißt, group1 und group2 sind Domänen Controller, die auf virtuellen Computern ausgeführt werden und am besten auf verschiedenen Knoten ausgeführt werden.  Da es sich hierbei um Domänen Controller handelt, verwende ich DC als Klassenname.  Um den Wert festzulegen, lauten der PowerShell-Befehl und die folgenden Ergebnisse:

    PS> $AntiAffinity = New-Object System.Collections.Specialized.StringCollection
    PS> $AntiAffinity.Add("DC")
    PS> (Get-ClusterGroup -Name "Group1").AntiAffinityClassNames = $AntiAffinity
    PS> (Get-ClusterGroup -Name "Group2").AntiAffinityClassNames = $AntiAffinity

    PS> Get-ClusterGroup "Group1" | fl AntiAffinityClassNames
    AntiAffinityClassNames : {DC}

    PS> Get-ClusterGroup "Group2" | fl AntiAffinityClassNames
    AntiAffinityClassNames : {DC}

Nachdem Sie festgelegt wurden, versucht das Failoverclustering, Sie zu trennen.  

Der antiaffinityclassname-Parameter ist ein "Soft"-Block.  Das heißt, es wird versucht, Sie zu trennen, aber wenn dies nicht möglich ist, können Sie es dennoch auf demselben Knoten ausführen.  Beispielsweise werden die Gruppen auf einem Failovercluster mit zwei Knoten ausgeführt.  Wenn ein Knoten für die Wartung Herunterfahren muss, bedeutet dies, dass beide Gruppen auf demselben Knoten ausgeführt werden.  In diesem Fall wäre es in Ordnung, dies zu tun.  Dies ist möglicherweise nicht die ideale, aber beide virtial Computer werden weiterhin in akzeptablen Leistungsbereichen ausgeführt.

## <a name="i-need-more"></a>Ich benötige weitere

Wie bereits erwähnt, ist AntiAffinityClassNames ein weicher Block.  Aber was ist, wenn eine harte Blockierung erforderlich ist?  Die virtuellen Maschinen können nicht auf demselben Knoten ausgeführt werden. Andernfalls treten Leistungseinbußen auf und bewirken, dass einige Dienste möglicherweise ausfallen.

In diesen Fällen ist eine zusätzliche Cluster Eigenschaft von clusterenforcedantiaffinität vorhanden.  Diese antiaffinitäts Ebene verhindert, dass alle gleichen AntiAffinityClassNames-Werte auf demselben Knoten ausgeführt werden.

Zum Anzeigen der Eigenschaft und des Werts lautet der PowerShell-Befehl (und das Ergebnis) wie folgt:

    PS> Get-Cluster | fl ClusterEnforcedAntiAffinity
    ClusterEnforcedAntiAffinity : 0

Der Wert "0" bedeutet, dass er deaktiviert ist und nicht erzwungen werden soll.  Der Wert "1" aktiviert dies und ist der feste Block.  Zum Aktivieren dieser festen Blockierung lautet der Befehl (und das Ergebnis) wie folgt:

    PS> (Get-Cluster).ClusterEnforcedAntiAffinity = 1
    ClusterEnforcedAntiAffinity : 1

Wenn beide festgelegt sind, wird verhindert, dass die Gruppe online geschaltet wird.  Wenn Sie sich auf demselben Knoten befinden, werden Sie in Failovercluster-Manager angezeigt.

![Cluster Affinität](media/Cluster-Affinity/Cluster-Affinity-1.png)

In einer PowerShell-Auflistung der Gruppen würden Sie Folgendes sehen:

    PS> Get-ClusterGroup

    Name       State
    ----       -----
    Group1     Offline(Anti-Affinity Conflict)
    Group2     Online

## <a name="additional-comments"></a>Zusätzliche Kommentare

- Stellen Sie sicher, dass Sie die richtige antiaffinitäts Einstellung abhängig von den Anforderungen verwenden.
- Beachten Sie, dass in einem Szenario mit zwei Knoten und clusterenforcedantiaffinität, wenn ein Knoten instand ist, beide Gruppen nicht ausgeführt werden.  

- Die Verwendung bevorzugter Besitzer für Gruppen kann mit der antiaffinität in einem Cluster mit drei oder mehr Knoten kombiniert werden.
- Die Einstellungen für "AntiAffinityClassNames" und "clusterenforcedantiaffinität" werden erst nach der Wiederverwendung der Ressourcen ausgeführt. Das heißt, Sie können diese festlegen, aber wenn beide Gruppen auf dem gleichen Knoten online sind, wenn Sie festgelegt sind, bleiben beide weiterhin online.
