---
ms.assetid: f0d4cecc-5a03-448c-bef9-86c4730b4eb0
title: VM-Netzwerklastenausgleich (Übersicht)
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: 125dd7421cc1876c07983016498a9689d8a507ac
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475987"
---
# <a name="virtual-machine-load-balancing-overview"></a>VM-Netzwerklastenausgleich (Übersicht)

> Gilt für: Windows Server 2019, Windows Server 2016

Eine wichtige Überlegung bei Bereitstellungen privater Clouds ist die Investitionen (<abbr title="Planungsrisiken">CapEx</abbr>) erforderlich, um in die Produktion gehen. Es kommt sehr häufig zum Hinzufügen von Redundanz für private cloudbereitstellungen unterdimensionierte Kapazität während der Datenverkehr zu Spitzenzeiten in der Produktion zu vermeiden, aber dies erhöht die <abbr title="Planungsrisiken">CapEx</abbr>. Die Notwendigkeit für höhere Redundanz hängt von unausgeglichenen privaten Clouds, in denen einige Knoten sind mehr virtuelle Computer hosten (<abbr title="virtuelle Computer">VMs</abbr>) und andere unterausgelasteter (z. B. einem Server wird gerade neu gestartet).

<strong>Überblick per Video</strong><br>(6 Minuten)<br>
> [!VIDEO https://channel9.msdn.com/Blogs/windowsserver/Virtual-Machine-Load-Balancing-in-Windows-Server-2016/player]

## <a id="what-is-vm-load-balancing"></a>Was ist die VM-Lastenausgleich?
<abbr title="virtuellen Computer">VM</abbr> Lastenausgleich ist ein integriertes Feature in Windows Server-2019 und Windows Server 2016, die Ihnen ermöglicht, die Auslastung von Knoten in einem Failovercluster zu optimieren. Es identifiziert überbelegt Knoten und neu verteilt <abbr title="virtuelle Computer">VMs</abbr> aus diesen Knoten zu Knoten committed-klicken Sie unter. Nachfolgend sind einige wichtige Aspekte dieses Features:

* *Es ist eine Lösung ohne Ausfallzeiten*: <abbr title="Virtuelle Computer">VMs</abbr> werden die auf Knoten im Leerlauf.
* *Nahtlose Integration in Ihre vorhandenen Clusterumgebung*: Fehler-Richtlinien wie z. B. Anti-Affinität, Fehler- und mögliche Besitzer werden berücksichtigt.
* *Die Heuristik für Lastenausgleich*: <abbr title="virtuellen Computer">VM</abbr> ungenügender Arbeitsspeicher und CPU-Auslastung des Knotens.
* *Eine präzise Kontrolle*: Standardmäßig aktiviert. Kann bei Bedarf oder in regelmäßigen Abständen aktiviert werden.
* *Aggressivität Schwellenwerte*: Drei Schwellenwerte verfügbaren basierend auf den Merkmalen Ihrer Bereitstellung.

## <a id="feature-in-action"></a>Das Feature in Aktion
### <a id="new-node-added"></a>Ein neuer Knoten wird dem Failovercluster hinzugefügt.
![Grafik zu der ein neuer Knoten des Failoverclusters hinzugefügt wird](media/vm-load-balancing/overview-VM-load-balancing-1.png)

Wenn Sie den Failovercluster, neue Kapazität hinzufügen der <abbr title="VM">VM</abbr> Lastenausgleichsfunktion gleicht automatisch die Kapazität von den vorhandenen Knoten, auf den neu hinzugefügten Knoten in der folgenden Reihenfolge:

1. Der Druck wird auf den vorhandenen Knoten im Failovercluster ausgewertet.
2. Alle Knoten, der Schwellenwert überschritten werden identifiziert.
3. Die Knoten mit der höchsten Auslastung werden identifiziert, um die Priorität des Lastenausgleichs zu bestimmen.
4. <abbr title="Virtuelle Computer">VMs</abbr> (ohne Downtime zu) von einem Knoten überschreiten Schwellenwert auf einen neu hinzugefügten Knoten im Failovercluster werden Live migriert.

### <a id="recurring-load-balancing"></a>Wiederholt den Lastenausgleich
![Grafik zu einer sich wiederholenden VM des Lastenausgleichs](media/vm-load-balancing/overview-VM-load-balancing-2.png)

Wenn für regelmäßige Lastenausgleich konfiguriert wird, wird der Druck auf den Clusterknoten für Lastenausgleich alle 30 Minuten ausgewertet. Alternativ können Sie können der Druck bedarfsgesteuert ausgewertet werden. So sieht der Ablauf der Schritte aus:

1. Der Druck wird auf allen Knoten in der privaten Cloud ausgewertet.
2. Alle Knoten überschreiten Schwellenwert und die darunter Schwellenwert werden identifiziert.
3. Die Knoten mit der höchsten Auslastung werden identifiziert, um die Priorität des Lastenausgleichs zu bestimmen.
4. <abbr title="Virtuelle Computer">VMs</abbr> (ohne Downtime zu) werden Live migriert, von einem Knoten, die der Schwellenwert zum Knoten unter minimaler Schwellenwert überschritten.

## <a name="see-also"></a>Siehe auch
* [VM-Lastenausgleich – ausführliche Informationen](vm-load-balancing-deep-dive.md)
* [Failoverclustering](failover-clustering-overview.md)
* [Hyper-V: Übersicht](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
