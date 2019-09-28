---
ms.assetid: f0d4cecc-5a03-448c-bef9-86c4730b4eb0
title: Übersicht über den Lastenausgleich virtueller Computer
ms.prod: windows-server
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: 1fea9e6297399a5081eb8fef1876f1b11d23c745
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360979"
---
# <a name="virtual-machine-load-balancing-overview"></a>Übersicht über den Lastenausgleich virtueller Computer

> Gilt für: Windows Server 2019, Windows Server 2016

Ein wichtiger Aspekt bei Private Cloud Bereitstellungen sind die Kapitalausgaben (<abbr title="Kapitalausgaben">CAPEX)</abbr>) erforderlich, um in die Produktion zu wechseln. Es kommt häufig vor, dass Sie Redundanz zu Private Cloud bereit Stellungen hinzufügen, um eine unter Kapazität bei Spitzen Datenverkehr in der Produktion zu vermeiden. <abbr title="Kapitalausgaben">CAPEX)</abbr>. Der Bedarf an Redundanz wird durch unausgeglichene Private Clouds gesteuert, bei denen einige Knoten mehr Virtual Machines (<abbr title="Virtuelle Computer">VMs</abbr>) und andere unterausgelastet sind (z. b. ein neu gestartetes Server).

<strong>Übersicht über Quick Videos</strong><br>(6 Minuten)<br>
> [!VIDEO https://channel9.msdn.com/Blogs/windowsserver/Virtual-Machine-Load-Balancing-in-Windows-Server-2016/player]

## <a id="what-is-vm-load-balancing"></a>Was ist der Lastenausgleich für virtuelle Computer?
<abbr title="Virtueller Computer">Virtuelle Maschine</abbr> Der Lastenausgleich ist ein in-Box-Feature in Windows Server 2019 und Windows Server 2016, mit dem Sie die Auslastung von Knoten in einem Failovercluster optimieren können. Es identifiziert Knoten, für die ein Commit ausgeführt wurde, und verteilt Sie erneut <abbr title="Virtuelle Computer">VMs</abbr> von diesen Knoten zu Knoten, für die ein Commit ausgeführt wurde. Einige der wichtigsten Aspekte dieses Features lauten wie folgt:

* *Dabei handelt es sich um eine Lösung ohne Ausfallzeiten*: <abbr title="Virtuelle Computer">VMs</abbr> werden in Knoten im Leerlauf migriert.
* *Nahtlose Integration in Ihre vorhandene Cluster Umgebung*: Fehler Richtlinien, wie z. b. antiaffinität, Fehler Domänen und mögliche Besitzer, werden berücksichtigt.
* *Heuristik für den Ausgleich*: <abbr title="Virtueller Computer">Virtuelle Maschine</abbr> Arbeitsspeicher Auslastung und CPU-Auslastung des Knotens.
* *Granulare Steuerung*: Standardmäßig aktiviert. Kann Bedarfs gesteuert oder in regelmäßigen Abständen aktiviert werden.
* *Schwellenwerte für Aggressivität*: Basierend auf den Merkmalen Ihrer Bereitstellung sind drei Schwellenwerte verfügbar.

## <a id="feature-in-action"></a>Das Feature in Aktion
### <a id="new-node-added"></a>Dem Failovercluster wird ein neuer Knoten hinzugefügt.
![Grafik eines neuen Knotens, der dem Failovercluster hinzugefügt wird](media/vm-load-balancing/overview-VM-load-balancing-1.png)

Wenn Sie dem Failovercluster neue Kapazität hinzufügen, wird der <abbr title="Virtuelle Maschine">Virtuelle Maschine</abbr> Der Lasten Ausgleichs Feature gleicht die Kapazität der vorhandenen Knoten automatisch mit dem neu hinzugefügten Knoten in der folgenden Reihenfolge ab:

1. Der Druck wird auf den vorhandenen Knoten im Failovercluster ausgewertet.
2. Alle Knoten, die den Schwellenwert überschreiten, werden identifiziert
3. Die Knoten mit dem höchsten Druck werden identifiziert, um die Priorität des Ausgleichs zu ermitteln.
4. <abbr title="Virtuelle Computer">VMs</abbr> von einem Knoten, der den Schwellenwert überschreitet, zu einem neu hinzugefügten Knoten im Failovercluster werden Live migriert (ohne Zeitüberschreitung).

### <a id="recurring-load-balancing"></a>Wiederkehrender Lastenausgleich
![Grafik eines wiederkehrenden VM-Lasten Ausgleichs](media/vm-load-balancing/overview-VM-load-balancing-2.png)

Bei der Konfiguration des regelmäßigen Ausgleichs wird der Druck auf den Cluster Knoten alle 30 Minuten für den Lastenausgleich ausgewertet. Alternativ kann der Druck bei Bedarf ausgewertet werden. Im folgenden finden Sie den Ablauf der Schritte:

1. Der Druck wird auf allen Knoten im Private Cloud ausgewertet.
2. Alle Knoten, die den Schwellenwert überschreiten, und die Untergrenze werden identifiziert
3. Die Knoten mit dem höchsten Druck werden identifiziert, um die Priorität des Ausgleichs zu ermitteln.
4. <abbr title="Virtuelle Computer">VMs</abbr> von einem Knoten, der den Schwellenwert für den Knoten unter dem minimalen Schwellenwert überschreitet, werden Live migriert (ohne Zeitüberschreitung).

## <a name="see-also"></a>Siehe auch
* [Eingehender Einblick in den Lastenausgleich virtueller Computer](vm-load-balancing-deep-dive.md)
* [Failoverclustering](failover-clustering-overview.md)
* [Übersicht über Hyper-V](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
