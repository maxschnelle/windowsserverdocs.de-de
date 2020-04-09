---
title: Grundlegendes zum Cluster- und Poolquorum
description: Grundlegendes zum Cluster-und Pool Quorum mit speziellen Beispielen, um die Feinheiten zu überschreiten.
ms.prod: windows-server
ms.author: adagashe
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 01/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: f13affc3ef15c3a39f4fd3839506897f7807d93a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820993"
---
# <a name="understanding-cluster-and-pool-quorum"></a>Grundlegendes zum Cluster- und Poolquorum

>Gilt für: Windows Server 2019, Windows Server 2016

[Windows Server-Failoverclustering](../../failover-clustering/failover-clustering-overview.md) bietet hohe Verfügbarkeit für Arbeits Auslastungen. Diese Ressourcen werden als hoch verfügbar angesehen, wenn die Knoten, die Ressourcen hosten, hoch verfügbar sind. der Cluster erfordert jedoch in der Regel mehr als die Hälfte der Knoten, die ausgeführt werden müssen. Dies wird als vorhanden sein eines *Quorums*bezeichnet.

Das Quorum ist so konzipiert, dass *Split-Brain-* Szenarien vermieden werden, die auftreten können, wenn eine Partition im Netzwerk vorhanden ist und Teilmengen von Knoten nicht miteinander kommunizieren können. Dies kann dazu führen, dass beide Teilmengen der Knoten den Besitzer der Arbeitsauslastung haben und auf den gleichen Datenträger schreiben, was zu zahlreichen Problemen führen kann. Dies wird jedoch durch das Quorum Konzept des Failoverclustering verhindert, das zwingt, dass nur eine dieser Knotengruppen weiter ausgeführt wird, sodass nur eine dieser Gruppen online bleibt.

Das Quorum bestimmt die Anzahl von Fehlern, die der Cluster unterstützen kann, während er weiterhin online bleibt. Das Quorum ist so konzipiert, dass es das Szenario behandelt, wenn ein Problem mit der Kommunikation zwischen Teilmengen von Cluster Knoten vorliegt, sodass mehrere Server nicht versuchen, gleichzeitig eine Ressourcengruppe zu hosten und gleichzeitig auf denselben Datenträger zu schreiben. Durch dieses Konzept des Quorums erzwingt der Cluster, dass der Cluster Dienst in einer der Teilmengen von Knoten angehalten wird, um sicherzustellen, dass nur ein echter Besitzer einer bestimmten Ressourcengruppe vorhanden ist. Wenn die wieder beendeten Knoten erneut mit der Haupt Knotengruppe kommunizieren können, treten Sie automatisch dem Cluster bei und starten Ihren Cluster Dienst.

In Windows Server 2019 und Windows Server 2016 gibt es zwei Komponenten des Systems, die über eigene Quorum Mechanismen verfügen:

- **Cluster Quorum**: Dies wird auf Cluster Ebene betrieben (d. h., Sie können Knoten verlieren, und der Cluster bleibt in Betrieb).
- **Pool Quorum**: Dies funktioniert auf Poolebene, wenn direkte Speicherplätze aktiviert ist (d. h., Sie können Knoten und Laufwerke verlieren und den Pool in Betrieb behalten). Speicherpools wurden so entworfen, dass Sie in gruppierten und nicht gruppierten Szenarien verwendet werden, weshalb Sie über einen anderen Quorum Mechanismus verfügen.

## <a name="cluster-quorum-overview"></a>Übersicht über Cluster Quorum

Die folgende Tabelle enthält eine Übersicht über die Cluster Quorum Ergebnisse pro Szenario:

| Server Knoten | Kann einen Server Knoten Fehler überstehen. | Kann einen Server Knoten Fehler überstehen, ein weiterer | Kann zwei gleichzeitige Server Knoten Ausfälle überstehen |
|--------------|-------------------------------------|---------------------------------------------------|----------------------------------------------------|
| 2            | 50/50                               | Nein                                                | Nein                                                 |
| 2 + Zeuge  | Ja                                 | Nein                                                | Nein                                                 |
| 3            | Ja                                 | 50/50                                             | Nein                                                 |
| 3 + Zeuge  | Ja                                 | Ja                                               | Nein                                                 |
| 4            | Ja                                 | Ja                                               | 50/50                                              |
| 4 + Zeuge  | Ja                                 | Ja                                               | Ja                                                |
| 5 und höher  | Ja                                 | Ja                                               | Ja                                                |

### <a name="cluster-quorum-recommendations"></a>Cluster Quorum Empfehlungen

- Wenn Sie über zwei Knoten verfügen, ist ein Zeuge **erforderlich**.
- Wenn Sie über drei oder vier Knoten verfügen, wird Zeuge **dringend empfohlen**.
- Wenn Sie über Internet Zugang verfügen, verwenden Sie einen  **[cloudzeugen](../../failover-clustering/deploy-cloud-witness.md) .**
- Wenn Sie sich in einer IT-Umgebung mit anderen Computern und Dateifreigaben befinden, verwenden Sie einen Dateifreigabe Zeugen.

## <a name="how-cluster-quorum-works"></a>Funktionsweise des Cluster Quorums

Wenn Knoten ausfallen oder eine Teilmenge der Knoten den Kontakt mit einer anderen Teilmenge verliert, müssen die übergeordneten Knoten sicherstellen, dass Sie den *Großteil* des Clusters darstellen, der Online bleibt. Wenn Sie dies nicht überprüfen können, werden Sie offline geschaltet.

Das Konzept der *Mehrheit* funktioniert jedoch nur ordnungsgemäß, wenn die Gesamtzahl der Knoten im Cluster ungerade ist (z. b. drei Knoten in einem Cluster mit fünf Knoten). Was ist also mit Clustern mit einer geraden Anzahl von Knoten (z. a. einem Cluster mit vier Knoten)?

Es gibt zwei Möglichkeiten, wie der Cluster die *Gesamtzahl der Stimmen* ungerade machen kann:

1. Zuerst können *Sie einen* *Zeugen* mit einer zusätzlichen Stimme hinzufügen. Hierfür ist ein Benutzer Setup erforderlich.
2.    Oder Sie können einen Schritt *nach unten* durchlaufen, indem Sie die Stimme eines nicht glücklichen Knotens NULLS (erfolgt bei Bedarf automatisch).

Wenn die Überprüfung erfolgreich ist, ob die Knoten die *Mehrheit*sind, wird die Definition der *Mehrheit* so aktualisiert, dass Sie nur zu den übergeordneten Knoten gehört. Dadurch kann der Cluster einen Knoten verlieren, dann einen anderen Knoten usw. Dieses Konzept der *Gesamtzahl der Stimmen* , die sich nach aufeinander folgenden Fehlern anpasst, wird als ***dynamisches Quorum***bezeichnet.  

### <a name="dynamic-witness"></a>Dynamischer Zeuge

Der dynamische Zeuge schaltet die Stimme des Zeugen um, um sicherzustellen, dass die *Gesamtzahl der Stimmen* ungerade ist. Wenn eine ungerade Anzahl von Stimmen vorliegt, hat der Zeuge keine Stimme. Wenn eine gerade Anzahl von Stimmen vorliegt, hat der Zeuge eine Stimme. Der dynamische Zeuge verringert das Risiko, dass der Cluster aufgrund eines Zeugen Fehlers ausfällt. Der Cluster entscheidet, ob die Zeugen Abstimmung basierend auf der Anzahl der Abstimmungs Knoten, die im Cluster verfügbar sind, verwendet werden soll.

Dynamisches Quorum funktioniert mit dynamischem Zeuge wie unten beschrieben.

### <a name="dynamic-quorum-behavior"></a>Dynamisches Quorum Verhalten

- Wenn Sie über eine **gerade** Anzahl von Knoten und keinen Zeugen verfügen, *erhält ein Knoten seine Stimme als nullt*. Beispielsweise erhalten nur drei der vier Knoten Stimmen, sodass die *Gesamtzahl der Stimmen* drei beträgt und zwei übergeordnete Knoten mit Stimmen als Mehrheit angesehen werden.
- Wenn Sie über eine **ungerade** Anzahl von Knoten und keinen Zeugen verfügen, *erhalten alle Stimmen*.
- Wenn Sie über eine **gerade** Anzahl von Knoten Plus Witness verfügen, *Stimmen der Zeuge*ab, sodass die Summe ungerade ist.
- Wenn Sie über eine **ungerade** Anzahl von Knoten Plus Witness verfügen, *stimmt der Zeuge nicht*.

Mithilfe des dynamischen Quorums kann einem Knoten eine Stimme dynamisch zugewiesen werden, um zu vermeiden, dass die Mehrheit der Stimmen verloren geht und der Cluster mit einem Knoten ausgeführt werden kann (auch als letzter als letzter bekannt). Nehmen wir als Beispiel einen Cluster mit vier Knoten. Angenommen, das Quorum erfordert 3 Stimmen. 

In diesem Fall wäre der Cluster ausgefallen, wenn Sie zwei Knoten verloren haben.

![Das Diagramm zeigt vier Cluster Knoten, von denen jeder eine Stimme erhält.](media/understand-quorum/dynamic-quorum-base.png)

Das dynamische Quorum verhindert jedoch, dass dies geschieht. Die *Gesamtanzahl der Stimmen* , die für das Quorum erforderlich sind, wird jetzt basierend auf der Anzahl der verfügbaren Knoten bestimmt. Mit dynamischem Quorum bleibt der Cluster auch dann in der Hand, wenn Sie drei Knoten verlieren.

![Diagramm, das vier Cluster Knoten anzeigt, bei denen Knoten nacheinander fehlschlagen, und die Anzahl erforderlicher Stimmen, die nach jedem Fehler angepasst werden.](media/understand-quorum/dynamic-quorum-step-through.png)

Das obige Szenario gilt für einen allgemeinen Cluster, für den direkte Speicherplätze nicht aktiviert ist. Wenn direkte Speicherplätze aktiviert ist, kann der Cluster jedoch nur zwei Knoten Ausfälle unterstützen. Dies wird im [Abschnitt Pool Quorum](#pool-quorum-overview)ausführlicher erläutert.

### <a name="examples"></a>Beispiele

#### <a name="two-nodes-without-a-witness"></a>Zwei Knoten ohne Zeugen. 
Die Stimme eines Knotens wird auf NULL gesetzt, sodass die *Mehrheit* der Stimme von insgesamt **1 Stimme**bestimmt wird. Wenn der Knoten ohne Abstimmung unerwartet ausfällt, verfügt der Survivor über 1/1, und der Cluster wird noch nicht angezeigt. Wenn der Abstimmungs Knoten unerwartet ausfällt, verfügt der Survivor über 0/1, und der Cluster wird herunterfährt. Wenn der Abstimmungs Knoten ordnungsgemäß heruntergefahren wird, wird die Stimme an den anderen Knoten übertragen, und der Cluster wird nicht mehr angezeigt. ***Aus diesem Grund ist es wichtig, einen Zeugen zu konfigurieren.***

![Quorum, das im Fall von zwei Knoten ohne Zeugen erläutert wird](media/understand-quorum/2-node-no-witness.png)

- Kann einen Server Fehler überstehen: **50-prozentige Chance**.
- Kann einen Server Fehler überstehen, dann ein weiterer: **Nein**.
- Kann zwei Server Fehler gleichzeitig überstehen: **Nein**. 

#### <a name="two-nodes-with-a-witness"></a>Zwei Knoten mit einem Zeugen. 
Beide Knoten Stimmen zusammen mit den Zeugen Stimmen, sodass die *Mehrzahl* aus insgesamt **3 Stimmen**ergibt. Wenn ein Knoten ausfällt, verfügt der Survivor über 2/3, und der Cluster wird noch nicht angezeigt.

![Quorum, das im Fall von zwei Knoten mit einem Zeugen erläutert wird](media/understand-quorum/2-node-witness.png)

- Kann einen Server Fehler überstehen: **Ja**.
- Kann einen Server Fehler überstehen, dann ein weiterer: **Nein**.
- Kann zwei Server Fehler gleichzeitig überstehen: **Nein**. 

#### <a name="three-nodes-without-a-witness"></a>Drei Knoten ohne Zeugen.
Alle Knoten Stimmen ab, sodass die *Mehrheit* von insgesamt **3 Stimmen**bestimmt wird. Wenn ein Knoten ausfällt, sind die Überlebenden 2/3, und der Cluster wird nicht mehr vorhanden sein. Der Cluster wird zu zwei Knoten ohne Zeugen – zu diesem Zeitpunkt befinden Sie sich in Szenario 1.

![Das Quorum wird im Fall von drei Knoten ohne Zeugen erläutert.](media/understand-quorum/3-node-no-witness.png)

- Kann einen Server Fehler überstehen: **Ja**.
- Kann einen Server Fehler überstehen, dann ein weiterer Wert: **50 Prozent**.
- Kann zwei Server Fehler gleichzeitig überstehen: **Nein**. 

#### <a name="three-nodes-with-a-witness"></a>Drei Knoten mit einem Zeugen.
Alle Knoten Stimmen ab, sodass der Zeuge nicht anfänglich stimmt. Die *Mehrheit* wird aus insgesamt **3 Stimmen**ermittelt. Nach einem Fehler verfügt der Cluster über zwei Knoten mit einem Zeugen – der wieder zu Szenario 2 gehört. Nun stimmen die beiden Knoten und der Zeuge ab.

![Quorum, das im Fall von drei Knoten mit einem Zeugen erläutert wird](media/understand-quorum/3-node-witness.png)

- Kann einen Server Fehler überstehen: **Ja**.
- Kann einen Server Fehler überstehen, dann einen weiteren: **Ja**.
- Kann zwei Server Fehler gleichzeitig überstehen: **Nein**. 

#### <a name="four-nodes-without-a-witness"></a>Vier Knoten ohne Zeugen
Die Stimme eines Knotens wird als nulloverwert festgelegt, sodass die *Mehrheit* aus insgesamt **3 Stimmen**ergibt. Nach einem Fehler wird der Cluster zu drei Knoten, und Sie sind in Szenario 3.

![Das Quorum wird im Fall von vier Knoten ohne Zeugen erläutert.](media/understand-quorum/4-node-no-witness.png)

- Kann einen Server Fehler überstehen: **Ja**.
- Kann einen Server Fehler überstehen, dann einen weiteren: **Ja**.
- Kann zwei Serverausfälle gleichzeitig überstehen: **50 Prozent der Chance**. 

#### <a name="four-nodes-with-a-witness"></a>Vier Knoten mit einem Zeugen.
Alle Knoten Stimmen und der Zeuge Stimmen ab, sodass die *Mehrheit* von insgesamt **5 Stimmen**bestimmt wird. Nach einem Fehler sind Sie in Szenario 4. Nach zwei gleichzeitigen Fehlern überspringen Sie das Szenario 2.

![Quorum, das im Fall von vier Knoten mit einem Zeugen erläutert wird](media/understand-quorum/4-node-witness.png)

- Kann einen Server Fehler überstehen: **Ja**.
- Kann einen Server Fehler überstehen, dann einen weiteren: **Ja**.
- Kann zwei Server Fehler gleichzeitig überstehen: **Ja**. 

#### <a name="five-nodes-and-beyond"></a>Fünf Knoten und darüber hinaus.
Alle Knoten Stimmen oder nur eine Stimme ab, je nachdem, was das Gesamtergebnis ist. Direkte Speicherplätze können nicht mehr als zwei Knoten gleich sehen. an diesem Punkt ist daher kein Zeuge erforderlich oder nützlich.

![Das Quorum wird im Fall von fünf Knoten und darüber hinaus erläutert.](media/understand-quorum/5-nodes.png)

- Kann einen Server Fehler überstehen: **Ja**.
- Kann einen Server Fehler überstehen, dann einen weiteren: **Ja**.
- Kann zwei Server Fehler gleichzeitig überstehen: **Ja**. 

Nachdem wir nun wissen, wie das Quorum funktioniert, betrachten wir die Typen von Quorum Zeugen.

### <a name="quorum-witness-types"></a>Quorum Zeugen Typen

Failoverclustering unterstützt drei Arten von Quorum Zeugen:

- **[Cloud Witness](../../failover-clustering/deploy-cloud-witness.md)** : BLOB Storage in Azure, auf den alle Knoten des Clusters zugreifen. Sie verwaltet Clustering-Informationen in einer Datei "Witness. log", speichert jedoch keine Kopie der Cluster Datenbank.
- **Datei** frei gaben Zeuge – eine SMB-Dateifreigabe, die auf einem Dateiserver konfiguriert ist, auf dem Windows Server ausgeführt wird. Sie verwaltet Clustering-Informationen in einer Datei "Witness. log", speichert jedoch keine Kopie der Cluster Datenbank.
- Datenträger **Zeuge** : ein kleiner gruppierter Datenträger, der sich in der verfügbaren Speicher Gruppe des Clusters befindet. Dieser Datenträger ist hoch verfügbar und kann ein Failover zwischen Knoten durch finden. Sie enthält eine Kopie der Cluster Datenbank.  ***Ein Datenträger Zeuge wird von direkte Speicherplätze nicht unterstützt***.

## <a name="pool-quorum-overview"></a>Übersicht über das Pool Quorum

Wir haben soeben über das Cluster Quorum gesprochen, das auf Cluster Ebene funktioniert. Sehen wir uns nun das Pool Quorum an, das auf Poolebene funktioniert (d. h. Sie können Knoten und Laufwerke verlieren und den Pool in Betrieb nehmen). Speicherpools wurden so entworfen, dass Sie in gruppierten und nicht gruppierten Szenarien verwendet werden, weshalb Sie über einen anderen Quorum Mechanismus verfügen.

Die folgende Tabelle enthält eine Übersicht über die Ergebnisse des Pool Quorums pro Szenario:

| Server Knoten | Kann einen Server Knoten Fehler überstehen. | Kann einen Server Knoten Fehler überstehen, ein weiterer | Kann zwei gleichzeitige Server Knoten Ausfälle überstehen |
|--------------|-------------------------------------|---------------------------------------------------|----------------------------------------------------|
| 2            | Nein                                  | Nein                                                | Nein                                                 |
| 2 + Zeuge  | Ja                                 | Nein                                                | Nein                                                 |
| 3            | Ja                                 | Nein                                                | Nein                                                 |
| 3 + Zeuge  | Ja                                 | Nein                                                | Nein                                                 |
| 4            | Ja                                 | Nein                                                | Nein                                                 |
| 4 + Zeuge  | Ja                                 | Ja                                               | Ja                                                |
| 5 und höher  | Ja                                 | Ja                                               | Ja                                                |

## <a name="how-pool-quorum-works"></a>Funktionsweise des Pool Quorums

Wenn Laufwerke fehlschlagen oder eine Teilmenge der Laufwerke den Kontakt mit einer anderen Teilmenge verliert, müssen die überprüfenden Laufwerke sicherstellen, dass Sie den *Großteil* des Pools als online bleiben. Wenn Sie dies nicht überprüfen können, werden Sie offline geschaltet. Der Pool ist die Entität, die offline geschaltet wird oder online bleibt, je nachdem, ob Sie über genügend Datenträger für das Quorum verfügt (50% + 1). Der Besitzer der Pool Ressource (aktiver Cluster Knoten) kann + 1 sein.

Das Pool Quorum funktioniert jedoch auf folgende Weise anders als das Cluster Quorum:

- der Pool verwendet einen Knoten im Cluster als Zeuge, um die Hälfte der Laufwerke zu überstehen (dieser Knoten ist der Besitzer der Pool Ressource).
- der Pool weist kein dynamisches Quorum auf.
- der Pool implementiert nicht seine eigene Version zum Entfernen einer Stimme.

### <a name="examples"></a>Beispiele

#### <a name="four-nodes-with-a-symmetrical-layout"></a>Vier Knoten mit einem symmetrischen Layout. 
Jedes der 16 Laufwerke verfügt über eine Stimme, und Knoten zwei hat ebenfalls eine Stimme (da es sich um den Pool Ressourcen Besitzer handelt). Die *Mehrheit* wird von insgesamt **16 Stimmen**bestimmt. Wenn die Knoten drei und vier ausfallen, verfügt die verbleibende Teilmenge über 8 Laufwerke und den Pool Ressourcen Besitzer (9/16 Stimmen). Der Pool wird also nicht mehr angezeigt.

![Pool Quorum 1](media/understand-quorum/pool-1.png)

- Kann einen Server Fehler überstehen: **Ja**.
- Kann einen Server Fehler überstehen, dann einen weiteren: **Ja**.
- Kann zwei Server Fehler gleichzeitig überstehen: **Ja**. 

#### <a name="four-nodes-with-a-symmetrical-layout-and-drive-failure"></a>Vier Knoten mit einem symmetrischen Layout und Laufwerk Fehler. 
Alle 16 Laufwerke haben eine Stimme, und Knoten 2 verfügt auch über eine Stimme (da es sich um den Besitzer der Pool Ressource handelt). Die *Mehrheit* wird von insgesamt **16 Stimmen**bestimmt. Zuerst wird Laufwerk 7 heruntergefahren. Wenn die Knoten drei und vier ausfallen, verfügt die verbleibende Teilmenge über 7 Laufwerke und den Pool Ressourcen Besitzer (8/16 Stimmen). Der Pool hat also keine Mehrheit und ist nicht mehr vorhanden.

![Pool Quorum 2](media/understand-quorum/pool-2.png)

- Kann einen Server Fehler überstehen: **Ja**.
- Kann einen Server Fehler überstehen, dann ein weiterer: **Nein**.
- Kann zwei Server Fehler gleichzeitig überstehen: **Nein**. 

#### <a name="four-nodes-with-a-non-symmetrical-layout"></a>Vier Knoten mit einem nicht symmetrischen Layout. 
Jedes der 24 Laufwerke verfügt über eine Stimme, und Knoten zwei hat ebenfalls eine Stimme (da es sich um den Pool Ressourcen Besitzer handelt). Die *Mehrheit* wird von insgesamt **24 Stimmen**bestimmt. Wenn die Knoten drei und vier ausfallen, verfügt die verbleibende Teilmenge über 8 Laufwerke und den Pool Ressourcen Besitzer (9/24 Stimmen). Der Pool hat also keine Mehrheit und ist nicht mehr vorhanden.

![Pool Quorum 3](media/understand-quorum/pool-3.png)

- Kann einen Server Fehler überstehen: **Ja**.
- Kann einen Server Fehler überstehen, ein anderes: * * hängt von * * ab (kann nicht überleben, wenn beide Knoten drei und vier ausfallen, aber alle anderen Szenarien überstehen können.
- Kann zwei Server Fehler gleichzeitig überstehen: * * hängt von * * ab (kann nicht überleben, wenn beide Knoten drei und vier ausfallen, aber alle anderen Szenarien überstehen können.

### <a name="pool-quorum-recommendations"></a>Empfehlungen für Pool Quorum

- Stellen Sie sicher, dass jeder Knoten im Cluster symmetrisch ist (jeder Knoten verfügt über die gleiche Anzahl von Laufwerken).
- Aktivieren Sie drei-Wege-Spiegelung oder duale Parität, damit Sie Knoten Ausfälle tolerieren und die virtuellen Datenträger online halten können. Weitere Informationen finden Sie auf unserer Seite mit den [Volumen Anleitungen](plan-volumes.md) .
- Wenn mehr als zwei Knoten heruntergefahren sind oder zwei Knoten und ein Datenträger auf einem anderen Knoten ausfällt, haben die Volumes möglicherweise keinen Zugriff auf alle drei Kopien Ihrer Daten und werden deshalb offline geschaltet und sind nicht verfügbar. Es wird empfohlen, die Server wieder zu nutzen oder die Datenträger schnell zu ersetzen, um die höchste Resilienz für alle Daten auf dem Volume sicherzustellen.

## <a name="more-information"></a>Weitere Informationen

- [Konfigurieren und Verwalten des Quorums](../../failover-clustering/manage-cluster-quorum.md)
- [Bereitstellen eines Cloudzeugen](../../failover-clustering/deploy-cloud-witness.md)
