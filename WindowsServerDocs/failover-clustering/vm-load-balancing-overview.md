---
ms.assetid: f0d4cecc-5a03-448c-bef9-86c4730b4eb0
title: VM-Lastenausgleich – Übersicht
ms.topic: article
manager: eldenc
ms.author: johnmar
author: JasonGerend
ms.date: 09/19/2016
ms.openlocfilehash: 868f5c0646b3842f605447d1fe8fdbe74593c2a6
ms.sourcegitcommit: 7a8a608df059b4278a974c52ed7b865421a83aa6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/08/2020
ms.locfileid: "91833307"
---
# <a name="virtual-machine-load-balancing-overview"></a>VM-Lastenausgleich – Übersicht

> Gilt für: Windows Server 2019, Windows Server 2016

Ein wichtiger Aspekt bei Private Cloud Bereitstellungen sind die Kapitalausgaben (<abbr title="Kapitalausgaben">CAPEX)</abbr>) erforderlich, um in die Produktion zu wechseln. Es kommt häufig vor, dass Sie Redundanz zu Private Cloud bereit Stellungen hinzufügen, um eine unter Kapazität bei Spitzen Datenverkehr in der Produktion zu vermeiden. <abbr title="Kapitalausgaben">CAPEX)</abbr>. Der Bedarf an Redundanz wird durch unausgeglichene Private Clouds gesteuert, bei denen einige Knoten mehr Virtual Machines (<abbr title="Virtuelle Computer">VMs</abbr>) und andere unterausgelastet sind (z. b. ein neu gestartetes Server).

<strong>Übersicht über Quick Videos</strong><br>(6 Minuten)<br>
> [!VIDEO https://channel9.msdn.com/Blogs/windowsserver/Virtual-Machine-Load-Balancing-in-Windows-Server-2016/player]

## <a name="what-is-virtual-machine-load-balancing"></a><a id="what-is-vm-load-balancing"></a>Was ist der Lastenausgleich für virtuelle Computer?
<abbr title="Virtueller Computer">VM</abbr> Der Lastenausgleich ist ein in-Box-Feature in Windows Server 2019 und Windows Server 2016, mit dem Sie die Auslastung von Knoten in einem Failovercluster optimieren können. Es identifiziert Knoten, für die ein Commit ausgeführt wurde, und verteilt Sie erneut <abbr title="Virtuelle Computer">VMs</abbr> von diesen Knoten zu Knoten, für die ein Commit ausgeführt wurde. Einige der wichtigsten Aspekte dieses Features lauten wie folgt:

* *Dabei handelt es sich um eine Lösung ohne Ausfallzeiten*: <abbr title="Virtuelle Computer">VMs</abbr> werden in Knoten im Leerlauf migriert.
* *Nahtlose Integration in Ihre vorhandene Cluster Umgebung*: Fehler Richtlinien, wie z. b. antiaffinität, Fehler Domänen und mögliche Besitzer, werden berücksichtigt.
* *Heuristik für den Ausgleich*: <abbr title="Virtueller Computer">VM</abbr> Arbeitsspeicher Auslastung und CPU-Auslastung des Knotens.
* *Granulare Steuerung*: standardmäßig aktiviert. Kann Bedarfs gesteuert oder in regelmäßigen Abständen aktiviert werden.
* *Schwellenwerte*für die Aggressivität: basierend auf den Merkmalen Ihrer Bereitstellung sind drei Schwellenwerte verfügbar.

## <a name="the-feature-in-action"></a><a id="feature-in-action"></a>Das Feature in Aktion
### <a name="a-new-node-is-added-to-your-failover-cluster"></a><a id="new-node-added"></a>Dem Failovercluster wird ein neuer Knoten hinzugefügt.
![Grafik eines neuen Knotens, der dem Failovercluster hinzugefügt wird](media/vm-load-balancing/overview-VM-load-balancing-1.png)

Wenn Sie dem Failovercluster neue Kapazität hinzufügen, wird der <abbr title="Virtueller Computer">VM</abbr> Der Lasten Ausgleichs Feature gleicht die Kapazität der vorhandenen Knoten automatisch mit dem neu hinzugefügten Knoten in der folgenden Reihenfolge ab:

1. Der Druck wird auf den vorhandenen Knoten im Failovercluster ausgewertet.
2. Alle Knoten, die den Schwellenwert überschreiten, werden identifiziert
3. Die Knoten mit dem höchsten Druck werden identifiziert, um die Priorität des Ausgleichs zu ermitteln.
4. <abbr title="Virtuelle Computer">VMs</abbr> von einem Knoten, der den Schwellenwert überschreitet, zu einem neu hinzugefügten Knoten im Failovercluster werden Live migriert (ohne Zeitüberschreitung).

### <a name="recurring-load-balancing"></a><a id="recurring-load-balancing"></a>Wiederkehrender Lastenausgleich
![Grafik eines wiederkehrenden VM-Lasten Ausgleichs](media/vm-load-balancing/overview-VM-load-balancing-2.png)

Bei der Konfiguration des regelmäßigen Ausgleichs wird der Druck auf den Cluster Knoten alle 30 Minuten für den Lastenausgleich ausgewertet. Alternativ kann der Druck bei Bedarf ausgewertet werden. Im folgenden finden Sie den Ablauf der Schritte:

1. Der Druck wird auf allen Knoten im Private Cloud ausgewertet.
2. Alle Knoten, die den Schwellenwert überschreiten, und die Untergrenze werden identifiziert
3. Die Knoten mit dem höchsten Druck werden identifiziert, um die Priorität des Ausgleichs zu ermitteln.
4. <abbr title="Virtuelle Computer">VMs</abbr> von einem Knoten, der den Schwellenwert für den Knoten unter dem minimalen Schwellenwert überschreitet, werden Live migriert (ohne Zeitüberschreitung).

## <a name="see-also"></a>Weitere Informationen
* [Eingehender Einblick in den Lastenausgleich virtueller Computer](vm-load-balancing-deep-dive.md)
* [Failoverclustering](failover-clustering-overview.md)
* [Übersicht über Hyper-V](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
