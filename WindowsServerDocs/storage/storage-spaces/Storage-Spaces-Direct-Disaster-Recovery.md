---
title: Notfall Wiederherstellungs Szenarien für hyperkonvergierte Infrastrukturen
ms.prod: windows-server
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: johnmarlin-msft
ms.author: johnmar
ms.date: 03/29/2018
description: In diesem Artikel werden die heute für die Notfall Wiederherstellung von Microsoft HCI (direkte Speicherplätze) verfügbaren Szenarios beschrieben.
ms.localizationpriority: medium
ms.openlocfilehash: 5c9c36e90f9bfae053197b6a36201748cb7e88d7
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966452"
---
# <a name="disaster-recovery-with-storage-spaces-direct"></a>Notfall Wiederherstellung mit direkte Speicherplätze

> Gilt für: Windows Server 2019, Windows Server 2016

In diesem Thema wird erläutert, wie die hyperkonvergierte Infrastruktur (HCI) für die Notfall Wiederherstellung konfiguriert werden kann.

Viele Unternehmen führen hyperkonvergierte Lösungen aus, und die Planung eines Notfalls bietet die Möglichkeit, in der Produktion schnell zu bleiben, wenn ein Notfall eintritt. Es gibt mehrere Möglichkeiten, HCI für die Notfall Wiederherstellung zu konfigurieren. in diesem Dokument werden die Optionen erläutert, die Ihnen heute zur Verfügung stehen.

Wenn sich die Diskussion über das Wiederherstellen von Verfügbarkeit bei einem Notfall in Notfällen um das als Wiederherstellungszeit Ziel (RTO) bekannte Problem dreht Dies ist die Zeitspanne, in der Dienste wieder hergestellt werden müssen, um nicht akzeptable Konsequenzen für das Unternehmen zu vermeiden. In einigen Fällen kann dieser Prozess automatisch ausgeführt werden, wenn die Produktion fast sofort wieder hergestellt wird. In anderen Fällen muss ein manueller Administrator Eingriff erfolgen, um Dienste wiederherzustellen.

Die Notfall Wiederherstellungsoptionen mit einem hyperkonvergierten heute sind:

1. Mehrere Cluster mit Speicher Replikat
2. Hyper-V-Replikat zwischen Clustern
3. Sichern und Wiederherstellen

## <a name="multiple-clusters-utilizing-storage-replica"></a>Mehrere Cluster mit Speicher Replikat

Das [Speicher](../storage-replica/storage-replica-overview.md) Replikat ermöglicht die Replikation von Volumes und unterstützt die synchrone und asynchrone Replikation. Bei der Wahl zwischen synchroner oder asynchroner Replikation sollten Sie Ihr Wiederherstellungspunkt Ziel (RPO) als Ziel verwenden. Das Wiederherstellungspunkt Ziel ist die Menge möglicher Datenverluste, die Sie bereitstellen können, bevor Sie als schwerer Verlust angesehen werden. Wenn Sie die synchrone Replikation durchlaufen, werden beide gleichzeitig nacheinander in beide Enden geschrieben. Wenn Sie asynchron wechseln, werden Schreibvorgänge sehr schnell repliziert, können aber trotzdem verloren gehen. Sie sollten die Anwendungs-oder Datei Verwendung in Erwägung gezogen, um zu sehen, was für Sie am besten funktioniert.

Das Speicher Replikat ist ein Kopiermechanismus auf Blockebene im Vergleich zur Dateiebene. Das heißt, es spielt keine Rolle, welche Datentypen repliziert werden. Dies ist eine beliebte Option für hyperkonvergierte Infrastrukturen. Das Speicher Replikat kann auch verschiedene Arten von Laufwerken zwischen den Replikations Partnern nutzen, sodass sich der gesamte Typspeicher in einem HCI und in einem anderen Speicherplatz auf dem anderen Speicherort ganz problemlos eignet. 

Eine wichtige Funktion des Speicher Replikats ist, dass Sie sowohl in Azure als auch lokal ausgeführt werden kann. Sie können lokal in Azure, Azure in Azure oder sogar lokal in Azure (oder umgekehrt) einrichten.

In diesem Szenario gibt es zwei separate unabhängige Cluster. Zum Konfigurieren des Speicher Replikats zwischen HCI können Sie die Schritte unter [Cluster-zu-Cluster-Speicher Replikation](../storage-replica/cluster-to-cluster-storage-replication.md)ausführen.

![Speicher Replikations Diagramm](media/storage-spaces-direct-disaster-recovery/Disaster-Recovery-Figure1.png)

Beim Bereitstellen des Speicher Replikats gelten die folgenden Überlegungen. 

1.    Das Konfigurieren der Replikation erfolgt außerhalb des Failoverclustering. 
2.    Die Auswahl der Replikations Methode hängt von der Netzwerk Latenz und den RPO-Anforderungen ab. Synchron repliziert die Daten in Netzwerken mit geringer Latenz mit Absturz Konsistenz, um zu einem Zeitpunkt, an dem ein Fehler aufgetreten ist, keinen Datenverlust sicherzustellen. Asynchrone repliziert die Daten über Netzwerke mit höheren Wartezeiten, aber die einzelnen Standorte verfügen möglicherweise nicht über identische Kopien, wenn ein Fehler aufgetreten ist. 
3.    Bei einem Notfall erfolgen Failover zwischen den Clustern nicht automatisch und müssen manuell über die PowerShell-Cmdlets des Speicher Replikats orchestriert werden. In der obigen Abbildung ist clustera das primäre Element, und clusterb ist das sekundäre Objekt. Wenn clustera ausfällt, müssen Sie "clusterb" manuell als "Primär" festlegen, bevor Sie die Ressourcen übernehmen können. Nach der Wiederherstellung von clustera müssen Sie es als sekundär festlegen. Nachdem alle Daten synchronisiert wurden, nehmen Sie die Änderung vor, und tauschen Sie die Rollen so zurück, wie Sie ursprünglich festgelegt wurden.
4.    Da das Speicher Replikat nur die Daten replizieren, muss ein neuer virtueller Computer oder Scale Out Datei Server (sofs), der diese Daten nutzt, in Failovercluster-Manager auf dem Replikat Partner erstellt werden.

Das Speicher Replikat kann verwendet werden, wenn Sie über virtuelle Computer oder einen sofs verfügen, die in Ihrem Cluster ausgeführt werden. Das Online schalten von Ressourcen im Replikat-HCI kann durch die Verwendung von PowerShell-Skripts manuell oder automatisiert erfolgen.

## <a name="hyper-v-replica"></a>Hyper-V-Replikat

Das [Hyper-V-](../../virtualization/hyper-v/manage/set-up-hyper-v-replica.md) Replikat stellt Replikation auf virtuellen Computern für die Notfall Wiederherstellung in hyperkonvergenten Infrastrukturen bereit. Das Hyper-V-Replikat kann eine virtuelle Maschine erstellen und auf einem sekundären Standort oder in Azure replizieren (Replikat). Vom sekundären Standort aus kann das Hyper-V-Replikat den virtuellen Computer dann auf ein drittes (erweitertes Replikat) replizieren.

![Hyper-V-Replikations Diagramm](media/storage-spaces-direct-disaster-recovery/Disaster-Recovery-Figure2.png)

Mit dem Hyper-v-Replikat wird die Replikation von Hyper-v übernommen. Wenn Sie zum ersten Mal einen virtuellen Computer für die Replikation aktivieren, gibt es drei Möglichkeiten, wie die anfängliche Kopie an die entsprechenden Replikat Cluster gesendet werden soll.

1.    Erste Kopie über das Netzwerk senden
2.    Senden Sie die anfängliche Kopie an externe Medien, damit Sie manuell auf den Server kopiert werden kann.
3.    Vorhandenen virtuellen Computer verwenden, der bereits auf den Replikat Hosts erstellt wurde

Die andere Option ist, wenn Sie möchten, dass diese erste Replikation stattfindet.

1.    Replikation sofort starten
2.    Planen Sie einen Zeitpunkt, zu dem die erste Replikation stattfindet. 

Weitere Aspekte, die Sie benötigen, sind:

- Die VHD/vhdx-Dateien, die Sie replizieren möchten. Sie können auswählen, ob Sie alle oder nur eine davon replizieren möchten.
- Anzahl der Wiederherstellungspunkte, die Sie speichern möchten. Wenn Sie mehrere Optionen zu den Zeitpunkten haben möchten, die Sie wiederherstellen möchten, sollten Sie angeben, wie viele Sie möchten. Wenn Sie nur einen Wiederherstellungspunkt möchten, können Sie dies auch auswählen.
- Gibt an, wie oft die Volumeschattenkopie-Dienst (VSS) eine inkrementelle Schatten Kopie replizieren soll.
- Wie oft Änderungen repliziert werden (30 Sekunden, 5 Minuten, 15 Minuten).

Wenn HCI an einem Hyper-v-Replikat teilnimmt, muss die [Hyper-v-Replikat Broker](https://techcommunity.microsoft.com/t5/virtualization/bg-p/Virtualization) -Ressource in jedem Cluster erstellt werden. Diese Ressource führt verschiedene Aktionen aus:

1.    Bietet Ihnen einen einzelnen Namespace für jeden Cluster, mit dem das Hyper-V-Replikat eine Verbindung herstellen soll.
2.    Bestimmt, auf welchem Knoten sich das Replikat (oder das erweiterte Replikat) beim ersten Erhalt der Kopie befindet.
3.    Verfolgt, welcher Knoten das Replikat (oder das erweiterte Replikat) besitzt, falls der virtuelle Computer auf einen anderen Knoten verschoben wird. Dies muss nachverfolgt werden, damit die Informationen bei der Replikation an den entsprechenden Knoten gesendet werden können.

## <a name="backup-and-restore"></a>Sichern und Wiederherstellen

Eine herkömmliche Notfall Wiederherstellungsoption, die nicht sehr häufig erwähnt wird, sondern ebenso wichtig ist, ist das Fehlschlagen des gesamten Clusters oder eines Knotens im Cluster. Bei beiden Optionen in diesem Szenario wird die Windows NT-Sicherung verwendet. 

Es ist immer eine Empfehlung, regelmäßige Sicherungen der hyperkonvergierten Infrastruktur zu haben. Während der Cluster Dienst ausgeführt wird, ist die Cluster Registrierungsdatenbank ein Teil dieser Sicherung, wenn Sie eine System Status Sicherung durchführen. Die Wiederherstellung des Clusters oder der Datenbank hat zwei verschiedene Methoden (nicht autoritativ und autorisierend).

### <a name="non-authoritative"></a>Nicht autoritativ

Eine nicht autoritative Wiederherstellung kann mithilfe der Windows NT-Sicherung durchgeführt werden und entspricht der vollständigen Wiederherstellung nur des Cluster Knotens. Wenn Sie nur einen Cluster Knoten (und die Cluster Registrierungsdatenbank) und alle aktuellen Cluster Informationen wiederherstellen müssen, können Sie die Wiederherstellung mit einem nicht autoritativen Vorgang durchsetzen. Nicht autoritative Wiederherstellungen können über die Windows NT-Sicherungs Schnittstelle oder über die Befehlszeile WBADMIN.EXE durchgeführt werden.

Nachdem Sie den Knoten wieder hergestellt haben, lassen Sie ihn dem Cluster beitreten. Dies geschieht, wenn der vorhandene Cluster auf den vorhandenen Cluster aktualisiert wird und alle seine Informationen mit dem aktuell vorhandenen Cluster aktualisiert werden.

### <a name="authoritative"></a>Tärer

Eine autoritative Wiederherstellung der Cluster Konfiguration hingegen nimmt die Cluster Konfiguration zurück. Diese Art der Wiederherstellung sollte nur ausgeführt werden, wenn die Cluster Informationen selbst verloren gegangen sind und wieder hergestellt werden müssen. Beispielsweise hat jemand versehentlich einen Datei Server gelöscht, der über 1000 Freigaben enthielt und Sie wieder benötigen. Zum Abschließen einer autorisierenden Wiederherstellung des Clusters muss die Sicherung über die Befehlszeile ausgeführt werden.

Wenn eine autoritative Wiederherstellung auf einem Cluster Knoten initiiert wird, wird der Cluster Dienst auf allen anderen Knoten in der Cluster Ansicht angehalten, und die Cluster Konfiguration ist fixiert. Daher ist es von entscheidender Bedeutung, dass der Cluster Dienst auf dem Knoten, auf dem die Wiederherstellung ausgeführt wurde, zuerst gestartet wird, sodass der Cluster mithilfe der neuen Kopie der Cluster Konfiguration erstellt wird.

Zum Ausführen einer autorisierenden Wiederherstellung können die folgenden Schritte ausgeführt werden.

1.    Führen Sie WBADMIN.EXE an einer administrativen Eingabeaufforderung aus, um die neueste Version der Sicherungen zu erhalten, die Sie installieren möchten, und stellen Sie sicher, dass der System Status eine der Komponenten ist, die Sie wiederherstellen können.

    ```powershell
    Wbadmin get versions
    ```

2.    Stellen Sie fest, ob die Versions Sicherung, die Sie besitzen, über die Cluster Registrierungsinformationen als Komponente verfügt. Es gibt einige Elemente, die Sie mit diesem Befehl benötigen, die Version und die Anwendung bzw. Komponente für die Verwendung in Schritt 3. Für die Version, z. b.: die Sicherung wurde am 3. Januar 2018 um 2:04uhr durchgeführt, und das ist das, das Sie wiederherstellen müssen.

    ```powershell
    wbadmin get items -backuptarget:\\backupserver\location
    ```

3.  Starten Sie die autoritative Wiederherstellung, um nur die benötigte Cluster Registrierungs Version wiederherzustellen. 

    ```powershell
    wbadmin start recovery -version:01/03/2018-02:04 -itemtype:app -items:cluster
    ```

Nachdem die Wiederherstellung erfolgt ist, muss es sich bei diesem Knoten um den Cluster Dienst handeln, um zuerst den Cluster Dienst zu starten und den Cluster zu bilden. Alle anderen Knoten müssen dann gestartet werden und dem Cluster beitreten.

## <a name="summary"></a>Zusammenfassung 

Um diese Summe zu addieren, ist die hyperkonvergierte Notfall Wiederherstellung etwas, das sorgfältig geplant werden sollte. Es gibt mehrere Szenarien, die Ihren Anforderungen am besten entsprechen und gründlich getestet werden können. Beachten Sie Folgendes: Wenn Sie in der Vergangenheit mit Failoverclustern vertraut sind, sind Stretch-Cluster im Laufe der Jahre eine sehr beliebte Option. Bei der hyperkonvergierten Lösung gab es eine gewisse Entwurfs Änderung, die auf Resilienz basiert. Wenn Sie zwei Knoten in einem hyperkonvergierten Cluster verlieren, wird der gesamte Cluster herunterfahren. Dies ist der Fall, in einer hyperkonvergierten Umgebung wird das Stretch-Szenario nicht unterstützt.
