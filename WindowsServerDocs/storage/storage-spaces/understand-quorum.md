---
title: Grundlegendes zu-Cluster und Pool quorum
description: Grundlegendes zu-Cluster und Pool-Quorum mit bestimmten Beispielen über die Komplexität geleitet.
keywords: "\"Direkte Speicherplätze\", Quorum, Zeugen, S2D, Cluster-Pool Quorum, Quorumcluster, Threadpool"
ms.prod: windows-server-threshold
ms.author: adagashe
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 01/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 24890b191db8bc6934132857e830d4f77c394b02
ms.sourcegitcommit: 28dc7c7f1e44fee7ab2112228af329a9ce0e02ba
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/22/2019
ms.locfileid: "9024139"
---
# Grundlegendes zu-Cluster und Pool quorum

>Gilt für: WindowsServer 2019, WindowsServer 2016

[Windows Server-Failoverclustering](../../failover-clustering/failover-clustering-overview.md) bietet hohen Verfügbarkeit von Workloads. Diese Ressourcen gelten als hoch verfügbare, wenn Sie die Knoten, die Ressourcen enthalten sind. Allerdings muss der Cluster in der Regel mehr als die Hälfte die Knoten ausgeführt werden, die wird als mit *Quorum*bezeichnet.

Quorum soll verhindern, dass *Split Brain* Szenarien, die auftreten können, wenn es eine Partition im Netzwerk und Teilmengen von Knoten können nicht miteinander kommunizieren. Dies kann dazu führen, dass beide Teilmengen von Knoten zu versuchen, die Workload und die Schreiben auf dem gleichen Datenträger, die zahlreiche Probleme verursachen kann. Dies wird jedoch mit Failover-Clusterunterstützung Konzept des Quorums verhindert die erzwingt, nur eine dieser Gruppen von Knoten dass, die weiterhin ausgeführt, damit nur eine dieser Gruppen online bleibt.

Quorum bestimmt die Anzahl der Fehler, die der Cluster trotzdem online tolerieren kann. Quorum wurde entwickelt, um das Szenario, wenn ein bei der Kommunikation zwischen Teilmengen von Clusterknoten Problem, damit mehrere Server sollten Sie nicht gleichzeitig eine Ressourcengruppe hosten und zur gleichen Zeit auf dem gleichen Datenträger zu schreiben. Da dieses Konzept des Quorums, erzwingt Cluster den Clusterdienst beenden in einem der Teilmengen von Knoten, um sicherzustellen, dass nur eine "true" Besitzer einer bestimmten Gruppe vorhanden ist. Nachdem der Knoten, die angehalten wurden erneut mit der wichtigsten Gruppe von Knoten kommunizieren können, werden sie automatisch treten Sie dem Cluster und starten Sie den Clusterdienst.

In Windows Server 2016 gibt es zwei Komponenten des Systems, die über eigene Mechanismen Quorum verfügen:

- <strong>Clusterquorum</strong>: Dies erfolgt auf der Clusterebene (d. h. Sie können verlorengeht Knoten und Cluster bleibt)
- <strong>Pool Quorum</strong>: Dies erfolgt auf der Poolebene, wenn "direkte Speicherplätze" aktiviert ist (d. h. Sie können verlorengeht Knoten und Laufwerke und den Pool bleibt). Speicher-Pools wurden entwickelt, um in gruppierten und nicht-Cluster-Szenarien verwendet werden, wird sie einen Quorummechanismus für die verschiedenen haben.

## Übersicht über die Cluster-quorum

Die folgende Tabelle enthält eine Übersicht über die Ergebnisse Clusterquorum pro Szenario:

| Server-Knoten | Ein Fehler der Server-Knoten können Überleben werden. | Kann ein Server-Knoten-Fehler, und dann eine andere übersteht. | Zwei gleichzeitige Server Knotenausfällen noch können vorhanden sind. |
|--------------|-------------------------------------|---------------------------------------------------|----------------------------------------------------|
| 2            | 50/50                               | Nein                                                | Nein                                                 |
| 2 + Zeugen  | Ja                                 | Nein                                                | Nein                                                 |
| 3            | Ja                                 | 50/50                                             | Nein                                                 |
| 3 + Zeugen  | Ja                                 | Ja                                               | Nein                                                 |
| 4            | Ja                                 | Ja                                               | 50/50                                              |
| 4 + Zeugen  | Ja                                 | Ja                                               | Ja                                                |
| 5 und höher  | Ja                                 | Ja                                               | Ja                                                |

### Cluster Quorum Empfehlungen

- Wenn Sie zwei Knoten vorhanden sind, ist ein Zeuge <strong>erforderlich</strong>.
- Wenn Sie drei oder vier Knoten vorhanden sind, ist Zeugen <strong>dringend empfohlen</strong>.
- Wenn Sie Zugriff auf das Internet haben, verwenden Sie eine <strong> [cloudzeugen](../../failover-clustering/deploy-cloud-witness.md)</strong>
- Wenn Sie in einer IT-Umgebung mit anderen Computern und Dateifreigaben sind, verwenden Sie einen dateifreigabezeugen

## Funktionsweise von Clusterquorum

Wenn Knoten ein Fehler oder eine Teilmenge der Knoten Kontakt mit einem anderen Teilmenge verliert, müssen verbleibenden Knoten, um sicherzustellen, dass sie die *Mehrzahl* der Cluster online bleiben bilden. Sie, die überprüfen, gehen sie offline.

Aber das Konzept der *meisten* nur funktioniert ordnungsgemäß, wenn die Gesamtzahl der Knoten im Cluster ungerade (z. B. drei Knoten in einem Cluster mit fünf Knoten) ist. Was ist Cluster mit eine gerade Zahl von Knoten (z. B. einen Cluster mit vier Knoten)?

Es gibt zwei Möglichkeiten, die der Cluster die *Gesamtzahl der stimmen* ungerade vornehmen kann:

1. Zunächst gelangen sie *Einrichten* eines durch *Zeugen* mit einer zusätzlichen Abstimmung hinzufügen. Dazu muss der Benutzer einrichten.
2.  Alternativ können *Sie* eine durch das Löschen des stimmen Sie einem weniger Knoten (geschieht automatisch nach Bedarf) wechseln.

Bei jedem verbleibenden Knoten erfolgreich stellen Sie, dass sie die *meisten*sind sicher, ist die Definition der *meisten* auf genau die überlebenden werden aktualisiert. Dies ermöglicht den Cluster einen Knoten einem anderen und dann eine andere, und so weiter. Dieses Konzept der *Gesamtzahl der stimmen* Anpassung nach aufeinander folgende Fehler genannt <strong> *dynamische Quorum*</strong>.  

### Dynamische Zeugen

Dynamische Zeugen Schaltet die Abstimmung der Zeugen, um sicherzustellen, dass die *Gesamtzahl der stimmen* ungerade ist. Wenn es eine ungerade Anzahl von stimmen gibt, nicht Zeugen verfügt über eine Stimme. Ist eine gerade Zahl von stimmen, hat der Zeuge hören. Dynamische Zeugen wird erheblich reduziert das Risiko, die der Cluster aufgrund Zeugen Fehler wird nach unten. Die Cluster entscheidet, ob verwenden die Zeugen Abstimmung basierend auf der Anzahl der Abstimmungsschaltflächen Knoten, die im Cluster verfügbar sind.

Dynamische Quorum funktioniert mit dynamischen Zeugen auf die unten beschriebenen Weise.

### Dynamische Quorum Verhalten

- Wenn Sie haben eine <strong>auch</strong> Anzahl der Knoten und keine Zeugen, *einem Knoten erhält seine Zustimmung auf NULL gesetzt*. Z. B. erhalten nur drei der vier Knoten stimmen, sodass die *Gesamtzahl der stimmen* drei und zwei Hinterbliebenen mit stimmen ein Großteil als gelten.
- Wenn Sie haben eine <strong>ungerade</strong> Anzahl der Knoten und keine Zeugen, *Alle erhalten wurde*.
- Wenn Sie haben eine <strong>auch</strong> Anzahl der Knoten sowie Zeugen, *Zeugen stimmen*, damit die Summe ungerade ist.
- Wenn Sie haben eine <strong>ungerade</strong> Anzahl der Knoten sowie Zeugen, *Zeugen stimmen nicht*.

Dynamische Quorum ermöglicht die Möglichkeit, eine Stimme zu einem Knoten dynamisch, um zu vermeiden, verlieren die Mehrzahl der stimmen und Cluster mit einem Knoten (bezeichnet als letzten Man geführt) ausführen können. Nehmen wir als Beispiel einen Cluster mit vier Knoten. Wird davon ausgegangen Sie, dass, wenn das Quorum 3 stimmen erfordert. 

In diesem Fall würde des Clusters unterbrochen haben Sie zwei Knoten verloren.

![Diagramm mit vier Clusterknoten, von denen jede eine Stimme erhält](media/understand-quorum/dynamic-quorum-base.png)

Verhindert, dass dynamische Quorum dies nicht der Fall. Die *Gesamtzahl der stimmen* für Quorum erforderlich ist jetzt bestimmt basierend auf der Anzahl von Knoten verfügbar. Ja, mit dynamischen Quorum Cluster einrichten bleibt, auch wenn Sie drei Knoten vergessen haben.

![Diagramm mit vier Clusterknoten mit Knoten fehl, eine, und die Anzahl der erforderlichen stimmen, die nach jeder Fehler anpassen.](media/understand-quorum/dynamic-quorum-step-through.png)

Die oben genannten Szenario gilt für eine allgemeine Cluster, der nicht "direkte Speicherplätze" aktiviert haben. Wenn "direkte Speicherplätze" aktiviert ist, kann jedoch Cluster nur zwei Knotenfehler unterstützen. Dies ist mehr im [Pool Quorum Abschnitt](#poolQuorum)erläutert.

### Beispiele

#### Zwei Knoten ohne einen Zeugen. 
Stimmen Sie einem Knoten wird gelöscht, damit *die Mehrheit* von insgesamt bestimmt wird <strong>1 Stimme</strong>. Wenn der Knoten nicht an der Abstimmung unerwartet ausfällt, die Hinterbliebenenversorgung ist 1/1 und Cluster zurückgegriffen werden kann. Wenn der Abstimmungsschaltflächen Knoten unerwartet ausfällt, die Hinterbliebenenversorgung hat 0/1 und Cluster ausfällt. Wenn der Abstimmungsschaltflächen Knoten problemlos ausgeschaltet ist, wird die Abstimmung auf den anderen Knoten übertragen und Cluster zurückgegriffen werden kann. *<strong>Daher ist es wichtig, einen Zeugen konfigurieren ist.</strong>*

![Im Fall mit zwei Knoten ohne einen Zeugen erläutert Quorum](media/understand-quorum/2-node-no-witness.png)

- Kann ein Serverfehler Überleben: <strong>50 % Wahrscheinlichkeit</strong>.
- Kann ein Serverfehler, und klicken Sie dann einen anderen Überleben: <strong>Nein</strong>.
- Zwei Serverfehler können gleichzeitig Überleben: <strong>Nein</strong>. 

#### Zwei Knoten mit Zeugen. 
Beide Knoten stimmen, sowie die Zeugen stimmen, damit die *meisten* von insgesamt bestimmt wird <strong>3 stimmen</strong>. Wenn Knoten ausfällt, die Hinterbliebenenversorgung hat 2/3 und Cluster zurückgegriffen werden kann.

![Im Fall mit zwei Knoten mit Zeugen erläutert Quorum](media/understand-quorum/2-node-witness.png)

- Kann ein Serverfehler Überleben: <strong>Ja</strong>.
- Kann ein Serverfehler, und klicken Sie dann einen anderen Überleben: <strong>Nein</strong>.
- Zwei Serverfehler können gleichzeitig Überleben: <strong>Nein</strong>. 

#### Drei Knoten ohne einen Zeugen.
Alle Knoten stimmen, so dass die *meisten* von insgesamt bestimmt wird <strong>3 stimmen</strong>. Wenn ein Knoten ausfällt, Hinterbliebene sind 2/3 und Cluster zurückgegriffen werden kann. Cluster wird zwei Knoten ohne einen Zeugen – an diesem Punkt befinden sich im Szenario 1.

![Im Fall mit drei Knoten ohne einen Zeugen erläutert Quorum](media/understand-quorum/3-node-no-witness.png)

- Kann ein Serverfehler Überleben: <strong>Ja</strong>.
- Kann ein Serverfehler, und klicken Sie dann einen anderen Überleben: <strong>50 % Wahrscheinlichkeit</strong>.
- Zwei Serverfehler können gleichzeitig Überleben: <strong>Nein</strong>. 

#### Drei Knoten mit Zeugen.
Alle Knoten stimmen, damit der Zeuge anfänglich stimmen nicht. Die *meisten* wird bestimmt, von insgesamt <strong>3 stimmen</strong>. Nach einem Fehler hat Cluster zwei Knoten mit Zeugen – das Szenario 2 ist. Ja, stimmen jetzt zwei Knoten und Zeugen.

![Im Fall mit drei Knoten mit Zeugen erläutert Quorum](media/understand-quorum/3-node-witness.png)

- Kann ein Serverfehler Überleben: <strong>Ja</strong>.
- Kann ein Serverfehler, und klicken Sie dann einen anderen Überleben: <strong>Ja</strong>.
- Zwei Serverfehler können gleichzeitig Überleben: <strong>Nein</strong>. 

#### Vier Knoten ohne einen Zeugen
Stimmen Sie einem Knoten wird gelöscht, so dass die *meisten* von insgesamt bestimmt wird <strong>3 stimmen</strong>. Klicken Sie nach einem Fehler des Clusters wird drei Knoten, und Sie befinden sich im Szenario 3.

![Im Fall mit vier Knoten ohne einen Zeugen erläutert Quorum](media/understand-quorum/4-node-no-witness.png)

- Kann ein Serverfehler Überleben: <strong>Ja</strong>.
- Kann ein Serverfehler, und klicken Sie dann einen anderen Überleben: <strong>Ja</strong>.
- Zwei Serverfehler können gleichzeitig Überleben: <strong>50 % Wahrscheinlichkeit</strong>. 

#### Vier Knoten mit Zeugen.
Alle Knoten wurde und die Zeugen stimmen, so dass die *meisten* von insgesamt bestimmt wird <strong>5 stimmen</strong>. Sie können nach einem Fehler in Szenario 4. Nach zwei gleichzeitige Ausfälle überspringen Sie auf Szenario 2.

![Im Fall mit vier Knoten mit Zeugen erläutert Quorum](media/understand-quorum/4-node-witness.png)

- Kann ein Serverfehler Überleben: <strong>Ja</strong>.
- Kann ein Serverfehler, und klicken Sie dann einen anderen Überleben: <strong>Ja</strong>.
- Zwei Serverfehler können gleichzeitig Überleben: <strong>Ja</strong>. 

#### Fünf Knoten und mehr.
Stimmen Sie alle Knoten, oder alle bis auf eine Stimme, unabhängig ist die Summe ungerade. "Direkte Speicherplätze" kann nicht mehr als zwei Knoten nach unten trotzdem, behandelt, an dieser Stelle keine Zeugen erforderlichen oder hilfreich.

![Im Fall mit fünf Knoten und darüber hinaus erläutert Quorum](media/understand-quorum/5-nodes.png)

- Kann ein Serverfehler Überleben: <strong>Ja</strong>.
- Kann ein Serverfehler, und klicken Sie dann einen anderen Überleben: <strong>Ja</strong>.
- Zwei Serverfehler können gleichzeitig Überleben: <strong>Ja</strong>. 

Nun, da wir Verständnis der Funktionsweise von Quorum sehen wir uns die Arten von Quorum Zeugen.

### Quorum Zeugen Typen

Failover-Clusterunterstützung unterstützt drei Arten von Quorum Zeugen:

- <strong>[Cloud Witness](../../failover-clustering\deploy-cloud-witness.md) </strong> -BLOB-Speicher in Azure zugegriffen werden alle Knoten im Cluster. Es clustering Informationen in einer Datei witness.log verwaltet, aber keine Kopie der Clusterdatenbank gespeichert.
- <strong>Datei Teilen Zeugen</strong> – eine SMB-Dateifreigabe, die auf einem Dateiserver unter Windows Server konfiguriert ist. Es clustering Informationen in einer Datei witness.log verwaltet, aber keine Kopie der Clusterdatenbank gespeichert.
- <strong>Datenträger Zeugen</strong> -einen kleinen Clusterdatenträger die in der Gruppe Cluster verfügbaren Speicher ist. Die Festplatte ist hoch verfügbare und zwischen Knoten werden können. Es enthält eine Kopie der Clusterdatenbank.  <strong>*Ein Datenträger-Zeuge wird nicht unterstützt, mit "direkte Speicherplätze"*</strong>.

## <a id="poolQuorum"></a>Übersicht über die Pool quorum

Nur erwähnten wir Clusterquorum, das auf die Cluster-Ebene verwendet wird. Jetzt, fangen wir in Pool Quorum, die auf der Ebene des Pools ausgeführt wird (d. h. Sie können Knoten und Laufwerke und den Pool bleibt). Speicher-Pools wurden entwickelt, um in gruppierten und nicht-Cluster-Szenarien verwendet werden, wird sie einen Quorummechanismus für die verschiedenen haben.

Die folgende Tabelle enthält eine Übersicht über die Ergebnisse Pool Quorum pro Szenario:

| Server-Knoten | Ein Fehler der Server-Knoten können Überleben werden. | Kann ein Server-Knoten-Fehler, und dann eine andere übersteht. | Zwei gleichzeitige Server Knotenausfällen noch können vorhanden sind. |
|--------------|-------------------------------------|---------------------------------------------------|----------------------------------------------------|
| 2            | Nein                                  | Nein                                                | Nein                                                 |
| 2 + Zeugen  | Ja                                 | Nein                                                | Nein                                                 |
| 3            | Ja                                 | Nein                                                | Nein                                                 |
| 3 + Zeugen  | Ja                                 | Nein                                                | Nein                                                 |
| 4            | Ja                                 | Nein                                                | Nein                                                 |
| 4 + Zeugen  | Ja                                 | Ja                                               | Ja                                                |
| 5 und höher  | Ja                                 | Ja                                               | Ja                                                |

## Funktionsweise von Pool quorum

Wenn Laufwerke ausgefallen oder eine Untermenge von Laufwerken Kontakt mit einem anderen Teilmenge verliert, müssen verbliebenen Laufwerke, um sicherzustellen, dass sie den Pool online bleiben die *meisten* bilden. Sie, die überprüfen, gehen sie offline. Der Pool ist die Person, die offline geschaltet wird oder bleibt online basierend auf dessen genügend Laufwerke für Quorum (50 % + 1). Der Pool Ressourcenbesitzer (aktiven Clusterknoten) kann der + 1 sein.

Jedoch Pool Quorum funktioniert anders aus Clusterquorum auf folgende Weise:

- Pool verwendet einen Knoten im Cluster als Zeugen als Unterscheidung Überleben Hälfte der Laufwerke wurden (diese Knoten, der Besitzer des Pools Ressource ist)
- Pool hat keinen dynamischen quorum
- eine eigene Version der Abstimmung entfernen implementiert des Pools nicht.

### Beispiele

#### Vier Knoten mit einem symmetrisch Layout. 
Jedes 16 Laufwerke verfügt über eine Stimme und Knoten zwei verfügt auch über eine Stimme (da es der Besitzer des Pools Ressource ist). Die *meisten* wird bestimmt, von insgesamt <strong>16 stimmen</strong>. Wenn Knoten 3 und 4 abstürzt, hat die verbleibende Teilmenge 8 Laufwerke und der Besitzer der Pool-Ressource, der 9/16 stimmen ist. Daher aufgenommen wurde des Pools.

![Pool Quorum 1](media/understand-quorum/pool-1.png)

- Kann ein Serverfehler Überleben: <strong>Ja</strong>.
- Kann ein Serverfehler, und klicken Sie dann einen anderen Überleben: <strong>Ja</strong>.
- Zwei Serverfehler können gleichzeitig Überleben: <strong>Ja</strong>. 

#### Vier Knoten mit einem symmetrisch Fehler-Layout und -Laufwerk. 
Jedes 16 Laufwerke verfügt über eine Stimme und Knoten 2 verfügt auch über eine Stimme (da es der Besitzer des Pools Ressource ist). Die *meisten* wird bestimmt, von insgesamt <strong>16 stimmen</strong>. Zunächst fällt Laufwerk 7 aus. Wenn Knoten 3 und 4 abstürzt, hat die verbleibende Teilmenge 7 Laufwerke und der Besitzer der Pool-Ressource, der 8/16 stimmen ist. Pool keine also Mehrheit und ausfällt.

![Pool Quorum 2](media/understand-quorum/pool-2.png)

- Kann ein Serverfehler Überleben: <strong>Ja</strong>.
- Kann ein Serverfehler, und klicken Sie dann einen anderen Überleben: <strong>Nein</strong>.
- Zwei Serverfehler können gleichzeitig Überleben: <strong>Nein</strong>. 

#### Vier Knoten mit einem nicht symmetrisch Layout. 
Jedes der 24 Laufwerke hat eine Stimme und Knoten zwei verfügt auch über eine Stimme (da es der Besitzer des Pools Ressource ist). Die *meisten* wird bestimmt, von insgesamt <strong>24 stimmen</strong>. Wenn Knoten 3 und 4 abstürzt, hat die verbleibende Teilmenge 8 Laufwerke und der Besitzer der Pool-Ressource, der 9/24 stimmen ist. Pool keine also Mehrheit und ausfällt.

![Pool Quorum 3](media/understand-quorum/pool-3.png)

- Kann ein Serverfehler Überleben: <strong>Ja</strong>.
- Kann ein Serverfehler, und klicken Sie dann einen anderen Überleben: <strong>Depends </strong>(kann nicht überleben können, wenn beide Knoten 3 und 4 abstürzt, aber in allen anderen Szenarien können übersteht.
- Zwei Serverfehler können gleichzeitig Überleben: <strong>Depends </strong>(kann nicht überleben können, wenn beide Knoten 3 und 4 abstürzt, aber in allen anderen Szenarien können übersteht.

### Pool Quorum Empfehlungen

- Stellen Sie sicher, dass jeder Knoten im Cluster symmetrisch ist (jeder Knoten hat die gleiche Anzahl von Laufwerken)
- Aktivieren Sie drei-Wege-Spiegelung bzw. der dualen Parität, sodass Sie eine Knotenausfällen tolerieren und halten Sie die virtueller Datenträger online. Finden Sie auf unserer [Seite "Leitfaden" Volume](plan-volumes.md) für Weitere Informationen.
- Wenn mehr als zwei Knoten ausgefallen sind oder zwei Knoten und einen Datenträger auf einem anderen Knoten nach unten sind, Volumes unter Umständen keinen Zugriff auf alle drei Kopien ihrer Daten und daher offline geschaltet werden und nicht verfügbar. Es wird empfohlen, die Server wieder einblenden oder ersetzen die Datenträger schnell, um sicherzustellen, dass die meisten Stabilität für alle Daten auf dem Datenträger.

## Weitere Informationen

- [Konfigurieren und Verwalten des Quorums](../../failover-clustering/manage-cluster-quorum.md)
- [Bereitstellen eines cloudzeugen](../../failover-clustering/deploy-cloud-witness.md)
