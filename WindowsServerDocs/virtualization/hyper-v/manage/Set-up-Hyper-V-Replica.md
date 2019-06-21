---
title: Einrichten von Hyper-V-Replikaten
ms.technology: compute-hyper-v
description: Enthält Anweisungen für das Einrichten eines Replikats, Testen Failover und eine erste Replikation ausführen.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.topic: article
ms.assetid: eea9e996-bfec-4065-b70b-d8f66e7134ac
author: KBDAzure
ms.author: kathydav
ms.date: 10/10/2016
ms.openlocfilehash: b8dcf23946d99509aafba0f8af58bf633bedd069
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280233"
---
# <a name="set-up-hyper-v-replica"></a>Einrichten von Hyper-V-Replikaten

>Gilt für: Windows Server 2016

Hyper-V-Replikat ist ein wesentlicher Bestandteil der Hyper-V-Rolle. Es unterstützt Ihre Strategie zur notfallwiederherstellung, indem Sie zum Replizieren von virtuellen Computern von einem Hyper-V-Host-Server zu einem anderen, Ihre Workloads verfügbar zu halten.  Hyper-V-Replikat erstellt eine Kopie eines aktiven virtuellen Computers auf einer offline virtuellen replikatcomputer. Beachten Sie Folgendes:  

-   **Hyper-V-Hosts**: Primären und sekundären Hostserver können werden physisch nebeneinander befinden oder an unterschiedlichen geografischen Orten, bei der Replikation über ein WAN verknüpfen. Hyper-V-Hosts können es sich um eigenständige, geclustert ist, oder eine Kombination aus beidem sein. Es gibt keine Active Directory-Abhängigkeit zwischen den Servern aus, und sie müssen keine Domänenmitglieder sein.  

-   **Replikation und änderungsnachverfolgung**: Wenn Sie Hyper-V-Replikat für einen bestimmten virtuellen Computer aktivieren, erstellt die erste Replikation eine identische virtuelle replikatcomputer auf einem sekundären Hostserver. Nach dem in diesem Fall werden änderungsnachverfolgung in Hyper-V-Replikat erstellt und verwaltet eine Protokolldatei, die Änderungen auf einer VHD des virtuellen Computers erfasst. Die Protokolldatei wird in umgekehrter Reihenfolge auf das Replikat abgespielt replikationshäufigkeit VHD abhängig. Dies bedeutet, dass die aktuellen Änderungen gespeichert und asynchron repliziert werden. Replikation kann über HTTP oder HTTPS sein.  

-   **Erweitert (verkettete) Replikation**: Dadurch können Sie die Replikation eines virtuellen Computers von einem primären Host auf einem sekundären Hosts, und anschließend darin replizieren die sekundäre Datenbank gehostet wird, um eine dritte zu hosten. Beachten Sie, dass Sie nicht vom primären Host direkt in der zweiten und dritten replizieren können.  

    Dieses Feature macht Hyper-V-Replikat stabiler für die notfallwiederherstellung, da Sie bei einem Ausfall des primären und erweiterten Replikats wiederherstellen können.  Sie können Failover zum erweiterten Replikat durchführen, wenn Ihre primären und sekundären Standorte ausfallen. Beachten Sie, dass das erweiterte Replikat keine anwendungskonsistente Replikation unterstützt und muss die gleichen VHDs, die das sekundäre Replikat verwendet wird.  

-   **Failover**: Wenn in Ihrer primären Datenbank zu einem Ausfall kommt (oder sekundäre Datenbank im Fall von erweiterten) Speicherort, Sie können manuell initiieren einer Test-, Geplantes, oder ungeplantes Failover.  

    ||Test|Geplant|Ungeplant|  
    |-|--------|-----------|-------------|  
    |Wann sollte ich ausführen?|Stellen Sie sicher, dass ein virtueller Computer ein Failover und am sekundären Standort starten können<br /><br />Nützlich für Tests und Schulungen|Während einer geplanten Downtime und Ausfälle|Bei unerwarteten Ereignissen|  
    |Ist ein Duplikat der virtuellen Maschine werden erstellt?|Ja|Nein|Nein|  
    |Wo ist es initiiert?|Klicken Sie auf den replizierten virtuellen Computer|Initiiert auf dem primären und abgeschlossen auf dem sekundären Computer|Klicken Sie auf den replizierten virtuellen Computer|  
    |Wie oft sollte werden ausgeführt?|Es wird empfohlen, einmal im Monat zum Testen|Alle sechs Monate oder gemäß den konformitätsanforderungen|Nur im Notfall, wenn der primäre virtuelle Computer nicht verfügbar ist.|  
    |Weiterhin der primäre virtuelle Computer replizieren?|Ja|Ja. Sobald der Ausfall ist beheben Sie die umgekehrte Replikation repliziert, die Änderungen an den primären Standort zu sichern, sodass primären und sekundären synchronisiert werden.|Nein|  
    |Gibt es Daten verloren gehen?|Keine|Keine Nach dem letzten Satz von Überarbeitungen durch Hyper-V-Replikat ein Failover zurück auf das primäre Replikat, um sicherzustellen, dass keine Daten verloren gehen repliziert wird.|Hängt das Ereignis und die Wiederherstellungspunkte|  
    |Gibt es Ausfallzeiten?|Keine Auf diese Weise beeinträchtigt Ihre produktionsumgebung. Es wird einen doppelter virtueller Testcomputer erstellt, während des Failovers. Nach dem Failover abgeschlossen ist, die Sie auswählen, **Failover** für das Replikat virtuelle Computer, und es hat automatisch bereinigt und gelöscht.|Die Dauer der geplanten Ausfall|Die Dauer eines ungeplanten Ausfalls|  

-   **Wiederherstellungspunkte**: Wenn Sie Einstellungen für die Replikation für einen virtuellen Computer konfigurieren, geben Sie die Wiederherstellungspunkte an, die Sie davon speichern möchten. Wiederherstellungspunkte stellen eine Momentaufnahme dar, in Zeit, die von dem Sie einen virtuellen Computer wiederherstellen können. Offensichtlich weniger Daten geht verloren, wenn Sie von einem erst vor kurzem Wiederherstellungspunkt wiederherstellen. Sie können auf Wiederherstellungspunkte zugreifen, bis zu 24 Stunden zurück.  

## <a name="deployment-prerequisites"></a>Bereitstellungsvoraussetzungen  
Hier ist, was Sie überprüfen sollten, bevor Sie beginnen:  

-   **Ermitteln, welche virtuellen Festplatten müssen repliziert werden**. Insbesondere enthalten VHDs, die Daten, die sich schnell ändernden ist und nicht vom Replikatserver verwendet werden, nach dem Failover, z. B. Datenträger mit Auslagerungsdateien, von der Replikation zum Einsparen von Netzwerkbandbreite ausgeschlossen werden sollen. Notieren Sie sich die virtuellen Festplatten ausgeschlossen werden können.  

-   **Entscheiden, wie oft Sie benötigen zum Synchronisieren von Daten**:  Die Daten auf dem Replikatserver werden gemäß der replikationshäufigkeit aktualisierte synchronisiert (30 Sekunden, 5 Minuten oder 15 Minuten) zu konfigurieren. Die Häufigkeit sollte Folgendes berücksichtigen: Werden die virtuellen Computer wichtige Daten mit der ein niedriges RPO ausgeführt? Was sind Sie Überlegungen zur Netzwerkbandbreite?  Ihre gegenüber sehr kritisch virtuellen Computer benötigen natürlich häufigere Replikationen.  

-   **Entscheiden, wie Sie Daten wiederherstellen**:  Standardmäßig speichert Hyper-V-Replikat nur einen einzelnen Wiederherstellungspunkt, der der neuesten Replikation vom primären auf die sekundäre Datenbank gesendet werden. Wenn Sie die Möglichkeit, Daten zu einem früheren Zeitpunkt wiederherstellen möchten Sie jedoch angeben können, dass zusätzliche Wiederherstellungspunkte (auf maximal 24 stündlichen Punkt) gespeichert werden sollen. Wenn Sie zusätzliche Wiederherstellungspunkte benötigen beachten, dass dies mehr Aufwand auf Verarbeitung und Speicherung Ressourcen erfordert.  

-   **Ermitteln, welche Workloads, die Sie replizieren**: Hyper-V-Replikat-Standardreplikation behält die Konsistenz in den Zustand der das Betriebssystem des virtuellen Computers nach einem Failover, aber nicht den Zustand von Anwendungen, auf dem virtuellen Computer ausgeführt. Sollten Sie können Recovery zeigt Ihre Workload-Status, die Sie app-konsistente Wiederherstellung erstellen können. Beachten Sie, dass app-konsistente Wiederherstellung ist nicht verfügbar auf der Website für die erweiterten Replikat bei Verwendung von erweiterten (verkettete) Replikation.  

-   **Entscheiden Sie, wie Sie die anfängliche Replikation der Daten des virtuellen Computers**: Replikation wird gestartet, durch die Übertragung von der Anforderungen, um den aktuellen Zustand der virtuellen Computer zu übertragen. Dieser anfängliche Zustand kann direkt über das vorhandene Netzwerk übermittelt werden – entweder sofort oder zu einem konfigurierbaren späteren Zeitpunkt. Sie können auch einen bereits vorhandenen wiederhergestellten virtueller Computer verwenden (beispielsweise, wenn Sie eine frühere Sicherung des virtuellen Computers auf dem Replikatserver wiederhergestellt haben) als erste Kopie. Alternativ können Sie Netzwerkbandbreite einsparen, indem Sie die Erstkopie auf externe Medien kopieren und diese physisch an den Replikatstandort senden.  Wenn Sie eine bereits vorhandene verwenden möchten virtuellen Computer löschen alle vorherige Momentaufnahmen zugeordnet.  

## <a name="deployment-steps"></a>Bereitstellungsschritte  

### <a name="step-1-set-up-the-hyper-v-hosts"></a>Schritt 1: Richten Sie die Hyper-V-hosts  
Sie benötigen mindestens zwei Hyper-V-Hosts mit einem oder mehreren virtuellen Computern auf jedem Server. [Erste Schritte mit Hyper-V](../get-started/Get-started-with-Hyper-V-on-Windows.md). Der Hostserver, dem Sie virtuelle Computer replizieren, werden als Replikatserver eingerichtet werden müssen.  

1.  In den Hyper-V-Einstellungen für den Server replizieren Sie virtuelle Computer, in **Replikationskonfiguration**Option **diesen Computer aktivieren als Replikatserver**.  

2.  Sie können über HTTP oder HTTPS von verschlüsselten replizieren. Wählen Sie **verwenden Kerberos (HTTP)** oder **zertifikatbasierte Authentifizierung verwenden (HTTPS**). Standardmäßig werden als Firewallausnahmen auf dem Hyper-V-Replikatserver HTTP 80 und 443 für HTTPS aktiviert. Wenn Sie die standardporteinstellungen ändern, müssen Sie auch die Firewall-Ausnahme zu ändern. Wenn Sie über HTTPS replizieren, müssen Sie ein Zertifikat auszuwählen, und müssen Sie die Zertifikatauthentifizierung eingerichtet.  

3.  Wählen Sie für die Autorisierung **zulassen der Replikation von einem authentifizierten Server** fest, damit die Replikatserver, virtuelle Computer-Replikationsdatenverkehr von beliebigen Primärservern zu akzeptieren, die erfolgreich authentifiziert. Wählen Sie **zulassen der Replikation von den angegebenen Servern** Datenverkehr nur von den primären Servern akzeptiert Sie explizit auszuwählen.  

    Für beide Optionen können Sie angeben, aus, in dem die replizierten VHDs auf dem Hyper-V-Replikatserver gespeichert werden sollen.  

4.  Klicken Sie auf **OK** oder **Übernehmen**.  

### <a name="step-2-set-up-the-firewall"></a>Schritt 2: Einrichten der Firewall  
Um die Replikation zwischen den primären und sekundären Servern zu ermöglichen, muss Datenverkehr über die Windows-Firewall (oder andere Firewalls von Drittanbietern) abrufen. Wenn Sie die Hyper-V-Rolle auf den Servern installiert, von Standardausnahmen für die HTTP-(80) und HTTPS (443) werden erstellt. Wenn Sie diese standard-Ports verwenden, müssen Sie nur die Regeln zu aktivieren:  

-  So aktivieren Sie die Regeln auf einem eigenständigen Host-Server:  

    1. Windows-Firewall mit erweiterter Sicherheit öffnen und auf **Eingangsregeln**.  

    2. Zum Aktivieren der Authentifizierung für HTTP (Kerberos) Maustaste **Hyper-V-Replikat-HTTP-Listener (TCP eingehend)**  >**Regel aktivieren.** Um HTTPS-Zertifikat-basierte Authentifizierung zu aktivieren, Maustaste **Hyper-V-Replikat-HTTPS-Listener (TCP eingehend)** > E**aktiviere Regel**.  

-  Um Regeln in einem Hyper-V-Cluster zu aktivieren, öffnen Sie eine Windows PowerShell-Sitzung mit **als Administrator ausführen**, führen Sie dann einen der folgenden Befehle:  

    -   Für HTTP:  `get-clusternode | ForEach-Object  {Invoke-command -computername $_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"}}`  

    -   Für HTTPS: `get-clusternode | ForEach-Object  {Invoke-command -computername $_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"}}`  

### <a name="enable-virtual-machine-replication"></a>Aktivieren der Replikation der virtuellen Computer  
Gehen Sie auf jedem virtuellen Computer, die Sie replizieren möchten:  

1.  In der **Details** Bereich von Hyper-V-Manager, eine virtuelle Maschine auswählen, indem Sie darauf klicken.  
    Mit der rechten Maustaste in den ausgewählten virtuellen Computer aus, und klicken Sie auf **Aktivieren der Replikation** zum Öffnen des Assistenten für die Replikation aktivieren.  

2.  Klicken Sie auf der Seite **Vorbemerkungen** auf **Weiter**.  

3.  Auf der **Replikatserver angeben** Seite Replikatserver, geben Sie im den NetBIOS- oder FQDN des Replikat-Servers. Wenn der Replikatserver Teil eines Failoverclusters ist, geben Sie den Namen des Hyper-V-Replikatbrokers ein. Klicken Sie auf **Weiter**.  

4.  Auf der **Verbindungsparameter angeben** Seite Hyper-V-Replikat übernimmt automatisch die Authentifizierung und den Port-Einstellungen, die Sie für den Replikatserver konfiguriert. Wenn die Werte werden, werden nicht abgerufen suchen, die der Server als Replikatserver konfiguriert ist, und im DNS registriert ist. Bei Bedarf geben Sie die Einstellung manuell.  

5.  Auf der **virtuelle Festplatten für Replikation auswählen** stellen Sie sicher, dass die VHDs, die Sie replizieren möchten, ausgewählt sind, und deaktivieren Sie die Kontrollkästchen für sämtliche virtuellen Festplatten, die Sie von der Replikation ausschließen möchten. Klicken Sie dann auf **Weiter**.  

6.  Auf der **Replikationshäufigkeit konfigurieren** Seite, die angeben, wie häufig Änderungen vom primären zum sekundären Standort synchronisiert werden sollen. Klicken Sie dann auf **Weiter**.  

7.  Auf der **zusätzliche Wiederherstellungspunkte konfigurieren** Seite an, ob nur den letzten Wiederherstellungspunkt beibehalten oder zusätzliche Wiederherstellungspunkte erstellt werden sollen.    Wenn Sie Anwendungen wiederherstellen möchten, und wählen Sie die arbeitsauslastungen, die ihre eigenen VSS Writer-Instanzen haben, Sie sollten **Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) Frequenc**y und gibt an, wie häufig anwendungskonsistente Momentaufnahmen erstellt. Beachten Sie, dass der Hyper-V-VMM-Requestor-Dienst auf dem primären und sekundären Hyper-V-Servern ausgeführt werden muss. Klicken Sie dann auf **Weiter**.  

8.  Auf der **erste Replikation auswählen** Seite, wählen Sie die Methode für anfängliche Replikation verwendet.  Die Standardeinstellung um zu senden, dass die erste Kopie über das Netzwerk der primäre virtuelle Computer-Konfigurationsdatei (VMCX) und die virtuellen Festplattendateien (VHDX und virtuelle Festplatte) kopiert, die Sie über die Netzwerkverbindung ausgewählt haben. Überprüfen Sie die Netzwerkbandbreiten-Verfügbarkeit, wenn Sie vorhaben, um diese Option verwenden. Wenn der primäre virtuelle Computer am sekundären Standort als replizieren virtueller Computer bereits konfiguriert ist es kann hilfreich sein, wählen Sie **verwenden eine vorhandene virtuellen Maschine auf dem Replikationsserver als erste Kopie**. Sie können verwenden Hyper-V zu exportieren der primäre virtuelle Computer, und importieren sie als ein virtueller replikatcomputer auf dem sekundären Server. Für größere virtuelle Computer oder begrenzter Bandbreite können Sie es auswählen, haben Sie die erste Replikation über das Netzwerk zu einem späteren Zeitpunkt auftreten, und konfigurieren Sie Stunden außerhalb der Spitzenzeiten, oder senden die Informationen für die erste Replikation als offline-Medien.  

    Wenn Sie die Offlinereplikation durchführen müssen Sie die erste Kopie auf dem sekundären Server mit einer externen Speichermedium, z. B. eine Festplatte oder ein USB-Laufwerk transport. Zu diesem Zweck Sie die externe Verbindung müssen senden Speicherung auf dem primären Server (oder von Besitzerknoten in einem Cluster), und klicken Sie dann bei der Auswahl Erstkopie mithilfe von externen Medien, die Sie einen Speicherort angeben können, lokal oder auf Ihre externen Medien, in dem die erste Kopie gespeichert werden kann.  Eine Platzhalter-VM wird am Replikatstandort erstellt. Nach Abschluss der Erstreplikation kann der externe Speicher zum Replikatstandort geliefert werden. Es müssen Sie die externen Medien auf dem sekundären Server oder auf den Besitzerknoten des dem sekundären Cluster verbinden. Klicken Sie dann Sie importieren das ursprüngliche Replikat in einer angegebenen Position und die Platzhalter virtuelle Maschine zusammenführen.  

9. Auf der **das Aktivieren der Replikation abschließen** Seite, überprüfen Sie die Informationen in der Zusammenfassung, und klicken Sie dann auf **Fertig stellen.** . Daten des virtuellen Computers werden in Übereinstimmung mit den ausgewählten Einstellungen übertragen werden. und ein Dialogfeld wird angezeigt, der angibt, dass die Replikation erfolgreich aktiviert wurde.  

10. Wenn Sie erweiterte (verkettete) Replikation konfigurieren möchten, öffnen Sie den Replikatserver, und mit der rechten Maustaste den virtuellen Computer, die, den Sie replizieren möchten. Klicken Sie auf **Replikation** > **Erweitern der Replikation** , und geben Sie Einstellungen für die Replikation.  

## <a name="run-a-failover"></a>Ausführen eines Failovers  
Nach Abschluss dieser Bereitstellungsschritte wird Ihrer replizierten Umgebung ausgeführt. Jetzt können Sie ein Failover ausführen, je nach Bedarf.  

**Test-Failover**:  Wenn Sie verwenden möchten, führen Sie den primären virtuellen Computer eine Test-Failover mit der rechten Maustaste und wählen **Replikation** > **Test-Failover**. Wählen Sie den neuesten oder anderen Wiederherstellungspunkt aus, wenn konfiguriert. Ein neuen virtuellen Testcomputer erstellt und am sekundären Standort gestartet. Nachdem Sie die Tests abgeschlossen haben, wählen Sie **Testfailover beenden** auf den replizierten virtuellen Computer zu bereinigen. Beachten Sie, dass für eine virtuelle Maschine, die Sie nur ausführen können Failover zu einem Zeitpunkt zu testen. [Erfahren Sie mehr](https://blogs.technet.com/b/virtualization/archive/2012/07/26/types-of-failover-operations-in-hyper-v-replica.aspx).  

**Geplantes Failover**: Führen ein geplantes Failover mit der rechten Maustaste den primären virtuellen Computer und wählen dann **Replikation** > **Geplantes Failover**. Geplantes Failover führt die Voraussetzungen überprüft, um sicherzustellen, dass keine Daten verloren gehen. Er überprüft, dass der primäre virtuelle Computer vor Beginn des Failovers heruntergefahren ist. Nach dem Failover der virtuelle Computer ausgeführt wird, startet es die Änderungen zurück an den primären Standort repliziert werden, sobald diese verfügbar ist. Beachten Sie, dass den primären Server dazu zu empfangsseitennachrichten Replikation vom sekundären Server oder von der Hyper-V-Replikatbroker im Fall von einem primären Cluster konfiguriert werden soll. Geplantes Failover sendet der letzten Überarbeitungen festgelegt. [Erfahren Sie mehr](https://blogs.technet.com/b/virtualization/archive/2012/07/31/types-of-failover-operations-in-hyper-v-replica-part-ii-planned-failover.aspx).  

**Ungeplantes Failover**: Führen Sie ein ungeplantes Failover mit der rechten Maustaste auf den replizierten virtuellen Computer aus, und wählen Sie **Replikation** > **ungeplantes Failover** von Hyper-V-Manager oder Failover-Clustering-Manager. Sie können aus dem letzten verfügbaren Wiederherstellungspunkt oder von vorherigen Wiederherstellungspunkten wiederherstellen, wenn diese Option aktiviert ist. Nach dem Failover, überprüfen Sie, dass alles wie erwartet nach dem Failover für virtuellen Computer, klicken Sie dann auf **abschließen** auf den replizierten virtuellen Computer. [Erfahren Sie mehr](https://blogs.technet.com/b/virtualization/archive/2012/08/08/types-of-failover-operations-in-hyper-v-replica-part-iii-unplanned-failover.aspx).  
