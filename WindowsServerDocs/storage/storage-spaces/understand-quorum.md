---
title: Grundlegendes zu-Cluster und Pool-quorum
description: Weitere Informationen zu und Poolquorum, Beispiele, um über die feinheiten zu wechseln.
keywords: "\"Direkte Speicherplätze\", Quorum, Zeuge und S2D, Cluster-Quorum Poolquorum, Cluster, Pool"
ms.prod: windows-server-threshold
ms.author: adagashe
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 01/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 30958b8b1e8b0009626509409d1f031611c76a20
ms.sourcegitcommit: fe621b72d45d0259bac1d5b9031deed3dcbed29d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2019
ms.locfileid: "66455433"
---
# <a name="understanding-cluster-and-pool-quorum"></a>Grundlegendes zu-Cluster und Pool-quorum

>Gilt für: Windows Server 2019, Windows Server 2016

[Windows Server Failover Clustering](../../failover-clustering/failover-clustering-overview.md) bietet hohe Verfügbarkeit für arbeitsauslastungen. Diese Ressourcen gelten als hoch verfügbar, wenn die Knoten, die Ressourcen hosten betriebsbereit sind. der Cluster im Allgemeinen erfordert jedoch mehr als die Hälfte der Knoten ausgeführt werden, dies wird auch als bezeichnet *Quorum*.

Quorum wurde entwickelt, um zu verhindern, dass *Split-Brain* Szenarien, in denen passieren können, wenn eine Partition vorhanden, im Netzwerk ist und Teilmengen von Knoten nicht miteinander kommunizieren. Dies kann dazu führen, dass beide Teilmengen von Knoten, um zu versuchen, besitzen die Workload, und Schreiben in den gleichen Datenträger kann zu zahlreichen Problemen führen. Dies wird jedoch mit Failover-Clusterunterstützung Konzept des Quorums verhindert die erzwingt, nur einer dieser Gruppen von Knoten dass, die Ausführung so fortgesetzt, damit nur einer dieser Gruppen online bleibt.

Quorum bestimmt die Anzahl von Fehlern, die der Cluster tolerieren kann, während Sie weiterhin online bleiben. Quorum wurde entwickelt, um das Szenario abzudecken, wenn ein Problem bei der Kommunikation zwischen Teilmengen von Clusterknoten vorhanden ist, damit mehrere Server nicht versuchen, gleichzeitig hosten eine Ressourcengruppe aus, und gleichzeitig auf demselben Datenträger zu schreiben. Wenn Sie dieses Konzept des Quorums, erzwingt der Cluster den Clusterdienst beenden in eine der Teilmengen von Knoten, um sicherzustellen, dass nur eine "true" Besitzer einer bestimmten Ressourcengruppe vorhanden ist. Nach Knoten, die beendet wurden, erneut mit der primären Gruppe von Knoten kommunizieren können, werden sie automatisch dem Cluster wieder beitreten und starten Sie ihren Clusterdienst.

In Windows Server-2019 und Windows Server 2016 gibt es zwei Komponenten des Systems, die über eigene Mechanismen Quorum verfügen:

- **Cluster-Quorum**: Dies funktioniert auf Clusterebene (d. h. Sie können Knoten verlieren und über den Betrieb aufrecht Cluster)
- **Pool Quorum**: Dies funktioniert auf der Ebene des Pools, wenn "direkte Speicherplätze" aktiviert ist (d. h. Sie können verloren gehen, Knoten und Laufwerke und über den Pool, der immer verfügbar sein). Speicherpools wurden entwickelt, in gruppierten und nicht gruppierten Szenarios verwendet werden, d.h., warum sie einen Quorummechanismus für die verschiedenen verfügen.

## <a name="cluster-quorum-overview"></a>Cluster-Quorum-Überblick

Die folgende Tabelle bietet einen Überblick über die Cluster-Quorum-Ergebnisse pro Szenario:

| Server-Knoten | Ein Server Knotenfehler können Überleben werden. | Ausfall eines Knotens von einem Server, und klicken Sie dann eine andere können Überleben werden. | Zwei gleichzeitigen Ausfall von Serverknoten können Überleben werden. |
|--------------|-------------------------------------|---------------------------------------------------|----------------------------------------------------|
| 2            | 50/50                               | Nein                                                | Nein                                                 |
| 2 + Zeugen  | Ja                                 | Nein                                                | Nein                                                 |
| 3            | Ja                                 | 50/50                                             | Nein                                                 |
| 3 + Zeugen  | Ja                                 | Ja                                               | Nein                                                 |
| 4            | Ja                                 | Ja                                               | 50/50                                              |
| 4 + Zeugen  | Ja                                 | Ja                                               | Ja                                                |
| 5 und höher  | Ja                                 | Ja                                               | Ja                                                |

### <a name="cluster-quorum-recommendations"></a>Cluster-Quorum-Empfehlungen

- Wenn Sie über zwei Knoten verfügen, wird ein Zeuge **erforderlichen**.
- Wenn Sie drei oder vier Knoten verfügen, Zeuge ist **dringend empfohlen,** .
- Wenn Sie Zugriff auf das Internet haben, verwenden Sie eine  **[cloudzeugen](../../failover-clustering/deploy-cloud-witness.md)**
- Wenn Sie in einer IT-Umgebung mit anderen Computern und Dateifreigaben sind, verwenden Sie einen Dateifreigabenzeugen

## <a name="how-cluster-quorum-works"></a>Wie funktioniert der Clusterquorum

Wenn Knoten ausfallen, oder wenn eine Teilmenge der Knoten, wenden Sie sich an, mit einer anderen Teilmenge verliert, müssen die verbleibenden Knoten um sicherzustellen, dass sie bilden die *Mehrheit* des Clusters online bleiben. Wenn sie nicht, die überprüfen können, müssen sie offline geschaltet werden.

Aber das Konzept der *Mehrheit* funktioniert nur ordnungsgemäß bei die Gesamtzahl der Knoten im Cluster ungerade (z. B. drei Knoten in einem Cluster mit fünf Knoten) ist. Was ist der Cluster mit einer geraden Anzahl von Knoten (z. B. ein Cluster mit vier Knoten)?

Es gibt zwei Möglichkeiten, die der Cluster möglich die *Gesamtzahl der stimmen* ungerade:

1. Zunächst können sie wechseln *einrichten* einen durch das Hinzufügen einer *Zeugen* mit eine zusätzliche Stimme. Dazu müssen Benutzer einrichten.
2.  Oder, *unten* eine durch Ausfüllen des weniger Knoten eine Stimme (geschieht automatisch nach Bedarf).

Wenn Knoten erfolgreich überstehen überprüfen Sie, ob sie die *Mehrheit*, die Definition der *Mehrheit* wird aktualisiert, um auf nur die überlebenden werden. Dadurch wird den Cluster verloren gehen, ein Knoten einen anderen und dann eine andere und so weiter. Dieses Konzept der *Gesamtzahl der stimmen* nach aufeinander folgenden Fehlern zur Anpassung der sogenannte ***dynamisches Quorum***.  

### <a name="dynamic-witness"></a>Dynamische Zeugen

Dynamische Zeuge Schaltet die Stimme des Zeugen sicherstellen, dass die *Gesamtzahl der stimmen* ungerade ist. Wenn es eine ungerade Zahl von abstimmungen gibt, nicht der Zeuge über eine Stimme verfügen. Ist eine gerade Zahl von abstimmungen, weist der Zeuge eine Stimme an. Dynamische Zeuge wird erheblich reduziert das Risiko, das der Cluster aufgrund Zeuge ausfällt. Der Cluster entscheidet, ob verwenden die zeugenstimme basierend auf der Anzahl von abstimmenden Knoten, die im Cluster verfügbar sind.

Dynamisches Quorum funktioniert mit dynamischen Zeugen wie unten beschrieben.

### <a name="dynamic-quorum-behavior"></a>Dynamisches Quorum-Verhalten

- Wenn Sie haben eine **sogar** Anzahl von Knoten und kein Zeuge, *ein Knoten ruft seine Zustimmung, die auf NULL gesetzt*. Beispielsweise erhalten nur drei der vier Knoten stimmen, sodass die *Gesamtzahl der stimmen* ist der dritte und zwei beibehaltene Objekte mit stimmen gelten die meisten.
- Wenn Sie haben eine **ungerade** Anzahl von Knoten und kein Zeuge, *erhalten sie alle stimmen*.
- Wenn Sie haben eine **sogar** Anzahl von Knoten plus Zeugen *stimmen Sie der Zeugen*, sodass die Summe ungerade ist.
- Wenn man eine **ungerade** Anzahl von Knoten plus Zeugen *der Zeuge nicht abstimmen*.

Dynamisches Quorum können Sie einen Knoten dynamisch, um zu vermeiden, verlieren die Mehrheit der stimmen und der Cluster zum Ausführen von mit einem Knoten (als letzten-Man ständigen bezeichnet) ermöglichen eine Stimme zugewiesen. Als Beispiel werfen wir einen Cluster mit vier Knoten. Wird davon ausgegangen Sie, dass diese 3 stimmen erforderlich ist. 

In diesem Fall würde der Cluster aufgetreten nach unten, wenn Sie zwei Knoten verloren.

![Diagramm mit vier Clusterknoten, von denen jede eine Stimme Ruft](media/understand-quorum/dynamic-quorum-base.png)

Allerdings verhindert dynamisches Quorum dies. Die *Gesamtzahl der stimmen* erforderlich für das Quorum jetzt bestimmt wird basierend auf der Anzahl verfügbarer Knoten. Also bleiben dynamisches Quorum der Cluster sich, selbst wenn Sie die drei Knoten verlieren.

![Das Diagramm zeigt die vier Clusterknoten mit Knoten, die jeweils eine Zeit, und die Anzahl der erforderlichen stimmen anpassen, die nach jedem Fehler fehlschlägt.](media/understand-quorum/dynamic-quorum-step-through.png)

Das oben beschriebene Szenario gilt für einen allgemeinen Cluster, der keine "direkte Speicherplätze" aktiviert. Wenn "direkte Speicherplätze" aktiviert ist, kann der Cluster unterstützen jedoch nur zwei Knotenausfällen. Dies wird ausführlicher den [Quorum Abschnitt Anwendungspool](#pool-quorum-overview).

### <a name="examples"></a>Beispiele

#### <a name="two-nodes-without-a-witness"></a>Zwei Knoten ohne einen Zeugen. 
Stimme des Knotens für den eine auf NULL gesetzt, sodass die *Mehrheit* Stimme richtet sich insgesamt **1 Stimme**. Wenn der Knoten ohne Stimmrecht unerwartet ausfällt, Survivor ist 1/1 und Cluster zurückgegriffen werden kann. Wenn der abstimmenden Knoten unerwartet ausfällt, Survivor hat 0/1 und der Cluster ausfällt. Wenn der abstimmenden Knoten ordnungsgemäß heruntergefahren ist, die Stimme wird auf dem anderen Knoten übertragen und überdauert, der Cluster. ***Daher ist es wichtig, einen Zeugen zu konfigurieren.***

![Im Fall mit zwei Knoten, ohne einen Zeugen erläutert Quorum](media/understand-quorum/2-node-no-witness.png)

- Kann ein Ausfall des Servers überstehen: **Fünfzig Prozent Wahrscheinlichkeit**.
- Kann ein Server-Fehler und dann noch einen überstehen: **Nein**:
- Zwei Serverfehler können auf einmal verkraftet werden: **Nein**: 

#### <a name="two-nodes-with-a-witness"></a>Zwei Knoten mit einem Zeugen. 
Stimmen beide Knoten sowie der Zeuge stimmen, sodass die *Mehrheit* richtet sich insgesamt **3 stimmen**. Wenn entweder Knoten ausfällt, Survivor hat 2/3, wobei überdauert, des Clusters.

![Im Fall mit zwei Knoten mit einem Zeugen erläutert Quorum](media/understand-quorum/2-node-witness.png)

- Kann ein Ausfall des Servers überstehen: **Ja**:
- Kann ein Server-Fehler und dann noch einen überstehen: **Nein**:
- Zwei Serverfehler können auf einmal verkraftet werden: **Nein**: 

#### <a name="three-nodes-without-a-witness"></a>Drei Knoten ohne einen Zeugen.
Allen Knoten stimmen, sodass die *Mehrheit* richtet sich insgesamt **3 stimmen**. Wenn Sie einen beliebigen Knoten ausfällt, beibehaltenen Objekte sind 2/3 und überdauert, der Cluster. Der Cluster wird von zwei Knoten, ohne einen Zeugen – an diesem Punkt in dem Sie in Szenario 1 sind.

![Im Fall mit drei Knoten ohne einen Zeugen erläutert Quorum](media/understand-quorum/3-node-no-witness.png)

- Kann ein Ausfall des Servers überstehen: **Ja**:
- Kann ein Server-Fehler und dann noch einen überstehen: **Fünfzig Prozent Wahrscheinlichkeit**.
- Zwei Serverfehler können auf einmal verkraftet werden: **Nein**: 

#### <a name="three-nodes-with-a-witness"></a>Drei Knoten mit einem Zeugen.
Alle Knoten abstimmen, damit der Zeuge zuerst stimmen nicht. Die *Mehrheit* richtet sich insgesamt **3 stimmen**. Nach einem Fehler befindet sich der Cluster zwei Knoten mit einem Zeugen – die zurück zum Szenario 2 ist. Daher stimmen jetzt die beiden Knoten und den Zeugen.

![Im Fall mit drei Knoten mit einem Zeugen erläutert Quorum](media/understand-quorum/3-node-witness.png)

- Kann ein Ausfall des Servers überstehen: **Ja**:
- Kann ein Server-Fehler und dann noch einen überstehen: **Ja**:
- Zwei Serverfehler können auf einmal verkraftet werden: **Nein**: 

#### <a name="four-nodes-without-a-witness"></a>Vier Knoten ohne einen Zeugen
Stimme des Knotens für den eine auf NULL gesetzt, sodass die *Mehrheit* richtet sich insgesamt **3 stimmen**. Klicken Sie nach einem Fehler der Cluster wird drei Knoten, und Sie können in Szenario 3.

![Im Fall mit vier Knoten ohne einen Zeugen erläutert Quorum](media/understand-quorum/4-node-no-witness.png)

- Kann ein Ausfall des Servers überstehen: **Ja**:
- Kann ein Server-Fehler und dann noch einen überstehen: **Ja**:
- Zwei Serverfehler können auf einmal verkraftet werden: **Fünfzig Prozent Wahrscheinlichkeit**. 

#### <a name="four-nodes-with-a-witness"></a>Vier Knoten mit einem Zeugen.
Alle stimmen von Knoten und der Zeuge stimmen, sodass die *Mehrheit* richtet sich insgesamt **5 stimmen**. Nachdem ein Fehler auftritt können Sie in Szenario 4 aus. Nach zwei gleichzeitigen Fehlern fortfahren Sie Szenario 2.

![Im Fall mit vier Knoten mit einem Zeugen erläutert Quorum](media/understand-quorum/4-node-witness.png)

- Kann ein Ausfall des Servers überstehen: **Ja**:
- Kann ein Server-Fehler und dann noch einen überstehen: **Ja**:
- Zwei Serverfehler können auf einmal verkraftet werden: **Ja**: 

#### <a name="five-nodes-and-beyond"></a>Fünf Knoten und darüber hinaus.
Abstimmen von allen Knoten oder alle bis auf eine Stimme, unabhängig erstellt, die ungerade Summe. "Direkte Speicherplätze" kann nicht mehr als zwei Knoten nach unten jedenfalls behandelt, hat an diesem Punkt ist kein Zeuge erforderlich oder nützlich ist.

![Im Fall mit fünf Knoten und darüber hinaus erläutert Quorum](media/understand-quorum/5-nodes.png)

- Kann ein Ausfall des Servers überstehen: **Ja**:
- Kann ein Server-Fehler und dann noch einen überstehen: **Ja**:
- Zwei Serverfehler können auf einmal verkraftet werden: **Ja**: 

Nun, da wir die Funktionsweise des Quorums verstehen, sehen wir uns die Arten von Quorum-Zeugen.

### <a name="quorum-witness-types"></a>Quorumzeugentypen

Failover-Clusterunterstützung unterstützt drei Arten von Quorum Zeugen hinzu:

- **[Cloudzeugen](../../failover-clustering/deploy-cloud-witness.md)**  -Blob-Speicher in Azure zugegriffen werden kann, von allen Knoten des Clusters. Es verwaltet clustering Informationen in eine Datei "witness.log", aber eine Kopie der Clusterdatenbank speichert nicht.
- **Datei Dateifreigabenzeugen** – ein SMB-Dateifreigabe, die auf einem Dateiserver unter Windows Server konfiguriert ist. Es verwaltet clustering Informationen in eine Datei "witness.log", aber eine Kopie der Clusterdatenbank speichert nicht.
- **Datenträgerzeuge** -einen kleinen Clusterdatenträger, die im Cluster verfügbaren Speichergruppe ist. Dieser Datenträger ist hoch verfügbar und kann ein Failover zwischen Knoten. Sie enthält eine Kopie der Clusterdatenbank.  ***Ein Datenträgerzeuge wird nicht unterstützt, mit "direkte Speicherplätze"***.

## <a name="pool-quorum-overview"></a>Pool-Quorum-Überblick

Wurden nur Cluster-Quorum, das auf der Clusterebene ausgeführt wird. Nun, uns einen näheren Poolquorum, operiert auf der Pool-Ebene (d. h. Sie können Knoten verlieren und Laufwerke und über den Pool, der immer verfügbar sein). Speicherpools wurden entwickelt, in gruppierten und nicht gruppierten Szenarios verwendet werden, d.h., warum sie einen Quorummechanismus für die verschiedenen verfügen.

Die folgende Tabelle bietet einen Überblick über die Ergebnisse Poolquorum pro Szenario:

| Server-Knoten | Ein Server Knotenfehler können Überleben werden. | Ausfall eines Knotens von einem Server, und klicken Sie dann eine andere können Überleben werden. | Zwei gleichzeitigen Ausfall von Serverknoten können Überleben werden. |
|--------------|-------------------------------------|---------------------------------------------------|----------------------------------------------------|
| 2            | Nein                                  | Nein                                                | Nein                                                 |
| 2 + Zeugen  | Ja                                 | Nein                                                | Nein                                                 |
| 3            | Ja                                 | Nein                                                | Nein                                                 |
| 3 + Zeugen  | Ja                                 | Nein                                                | Nein                                                 |
| 4            | Ja                                 | Nein                                                | Nein                                                 |
| 4 + Zeugen  | Ja                                 | Ja                                               | Ja                                                |
| 5 und höher  | Ja                                 | Ja                                               | Ja                                                |

## <a name="how-pool-quorum-works"></a>Funktionsweise des Quorums für pool

Wenn Laufwerke fehlschlagen oder eine Teilmenge der Laufwerke, wenden Sie sich an, mit einer anderen Teilmenge verliert, müssen noch vorhandenen Laufwerke sicherstellen, dass sie bilden die *Mehrheit* des Pools online bleiben. Wenn sie nicht, die überprüfen können, müssen sie offline geschaltet werden. Der Pool ist die Entität, die offline geschaltet wird, oder bleibt online basierend auf, ob sie genügend Datenträger für das Quorum verfügt (50 % + 1). Der Besitzer der Ressource Pool (aktiven Clusterknoten) kann die + 1 sein.

Aber das poolquorum funktioniert anders als Clusterquorum auf folgende Weise:

- Dieser Pool verwendet einen Knoten im Cluster als Zeuge als Tiebreaker überstehen die Hälfte der Laufwerke durchgeführt (dieser Knoten, der der Besitzer der Pool ist)
- der Pool hat keine dynamisches quorum
- der Pool implementiert eine eigene Version der Löschung einer Abstimmung nicht

### <a name="examples"></a>Beispiele

#### <a name="four-nodes-with-a-symmetrical-layout"></a>Vier Knoten mit einem symmetrischen Layout. 
Jedes Laufwerk 16 hat es sich um eine Stimme und Knoten zwei verfügt auch über eine Stimme (da sie der Besitzer der Pool ist). Die *Mehrheit* richtet sich insgesamt **16 stimmen**. Wenn Knoten, drei und vier ausfallen, hat die überdauernden Teilmenge 8 Laufwerke und der Pool der Besitzer der Ressource, 9/16 stimmen handelt. Also, überdauert der Pool ein.

![Poolquorum 1](media/understand-quorum/pool-1.png)

- Kann ein Ausfall des Servers überstehen: **Ja**:
- Kann ein Server-Fehler und dann noch einen überstehen: **Ja**:
- Zwei Serverfehler können auf einmal verkraftet werden: **Ja**: 

#### <a name="four-nodes-with-a-symmetrical-layout-and-drive-failure"></a>Vier Knoten mit einem symmetrischen Layout und die Laufwerk-Fehler. 
Jedes Laufwerk 16 hat es sich um eine Stimme und Knoten 2 verfügen auch über eine Stimme (da sie der Besitzer der Pool ist). Die *Mehrheit* richtet sich insgesamt **16 stimmen**. Zuerst fällt ein Laufwerk 7 aus. Wenn Knoten, drei und vier ausfallen, hat die überdauernden Teilmenge 7 Laufwerke und der Pool der Besitzer der Ressource, 8/16 stimmen handelt. Daher wird der Pool keine Mehrheit und ausfällt.

![Poolquorum 2](media/understand-quorum/pool-2.png)

- Kann ein Ausfall des Servers überstehen: **Ja**:
- Kann ein Server-Fehler und dann noch einen überstehen: **Nein**:
- Zwei Serverfehler können auf einmal verkraftet werden: **Nein**: 

#### <a name="four-nodes-with-a-non-symmetrical-layout"></a>Vier Knoten mit einem Layout nicht symmetrisch. 
Jedes Laufwerk 24 hat es sich um eine Stimme und Knoten zwei verfügt auch über eine Stimme (da sie der Besitzer der Pool ist). Die *Mehrheit* richtet sich insgesamt **24 stimmen**. Wenn der Knoten, drei und vier ausfällt, hat die überdauernden Teilmenge 8 Laufwerke und der Pool der Besitzer der Ressource, die stimmen von 9/24 ist. Daher wird der Pool keine Mehrheit und ausfällt.

![Poolquorum 3](media/understand-quorum/pool-3.png)

- Kann ein Ausfall des Servers überstehen: **Ja**:
- Fehler von einem Server und dann noch einen überstehen können: ** Abhängigkeiten ** (kann nicht überstehen beide Knoten, drei und vier ausfallen, aber es können alle anderen Szenarien Überleben.
- Können überstehen zwei Server gleichzeitig: ** Abhängigkeiten ** (kann nicht überstehen beide Knoten, drei und vier ausfallen, aber es können alle anderen Szenarien Überleben.

### <a name="pool-quorum-recommendations"></a>Empfehlungen für Pools quorum

- Stellen Sie sicher, dass jeder Knoten in Ihrem Cluster symmetrisch ist (jeder Knoten verfügt über die gleiche Anzahl von Laufwerken)
- Aktivieren Sie drei-Wege-Spiegelung oder duale Parität, sodass Sie einem Knotenfehler tolerieren und die virtuellen Datenträger online halten. Finden Sie in unserer [Volumes-Seite "Leitfaden"](plan-volumes.md) Weitere Details.
- Wenn mehr als zwei Knoten ausgefallen sind, oder zwei Knoten und einen Datenträger auf einem anderen Knoten ausgefallen sind, Volumes möglicherweise keinen Zugriff auf alle drei Kopien ihrer Daten, und daher offline geschaltet werden und ist nicht verfügbar. Es wird empfohlen, schalten Sie wieder auf die Servern, oder ersetzen die Datenträger schnell, um sicherzustellen, dass die meisten Flexibilität in Bezug auf alle Daten auf dem Volume.

## <a name="more-information"></a>Weitere Informationen

- [Konfigurieren und Verwalten des Quorums](../../failover-clustering/manage-cluster-quorum.md)
- [Bereitstellen eines cloudzeugen](../../failover-clustering/deploy-cloud-witness.md)
