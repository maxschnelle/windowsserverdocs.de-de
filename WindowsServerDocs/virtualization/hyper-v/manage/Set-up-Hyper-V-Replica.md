---
title: Einrichten von Hyper-V-Replikaten
ms.technology: compute-hyper-v
description: Enthält Anweisungen zum Einrichten des Replikats, Testen des Failovers und Durchführung einer ersten Replikation.
ms.prod: windows-server
manager: dongill
ms.topic: article
ms.assetid: eea9e996-bfec-4065-b70b-d8f66e7134ac
author: kbdazure
ms.author: kathydav
ms.date: 10/10/2016
ms.openlocfilehash: c24b26617f7174632bc39842afc9e83843e7673b
ms.sourcegitcommit: acfdb7b2ad283d74f526972b47c371de903d2a3d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87769688"
---
# <a name="set-up-hyper-v-replica"></a>Einrichten von Hyper-V-Replikaten

>Gilt für: Windows Server 2016

Hyper-V-Replikat ist ein wesentlicher Bestandteil der Hyper-V-Rolle. Es trägt zu ihrer Strategie für die Notfall Wiederherstellung bei, indem virtuelle Computer von einem Hyper-V-Host Server auf einen anderen replizieren werden, um Ihre Workloads verfügbar zu halten.  Das Hyper-V-Replikat erstellt eine Kopie eines virtuellen Live Computers auf einem virtuellen Replikat Computer, der offline ist. Beachten Sie Folgendes:

-   **Hyper-V-Hosts**: primäre und sekundäre Host Server können sich physisch nebeneinander befinden oder sich an verschiedenen geografischen Standorten mit Replikation über eine WAN-Verbindung befinden. Hyper-V-Hosts können eigenständig, gruppiert oder eine Kombination aus beidem sein. Es gibt keine Active Directory Abhängigkeit zwischen den Servern, und Sie müssen keine Domänen Mitglieder sein.

-   **Replikation und Änderungs Nachverfolgung**: Wenn Sie das Hyper-V-Replikat für eine bestimmte virtuelle Maschine aktivieren, wird bei der ersten Replikation ein identischer virtueller Replikat Computer auf einem sekundären Host Danach erstellt und verwaltet die Hyper-V-Replikat-Änderungs Nachverfolgung eine Protokolldatei, mit der Änderungen auf der VHD einer virtuellen Maschine erfasst werden. Die Protokolldatei wird auf der Grundlage der Replikations Häufigkeits Einstellungen in umgekehrter Reihenfolge an die Replikat-VHD Dies bedeutet, dass die neuesten Änderungen gespeichert und asynchron repliziert werden. Die Replikation kann über HTTP oder HTTPS erfolgen.

-   **Erweiterte (verkettete) Replikation**: auf diese Weise können Sie eine virtuelle Maschine von einem primären Host auf einen sekundären Host replizieren und dann den sekundären Host auf einen dritten Host replizieren. Beachten Sie, dass Sie nicht vom primären Host direkt auf den zweiten und den dritten replizieren können.

    Mit diesem Feature ist das Hyper-V-Replikat für die Notfall Wiederherstellung stabiler, denn wenn ein Ausfall auftritt, können Sie das primäre und das erweiterte Replikat wiederherstellen.  Sie können ein Failover zum erweiterten Replikat ausführen, wenn der primäre und der sekundäre Standort ausfällt. Beachten Sie, dass das erweiterte Replikat keine Anwendungs konsistente Replikation unterstützt und die gleichen VHDs verwenden muss, die vom sekundären Replikat verwendet werden.

-   **Failover**: Wenn ein Ausfall in Ihrem primären (oder sekundären) Standort auftritt, können Sie manuell ein Test-, geplantes oder ungeplantes Failover initiieren.

    | Frage | Test | Geplant | Ungeplant |
    |--|--|--|--|
    | Wann sollte ich ausgeführt werden? | Überprüfen, ob für einen virtuellen Computer ein Failover und Start am sekundären Standort möglich ist<p>Nützlich für Tests und Schulungen | Während geplanter Ausfallzeiten und Ausfällen | Bei unerwarteten Ereignissen |
    | Wird ein doppelter virtueller Computer erstellt? | Ja | Nein | Nein |
    | Wo wird Sie initiiert? | Auf dem virtuellen Replikat Computer | Initiiert auf dem primären und abgeschlossen auf dem sekundären Computer | Auf dem virtuellen Replikat Computer |
    | Wie oft sollte ich ausgeführt werden? | Wir empfehlen, einmal pro Monat zu testen. | Einmal alle sechs Monate oder gemäß den Konformitätsanforderungen | Nur im Notfall, wenn der primäre virtuelle Computer nicht verfügbar ist |
    | Wird der primäre virtuelle Computer weiterhin repliziert? | Ja | Ja. Wenn der Ausfall gelöst wird, repliziert die umgekehrte Replikation die Änderungen zurück zum primären Standort, sodass die primäre und die sekundäre Datenbank synchronisiert werden. | Nein |
    | Gibt es Datenverluste? | Keine | Keine. Nach dem Failover repliziert das Hyper-V-Replikat den letzten Satz an nach verfolgten Änderungen zurück zum primären Replikat, um den Verlust von Daten zu | Hängt vom Ereignis und den Wiederherstellungs Punkten ab |
    | Gibt es Ausfallzeiten? | Keine. Dies wirkt sich nicht auf Ihre Produktionsumgebung aus. Während des Failovers wird ein doppelter virtueller Testcomputer erstellt. Nachdem das Failover abgeschlossen ist, wählen Sie ein **Failover** auf dem virtuellen Replikat Computer aus, das automatisch bereinigt und gelöscht wird. | Die Dauer des geplanten Ausfalls. | Die Dauer des ungeplanten Ausfalls. |

-   **Wiederherstellungspunkte**: beim Konfigurieren der Replikationseinstellungen für einen virtuellen Computer geben Sie die Wiederherstellungspunkte an, die Sie aus dem virtuellen Computer speichern möchten. Wiederherstellungspunkte stellen eine Momentaufnahme dar, von der aus Sie einen virtuellen Computer wiederherstellen können. Wenn Sie einen letzten Wiederherstellungspunkt wiederherstellen, gehen offensichtlich weniger Daten verloren. Sie können vor bis zu 24 Stunden auf Wiederherstellungspunkte zugreifen.

## <a name="deployment-prerequisites"></a>Voraussetzungen für die Bereitstellung
Bevor Sie beginnen, sollten Sie Folgendes überprüfen:

-   **Ermitteln Sie, welche VHDs repliziert werden müssen**. Insbesondere VHDs, die Daten enthalten, die sich schnell ändern und nach einem Failover nicht vom Replikat Server verwendet werden (z. b. Auslagerungs Datenträger), sollten von der Replikation ausgeschlossen werden, um Netzwerkbandbreite Notieren Sie sich, welche VHDs ausgeschlossen werden können.

-   **Entscheiden Sie, wie oft Daten synchronisiert werden müssen**: die Synchronisierung der Daten auf dem Replikat Server erfolgt entsprechend der von Ihnen konfigurierten Replikations Häufigkeit (30 Sekunden, 5 Minuten oder 15 Minuten). Die Häufigkeit, die Sie auswählen, sollte Folgendes berücksichtigen: sind die virtuellen Computer mit einem niedrigen RPO-Wert auf dem Computer ausgeführt? Was sind ihre Bandbreiten Aspekte?  Ihre äußerst kritischen virtuellen Computer benötigen offensichtlich häufigere Replikationen.

-   **Entscheiden, wie Daten wieder hergestellt werden sollen**: Standardmäßig speichert das Hyper-V-Replikat nur einen einzelnen Wiederherstellungspunkt, bei dem es sich um die letzte vom primären Replikat gesendete Replikation Wenn Sie jedoch die Option zum Wiederherstellen von Daten bis zu einem früheren Zeitpunkt möchten, können Sie angeben, dass zusätzliche Wiederherstellungspunkte gespeichert werden sollen (maximal 24 Stunden). Wenn Sie zusätzliche Wiederherstellungspunkte benötigen, sollten Sie beachten, dass dies mehr Aufwand für Verarbeitungs-und Speicherressourcen erfordert.

-   **Ermitteln Sie, welche Arbeits Auslastungen Sie replizieren**: bei der Hyper-V-Standard Replikation wird nach einem Failover die Konsistenz des Betriebssystems des virtuellen Computers gewahrt, aber nicht der Status der Anwendungen, die auf dem virtuellen Computer ausgeführt werden. Wenn Sie in der Lage sein möchten, ihren Arbeits Auslastungs Status wiederherzustellen, können Sie App-konsistente Wiederherstellungspunkte erstellen. Beachten Sie, dass die APP-konsistente Wiederherstellung auf dem erweiterten Replikat Standort nicht verfügbar ist, wenn Sie die erweiterte (verkettete) Replikation

-   Legen Sie fest **, wie die anfängliche Replikation der Daten virtueller Computer durchzuführen**ist: die Replikation beginnt mit dem übertragen der Anforderungen zum Übertragen des aktuellen Zustands der virtuellen Computer. Dieser anfängliche Zustand kann direkt über das vorhandene Netzwerk übermittelt werden – entweder sofort oder zu einem konfigurierbaren späteren Zeitpunkt. Sie können auch einen bereits vorhandenen wiederhergestellten virtuellen Computer verwenden (z. b., wenn Sie eine frühere Sicherung des virtuellen Computers auf dem Replikat Server wieder hergestellt haben) als Erstkopie. Alternativ können Sie Netzwerkbandbreite einsparen, indem Sie die Erstkopie auf externe Medien kopieren und diese physisch an den Replikatstandort senden.  Wenn Sie einen bereits vorhandenen virtuellen Computer verwenden möchten, löschen Sie alle vorherigen Momentaufnahmen, die ihm zugeordnet sind.

## <a name="deployment-steps"></a>Bereitstellungsschritte

### <a name="step-1-set-up-the-hyper-v-hosts"></a>Schritt 1: Einrichten der Hyper-V-Hosts
Sie benötigen mindestens zwei Hyper-V-Hosts mit einem oder mehreren virtuellen Computern auf jedem Server. [Beginnen Sie mit Hyper-V](../get-started/Get-started-with-Hyper-V-on-Windows.md). Der Host Server, auf dem Sie virtuelle Computer replizieren, muss als Replikat Server eingerichtet werden.

1.  Wählen Sie in den Hyper-V-Einstellungen für den Server, auf dem Sie virtuelle Computer replizieren, unter **Replikationskonfiguration**die Option **diesen Computer als**Replikat Server aktivieren aus.

2.  Sie können über HTTP oder verschlüsselte HTTPS replizieren. Wählen Sie **Kerberos (http) verwenden** oder **Zertifikat basierte Authentifizierung (HTTPS) verwenden**. Standardmäßig sind http 80 und HTTPS 443 als Firewallausnahmen auf dem Hyper-V-Replikat Server aktiviert. Wenn Sie die Standard Port Einstellungen ändern, müssen Sie auch die Firewallausnahme ändern. Wenn Sie über HTTPS replizieren, müssen Sie ein Zertifikat auswählen, und Sie sollten die Zertifikat Authentifizierung eingerichtet haben.

3.  Aktivieren Sie für die Autorisierung die Option **Replikation von einem beliebigen authentifizierten Server zulassen** , um dem Replikat Server zuzulassen, dass der Replikations Datenverkehr für virtuelle Computer von einem beliebigen primären Server Aktivieren Sie **Replikation von den angegebenen Servern zulassen** , um nur Datenverkehr von den primären Servern zu akzeptieren, die Sie speziell auswählen.

    Für beide Optionen können Sie angeben, wo die replizierten VHDs auf dem Hyper-V-Replikat Server gespeichert werden sollen.

4.  Klicken Sie auf **OK** oder **Übernehmen**.

### <a name="step-2-set-up-the-firewall"></a>Schritt 2: Einrichten der Firewall
Um die Replikation zwischen dem primären und dem sekundären Server zuzulassen, muss der Datenverkehr über die Windows-Firewall (oder andere Firewalls von Drittanbietern) durchlaufen werden. Wenn Sie die Hyper-V-Rolle auf den Servern installiert haben, werden standardmäßig Ausnahmen für http (80) und HTTPS (443) erstellt. Wenn Sie diese Standardports verwenden, müssen Sie nur die Regeln aktivieren:

-  So aktivieren Sie die Regeln auf einem eigenständigen Host Server:

    1. Öffnen Sie Windows-Firewall mit erweiterter Sicherheit , und klicken Sie auf **Eingehende Regeln**.

    2. Zum Aktivieren der HTTP-Authentifizierung (Kerberos) klicken Sie mit der rechten Maustaste auf **Hyper-V-Replikat-http-Listener (TCP-in)**  > **Regel aktivieren** Klicken Sie zum Aktivieren der HTTPS-Zertifikat basierten Authentifizierung mit der rechten Maustaste auf **Hyper-V-Replikat-HTTPS-Listener (TCP-in)** > E-**able-Regel**.

-  Um Regeln für einen Hyper-V-Cluster zu aktivieren, öffnen Sie eine Windows PowerShell-Sitzung mithilfe von **als Administrator ausführen**, und führen Sie dann einen der folgenden Befehle aus:

    -   Für http:`get-clusternode | ForEach-Object  {Invoke-command -computername $_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"}}`

    -   Für https:`get-clusternode | ForEach-Object  {Invoke-command -computername $_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"}}`

### <a name="enable-virtual-machine-replication"></a>Aktivieren der Replikation der virtuellen Computer
Führen Sie auf jedem virtuellen Computer, den Sie replizieren möchten, folgende Schritte aus:

1.  Wählen Sie im **Detail** Bereich von Hyper-V-Manager einen virtuellen Computer aus, indem Sie darauf klicken.
    Klicken Sie mit der rechten Maustaste auf den ausgewählten virtuellen Computer, und klicken Sie auf **Replikation aktivieren** , um den Assistenten zum Aktivieren

2.  Klicken Sie auf der Seite **Vorbemerkungen** auf **Weiter**.

3.  Geben Sie auf der Seite **Replikat Server angeben** im Feld Replikat Server den NetBIOS-oder FQDN des Replikat Servers ein. Wenn der Replikat Serverteil eines Failoverclusters ist, geben Sie den Namen des Hyper-V-Replikat Brokers ein. Klicken Sie auf **Weiter**.

4.  Auf der Seite **Verbindungsparameter angeben** Ruft das Hyper-V-Replikat automatisch die Authentifizierungs-und Port Einstellungen ab, die Sie für den Replikat Server konfiguriert haben. Wenn Werte nicht abgerufen werden, überprüfen Sie, ob der Server als Replikat Server konfiguriert und in DNS registriert ist. Falls erforderlich, müssen Sie die Einstellung manuell eingeben.

5.  Vergewissern Sie sich auf der Seite **Replikations-VHDs auswählen** , dass die VHDs, die Sie replizieren möchten, ausgewählt ist, und deaktivieren Sie die Kontrollkästchen für alle virtuellen Festplatten, die Sie von der Replikation ausschließen möchten. Klicken Sie dann auf **Weiter**.

6.  Geben Sie auf der Seite **Replikations Häufigkeit konfigurieren** an, wie oft Änderungen vom primären zum sekundären Replikat synchronisiert werden sollen. Klicken Sie dann auf **Weiter**.

7.  Wählen Sie auf der Seite **zusätzliche Wiederherstellungspunkte konfigurieren** aus, ob nur der letzte Wiederherstellungspunkt beibehalten oder zusätzliche Punkte erstellt werden sollen.    Wenn Sie Anwendungen und Arbeits Auslastungen mit ihren eigenen VSS-Writern konsistent wiederherstellen möchten, sollten Sie **Volumeschattenkopie-Dienst (VSS) frequenc**y auswählen und angeben, wie oft App-konsistente Momentaufnahmen erstellt werden sollen. Beachten Sie, dass der Hyper-v-VMM-requestdienst auf den primären und sekundären Hyper-v-Servern ausgeführt werden muss. Klicken Sie dann auf **Weiter**.

8.  Wählen Sie auf der Seite **erste Replikation auswählen** die zu verwendende anfängliche Replikations Methode aus.  Mit der Standardeinstellung zum Senden der ersten Kopie über das Netzwerk werden die Konfigurationsdatei des primären virtuellen Computers (vmcx) und die virtuellen Festplatten Dateien (vhdx und VHD), die Sie über die Netzwerkverbindung ausgewählt haben, kopiert. Überprüfen Sie die Verfügbarkeit der Netzwerkbandbreite, wenn Sie diese Option verwenden möchten. Wenn der primäre virtuelle Computer bereits auf dem sekundären Standort als replizierten virtuellen Computer konfiguriert ist, kann es hilfreich sein, **eine vorhandene virtuelle Maschine auf dem Replikationsserver als erste Kopie zu verwenden**. Sie können den Hyper-V-Export verwenden, um den primären virtuellen Computer zu exportieren und als virtuellen Replikat Computer auf dem sekundären Server zu importieren. Bei größeren virtuellen Computern oder eingeschränkter Bandbreite können Sie entscheiden, ob die erste Replikation über das Netzwerk zu einem späteren Zeitpunkt erfolgen soll, und anschließend außerhalb der Spitzenzeiten konfigurieren oder die Informationen zur ersten Replikation als Offline Medien senden.

    Wenn Sie Offline Replikation durchführen, transportieren Sie die anfängliche Kopie mithilfe eines externen Speichermediums (z. b. einer Festplatte oder eines USB-Laufwerks) auf den sekundären Server. Zu diesem Zweck müssen Sie den externen Speicher mit dem primären Server (oder Besitzer Knoten in einem Cluster) verbinden. Wenn Sie dann erste Kopie mithilfe externer Medien senden auswählen, können Sie einen Speicherort lokal oder auf dem externen Medium angeben, auf dem die anfängliche Kopie gespeichert werden kann.  Ein Platzhalter für einen virtuellen Computer wird am Replikat Standort erstellt. Nachdem die erste Replikation abgeschlossen ist, kann der externe Speicher an den Replikat Standort ausgeliefert werden. Dort verbinden Sie das externe Medium mit dem sekundären Server oder dem Besitzer Knoten des sekundären Clusters. Anschließend importieren Sie das erste Replikat an einen angegebenen Speicherort und führen es in den virtuellen Platzhalter Computer zusammen.

9. Überprüfen Sie auf der Seite Fertigstellen der **Replikation** die Informationen in der Zusammenfassung, und klicken Sie dann auf **Fertigstellen.** Die Daten des virtuellen Computers werden in Übereinstimmung mit den ausgewählten Einstellungen übertragen. Daraufhin wird ein Dialogfeld mit dem Hinweis angezeigt, dass die Replikation erfolgreich aktiviert wurde.

10. Wenn Sie die erweiterte (verkettete) Replikation konfigurieren möchten, öffnen Sie den Replikat Server, und klicken Sie mit der rechten Maustaste auf die zu replizierende virtuelle Maschine. Klicken Sie auf **Replikation**  >  **Replikation erweitern** und geben Sie die Replikations

## <a name="run-a-failover"></a>Ausführen eines Failovers
Nach Abschluss dieser Bereitstellungs Schritte ist Ihre replizierte Umgebung betriebsbereit. Nun können Sie Failover nach Bedarf ausführen.

**Test Failover**: Wenn Sie ein Test Failover ausführen möchten, klicken Sie mit der rechten Maustaste auf den primären virtuellen Computer, und wählen Sie **Replikations**  >  **Test Failover**aus. Wählen Sie bei der Konfiguration den neuesten oder einen anderen Wiederherstellungspunkt aus. Auf dem sekundären Standort wird ein neuer virtueller Testcomputer erstellt und gestartet. Nachdem Sie die Tests abgeschlossen haben, wählen Sie **Test Failover** auf dem virtuellen Replikat Computer beenden aus, um den Vorgang zu bereinigen. Beachten Sie, dass Sie für einen virtuellen Computer nur ein Test Failover gleichzeitig ausführen können. [Weitere Informationen](https://blogs.technet.com/b/virtualization/archive/2012/07/26/types-of-failover-operations-in-hyper-v-replica.aspx)

**Geplantes Failover**: zum Ausführen eines geplanten Failovers klicken Sie mit der rechten Maustaste auf den primären virtuellen Computer und wählen **Replikations**  >  **Geplantes Failover**aus. Beim geplanten Failover werden Voraussetzungs Prüfungen durchgeführt, um einen Datenverlust zu verhindern. Es wird überprüft, ob der primäre virtuelle Computer vor dem Failover heruntergefahren wird. Nach dem Failover des virtuellen Computers werden die Änderungen an den primären Standort replizieren, wenn der virtuelle Computer verfügbar ist. Beachten Sie, dass der primäre Server zu diesem Zweck so konfiguriert werden muss, dass die Replikation vom sekundären Server oder vom Hyper-V-Replikat Broker bei einem primären Cluster empfangen wird. Das geplante Failover sendet den letzten Satz an nach verfolgten Änderungen. [Weitere Informationen](https://blogs.technet.com/b/virtualization/archive/2012/07/31/types-of-failover-operations-in-hyper-v-replica-part-ii-planned-failover.aspx)

**Ungeplantes Failover**: Wenn Sie ein ungeplantes Failover ausführen möchten, klicken Sie mit der rechten Maustaste auf den virtuellen **Replikat**Computer, und wählen Sie im  >  **Unplanned Failover** Hyper-V-Manager oder Failoverclustering-Manager Replikations Wenn diese Option aktiviert ist, können Sie den letzten Wiederherstellungspunkt oder frühere Wiederherstellungspunkte wiederherstellen. Überprüfen Sie nach dem Failover, ob alles erwartungsgemäß auf dem virtuellen Computer ausgeführt wird, und klicken Sie dann auf dem virtuellen Replikat Computer auf **Fertig** stellen. [Weitere Informationen](https://blogs.technet.com/b/virtualization/archive/2012/08/08/types-of-failover-operations-in-hyper-v-replica-part-iii-unplanned-failover.aspx)
