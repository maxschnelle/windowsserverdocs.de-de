---
title: Szenarien für die notfallwiederherstellung für Hyper-konvergiert-Infrastruktur
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: johnmarlin-msft
ms.date: 03/29/2018
description: Dieser Artikel beschreibt die Szenarien, die heute verfügbar sind, für die notfallwiederherstellung von Microsoft HCI (Storage Spaces Direct)
ms.localizationpriority: medium
ms.openlocfilehash: 32bbf02ca78d5c6a2147162768c984d0e0b27e36
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879591"
---
# <a name="disaster-recovery-with-storage-spaces-direct"></a>Notfallwiederherstellung mit "direkte Speicherplätze"

> Gilt für: Windows Server 2019, Windows Server 2016

Dieses Thema enthält Sie Szenarien wie hyperkonvergenten Infrastruktur (HCL) für die notfallwiederherstellung können so konfiguriert werden.

Zahlreiche Unternehmen hyperkonvergenten Lösungen ausgeführt werden, und Planen eines Notfalls ermöglicht, noch in oder schnell wieder in die Produktion, wenn ein Notfall auftritt. Es gibt mehrere Möglichkeiten zum Konfigurieren von HCI für die notfallwiederherstellung und in diesem Dokument erläutert die Optionen, die heute für Sie verfügbar sind.

Wenn Diskussionen der Wiederherstellung der Verfügbarkeit bei einem Notfall als Recovery Time Objective (RTO genannten) betreffen. Dies ist die Zeitspanne, die als Ziel, in denen Dienste wiederhergestellt werden muss, um unzulässige Auswirkungen auf das Geschäft zu vermeiden. In einigen Fällen kann dieser Vorgang automatisch mit fast sofort wiederhergestellt auftreten. In anderen Fällen muss manuelle Administratoreingriff erfolgen, um Dienste wiederherzustellen.

Die Optionen für die notfallwiederherstellung mit einer hyperkonvergenten sind heute:

1. Funktion "Speicherreplikat" mithilfe mehrerer-Clustern
2. Hyper-V-Replikat zwischen Clustern
3. Sicherung und Wiederherstellung

## <a name="multiple-clusters-utilizing-storage-replica"></a>Funktion "Speicherreplikat" mithilfe mehrerer-Clustern

[Funktion "Speicherreplikat"](../storage-replica/storage-replica-overview.md) ermöglicht die Replikation von Volumes und unterstützt die synchrone und asynchrone Replikation. Bei der Auswahl zwischen der Verwendung von entweder synchron oder asynchron Replikation sollten Sie Ihre Recovery Point Objective (RPO). RPO ist die Menge eines möglichen Datenverlusts, die Sie bereit sind, entstehen, bevor sie mit wichtigen Verlust gilt. Wenn Sie bei der synchronen Replikation wechseln, wird es für beide Enden sequenziell zur gleichen Zeit schreiben. Wenn Sie mit asynchronen wechseln, werden Schreibvorgänge werden sehr schnell replizieren jedoch verloren gegangen sein könnte. Sie sollten berücksichtigen, dass die Anwendung oder Datei Nutzung finden Sie unter der sich am besten für Sie funktioniert.

Funktion "Speicherreplikat" ist eine Ebene kopiermechanismen Block im Vergleich zu Dateiebene. Das heißt, spielt es keine Rolle welche Arten von Daten, die repliziert werden. Dies macht es eine beliebte Option für den hyperkonvergenten Infrastruktur. Funktion "Speicherreplikat" kann auch andere Arten von Laufwerken zwischen den Replikationspartnern, daher haben alle eine Art von Speicher auf einem HCI nutzen und einen anderen Typenspeicher auf dem anderen ist in Ordnung. 

Eine wichtige Funktion von Funktion "Speicherreplikat" ist, dass es in Azure als auch lokal ausgeführt werden kann. Sie können lokal zu lokal, Azure zu Azure oder sogar lokal in Azure (oder umgekehrt) einrichten.

In diesem Szenario sind zwei separate unabhängige Cluster. Zum Konfigurieren von Funktion "Speicherreplikat" zwischen HCI, Sie können die Schritte in [Cluster-zu-Cluster-Speicherreplikation](../storage-replica/cluster-to-cluster-storage-replication.md).

![Diagramm der Storage-Replikation](media\storage-spaces-direct-disaster-recovery\Disaster-Recovery-Figure1.png)

Die folgenden Überlegungen gelten beim Bereitstellen der Funktion "Speicherreplikat". 

1.  Konfigurieren der Replikation erfolgt außerhalb der Failover-Clusterunterstützung. 
2.  Auswählen der Methode der Replikation werden abhängig von Ihren Netzwerklatenz und der RPO-Anforderungen. Synchron repliziert die Daten in Netzwerken mit geringer Latenz mit Absturzkonsistenz, um sicherzustellen, dass kein Datenverlust zu einem Zeitpunkt des Fehlers an. Asynchrone repliziert die Daten über Netzwerke mit höherer Latenz kommen, aber jeder Standort verfügen möglicherweise nicht identische Kopien zu einem Zeitpunkt des Fehlers. 
3.  Im Fall eines Notfalls Failover zwischen den Clustern werden nicht automatisch und manuell über die Storage-Replikat-PowerShell-Cmdlets koordiniert werden müssen. Im obigen Diagramm ClusterA ist der primäre und ClusterB der sekundäre Server. Wenn ClusterA ausfällt, müssen Sie würde manuell ClusterB als primär festlegen, bevor Sie die Ressourcen öffnen können. Sobald ClusterA wieder verfügbar ist, müssten Sie sekundäre Datenbank zu erleichtern. Nachdem alle Daten wurden Sie synchronisiert wurden, nehmen Sie die Änderung ein, und tauschen Sie die Rollen wieder auf die Möglichkeit, die sie ursprünglich festgelegt wurden.
4.  Da die Funktion "Speicherreplikat" nur die Daten repliziert wird, müssen eine neue virtuelle Maschine oder die Scale Out-Datei Server Skalierung (SOFS) verwenden diese Daten in Failovercluster-Manager auf das Replikat erstellt werden.

Funktion "Speicherreplikat" kann verwendet werden, wenn Sie virtuelle Maschinen oder eines SOFS, die in Ihrem Cluster ausgeführt haben. Onlineschalten von Ressourcen im Replikat HCI kann manuell oder durch die Verwendung von PowerShell-Skripts automatisiert sein.

## <a name="hyper-v-replica"></a>Hyper-V-Replikat

[Hyper-V-Replikat](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/set-up-hyper-v-replica) Ebene Replikation des virtuellen Computers für die notfallwiederherstellung für hyperkonvergente Infrastrukturen enthält. Hyper-V-Replikat Möglichkeiten ist, einen virtuellen Computer und auf einem sekundären Standort oder in Azure (Replikat) repliziert werden. Dann können vom sekundären Standort, Hyper-V-Replikat replizieren des virtuellen Computers in einer dritten (Erweiterte Replikat).

![Diagramm für Hyper-V-Replikation](media\storage-spaces-direct-disaster-recovery\Disaster-Recovery-Figure2.png)

Mit Hyper-V-Replikat wird die Replikation von Hyper-V übernommen. Wenn Sie erstmals einen virtuellen Computer für die Replikation aktivieren, gibt es drei Optionen für die sollen wie für der ersten Kopie an das entsprechende Replikat-Cluster gesendet werden.

1.  Die erste Kopie über das Netzwerk gesendet.
2.  Senden Sie die erste Kopie auf externe Medien, sodass sie manuell auf den Server kopiert werden können
3.  Verwenden einer vorhandenen virtuellen Maschine, die bereits auf den replikathosts erstellt.

Die andere Option ist für, wenn Sie möchten, dass diese anfängliche Replikation durchgeführt werden soll.

1.  Die Replikation sofort starten
2.  Planen Sie eine Uhrzeit für die bei die erste Replikation stattfindet. 

Weitere Überlegungen, die Sie benötigen werden:

- Welche VHD/VHDXs Sie replizieren möchten. Sie können auch alle oder nur einer von ihnen zu replizieren.
- Die Anzahl der Wiederherstellungspunkte, die Sie speichern möchten. Wenn Sie möchten, gibt es mehrere Möglichkeiten, zu welchem Zeitpunkt Punkt, die Sie wiederherstellen möchten, klicken Sie dann möchten Sie angeben, wie viele werden sollen. Wenn Sie nur einen Wiederherstellungspunkt möchten, können Sie, die ebenfalls auswählen.
- Wie oft Sie möchten die eine inkrementelle Schattenkopien replizieren Volume Shadow Copy Service (VSS) haben.
- Wie oft Änderungen repliziert (30 Sekunden, 5 Minuten, 15 Minuten).

Wenn HCI teilnehmen in Hyper-V-Replikat, benötigen Sie die [Hyper-V-Replikatbroker](https://blogs.technet.microsoft.com/virtualization/2012/03/27/why-is-the-hyper-v-replica-broker-required/) in jedem Cluster erstellten Ressource. Diese Ressource führt mehrere Aufgaben aus:

1.  Erhalten Sie einen einzelnen Namespace für jeden Cluster für Hyper-V-Replikat für die Verbindung.
2.  Bestimmt, welcher Knoten innerhalb dieses Clusters, der das Replikat (oder die erweiterten Replikat) auf befinden soll, wenn sie zuerst die Kopie erhält.
3.  Verfolgt des welchem Knoten das Replikat (oder die erweiterten Replikat) besitzt, für den Fall, dass die virtuelle Maschine auf einen anderen Knoten verschoben wird. Es muss dies nachverfolgen, sodass bei der Replikation erfolgt, die Informationen auf den richtigen Knoten senden können.

## <a name="backup-and-restore"></a>Sicherung und Wiederherstellung

Eine herkömmliche Disaster-Recovery-Option, die ist nicht gesprochen, sehr ähnlich, jedoch ist genauso wichtig ist, einen Fehler im gesamten Cluster oder einen Knoten im Cluster. Beiden Optionen in diesem Szenario wird von Windows NT Backup verwenden. 

Es ist immer eine Empfehlung für regelmäßige Sicherungen der hyperkonvergenten Infrastruktur haben. Während der Clusterdienst, ausgeführt wird Wenn Sie eine Systemstatussicherung verwenden, wäre die Registrierungsdatenbank für den Cluster ein Teil dieser Sicherung. Wiederherstellen des Clusters oder der Datenbank bietet zwei verschiedene Installationsmethoden, die (nicht-autorisierend und autorisiert).

### <a name="non-authoritative"></a>Nicht-autoritative

Eine nicht autoritative Wiederherstellung mithilfe von Windows NT Backup ausgeführt werden kann und entspricht einer vollständigen Wiederherstellung nur Cluster-Knoten selbst. Wenn Sie nur ein Knoten (und der Registrierung Clusterdatenbank) wiederherstellen müssen und alle aktuellen Clusterinformationen gut, Sie werden beim Wiederherstellen nicht autorisierend. Nicht-autorisierende Wiederherstellungen können über die Windows NT Backup-Benutzeroberfläche oder der Befehlszeile WBADMIN erfolgen. EXE-DATEI.

Nachdem Sie den Knoten wiederhergestellt haben, können sie dem Cluster beitreten. Was passiert ist, wird auf der die vorhandenen aktiven Cluster und alle zugehörigen Informationen mit, was derzeit es jedoch ist zu aktualisieren.

### <a name="authoritative"></a>Autorisierende

Einer autorisierenden Wiederherstellung der Clusterkonfiguration, wird auf der anderen Seite die Cluster-Konfiguration in der Zeit zurück. Diese Art von Wiederherstellung sollte nur erfolgen, wenn die Clusterinformationen selbst verloren gehen und muss wiederhergestellt wurde. Beispielsweise jemand versehentlich gelöscht, einen Dateiserver, die mehr als 1.000 Freigaben enthalten, und Sie benötigen diese später wieder. Eine autorisierende Wiederherstellung des Clusters erfordert, dass die Sicherung über die Befehlszeile ausgeführt werden.

Wenn auf einem Clusterknoten eine autorisierende Wiederherstellung initiiert wird, wird der Clusterdienst auf allen anderen Knoten in der Ansicht der Cluster beendet, und die Clusterkonfiguration ist fixiert. Daher ist es wichtig ist, dass der Clusterdienst auf dem Knoten, auf dem die Wiederherstellung ausgeführt wurde, zuerst gestartet werden, damit der Cluster gebildet wird, verwenden die neue Kopie der Clusterkonfiguration.

Führen Sie über eine autorisierende Wiederherstellung können die folgenden Schritte ausgeführt werden.

1.  Führen Sie WBADMIN. EXE-Datei aus einer administrativen Eingabeaufforderung um die neueste Version von Sicherungen zu erhalten, die Sie installieren möchten und stellen Sie sicher, dass den Systemstatus der Komponenten ist, können Sie wiederherstellen.

    ```powershell
    Wbadmin get versions
    ```

2.  Bestimmt, ob die Version-Sicherung haben Sie die Clusterinformationen für die Registrierung als Komponente enthält. Es gibt einige Punkte, die Sie von diesem Befehl, die Version und die Anwendung/Komponente für die Verwendung in Schritt 3 benötigen. Für die Version z. B. die Sicherung wurde am 3. Januar 2018 um 2:04 Uhr beendet, und dies ist der benötigten wiederhergestellt.

    ```powershell
    wbadmin get items -backuptarget:\\backupserver\location
    ```

3.  Starten Sie die autorisierende Wiederherstellung aus, um nur die Clusterversion Registrierung wiederherzustellen, die Sie benötigen. 

    ```powershell
    wbadmin start recovery -version:01/03/2018-02:04 -itemtype:app -items:cluster
    ```

Nach die Wiederherstellung stattgefunden hat, muss dieser Knoten die Vorlage zum Starten des Clusterdiensts zuerst und den Cluster bilden. Alle anderen Knoten müssten dann gestartet werden, und den Cluster beitreten.

## <a name="summary"></a>Zusammenfassung 

Wenn dies ganz summieren möchten, ist die hyper-konvergiert notfallwiederherstellung etwas, das Sie sorgfältig geplant werden sollte. Es gibt mehrere Szenarien, die können am besten Ihren Anforderungen und sollte gründlich getestet werden kann. Ein Element zu beachten ist, dass wenn Sie in der Vergangenheit mit Failoverclustern vertraut sind, Stretched Cluster eine sehr beliebte Option im Laufe der Jahre wurden. Gab es ein wenig einer entwurfsänderung mit der Lösung für die hyper-konvergiert, und sie basiert auf resilienz. Wenn Sie zwei Knoten in einem hyperkonvergenten Cluster verlieren, wird der gesamte Cluster ausfallen. Mit diesem wird der Fall, in einer Umgebung mit hyper-konvergiert ist die Stretch-Szenario nicht unterstützt.


