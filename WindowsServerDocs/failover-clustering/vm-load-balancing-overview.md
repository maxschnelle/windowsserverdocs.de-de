---
ms.assetid: f0d4cecc-5a03-448c-bef9-86c4730b4eb0
title: "Virtual Machine-Netzwerklastenausgleich (Übersicht)"
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: 0a106db25d476088898b914481e6041f20ce2e9e
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="virtual-machine-load-balancing-overview"></a>Virtual Machine-Netzwerklastenausgleich (Übersicht)

> Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Ein wichtiges Kriterium für die Bereitstellung der privaten Cloud ist das Kapitalausgaben (<abbr title="Kapitalausgaben">CapEx</abbr>) erforderlich, um in die Produktion gehen. Sehr häufig Redundanz für private cloudbereitstellungen Oberflächenbereich Kapazität bei der spitzenverkehrszeiten in der Produktion vermeiden hinzufügen, aber dies erhöht die <abbr title="Kapitalausgaben">CapEx</abbr>. Die Notwendigkeit von Redundanz über ausgeglichenen privaten Clouds, in denen einige Knoten mehr virtuelle Computer hosten, gesteuert (<abbr title="virtuelle Maschinen">VMs</abbr>) und andere sind nicht ausgelastet (z. B. einem Server neu neu gestartet wird).

## <a id="what-is-vm-load-balancing"></a>Was ist die VM-Lastenausgleich?
<abbr title="Virtuelle Maschine">VM</abbr> Lastenausgleich ist ein neues integriertes Feature in Windows Server 2016, mit dem Sie die Nutzung von Knoten in einem Failovercluster optimieren können. Es identifiziert überbelegt Knoten und erneut verteilt <abbr title="virtuelle Maschinen">VMs</abbr> aus diesen Knoten, klicken Sie unter zugesicherte Knoten. Einige der wichtigsten Aspekte dieser Funktion lauten wie folgt:

* *Dies ist eine Lösung ohne Ausfallzeiten*: <abbr title="virtuelle Maschinen">VMs</abbr> im Leerlauf Knoten live-migriert werden.
* *Nahtlose Integration in die vorhandene Clusterumgebung*: Fehler bei der Richtlinien wie z. B. antiaffinität, Fehlerdomänen und mögliche Besitzer berücksichtigt werden.
* *Mithilfe von Heuristik für Lastenausgleich*: <abbr title="virtuellen Computer">VM</abbr> ungenügenden Arbeitsspeicher und CPU-Auslastung des Knotens.
* *Präzisere Steuerung*: standardmäßig aktiviert. Kann bei Bedarf oder in regelmäßigen Intervallen aktiviert werden.
* *Aggressivität Schwellenwerte*: drei Schwellenwerte verfügbaren basierend auf den Merkmalen der Bereitstellung.

## <a id="feature-in-action"></a>Das Feature in Aktion
### <a id="new-node-added"></a>Den Failovercluster wird ein neuer Knoten hinzugefügt.
![Grafik eines neuen Knotens zum Failover Cluster hinzugefügt wird](media/vm-load-balancing/overview-VM-load-balancing-1.png)

Wenn Sie den Failovercluster, neue Kapazität hinzufügen der <abbr title="virtuellen Computer">VM</abbr> Lastenausgleich gleicht automatisch Kapazität von vorhandenen Knoten, auf den neu hinzugefügten Knoten in der folgenden Reihenfolge:

1. Der Druck auf die vorhandenen Knoten im Failovercluster ausgewertet.
2. Alle Knoten Schwellenwert überschreiten, werden identifiziert.
3. Die Knoten mit der höchsten Druck werden identifiziert, um die Priorität der Lastenausgleich zu bestimmen.
4. <abbr title="Virtuelle Computer">VMs</abbr> (ohne Ausfallzeiten) von einem Knoten kann der Schwellenwert für einen neu hinzugefügten Knoten im Failovercluster werden Live migriert.

### <a id="recurring-load-balancing"></a>Wiederholung des Netzwerklastenausgleichs
![Grafik für eine wiederholte VM-Lastenausgleich](media/vm-load-balancing/overview-VM-load-balancing-2.png)

Wenn für regelmäßiger Netzwerklastenausgleich konfiguriert sind, wird der Druck auf den Clusterknoten für alle 30 Minuten Lastenausgleich ausgewertet. Alternativ kann der Druck bei Bedarf ausgewertet. Hier ist der Fluss der Schritte aus:

1. Der Druck wird auf allen Knoten in der privaten Cloud bewertet.
2. Alle Knoten Schwellenwert und die darunter Schwellenwert überschreiten, werden identifiziert.
3. Die Knoten mit der höchsten Druck werden identifiziert, um die Priorität der Lastenausgleich zu bestimmen.
4. <abbr title="Virtuelle Computer">VMs</abbr> (ohne Ausfallzeiten) von einem Knoten kann der Schwellenwert zum Knoten unter Mindestschwellenwert werden Live migriert.

## <a name="see-also"></a>Siehe auch
* [VM-Lastenausgleich tiefer gehende](vm-load-balancing-deep-dive.md)
* [Failover-Clusterunterstützung](failover-clustering-overview.md)
* [Hyper-V (Übersicht)](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
