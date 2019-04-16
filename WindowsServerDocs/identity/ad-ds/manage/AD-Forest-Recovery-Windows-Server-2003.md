---
title: Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung auf Windows Server2003
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: daebbc65b9864554fde839c3865f507ab787e6b6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---windows-server-2003-recovery"></a>Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung auf Windows Server2003

>Gilt für: Windows Server 2003

Dieses Thema enthält Gesamtstruktur Wiederherstellungsschritte für Domänencontroller (DCs), auf denen Windows Server2003 ausgeführt wird. Der allgemeine Prozess für die Wiederherstellung der Gesamtstruktur unterscheidet sich nicht mit Windows Server2003-Domänencontrollern, die bestimmte Verfahren können aufgrund der unterschiedlichen Tools unterscheiden sich jedoch. Beispielsweise kann Ntdsutil.exe zum Sichern und Wiederherstellen von Domänencontrollern, auf denen Windows Server2003-Domänencontrollern, ausgeführt, während Windows Server-Sicherung oder Wbadmin.exe ist für Domänencontroller, auf denen Windows Server2008 ausgeführt oder höher verwendet werden.  
  
-   [Sichern von Daten des Systemstatus](#Backing-up-the-System-State-data)  
  
-   [Durchführen einer nicht autoritativen Wiederherstellung](#Performing-a-nonauthoritative restore)  
  
-   [Installieren Sie und konfigurieren Sie den DNS-Serverdienst](#Install-and-configure-the-DNS-Server-service)  
  
  
## <a name="backing-up-the-system-state-data"></a>Sichern von Daten des Systemstatus  
 Verwenden das folgende Verfahren, um die Systemstatusdaten zu sichern, sowie alle anderen Daten, die Sie für die aktuelle Sicherung ausgewählt haben, über einen Domänencontroller, die Windows Server2003 ausführt. Windows Server2003 enthält die Tools "Ntbackup", die Sie verwenden können, um Daten von Systemstatus zu sichern.  
  
 Mitgliedschaft in **Administratoren** oder **Sicherungsoperatoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um Dateien und Ordner sichern.   
  
 Sichern der Systemstatusdaten auf ein Band und das Backup-Programm weist darauf hin, dass keine Medien zur Verfügung steht, müssen Sie möglicherweise die Verwendung von Wechselmedien. Dadurch wird das Band der Pool freier Medien hinzugefügt, damit, dass die Sicherung, die sie verwenden kann.  
  
 Sie können nur die Systemstatusdaten auf einem lokalen Computer sichern. Sie können nicht auf einem Remotecomputer Sicherung.  
  
### <a name="to-back-up-the-system-state-data-on-a-domain-controller-that-runs-windows-server-2003"></a>Um die Systemstatusdaten auf einem Domänencontroller zu sichern, die Windows Server2003 ausgeführt wird  
  
1.  Klicken Sie auf **starten**, zeigen Sie auf **alle Programme**, zeigen Sie auf **Zubehör**, zeigen Sie auf **Systemprogramme**, und klicken Sie dann auf **Sicherung**.  
  
2.  Auf der **Willkommen** auf **erweiterten Modus**.  
  
3.  Auf der **Sicherung** Registerkarte, aktivieren Sie das Kontrollkästchen für Laufwerk, Ordner oder die Datei, die Sie sichern möchten.  
  
4.  Wählen Sie die **Systemstatus** Kontrollkästchen.  
  
5.  Klicken Sie auf **Sicherung starten**.  
  
  
## <a name="performing-a-nonauthoritative-restore"></a>Durchführen einer nicht autoritativen Wiederherstellung  
 Verwenden Sie das folgende Verfahren, eine nicht autoritative Wiederherstellung von einem Domänencontroller ausführen, die Windows Server2003 ausgeführt wird. Eine nicht autoritative Wiederherstellung auf Active Directory in Windows Server2003 ausführen, führen Sie automatisch eine nicht autoritative Wiederherstellung von SYSVOL. Es sind keine weiteren Schritteerforderlich.  
  
> [!NOTE]
>  Wenn Sie auch das Windows Server2003-Betriebssystem erneut installieren, Sie oder den Computer möglicherweise nicht der Domäne beitreten und können einen beliebigen Namen während der Installation des Betriebssystems auf dem Computer gewähren. Installieren Sie Active Directory nicht. Wechseln Sie nach der Neuinstallation des Betriebssystems, direkt zu Schritt4.  
  
 Auf Windows Server2003-Domänencontrollern, in denen Sie nur die Systemstatusdaten wiederhergestellt haben, müssen Sie auch alle softwareanwendungen neu installieren, die vor der Wiederherstellung auf dem Domänencontroller ausgeführt werden. Wiederherstellen von AD DS auf dem ersten Domänencontroller in der Domäne wird auch die Registrierung wiederhergestellt, da beide Systemstatusdaten gehören. Berücksichtigen Sie dies, wenn Sie alle Anwendungen, die auf diesen Domänencontrollern ausgeführt haben und alle Informationen, die in der Registrierung gespeichert mussten.  
  
 Zum Speichern der Zeitaufwand für die Neuinstallation der Software ermitteln Sie, ob Anwendungen, die auf den Domänencontrollern installiert werden müssen mit Klonen virtueller Domänencontroller kompatibel sind. Solche Anwendungen können auf dem Quelldomänencontroller installiert werden, vor dem Klonen, um Zeit und Aufwand erforderlich, um die Installation auf dem geklonten virtuellen Domänencontroller zu speichern.  
  
#### <a name="to-perform-a-nonauthoritative-restore"></a>Eine nicht autoritative Wiederherstellung  
  
1.  Nachdem Sie den Domänencontroller starten, drücken Sie F8, um den Computer in Directory Services-Wiederherstellungsmodus (DSRM) neu starten.  
  
2.  Wählen Sie **Modus "Verzeichnisdienste wiederherstellen" (nur Windows-Domänencontroller)**.  
  
3.  Wählen Sie das Betriebssystem, das Sie im Wiederherstellungsmodus starten möchten.  
  
4.  Melden Sie sich als Administrator (Sie können nur mithilfe eines lokalen Computerkontos keine Domäne Anmeldung Option verfügbar ist).  
  
5.  Geben Sie an einer Eingabeaufforderung **Ntbackup**, und drücken Sie dann die EINGABETASTE.  
  
6.  Auf der **Willkommen** auf **erweiterten Modus**, und wählen Sie dann die **Medien wiederherstellen und verwalten** Registerkarte (Wählen Sie nicht **Assistenten**.)  
  
7.  Wählen Sie die entsprechende Sicherungsdatei wiederherstellen aus, und stellen sicher, dass die **Systemdatenträger** und **Systemstatus** Kontrollkästchen aktiviert sind.  
  
8.  Klicken Sie auf **Wiederherstellung starten**.  
  
9. Wenn der Wiederherstellungsvorgang abgeschlossen ist, starten Sie den Computer neu.  
  
 Verwenden Sie das folgende Verfahren eine (auch bekannt als primäre) autorisierende Wiederherstellung von SYSVOL auf einem Domänencontroller ausführen, die Windows Server2003 ausgeführt wird. Führen Sie dieses Verfahren nur auf der ersten Windows Server2003-Domänencontroller, die in der Domäne wiederhergestellt wird.  
  
### <a name="to-perform-an-authoritative-restore-of-sysvol"></a>Eine autorisierende Wiederherstellung von SYSVOL  
  
1.  Führen Sie die Schritte1 bis 8, im vorherigen Verfahren.  
  
2.  In der **Wiederherstellung bestätigen** Dialogfeld, klicken Sie auf **erweitert**.  
  
3.  Aktivieren Sie das Kontrollkästchen, um eine autorisierende Wiederherstellung von SYSVOL **Wenn replizierten, markieren Sie die wiederhergestellten Daten als primären Daten für alle Replikate**.  
  
    > [!NOTE]
    >  Markieren die wiederhergestellten Daten, wie die primären Daten in die Sicherung Einstellung entspricht der **BurFlags** Eintrag D4 unter den folgenden Registrierungsunterschlüssel:  
    >   
    >  **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NtFrs\Parameters\Cumulative Replikat Sets\\***GUID*  
  
4.  Wenn der Wiederherstellungsvorgang abgeschlossen ist, starten Sie den Computer neu.  
  
 
## <a name="install-and-configure-the-dns-server-service"></a>Installieren Sie und konfigurieren Sie den DNS-Serverdienst  
 Wenn der Domänencontroller, die Sie aus einer Sicherung wiederhergestellt, Windows Server2003 ausgeführt wird, können Sie die DNS-Server installieren, ohne dass eine Verbindung des Domänencontrollers mit einem Netzwerk.  
  
### <a name="to-install-and-configure-the-dns-server-service"></a>So installieren und konfigurieren den DNS-Serverdienst  
  
1.  Öffnen Sie die Assistenten für Windows-Komponenten. Um den Assistenten zu öffnen:  
  
    -   Klicken Sie auf **starten**, klicken Sie auf **Systemsteuerung**, und klicken Sie dann auf **Software**.  
  
    -   Klicken Sie auf **Windows-Komponenten hinzufügen/entfernen**.  
  
2.  In **Komponenten**, wählen die **Netzwerkdienste**, und klicken Sie dann auf **Details**.  
  
3.  In **Unterkomponenten von Netzwerkdiensten**, wählen die **Domain Name System (DNS)** Kontrollkästchen, klicken Sie auf **OK**, und klicken Sie dann auf **Weiter**.  
  
4.  Wenn Sie, in aufgefordert werden **Dateien kopieren von**, geben Sie den vollständigen Pfad der Installationsdateien, und klicken Sie dann auf **OK**.  
  
     Nach Abschluss der Installation die folgenden Schritteaus, um den DNS-Server konfigurieren.  
  
5.  Klicken Sie auf **starten**, zeigen Sie auf **alle Programme**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DNS**.  
  
6.  Erstellen Sie DNS-Zonen für die gleichen DNS-Domänennamen, die gehostet wurden auf die DNS-Server vor der kritischen Fehler. Weitere Informationen finden Sie unter Hinzufügen einer Forward-Lookupzone ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574)).  
  
7.  Konfigurieren Sie die DNS-Daten vor kritischen Fehlfunktion vorhanden war. Zum Beispiel:  
  
    -   Konfigurieren Sie DNS-Zonen in AD DS gespeichert werden. Weitere Informationen finden Sie unter Ändern des Zonentyps ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579)).  
  
    -   Konfigurieren Sie die DNS-Zone, die für Domänencontroller (DC-Locator) Ressource-Locatoreinträgen sichere dynamische Updates zulassen autorisierend ist. Weitere Informationen finden Sie unter ermöglichen nur sichere dynamische Updates ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580)).  
  
8.  Stellen Sie sicher, dass die übergeordneten DNS-Zone Delegation-Ressourceneinträge (name Server (NS) und Kleben Host (A) Ressource Datensätze) für die untergeordnete Zone enthält, die auf diesen DNS-Server gehostet wird. Weitere Informationen finden Sie unter Erstellen einer Zonendelegierung ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562)).  
  
9. Nach dem Konfigurieren von DNS Geben Sie an der Eingabeaufforderung den folgenden Befehl, und drücken Sie dann die EINGABETASTE:  
  
     **Net Stop netlogon**  
  
10. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:  
  
     **Net Start netlogon**  
  
    > [!NOTE]
    >  Der Anmeldedienst wird die Domänencontrollerlocator-Ressourceneinträge in DNS für diesen Domänencontroller registriert werden. Bei der Installation des DNS-Serverdiensts auf einem Server in der untergeordneten Domäne werden diesen Domänencontroller nicht sofort die Datensätze registrieren können. Dies ist, da es derzeit isoliert ist als Bestandteil der Wiederherstellung, und der primäre DNS-Server der Gesamtstruktur Stamm-DNS-Server ist. Konfigurieren Sie diesen Computer mit der gleichen IP-Adresse wie vor dem Datenverlust DC-Lookup Dienstausfälle zu vermeiden.

## <a name="next-steps"></a>Nächste Schritte
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
-   [Wiederherstellung des AD-Gesamtstruktur - Konzipierung einen Wiederherstellungsplan benutzerdefinierte Gesamtstruktur](AD-Forest-Recovery-Devising-a-Plan.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - identifizieren](AD-Forest-Recovery-Identify-the-Problem.md)
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Bestimmen der Vorgehensweise beim Wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [Wiederherstellung der Active Directory-Gesamtstruktur - führen Sie erste wiederherstellen](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)  
-   [AD-Gesamtstruktur-Wiederherstellung – häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
-   [Wiederherstellung des AD-Gesamtstruktur - Wiederherstellung von einer einzelnen Domäne innerhalb einer Gesamtstruktur Multidomain](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung der Gesamtstruktur mit Windows Server2003-Domänencontroller](AD-Forest-Recovery-Windows-Server-2003.md) 
