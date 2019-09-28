---
title: Wiederherstellung der AD-Gesamtstruktur-Windows Server 2003
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 43a2034cb707d4333abdce5f5b2b09d6c4b5a33a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390058"
---
# <a name="ad-forest-recovery---windows-server-2003-recovery"></a>Wiederherstellung der AD-Gesamtstruktur-Windows Server 2003

>Gilt für: Windows Server 2003

Dieses Thema enthält Wiederherstellungs Prozeduren für Domänen Controller (DCS), auf denen Windows Server 2003 ausgeführt wird. Der allgemeine Vorgang für die Wiederherstellung der Gesamtstruktur unterscheidet sich nicht von Windows Server 2003-DCS, aber bestimmte Verfahren können aufgrund verschiedener Tools abweichen. Beispielsweise kann "Ntdsutil. exe" zum Sichern und Wiederherstellen von DCS verwendet werden, die Windows Server 2003 DCS ausführen, wohingegen "Windows Server-Sicherung" oder "Wbadmin. exe" für DCS verwendet wird, auf denen Windows Server 2008 oder höher ausgeführt wird.  
  
- [Sichern der System Statusdaten](#backing-up-the-system-state-data)  
- [Ausführen einer nicht autorisierenden Wiederherstellung](#performing-a-nonauthoritative-restore)  
- [Installieren und Konfigurieren des DNS-Server Dienstanbieter](#install-and-configure-the-dns-server-service)

## <a name="backing-up-the-system-state-data"></a>Sichern der System Statusdaten
Verwenden Sie das folgende Verfahren, um die System Statusdaten zusammen mit allen anderen Daten, die Sie für den aktuellen Sicherungs Vorgang ausgewählt haben, eines Domänen Controllers zu sichern, auf dem Windows Server 2003 ausgeführt wird. Windows Server 2003 umfasst das Tool Ntbackup, das Sie zum Sichern der System Statusdaten verwenden können.  
  
Sie müssen mindestens Mitglied der Gruppe " **Administratoren** " oder " **Sicherungs Operatoren**" oder einer entsprechenden Gruppe sein, um Dateien und Ordner zu sichern.   
  
Wenn Sie die System Statusdaten auf einem Band sichern und das Sicherungsprogramm anzeigt, dass kein nicht verwendetes Medium verfügbar ist, müssen Sie möglicherweise Wechsel Speicher verwenden. Dadurch wird das Band dem freien Medienpool hinzugefügt, sodass es von der Sicherung verwendet werden kann.  
  
Sie können nur die System Statusdaten auf einem lokalen Computer sichern. Sie können Sie nicht auf einem Remote Computer sichern.  
  
### <a name="to-back-up-the-system-state-data-on-a-domain-controller-that-runs-windows-server-2003"></a>So sichern Sie die System Statusdaten auf einem Domänen Controller, auf dem Windows Server 2003 ausgeführt wird  
  
1. Klicken Sie auf **Start**, zeigen Sie auf **Alle Programme**, auf **Zubehör**und auf **System**Programme, und klicken Sie dann auf **Sicherung**.  
2. Klicken Sie auf der **Willkommens** Seite auf erweiterter **Modus**.  
3. Aktivieren Sie auf der Registerkarte **Sicherung** das Kontrollkästchen für ein beliebiges Laufwerk, einen Ordner oder eine Datei, die Sie sichern möchten.  
4. Aktivieren Sie das Kontrollkästchen **System Status** .  
5. Klicken Sie auf **Sicherung starten**.  
  
## <a name="performing-a-nonauthoritative-restore"></a>Ausführen einer nicht autorisierenden Wiederherstellung  

Verwenden Sie das folgende Verfahren, um eine nicht autoritative Wiederherstellung eines Domänen Controllers auszuführen, auf dem Windows Server 2003 ausgeführt wird. Durch die Durchführung einer nicht autorisierenden Wiederherstellung auf Active Directory in Windows Server 2003 führen Sie automatisch eine nicht autoritative Wiederherstellung von SYSVOL aus. Es sind keine weiteren Schritte erforderlich.  
  
> [!NOTE]
> Wenn Sie auch das Betriebssystem Windows Server 2003 neu installieren, können Sie den Computer möglicherweise nicht der Domäne hinzufügen, und Sie können den Computer während des Setups des Betriebssystems beliebig benennen. Installieren Sie Active Directory nicht. Nachdem Sie das Betriebssystem neu installiert haben, fahren Sie direkt mit Schritt 4 fort.  
  
Auf Windows Server 2003-Domänen Controllern, auf denen nur Systemstatus Daten wieder hergestellt wurden, müssen Sie vor der Wiederherstellung alle Softwareanwendungen neu installieren, die auf DCS ausgeführt wurden. Wenn Sie AD DS auf dem ersten Domänen Controller in der Domäne wiederherstellen, wird auch die Registrierung wieder hergestellt, da beide Teil der System Statusdaten sind. Berücksichtigen Sie dies, wenn auf diesen DCS Anwendungen ausgeführt werden, die in der Registrierung gespeichert sind.  
  
Um Zeit zu sparen, die zur erneuten Installation der Software erforderlich ist, stellen Sie fest, ob Anwendungen, die auf den DCS installiert werden müssen, mit dem virtuellen Domänen Controller kompatibel sind. Solche Anwendungen können vor dem Klonen auf dem Quell Domänen Controller installiert werden, um die Zeit und den Aufwand für die Installation auf den geklonten virtuellen DCS zu sparen.  
  
### <a name="to-perform-a-nonauthoritative-restore"></a>So führen Sie eine nicht autoritative Wiederherstellung aus
  
1. Nachdem Sie den DC gestartet haben, drücken Sie F8, um den Computer im Verzeichnisdienste-Wiederherstellungs Modus (DSRM) neu zu starten.  
2. Wählen Sie **Verzeichnisdienst-Wiederherstellungs Modus (nur Windows-Domänen Controller)** aus.  
3. Wählen Sie das Betriebssystem aus, das Sie im Wiederherstellungs Modus starten möchten.  
4. Melden Sie sich als Administrator an (Sie können nur ein lokales Computer Konto verwenden, es ist keine Domänen Anmeldeoption verfügbar).  
5. Geben Sie an einer Eingabeaufforderung **Ntbackup**ein, und drücken Sie dann die EINGABETASTE.  
6. Klicken Sie auf der **Willkommens** Seite auf erweiterter **Modus**, und wählen Sie dann die Registerkarte **Medien wiederherstellen und verwalten** aus. (Wählen Sie nicht **Restore Wizard**aus.)  
7. Wählen Sie die entsprechende Sicherungsdatei aus, die Sie wiederherstellen möchten, und stellen Sie sicher, dass die Kontrollkästchen **System** Datenträger und **System**  
8. Klicken Sie auf **Wiederherstellung starten**.  
9. Wenn der Wiederherstellungs Vorgang beendet ist, starten Sie den Computer neu.  
  
Mithilfe des folgenden Verfahrens können Sie eine autoritative (auch als primär bezeichnet) Wiederherstellung von SYSVOL auf einem Domänen Controller ausführen, auf dem Windows Server 2003 ausgeführt wird. Führen Sie dieses Verfahren nur auf dem ersten Windows Server 2003-DC aus, der in der Domäne wieder hergestellt wird.  
  
### <a name="to-perform-an-authoritative-restore-of-sysvol"></a>So führen Sie eine autoritative Wiederherstellung von SYSVOL aus  
  
1. Führen Sie die Schritte 1 bis 8 im vorherigen Verfahren aus.  
2. Klicken Sie im Dialogfeld **Wiederherstellung bestätigen** auf **erweitert**.  
3. Wenn Sie eine autoritative Wiederherstellung von SYSVOL durchführen möchten, aktivieren Sie das Kontrollkästchen **beim Wiederherstellen replizierter Datasets, markieren Sie die wiederhergestellten Daten als primäre Daten für alle Replikate**  

   > [!NOTE]
   > Das Markieren der wiederhergestellten Daten als primäre Daten in der Sicherung entspricht dem Festlegen des **BurFlags** -Eintrags auf D4 unter dem folgenden Registrierungs Unterschlüssel:  
   >   
   > **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NtFrs\Parameters\Cumulative Replikat Sätze @ no__t-1** *GUID*  

4. Wenn der Wiederherstellungs Vorgang beendet ist, starten Sie den Computer neu.  
  
## <a name="install-and-configure-the-dns-server-service"></a>Installieren und Konfigurieren des DNS-Server Dienstanbieter

Wenn der von der Sicherung wiederhergestellte Domänen Controller unter Windows Server 2003 ausgeführt wird, können Sie den DNS-Server installieren, ohne den Domänen Controller mit einem Netzwerk zu verbinden.  
  
### <a name="to-install-and-configure-the-dns-server-service"></a>So installieren und konfigurieren Sie den DNS-Server Dienst  
  
1. Assistent zum Öffnen von Windows-Komponenten. So öffnen Sie den Assistenten:  

   - Klicken Sie auf **Start**, klicken Sie auf **Systemsteuerung**, und klicken Sie dann auf **Programme hinzufügen oder entfernen**.  
   - Klicken Sie auf **Windows-Komponenten hinzufügen/entfernen**.  

2. Aktivieren Sie unter **Komponenten**das Kontrollkästchen **Netzwerkdienste** , und klicken Sie dann auf **Details**.  
3. Aktivieren Sie in **unter Komponenten von Netzwerkdiensten**das Kontrollkästchen **Domain Name System (DNS)** , klicken Sie auf **OK**, und klicken Sie dann auf **weiter**.  
4. Wenn Sie dazu aufgefordert werden, geben Sie unter **Dateien kopieren von**den vollständigen Pfad der Verteilungs Dateien ein, und klicken Sie dann auf **OK**.  

   Führen Sie nach der Installation die folgenden Schritte aus, um den DNS-Server zu konfigurieren.  

5. Klicken Sie auf **Start**, zeigen Sie auf **Alle Programme**und auf **Verwaltung**, und klicken Sie dann auf **DNS**.  
6. Erstellen Sie DNS-Zonen für die gleichen DNS-Domänen Namen, die vor dem kritischen Funktionsfehler auf den DNS-Servern gehostet wurden. Weitere Informationen finden Sie unter Hinzufügen einer Forward-Lookupzone ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574)).  
7. Konfigurieren Sie die DNS-Daten so, wie Sie vor den kritischen Fehlern vorhanden waren. Zum Beispiel:  

   - Konfigurieren Sie DNS-Zonen, die in AD DS gespeichert werden sollen. Weitere Informationen finden Sie unter Ändern des Zonen Typs ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579)).  
   - Konfigurieren Sie die DNS-Zone, die für Domänen Controller-Serverlocatorpunkt-Ressourcen Einträge (DC Serverlocatorpunkt) autorisierend ist, um sicheres dynamisches Update zuzulassen. Weitere Informationen finden Sie unter nur sichere dynamische Updates zulassen ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580)).  

8. Stellen Sie sicher, dass die übergeordnete DNS-Zone Delegat-Ressourcen Einträge (Nameserver (NS) und Host (A)-Ressourcen Einträge) für die untergeordnete Zone enthält, die auf diesem DNS-Server gehostet wird. Weitere Informationen finden Sie unter Erstellen einer Zonen Delegierung ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562)).  
9. Geben Sie nach dem Konfigurieren von DNS an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:  

   **NET stoppt Netlogon**

10. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:  

    **NET Start Netlogon**

    > [!NOTE]
    > Bei der Anmeldung werden die Domänen Controller-Locator-Ressourcen Einträge für diesen Domänen Controller in DNS registriert. Wenn Sie den DNS-Server Dienst auf einem Server in der untergeordneten Domäne installieren, kann dieser DC seine Einträge nicht sofort registrieren. Dies liegt daran, dass Sie derzeit im Rahmen des Wiederherstellungsprozesses isoliert ist und der primäre DNS-Server der Gesamtstruktur-Stamm-DNS-Server ist. Konfigurieren Sie diesen Computer mit der gleichen IP-Adresse wie vor dem Notfall, um Fehler bei der Suche nach einem DC-Dienst zu vermeiden.

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
- [AD-Gesamtstruktur Wiederherstellung: Entwerfen eines benutzerdefinierten Wiederherstellungs Plans](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD-Gesamtstruktur Wiederherstellung: Identifizieren des Problems](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD-Gesamtstruktur Wiederherstellung: Bestimmen der Wiederherstellung](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD-Gesamtstruktur Wiederherstellung: Ausführen der ersten Wiederherstellung](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)  
- [AD-Gesamtstruktur Wiederherstellung: häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
- [Wiederherstellung der AD-Gesamtstruktur: Wiederherstellen einer einzelnen Domäne innerhalb einer Gesamtstruktur mit mehreren](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [Active Directory-Gesamtstruktur Wiederherstellung mit Windows Server 2003-Domänen Controllern](AD-Forest-Recovery-Windows-Server-2003.md) 
