---
title: Notfallwiederherstellungsszenarien für Hyperkonvergente Infrastruktur
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: johnmarlin-msft
ms.date: 03/29/2018
description: Dieser Artikel beschreibt die Szenarien erhältliche für die Wiederherstellung von Microsoft HCI ("direkte Speicherplätze")
ms.localizationpriority: medium
ms.openlocfilehash: 32bbf02ca78d5c6a2147162768c984d0e0b27e36
ms.sourcegitcommit: dfd25348ea3587e09ea8c2224237a3e8078422ae
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/16/2018
ms.locfileid: "4678609"
---
# Notfallwiederherstellung mit "direkte Speicherplätze"

> Gilt für: WindowsServer 2019, WindowsServer 2016

Dieses Thema enthält, dass Szenarien wie hyperkonvergente Infrastruktur (HCI) für die Wiederherstellung konfiguriert werden können.

Zahlreiche Unternehmen zusammengeführte Lösungen ausgeführt werden, und Planen von einem Notfall bietet die Möglichkeit, im verbleiben oder schnell wieder für die Produktion wäre eine Notfallsituation eintritt. Es gibt verschiedene Möglichkeiten zum Konfigurieren von HCI für notfallwiederherstellung und in diesem Dokument erläutert die Optionen, die heute für Sie verfügbar sind.

Wenn Diskussionen Verfügbarkeit wiederherstellen, wenn Notfall im Wesentlichen was als Recovery Time Objective (RTO) bekannt ist. Dies ist die Dauer bestimmt, in denen Dienste wiederhergestellt werden müssen, um unangemessen Folgen für das Unternehmen zu vermeiden. In einigen Fällen kann dieser Prozess automatisch bei Produktion wiederhergestellt fast sofort auftreten. In anderen Fällen muss Administrator manuelle Eingriffe erfolgen, um Dienste wiederherzustellen.

Notfall Wiederherstellungsoptionen mit einem hyperkonvergenten sind heute:

1. Mehrere Cluster für die Nutzung von Speicherreplikaten
2. Hyper-V-Replikat zwischen Clustern
3. Sichern und Wiederherstellen

## Mehrere Cluster für die Nutzung von Speicherreplikaten

[Das Speicherreplikat](../storage-replica/storage-replica-overview.md) ermöglicht die Replikation von Volumes und synchrone und asynchrone Replikation unterstützt. Bei der Entscheidung zwischen entweder synchron oder asynchron Replikation verwenden, sollten Sie Ihre Recovery Point Objective (RPO). Recovery Point Objective ist der Betrag möglichem Datenverlust, die Sie bereit sind, entstehen, bevor er größeren gilt. Wenn Sie bei der synchronen Replikation hinausgehen, wird er in beiden Enden nacheinander zur gleichen Zeit geschrieben. Wenn Sie mit asynchronen hinausgehen, Schreibvorgänge repliziert sehr schnell jedoch noch nicht mehr auffindbar sein. Sie sollten die Anwendung oder Datei Verwendung finden Sie unter dem für Sie am besten geeignet.

Das Speicherreplikatfeature ist ein Block Kopien Mechanismus im Vergleich zu Dateiebene; Was bedeutet, spielt es keine Rolle welche Arten von Daten, die repliziert. Dadurch wird eine beliebte Option für hyperkonvergenten Infrastrukturen. Speicher-Replikat kann auch verschiedene Arten von Laufwerken zwischen der Replikationspartner, also, da alle von einem Typenspeicher auf eine HCI nutzen und eine andere Art Speicher andererseits ist perfekt in Ordnung. 

Eine wichtige Funktion von Speicher-Replikat ist, dass sie in Azure als auch lokal ausgeführt werden kann. Sie können lokalen zu lokalen, Azure, Azure oder sogar lokale auf Azure (oder umgekehrt) einrichten.

In diesem Szenario gibt es zwei separate unabhängige Cluster. Konfigurieren von Speicherreplikaten zwischen HCI, können Sie die Schritte im [Cluster-zu-Cluster-Speicherreplikation](../storage-replica/cluster-to-cluster-storage-replication.md)ausführen.

![Diagramm der Speicher-Replikation](media\storage-spaces-direct-disaster-recovery\Disaster-Recovery-Figure1.png)

Bei der Bereitstellung von Speicher-Replikat ist Folgendes zu berücksichtigen. 

1.  Konfigurieren der Replikation erfolgt außerhalb des Failoverclustering. 
2.  Auswählen der Methode der Replikation wird die Netzwerklatenz und RPO Anforderungen abhängig sein. Synchrone Replikation der Daten in Netzwerken mit geringer Latenz mit Replikationsmodi Konsistenz um sicherzustellen, dass kein Datenverlust zu einem Zeitpunkt des Fehlers. Asynchrone Replikation die Daten über Netzwerke mit höherer Latenzen wider, jedoch mit jedem Standort verfügen möglicherweise nicht identische Kopien zu einem Zeitpunkt des Fehlers. 
3.  Bei einem Notfall Failovers zwischen Clustern sind nicht automatisch und manuell über die Speicher-Replikat PowerShell-Cmdlets koordiniert werden müssen. Im obigen Diagramm ClusterA ist das primäre und ClusterB ist eine sekundäre. Wenn ClusterA ausfällt, müssten Sie manuell ClusterB als primären festlegen, bevor Sie die Ressourcen bringen können. Sobald ClusterA wieder verfügbar ist, müssen Sie es sekundäre vereinfachen. Nachdem alle Daten wurden oben synchronisiert, nehmen Sie die Änderung und tauschen Sie die Rollen zurück an, wie, die er ursprünglich eingerichtet wurden.
4.  Da das Speicherreplikat nur die Daten repliziert wird, müssten einen neuen virtuellen Computer oder Skalierung, Datei-Server (sofs kontaktieren) unter Verwendung dieser Daten im Failovercluster-Manager auf dem Replikationspartner erstellt werden.

Das Speicherreplikatfeature kann verwendet werden, wenn Sie virtuelle Computer oder eine sofs kontaktieren in einem Cluster ausgeführt haben. Portieren von Ressourcen in das Replikat jederzeit HCI kann manuell oder automatisch durch die Verwendung von PowerShell-Skripting erfolgen.

## Hyper-V-Replikat

[Hyper-V-Replikat](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/set-up-hyper-v-replica) bietet Ebene VM-Replikation für die Wiederherstellung hyperkonvergenten Infrastrukturen. Was jedoch Hyper-V-Replikat können zu nutzen eines virtuellen Computers auf einen sekundären Standort oder Azure (Replikat) repliziert werden. Dann können Hyper-V-Replikat aus den sekundären Standort des virtuellen Computers in einem dritten (Erweiterte Replikat) replizieren.

![Hyper-V-Replikation-Diagramm](media\storage-spaces-direct-disaster-recovery\Disaster-Recovery-Figure2.png)

Mit Hyper-V-Replikat ist die Replikation von Hyper-V durchgeführt. Wenn Sie einen virtuellen Computer für die Replikation zunächst aktivieren, gibt es drei Optionen für die wie die anfängliche kopieren möchten, die an die entsprechenden Replikat-Cluster mit gesendet werden.

1.  Senden Sie die erste Kopie über das Netzwerk
2.  Senden Sie die erste Kopie um externe Datenträger, sodass es manuell auf dem Server kopiert werden kann
3.  Verwenden Sie einen vorhandenen virtuellen Computer bereits auf dem Replikat-Hosts erstellt

Die andere Möglichkeit ist für, wenn Sie möchten, dass diese erste Replikation stattfinden soll.

1.  Starten Sie die Replikation sofort
2.  Planen Sie eine Uhrzeit für den bei der erste Replikation stattfindet. 

Weitere Aspekte, die Sie benötigen sind:

- Welche VHD/VHDX repliziert werden sollen. Sie können auch alle oder nur einer davon repliziert.
- Anzahl der Wiederherstellungspunkte, die Sie speichern möchten. Wenn Sie möchten verfügen über mehrere Optionen zu welchem Zeitpunkt Punkt, die Sie wiederherstellen möchten, sollten Sie angeben, wie viele werden sollen. Wenn Sie nur ein Wiederherstellungspunkt möchten, können Sie, die ebenfalls auswählen.
- Wie oft Sie möchten die ein inkrementeller Schattenkopie replizieren Volume Shadow Copy Service (VSS).
- Wie oft Änderungen erhalten (30 Sekunden, 5 Minuten, 15 Minuten) repliziert.

Wenn HCI teilnehmen in Hyper-V-Replikat, benötigen Sie die [Hyper-V-Replikat-Broker](https://blogs.technet.microsoft.com/virtualization/2012/03/27/why-is-the-hyper-v-replica-broker-required/) -Ressource in jedem Cluster erstellt haben. Diese Ressource enthält Folgendes:

1.  Erhalten Sie einen einzigen Namespace für jeden Cluster für Hyper-V-Replikat zum herstellen.
2.  Bestimmt, welche Knoten innerhalb des Clusters das Replikat (oder den erweiterten Replikat) auf gespeichert werden soll, wenn sie zuerst die Kopie empfängt.
3.  Verfolgt der Knoten der Replikat (oder erweiterte Replikat) besitzt, für den Fall, dass Sie den virtuellen Computer auf einen anderen Knoten verschoben wird. Es muss zu verfolgen, damit beim Replikation durchgeführt wurde, die Informationen an den richtigen Knoten senden können.

## Sichern und Wiederherstellen

Eine herkömmliche Notfall-Wiederherstellung-Option, die nicht ist die Rede sehr viel aber ist genauso wichtig ist die Fehler der den gesamten Cluster oder einen Knoten im Cluster. Eine der Optionen in diesem Szenario nutzt Windows NT-Sicherung. 

Es ist immer eine Empfehlung regelmäßige Sicherungskopien der hyperkonvergenten Infrastruktur verfügen. Während der Cluster-Dienst, ausgeführt wird Wenn Sie ein System Zustand Sicherung durchführen, wäre die Registrierung Clusterdatenbank Teil dieser Sicherung. Wiederherstellen des Clusters oder die Datenbank verfügt über zwei unterschiedliche Methoden (Non-autoritativ und autoritativ).

### Nichtautorisierte

Eine nicht autorisierte Wiederherstellung mithilfe von Windows NT-Sicherung ausgeführt werden kann und eine vollständige Wiederherstellung von nur den Clusterknoten selbst entspricht. Wenn Sie nur einen Clusterknoten (und die Registrierung Clusterdatenbank) wiederherstellen müssen, und alle aktuellen Clusterinformationen gute, Sie würden Wiederherstellen mit der nicht autorisierte. Nichtautorisierte Wiederherstellung können über die Windows NT-Sicherung-Benutzeroberfläche oder über die Befehlszeile WBADMIN erfolgen. EXE-DATEI.

Nachdem Sie den Knoten wiederherstellen, können Sie es dem Cluster beizutreten. Was passiert ist, dass es die vorhandenen ausgeführten Cluster hinzugefügt werden und aktualisieren Sie alle Informationen mit was derzeit vorhanden ist.

### Autorisierend

Eine autoritativ Wiederherstellung von der Cluster-Konfiguration dauert andererseits, die Cluster-Konfiguration zurück. Diese Art der Wiederherstellung sollten nur erfolgen, wenn die Clusterinformationen selbst verloren und muss wiederhergestellt wurde. Z. B. eine Person ein Dateiserver, die mehr als 1.000 Freigaben enthalten versehentlich gelöscht, und Sie sie wieder benötigen. Abschluss eine autoritativ Wiederherstellung des Clusters erfordert, dass Sicherung über die Befehlszeile ausgeführt werden.

Wenn eine autoritativ Wiederherstellung auf einem Clusterknoten gestartet wird, der Cluster-Dienst auf allen anderen Knoten im Cluster-Ansicht beendet wird, und die Cluster-Konfiguration wird eingefroren. Daher ist es wichtig ist, dass der Cluster-Dienst auf dem Knoten auf dem die Wiederherstellung ausgeführt wurde zuerst gestartet werden, damit der Cluster gebildet wird mithilfe der neuen Kopie von der Cluster-Konfiguration.

Zum Ausführen von über eine autoritativ Wiederherstellung können die folgenden Schritte ausgeführt werden.

1.  Führen Sie WBADMIN. EXE-Datei über eine administrative Eingabeaufforderung um die neueste Version von Sicherungen abzurufen, die Sie installieren möchten und sicherstellen, dass Systemzustand eine Komponente ist können Sie wiederherstellen.

    ```powershell
    Wbadmin get versions
    ```

2.  Ermitteln Sie, ob die Sicherung Version haben Sie die Cluster-Registrierungsinformationen als Komponente enthält. Es gibt eine Reihe von diesen Befehl, die Version und die Anwendung/Komponente für den Einsatz in Schritt 3 benötigten Elemente. Für die Version z. B. die Sicherung erfolgte 3 Januar 2018 2:04:00 Uhr und dies ist die benötigten wiederhergestellt.

    ```powershell
    wbadmin get items -backuptarget:\\backupserver\location
    ```

3.  Starten Sie die autorisierend wiederherstellen, um nur die Clusterversion der Registrierung wiederherstellen, die Sie benötigen. 

    ```powershell
    wbadmin start recovery -version:01/03/2018-02:04 -itemtype:app -items:cluster
    ```

Nachdem die Wiederherstellung durchgeführt wurde, muss dieser Knoten sein, die der Cluster-Dienst zuerst starten und den Cluster zu bilden. Alle anderen Knoten müsste dann gestartet werden und den Cluster beitreten.

## Zusammenfassung 

Wenn dies alle summieren möchten, ist hyperkonvergenten notfallwiederherstellung etwas, das Sie sorgfältig geplant werden soll. Es gibt verschiedene Szenarien, die Ihre Anforderungen am besten gerecht können und sollten sorgfältig getestet werden. Ein Element zu beachten ist, wenn Sie in der Vergangenheit mit Failoverclustern vertraut sind, Stretched Cluster einen sehr beliebtere Option im Laufe der Jahre wurden. Es ist etwas einer Designänderung mit der zusammengeführte Lösung und basiert auf resilienz. Wenn Sie zwei Knoten in einem hyperkonvergenten Cluster vergessen haben, wird der gesamte Cluster sinken. Mit dieser wird in einer Umgebung mit hyperkonvergenter der Fall ist das Stretched Szenario nicht unterstützt.


