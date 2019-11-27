---
ms.assetid: 82918181-525d-4e93-af96-957dac6aedb6
title: Anhang B Einrichten der Test Umgebung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: af045545826269630af9327480cda59093d219df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407141"
---
# <a name="appendix-b-setting-up-the-test-environment"></a>Anhang B: Einrichten der Testumgebung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema werden die Schritte zum Erstellen eines praktischen Labors zum Testen der dynamischen Zugriffssteuerung beschrieben. Die Anweisungen müssen schrittweise befolgt werden, da viele Komponenten über Abhängigkeiten verfügen.  

## <a name="prerequisites"></a>Voraussetzungen  
**Hardware-und Softwareanforderungen**  

Anforderungen für die Einrichtung des Testlabors:  

-   Ein Hostserver unter Windows Server 2008 R2 mit SP1 und Hyper-V  

-   Eine Kopie von Windows Server 2012 ISO  

-   Eine Kopie von Windows 8 ISO  

-   Microsoft Office 2010  

-   Ein Server unter Microsoft Exchange Server 2003 oder höher  

Sie müssen die folgenden virtuellen Computer erstellen, um die Szenarien für die dynamische Zugriffssteuerung zu testen:  

-   DC1 (Domänencontroller)  

-   DC2 (Domänencontroller)  

-   FILE1 (Dateiserver und Active Directory-Rechteverwaltungsdienste)  

-   SRV1 (POP3- und SMTP-Server)  

-   CLIENT1 (Clientcomputer mit Microsoft Outlook)  

Die Kennwörter für die virtuellen Computer sollten wie folgt lauten:  

-   BUILTIN\Administrator: pass@word1  

-   Conto so\administrator: pass@word1  

-   Alle anderen Konten: pass@word1  

## <a name="build-the-test-lab-virtual-machines"></a>Erstellen der virtuellen Computer für das Testlabor  

### <a name="install-the-hyper-v-role"></a>Installieren der Hyper-V-Rolle  
Sie müssen die Hyper-V-Rolle auf einem Computer unter Windows Server 2008 R2 mit SP1 installieren.  

##### <a name="to-install-the-hyper-v-role"></a>So installieren Sie die Hyper-V-Rolle  

1.  Klicken Sie auf **Start**und anschließend auf „Server-Manager“.  

2.  Klicken Sie im Bereich „Rollenübersicht“ des Server-Manager-Hauptfensters auf **Rollen hinzufügen**.  

3.  Klicken Sie auf der Seite **Serverrollen auswählen** auf **Hyper-V**.  

4.  Klicken Sie auf der Seite **Virtuelle Netzwerke erstellen** auf mindestens eine Netzwerkkarte, wenn Sie möchten, dass ihre Netzwerkverbindung für virtuelle Computer verfügbar ist.  

5.  Klicken Sie auf der Seite **Installationsauswahl bestätigen** auf **Installieren**.  

6.  Zum Abschließen der Installation muss der Computer neu gestartet werden. Klicken Sie zum Beenden des Assistenten auf **Schließen**, und klicken Sie anschließend auf **Ja**, um den Computer neu zu starten.  

7.  Melden Sie sich nach dem Neustart des Computers mit demselben Konto an, das Sie zum Installieren der Rolle verwendet haben. Klicken Sie, nachdem der Assistent zum Fortsetzen der Konfiguration die Installation abgeschlossen hat, auf **Schließen**, um den Assistenten zu beenden.  

### <a name="create-an-internal-virtual-network"></a>Erstellen eines internen virtuellen Netzwerks  
Im Folgenden erstellen wir ein internes virtuelles Netzwerk mit dem Namen „ID_AD_Network“.  

##### <a name="to-create-a-virtual-network"></a>So erstellen Sie ein virtuelles Netzwerk  

1.  Öffnen Sie den Hyper-V-Manager.  

2.  Klicken Sie im Menü **Aktionen** auf **Manager für virtuelle Netzwerke**.  

3.  Wählen Sie **Intern**unter **Virtuelles Netzwerk erstellen**aus.  

4.  Klicken Sie auf **Hinzufügen**. Es wird die Seite **Neues virtuelles Netzwerk** angezeigt.  

5.  Geben Sie **ID_AD_Network** als den Namen für das neue Netzwerk ein. Prüfen Sie die anderen Eigenschaften, und ändern Sie sie bei Bedarf.  

6.  Klicken Sie auf **OK** , um das virtuelle Netzwerk zu erstellen, und schließen Sie den Manager für virtuelle Netzwerke, oder klicken Sie auf **Übernehmen** zum Erstellen des virtuellen Netzwerks, und fahren Sie mithilfe des Managers für virtuelle Netzwerke fort.  

### <a name="BKMK_Build"></a>Erstellen des Domänen Controllers  
Erstellen Sie einen virtuellen Computer, der als der Domänencontroller (DC1) verwendet wird. Installieren Sie den virtuellen Computer mit Windows Server 2012 ISO, und nennen Sie ihn DC1.  

##### <a name="to-install-active-directory-domain-services"></a>So installieren Sie Active Directory-Domänendienste  

1. Verbinden Sie den virtuellen Computer mit „ID_AD_Network“. Melden Sie sich mit dem Kennwort <strong>pass@word1</strong>bei DC1 als Administrator an.  

2. Klicken Sie im Server-Manager auf **Verwalten**und dann auf **Rollen und Features hinzufügen**.  

3. Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  

4. Klicken Sie auf der Seite **Installationstyp auswählen** auf **Rollenbasierte oder featurebasierte Installation**, und klicken Sie anschließend auf **Weiter**.  

5. Klicken Sie auf der Seite **Zielserver auswählen** auf **Weiter**.  

6. Klicken Sie auf der Seite **Serverrollen auswählen** auf **Active Directory-Domänendienste**. Klicken Sie im Dialogfeld **Assistent zum Hinzufügen von Rollen und Features** auf **Features hinzufügen**, und klicken Sie auf **Weiter**.  

7. Klicken Sie auf der Seite **Features auswählen** auf **Weiter**.  

8. Überprüfen Sie die Informationen auf der Seite **Active Directory-Domänendienste** , und klicken Sie dann auf **Weiter**.  

9. Klicken Sie auf der Seite **Installationsauswahl bestätigen** auf **Installieren**. Die Statusanzeige „Featureinstallation“ auf der Seite „Ergebnisse“ zeigt an, dass die Rolle installiert wird.  

10. Stellen Sie auf der Seite **Ergebnisse** die erfolgreiche Installation sicher, und klicken Sie auf **Schließen**. Klicken Sie im Server-Manager auf das Warnsymbol mit dem Ausrufezeichen auf der oberen rechten Ecke des Bildschirms neben **Verwalten**. Klicken Sie in der Liste „Aufgaben“ auf die Verknüpfung **Server zu einem Domänencontroller heraufstufen**.  

11. Klicken Sie auf der Seite **Bereitstellungskonfiguration** auf **Neue Gesamtstruktur hinzufügen**, geben Sie den Namen der Stammdomäne **contoso.com** ein, und klicken Sie dann auf **Weiter**.  

12. Wählen Sie auf der Seite **Domänen Controller Optionen** die Domänen-und Gesamtstruktur Funktionsebenen als Windows Server 2012 aus, geben Sie das DSRM-Kennwort an <strong>pass@word1</strong>und klicken Sie dann auf **weiter**.  

13. Klicken Sie auf der Seite **DNS-Optionen** auf **Weiter**.  

14. Klicken Sie auf der Seite **Zusätzliche Optionen** auf **Weiter**.  

15. Geben Sie auf der Seite **Pfade** die Speicherorte für die Active Directory-Datenbanken, -Protokolldateien und den Ordner „SYSVOL“ an (oder übernehmen Sie die Standardspeicherorte), und klicken Sie dann auf **Weiter**.  

16. Bestätigen Sie auf der Seite **Optionen prüfen** die Einstellungen, und klicken Sie dann auf **Weiter**.  

17. Bestätigen Sie auf der Seite **Voraussetzungsüberprüfung**, dass die Validierung der Voraussetzungen abgeschlossen ist, und klicken Sie dann auf **Installieren**.  

18. Stellen Sie auf der Seite **Ergebnisse** sicher, dass der Server erfolgreich als Domänencontroller konfiguriert wurde, und klicken Sie dann auf **Schließen**.  

19. Starten Sie den Server zum Abschließen der AD DS-Installation neu. (Dies erfolgt standardmäßig automatisch.)  

Erstellen Sie die folgenden Benutzer mithilfe des Active Directory-Verwaltungscenters.  

##### <a name="create-users-and-groups-on-dc1"></a>Erstellen von Benutzern und Gruppen auf DC1  

1. Melden Sie sich bei „contoso.com“ als Administrator an. Starten des Active Directory-Verwaltungscenters  

2. Erstellen Sie die folgenden Sicherheitsgruppen:  


   |    Gruppenname    |        E-Mail-Adresse         |
   |------------------|------------------------------|
   |   FinanceAdmin   |   financeadmin@contoso.com   |
   | FinanceException | financeexception@contoso.com |


3. Erstellen Sie die folgende Organisationseinheit:  


   |   Name der Organisationseinheit    | Computer |
   |--------------|-----------|
   | FileServerOU |   FILE1   |


4. Erstellen Sie die folgenden Benutzer mit den angegebenen Attributen:  


   |       Benutzer       |  Benutzername  |     E-Mail-Adresse      | Department |      Gruppe       | Land/Region |
   |------------------|------------|------------------------|------------|------------------|----------------|
   | Myriam Delesalle | MDelesalle | MDelesalle@contoso.com |  Finanzen   |                  |       USA       |
   |    Miles Reid    |   MReid    |   MReid@contoso.com    |  Finanzen   |   FinanceAdmin   |       USA       |
   |   Esther Valle   |   EValle   |   EValle@contoso.com   | Vorgänge | FinanceException |       USA       |
   |   Maira Wenzel   |  MWenzel   |  MWenzel@contoso.com   |     Personalabteilung     |                  |       USA       |
   |     Jeff Low     |    JLow    |    JLow@contoso.com    |     Personalabteilung     |                  |       USA       |
   |    RMS-Server    |    rms     |    rms@contoso.com     |            |                  |                |

   Weitere Informationen über das Erstellen von Sicherheitsgruppen finden Sie unter [Create a New Group](https://technet.microsoft.com/library/dd861305.aspx) auf der Windows Server-Website.  

##### <a name="to-create-a-group-policy-object"></a>So erstellen Sie ein Gruppenrichtlinienobjekt  

1.  Platzieren Sie den Cursor in der oberen rechten Ecke des Bildschirms, und klicken Sie auf das Suchsymbol. Geben Sie im Suchfeld **Gruppenrichtlinienverwaltung** ein, und klicken Sie auf **Gruppenrichtlinienverwaltung**.  

2.  Erweitern Sie **Gesamtstruktur: contoso.com**, und erweitern Sie anschließend **Domänen**. Wechseln Sie zu **contoso.com**, erweitern Sie **(contoso.com)** , und wählen Sie dann **FileServerOU**aus. Klicken Sie mit der rechten Maustaste auf **Create a GPO in dieser Domäne, und verknüpfen Sie Sie hier**

3.  Geben Sie einen beschreibenden Namen für das Gruppenrichtlinienobjekt wie **FlexibleAccessGPO**ein, und klicken Sie dann auf **OK**.  

##### <a name="to-enable-dynamic-access-control-for-contosocom"></a>So aktivieren Sie die dynamische Zugriffssteuerung für „contoso.com“  

1.  Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole, klicken Sie auf **contoso.com**, und doppelklicken Sie anschließend auf **Domänencontroller**.  

2.  Klicken Sie mit der rechten Maustaste auf **Standarddomänencontroller-Richtlinie**, und wählen Sie **Bearbeiten**aus.  

3.  Doppelklicken Sie im Fenster „Gruppenrichtlinienverwaltungs-Editor“ auf **Computerkonfiguration**, doppelklicken Sie auf **Richtlinien**, doppelklicken Sie auf **Administrative Vorlagen**, doppelklicken Sie auf **System**, und doppelklicken Sie dann auf **KDC**.  

4.  Doppelklicken Sie auf die Option **KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring** , und wählen Sie die Option neben **Aktiviert**aus. Sie müssen diese Einstellung aktivieren, um „Zentrale Zugriffsrichtlinien“ verwenden zu können.  

5.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und führen Sie den folgenden Befehl aus:  

    ```  
    gpupdate /force  
    ```  

### <a name="BKMK_FS1"></a>Erstellen des Dateiservers und AD RMS Servers (file1)  

1. Erstellen Sie einen virtuellen Computer mit dem Namen file1 aus der ISO-Datei von Windows Server 2012.  

2. Verbinden Sie den virtuellen Computer mit „ID_AD_Network“.  

3. Verknüpfen Sie den virtuellen Computer mit der contoso.com-Domäne, und melden Sie sich dann mit dem Kennwort <strong>pass@word1</strong>bei file1 als condeso\administrator an.  

#### <a name="install-file-services-resource-manager"></a>Installieren des Ressourcen-Managers für Dateiserver  

###### <a name="to-install-the-file-services-role-and-the-file-server-resource-manager"></a>So installieren Sie die Rolle „Dateidienste“ und den Ressourcen-Manager für Dateiserver  

1.  Klicken Sie im Server-Manager auf **Rollen und Features hinzufügen**.  

2.  Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  

3.  Klicken Sie auf der Seite **Installationstyp auswählen** auf **Weiter**.  

4.  Klicken Sie auf der Seite **Zielserver auswählen** auf **Weiter**.  

5.  Erweitern Sie auf der Seite **Serverrollen auswählen** den Knoten **Datei- und Speicherdienste**, aktivieren Sie das Kontrollkästchen neben **Datei- und iSCSI-Dienste**, erweitern und wählen Sie **Ressourcen-Manager für Dateiserver**aus.  

    Klicken Sie im Assistenten zum Hinzufügen von Rollen und Features auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.  

6.  Klicken Sie auf der Seite **Features auswählen** auf **Weiter**.  

7.  Klicken Sie auf der Seite **Installationsauswahl bestätigen** auf **Installieren**.  

8.  Klicken Sie auf der Seite **Installation progress** auf **Close**.  

#### <a name="install-the-microsoft-office-filter-packs-on-the-file-server"></a>Installieren der Microsoft Office Filter Packs auf dem Dateiserver  
Sie sollten die Microsoft Office Filter Packs auf Windows Server 2012 installieren, um IFilters für eine größere Anzahl von Office-Dateien zu aktivieren, als standardmäßig bereitgestellt werden.  Windows Server 2012 verfügt über keine IFilter für Microsoft Office Dateien, die standardmäßig installiert sind, und die Datei Klassifizierungs Infrastruktur verwendet IFilters zum Durchführen der Inhaltsanalyse.  

Informationen zum Herunterladen und Installieren der IFilter finden Sie unter [Microsoft Office 2010 Filter Packs](https://go.microsoft.com/fwlink/?LinkID=234122).  

#### <a name="configure-email-notifications-on-file1"></a>Konfigurieren von E-Mail-Benachrichtigungen auf FILE1  
Beim Erstellen von Kontingenten und Dateibildschirmen haben Sie die Option, E-Mail-Benachrichtigungen an Benutzer zu senden, wenn ihre Kontingentbegrenzung erreicht wird oder nachdem sie versucht haben, gesperrte Dateien zu speichern. Wenn Sie bestimmte Administratoren routinemäßig über Kontingent- und Dateiprüfungsereignisse benachrichtigen möchten, können Sie einen oder mehrere standardmäßige Empfänger konfigurieren. Zum Senden dieser Benachrichtigungen müssen Sie den zum Weiterleiten der E-Mails verwendeten SMTP-Server angeben.  

###### <a name="to-configure-email-options-in-file-server-resource-manager"></a>So konfigurieren Sie E-Mail-Optionen im Ressourcen-Manager für Dateiserver  

1. Öffnen Sie den Ressourcen-Manager für Dateiserver. Klicken Sie zum Öffnen des Ressourcen-Managers für Dateiserver auf **Start**, geben Sie **Ressourcen-Manager für Dateiserver**ein, und klicken Sie dann auf **Ressourcen-Manager für Dateiserver**.  

2. Klicken Sie im Ressourcen-Manager für Dateiserver mit der rechten Maustaste auf **Ressourcen-Manager für Dateiserver**, und klicken Sie dann auf **Optionen konfigurieren**. Das Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** wird geöffnet.  

3. Geben Sie auf der Registerkarte **E-Mail-Benachrichtigungen** unter „SMTP-Servername“ oder „IP-Adresse“ den Hostnamen oder die IP-Adresse für den SMTP-Server ein, der E-Mail-Benachrichtigungen weiterleiten soll.  

4. Wenn Sie bestimmte Administratoren regelmäßig über Kontingent-oder Datei Prüfungs Ereignisse benachrichtigen möchten, geben Sie unter **Standard Administrator Empfänger**jede e-Mail-Adresse ein, z. b. fileadmin@contoso.com. Verwenden Sie das Format account@domain, und verwenden Sie Semikolons zum Trennen mehrerer Konten.  

#### <a name="create-groups-on-file1"></a>Erstellen von Gruppen auf FILE1  

###### <a name="to-create-security-groups-on-file1"></a>So erstellen Sie Sicherheitsgruppen auf FILE1  

1. Melden Sie sich bei file1 als "Conto so\administrator" mit dem folgenden Kennwort an: <strong>pass@word1</strong>.  

2. Fügen Sie „NT AUTHORITY\Authenticated“-Benutzer zur Gruppe **WinRMRemoteWMIUsers__** hinzu.  

#### <a name="create-files-and-folders-on-file1"></a>Erstellen von Dateien und Ordnern auf FILE1  

1.  Erstellen Sie ein neues NTFS-Volume auf FILE1, und erstellen Sie dann den folgenden Ordner: D:\Finance Documents.  

2.  Erstellen Sie die folgenden Dateien mit den angegebenen Details:  

    -   **Finance Memo.docx**: Fügen Sie etwas finanztechnischen Text in das Dokument ein. "Die Geschäftsregeln für den Zugriff auf Finanzdokumente haben sich z. b. geändert. Ausschließlich die Mitglieder der Gruppe 'FinanceExpert' können nun auf die Finanzdokumente zugreifen. Keine anderen Abteilungen oder Gruppen haben Zugriff. " Sie müssen die Auswirkung dieser Änderung bewerten, bevor Sie sie in Ihrer Umgebung implementieren. Stellen Sie sicher, dass in diesem Dokument in der Fußzeile jeder Seite „CONTOSO CONFIDENTIAL“ steht.  

    -   **Request for Approval to Hire.docx**: Erstellen Sie ein Formular in diesem Dokument, das Bewerberinformationen erfasst. Im Dokument müssen folgende Felder vorhanden sein: **Name des Bewerbers, Sozialversicherungsnummer, Position, vorgeschlagenes Gehalt, Startdatum, Name des Vorgesetzten, Abteilung**. Fügen Sie einen zusätzlichen Abschnitt in das Dokument ein, das über ein Formular für **Unterschrift des Vorgesetzten, genehmigtes Gehalt, Bestätigung des Angebots** und **Status des Angebots** verfügt.   
        Aktivieren Sie das Dokument für die Rechteverwaltung.  

    -   **Word Document1.docx**: Fügen Sie diesem Dokument einige Testinhalte hinzu.  

    -   **Word Document2.docx**: Fügen Sie dem Dokument Testinhalte hinzu.  

    -   **Workbook1. xlsx**  

    -   **Workbook2. xlsx**  

    -   Erstellen Sie auf dem Desktop einen Ordner mit dem Namen „Reguläre Ausdrücke“. Erstellen Sie ein Textdokument unter dem Ordner mit dem Namen **RegEx-SSN**. Geben Sie den folgenden Inhalt in die Datei ein, und speichern und schließen Sie anschließend die Datei:   
        ^(?!000)([0-7]\d{4}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$  

3.  Geben Sie den Ordner „D:\Finance Documents“ als „Finance Documents“ frei, und ermöglichen Sie, dass alle Benutzer über Lese-/Schreibzugriff auf die Freigabe verfügen.  

> [!NOTE]  
> Zentrale Zugriffsrichtlinien sind auf dem System oder Startvolume C: standardmäßig nicht aktiviert.  

#### <a name="BKMK_CS1"></a>Installieren von Active Directory Rights Management Services  
Fügen Sie die Active Directory-Rechteverwaltungsdienste (AD RMS) und alle erforderlichen Features über den Server-Manager hinzu. Wählen Sie alle Standardeinstellungen aus.  

###### <a name="to-install-active-directory-rights-management-services"></a>So installieren Sie Active Directory-Rechteverwaltungsdienste  

1. Melden Sie sich an FILE1 als „CONTOSO\Administrator“ oder als ein Mitglied der Gruppe „Domänen-Admins“ an.  

   > [!IMPORTANT]  
   > Damit die AD RMS-Serverrolle installiert werden kann, muss dem Installationskonto (in diesem Fall „CONTOSO\Administrator“) sowohl eine Mitgliedschaft auf die logische Administratorengruppe auf dem Servercomputer, auf dem AD RMS installiert wird, als auch eine Mitgliedschaft in der Gruppe „Organisations-Admins“ in Active Directory gewährt werden.  

2. Klicken Sie im Server-Manager auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features erscheint.  

3. Klicken Sie auf dem Bildschirm **Vorbemerkungen** auf **Weiter**.  

4. Klicken Sie auf dem Bildschirm **Installationstyp auswählen** auf **Rollen- und Feature-basierte Installation**, und klicken Sie anschließend auf **Weiter**.  

5. Klicken Sie auf dem Bildschirm **Serverziele auswählen** auf **Weiter**.  

6. Aktivieren Sie auf dem Bildschirm **Serverrollen auswählen** das Kontrollkästchen neben **Active Directory-Rechteverwaltungsdienste**, und klicken Sie dann auf **Weiter**.  

7. Klicken Sie im Dialogfeld **Für Active Directory-Rechteverwaltungsdienste erforderliche Features hinzufügen?** auf **Features hinzufügen**.  

8. Klicken Sie auf dem Bildschirm **Serverrollen auswählen** auf **Weiter**.  

9. Klicken Sie auf dem Bildschirm **Zu installierende Features auswählen** auf **Weiter**.  

10. Klicken Sie auf dem Bildschirm **Active Directory-Rechteverwaltungsdienste** auf „Weiter“.  

11. Klicken Sie auf der Seite **Rollendienste auswählen** auf **Weiter**.  

12. Klicken Sie auf der Seite **Webserverrolle (IIS)** auf **Weiter**.  

13. Klicken Sie auf der Seite **Rollendienste auswählen** auf **Weiter**.  

14. Klicken Sie auf dem Bildschirm **Installationsauswahl bestätigen** auf **Installieren**.  

15. Klicken Sie nach dem Abschluss der Installation auf der Seite **Installationsfortschritt** auf **Zusätzliche Einstellungen konfigurieren**. Der AD RMS-Konfigurations-Assistent wird angezeigt.  

16. Klicken Sie auf dem Bildschirm **AD RMS** auf **Weiter**.  

17. Wählen Sie **AD RMS-Stammcluster erstellen** auf dem Bildschirm **AD RMS-Cluster** aus, und klicken Sie dann auf **Weiter**.  

18. Klicken Sie auf dem Bildschirm **Konfigurationsdatenbank** auf **Interne Windows-Datenbank auf diesem Server verwenden**, und klicken Sie dann auf **Weiter**.  

    > [!NOTE]  
    > Die Verwendung der internen Windows-Datenbank empfiehlt sich nur für Testumgebungen, da sie maximal einen Server im AD RMS-Cluster unterstützt. Produktionsbereitstellungen sollten einen separaten Datenbankserver verwenden.  

19. Klicken Sie auf dem Bildschirm **Dienst Konto** unter **Domänen Benutzerkonto**auf **angeben** , geben Sie den Benutzernamen ( **"contoso\rms"** ) und das Kennwort (<strong>pass@word1</strong>) an, und klicken Sie auf **OK**und dann auf **weiter**.  

20. Klicken Sie auf dem Bildschirm **Kryptografiemodus** auf **Kryptografiemodus 2**.  

21. Klicken Sie auf dem Bildschirm **Clusterschlüsselspeicher** auf **Weiter**.  

22. Geben Sie auf dem Bildschirm **Cluster Schlüssel Kennwort** in den Feldern **Kennwort** und **Kennwort bestätigen** <strong>pass@word1</strong>ein, und klicken Sie dann auf **weiter**.  

23. Stellen Sie auf dem Bildschirm **Clusterwebsite** sicher, dass **Standardwebsite** ausgewählt ist, und klicken Sie dann auf **Weiter**.  

24. Wählen Sie auf dem Bildschirm **Clusteradresse** die Option **Unverschlüsselte Verbindung (http://) verwenden** aus. Geben Sie **FILE1.contoso.com** in das Feld **Vollqualifizierter Domänenname** ein, und klicken Sie dann auf **Weiter**.  

25. Akzeptieren Sie auf dem Bildschirm **Name des lizenzgebenden Zertifikats** den Standardnamen (**FILE1**) im Textfeld, und klicken Sie auf **Weiter**.  

26. Wählen Sie auf dem Bildschirm **Dienstverbindungspunkt registrieren** die Option **Dienstverbindungspunkt jetzt registrieren**auf, und klicken Sie dann auf **Weiter**.  

27. Klicken Sie auf dem Bildschirm **Bestätigung** auf **Installieren**.  

28. Klicken Sie auf dem Bildschirm **Ergebnisse** auf **Schließen**, und klicken Sie dann auf **Schließen** im Bildschirm **Installationsstatus**. Melden Sie sich ab, und melden Sie sich als "" contoso\rms "" mithilfe des angegebenen Kennworts an (<strong>pass@word1</strong>).  

29. Starten Sie die AD RMS-Konsole, und wechseln Sie zu **Vorlagen für Benutzerrechterichtlinien**.  

    Klicken Sie zum Öffnen der AD RMS-Konsole in Server-Manager in der Konsolenstruktur auf **Lokaler Server** . Klicken Sie anschließend auf **Extras**und dann auf **Active Directory-Rechteverwaltungsdienste**.  

30. Klicken Sie auf **Verteilte Vorlage für Benutzerrechterichtlinien erstellen** im rechten Bereich, klicken Sie auf **Hinzufügen**, und wählen Sie folgende Informationen aus.  

    -   Sprache: Englisch (USA)  

    -   Name: Contoso Finance Admin Only  

    -   Beschreibung: Contoso Finance Admin Only  

    Klicken Sie auf **Hinzufügen** und dann auf **Weiter**.  

31. Klicken Sie im Abschnitt Benutzer und Rechte auf **Benutzer und Rechte**, klicken Sie auf **Hinzufügen**, geben Sie <strong>financeadmin@contoso.com</strong>ein, und klicken Sie auf **OK**.  

32. Wählen Sie **Vollzugriff**aus, und lassen Sie **Besitzer (Autor) permanenten Vollzugriff gewähren** ausgewählt.  

33. Klicken Sie sich durch die verbleibenden Registerkarten ohne Änderungen, und klicken Sie dann auf **Beenden**. Melden Sie sich als %%amp;quot;CONTOSO\Administrator%%amp;quot; an.  

34. Navigieren Sie zum Ordner c:\Inetpub\wwwroot\\_wmcs \Certification, wählen Sie die Datei ServerCertification. asmx aus, und fügen Sie authentifizierte Benutzer hinzu, um Lese-und Schreibberechtigungen für die Datei zu erhalten.  

35. Öffnen Sie Windows PowerShell, und führen Sie `Get-FsrmRmsTemplate`aus. Stellen Sie sicher, dass Sie die von Ihnen in den vorherigen Schritten erstellte RMS-Vorlage in dieser Prozedur mit diesem Befehl anzeigen können.  

> [!IMPORTANT]  
> Wenn Sie möchten, dass Ihre Dateiserver unmittelbar geändert werden, sodass Sie sie testen können, müssen Sie Folgendes vornehmen:  
>   
> 1.  Öffnen Sie auf dem Dateiserver „FILE1“ eine Eingabeaufforderung mit erhöhten Rechten, und führen Sie die folgenden Befehle aus:  
>   
>     -   gpupdate /force.  
>     -   NLTEST /SC_RESET:contoso.com  
> 2.  Replizieren Sie auf dem Domänencontroller (DC1) Active Directory.  
>   
>     Weitere Informationen zu den Schritten für das Erzwingen der Replikation von Active Directory finden Sie unter [Active Directory Replication](https://technet.microsoft.com/library/cc794809(WS.10).aspx).  

Anstelle den Assistenten zum Hinzufügen von Rollen und Features im Server-Manager zu verwenden, können Sie alternativ die Windows PowerShell zum Installieren und Konfigurieren der AD RMS-Serverrolle analog zur Darstellung im folgenden Vorgang verwenden.  

###### <a name="to-install-and-configure-an-ad-rms-cluster-in-windows-server-2012-using-windows-powershell"></a>So installieren und konfigurieren Sie einen AD RMS-Cluster in Windows Server 2012 mithilfe der Windows PowerShell  

1. Melden Sie sich als "condeso\administrator" mit dem Kennwort an: <strong>pass@word1</strong>.  

   > [!IMPORTANT]  
   > Damit die AD RMS-Serverrolle installiert werden kann, muss dem Installationskonto (in diesem Fall „CONTOSO\Administrator“) sowohl eine Mitgliedschaft auf die logische Administratorengruppe auf dem Servercomputer, auf dem AD RMS installiert wird, als auch eine Mitgliedschaft in der Gruppe „Organisations-Admins“ in Active Directory gewährt werden.  

2. Klicken Sie auf dem Server-Desktop mit der rechten Maustaste auf das Windows PowerShell-Symbol auf der Taskleiste, und wählen Sie **Als Administrator ausführen** aus, um eine Windows PowerShell-Eingabeaufforderung mit Administratorrechten zu öffnen.  

3. Geben Sie zum Verwenden von Server-Manager-Cmdlets für das Installieren der AD RMS-Serverrolle Folgendes ein:  

   ```  
   Add-WindowsFeature ADRMS '"IncludeAllSubFeature '"IncludeManagementTools  
   ```  

4. Erstellen Sie den Windows PowerShell-Datenträger, um den AD RMS-Server, den Sie installieren, darzustellen.  

   Geben Sie beispielsweise zum Erstellen eines Windows PowerShell-Datenträgers mit dem Namen „RC“ zum Installieren und Konfigurieren des ersten Servers in einem AD RMS-Stammcluster Folgendes ein:  

   ```  
   Import-Module ADRMS  
   New-PSDrive -PSProvider ADRMSInstall -Name RC -Root RootCluster  
   ```  

5. Legen Sie Eigenschaften auf Objekte im Datenträgernamespace fest, die erforderliche Konfigurationseinstellungen widerspiegeln.  

   Geben Sie beispielsweise zum Festlegen des AD RMS-Dienstkontos an der Windows PowerShell-Eingabeaufforderung Folgendes ein:  

   ```  
   $svcacct = Get-Credential  
   ```  

   Wenn das Dialogfeld „Windows-Sicherheit“ angezeigt wird, geben Sie den AD RMS-Dienstkonto-Domänenbenutzernamen „CONTOSO\RMS“ sowie das zugehörige Kennwort ein.  

   Geben Sie als Nächstes Folgendes ein, um das AD RMS-Dienstkonto den AD RMS-Clustereinstellungen zuzuweisen:  

   ```  
   Set-ItemProperty -Path RC:\ -Name ServiceAccount -Value $svcacct  
   ```  

   Geben Sie anschließend an der Windows PowerShell-Eingabeaufforderung Folgendes ein, um den AD RMS-Server so einzustellen, dass er die interne Windows-Datenbank verwendet:  

   ```  
   Set-ItemProperty -Path RC:\ClusterDatabase -Name UseWindowsInternalDatabase -Value $true  
   ```  

   Geben Sie danach an der Windows PowerShell-Eingabeaufforderung Folgendes ein, um das Clusterschlüsselkennwort in einer Variablen sicher zu speichern:  

   ```  
   $password = Read-Host -AsSecureString -Prompt "Password:"  
   ```  

   Geben Sie das Clusterschlüsselkennwort ein, und drücken Sie dann die EINGABETASTE.  

   Geben Sie als Nächstes an der Windows PowerShell-Eingabeaufforderung Folgendes ein, um das Kennwort zu Ihrer AD RMS-Installation zuzuweisen:  

   ```  
   Set-ItemProperty -Path RC:\ClusterKey -Name CentrallyManagedPassword -Value $password  
   ```  

   Geben Sie anschließend zum Festlegen der AD RMS-Clusteradresse an der Windows PowerShell-Eingabeaufforderung Folgendes ein:  

   ```  
   Set-ItemProperty -Path RC:\ -Name ClusterURL -Value "http://file1.contoso.com:80"  
   ```  

   Geben Sie als Nächstes an der Windows PowerShell-Eingabeaufforderung Folgendes ein, um den SLC-Namen zu Ihrer AD RMS-Installation zuzuweisen:  

   ```  
   Set-ItemProperty -Path RC:\ -Name SLCName -Value "FILE1"  
   ```  

   Geben Sie dann an der Windows PowerShell-Eingabeaufforderung Folgendes ein, um den Dienstverbindungspunkt für den AD RMS-Cluster festzulegen:  

   ```  
   Set-ItemProperty -Path RC:\ -Name RegisterSCP -Value $true  
   ```  

6. Führen Sie das Cmdlet **Install-ADRMS** aus. Zusätzlich zum Installieren der AD RMS-Serverrolle und zur Konfiguration des Servers installiert dieses Cmdlet auch andere Features, die ggf. für AD RMS erforderlich sind.  

   Geben Sie Folgendes ein, um beispielsweise den Namen „RC“ des Windows PowerShell-Datenträgers zu ändern und um AD RMS zu installieren bzw. zu konfigurieren:  

   ```  
   Set-Location RC:\  
   Install-ADRMS -Path.  
   ```  

   Geben Sie „Y“ ein, wenn Sie vom Cmdlet aufgefordert werden, den Start der Installation zu bestätigen.  

7. Melden Sie sich als "CONTOSO\Administrator" ab, und melden Sie sich als "contoso\rms" mithilfe des angegebenen Kennworts ("pass@word1") an  

   > [!IMPORTANT]  
   > Damit der AD RMS-Server das Konto verwalten kann, auf dem Sie angemeldet sind und zum Verwalten des Servers (in diesem Fall „CONTOSO\RMS“) verwenden, muss ihm die Mitgliedschaft in der lokalen Administratorgruppe auf dem AD RMS-Servercomputer sowie die Mitgliedschaft in der Gruppe „Organisations-Admins“ in Active Directory gewährt werden.  

8. Klicken Sie auf dem Server-Desktop mit der rechten Maustaste auf das Windows PowerShell-Symbol auf der Taskleiste, und wählen Sie **Als Administrator ausführen** aus, um eine Windows PowerShell-Eingabeaufforderung mit Administratorrechten zu öffnen.  

9. Erstellen Sie den Windows PowerShell-Datenträger, um den AD RMS-Server, den Sie konfigurieren, darzustellen.  

    Geben Sie beispielsweise zum Erstellen eines Windows PowerShell-Datenträgers mit dem Namen „RC“ zum Konfigurieren des AD RMS-Stammclusters Folgendes ein:  

    ```  
    Import-Module ADRMSAdmin `  
    New-PSDrive -PSProvider ADRMSAdmin -Name RC -Root http://localhost -Force -Scope Global  
    ```  

10. Geben Sie an der Windows PowerShell-Eingabeaufforderung Folgendes ein, um eine neue Rechtevorlage für den Contoso-Administrator zu erstellen und ihr Benutzerrechte mit Vollzugriff in Ihrer AD RMS-Installation zuzuweisen:  

    ```  
    New-Item -Path RC:\RightsPolicyTemplate '"LocaleName en-us -DisplayName "Contoso Finance Admin Only" -Description "Contoso Finance Admin Only" -UserGroup financeadmin@contoso.com  -Right ('FullControl')  
    ```  

11. So stellen Sie sicher, dass Sie die neue Rechtevorlage für den Contoso-Finanzadministrator an der Windows PowerShell-Eingabeaufforderung anzeigen können:  

    ```  
    Get-FsrmRmsTemplate  
    ```  

    Prüfen Sie die Ausgabe dieses Cmdlets, um sicherzustellen, dass die von Ihnen im vorherigen Schritt erstellte RMS-Vorlage vorhanden ist.  

### <a name="build-the-mail-server-srv1"></a>Erstellen des E-Mail-Servers (SRV1)  
SRV1 ist der SMTP-/POP3-E-Mail-Server. Sie müssen ihn einrichten, sodass Sie E-Mail-Benachrichtigungen als Teil des Szenarios „Unterstützung nach 'Zugriff verweigert'“ senden können.  

Konfigurieren Sie Microsoft Exchange Server auf diesem Computer. Weitere Informationen finden Sie unter [How to Install Exchange Server](https://go.microsoft.com/fwlink/?prd=12364).  

### <a name="build-the-client-virtual-machine-client1"></a>Erstellen des virtuellen Clientcomputers (CLIENT1)  

##### <a name="to-build-the-client-virtual-machine"></a>So erstellen Sie den virtuellen Clientcomputer  

1. Verbinden Sie „CLIENT1“ mit „ID_AD_Network“.  

2. Installieren Sie Microsoft Office 2010.  

3. Melden Sie sich als „Contoso\Administrator“ an, und verwenden Sie die folgenden Informationen zum Konfigurieren von Microsoft Outlook.  

   - Ihr Name: Dateiadministrator  

   - E-Mail-Adresse: fileadmin@contoso.com  

   - Kontotyp: POP3  

   - Eingehender E-Mail-Server: Statische IP-Adresse von SRV1  

   - Ausgehender E-Mail-Server: Statische IP-Adresse von SRV1  

   - Benutzername: fileadmin@contoso.com  

   - Kennwort speichern: Wählen Sie  

4. Erstellen Sie eine Verknüpfung zu Outlook auf dem Desktop „contoso\administrator“.  

5. Öffnen Sie Outlook, und behandeln Sie alle "erst malig gestarteten" Nachrichten.  

6. Löschen Sie jede generierte Testnachricht.  

7. Erstellen Sie für alle Benutzer auf dem virtuellen Client Computer, die auf \\\file1\finance Documents verweist, einen neuen Kurzschluss auf dem Desktop.  

8. Nehmen Sie ggf. einen Neustart vor.  

##### <a name="enable-access-denied-assistance-on-the-client-virtual-machine"></a>Aktivieren Sie „Unterstützung nach 'Zugriff verweigert'“ auf dem virtuellen Clientcomputer.  

1.  Öffnen Sie den Registrierungs-Editor, und wechseln Sie zu **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Explorer**.  

    -   Legen Sie **EnableShellExecuteFileStreamCheck** auf **1** fest.  

    -   Wert: DWORD  

## <a name="BKMK_CF"></a>Lab-Einrichtung für das Gesamtstruktur übergreifende Bereitstellen von Ansprüchen  

### <a name="BKMK_2.1"></a>Erstellen eines virtuellen Computers für DC2  

-   Erstellen Sie einen virtuellen Computer aus der Windows Server 2012-ISO-Datei.  

-   Erstellen Sie den virtuellen Computer mit dem Namen „DC2“.  

-   Verbinden Sie den virtuellen Computer mit „ID_AD_Network“.  

> [!IMPORTANT]  
> Das Verknüpfen von virtuellen Computern mit einer Domäne und das gesamtstrukturübergreifende Bereitstellen von Anspruchstypen erfordert, dass die virtuellen Computer die vollqualifizierten Domänennamen der relevanten Domänen auflösen können. Sie müssen die DNS-Einstellungen auf den virtuellen Computern möglicherweise manuell konfigurieren, um dies umzusetzen. Weitere Informationen finden Sie unter [Configuring a virtual network](https://technet.microsoft.com/library/cc732470%28v=ws.10%29.aspx).  
>   
> Sämtliche virtuelle Computerimages (Server und Clients) müssen erneut konfiguriert werden, um eine statische IP-Version 4-Adresse (IPv4) und DNS-Clienteinstellungen (Domain Name System) zu verwenden. Weitere Informationen finden Sie unter [Configure a DNS Client for Static IP Address](https://go.microsoft.com/fwlink/?LinkId=150952).  

### <a name="BKMK_2.2"></a>Einrichten einer neuen Gesamtstruktur namens adatum.com  

##### <a name="to-install-active-directory-domain-services"></a>So installieren Sie Active Directory-Domänendienste  

1. Verbinden Sie den virtuellen Computer mit „ID_AD_Network“. Melden Sie sich mit dem Kennwort <strong>Pass@word1</strong>bei DC2 als Administrator an.  

2. Klicken Sie im Server-Manager auf **Verwalten**und dann auf **Rollen und Features hinzufügen**.  

3. Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  

4. Klicken Sie auf der Seite **Installationstyp auswählen** auf **Rollenbasierte oder featurebasierte Installation**, und klicken Sie anschließend auf **Weiter**.  

5. Klicken Sie auf der Seite **Zielserver auswählen** auf **Einen Server aus dem Serverpool auswählen**, klicken Sie auf die Namen des Servers, auf dem Sie Active Directory-Domänendienste (AD DS) installieren möchten, und klicken Sie dann auf **Weiter**.  

6. Klicken Sie auf der Seite **Serverrollen auswählen** auf **Active Directory-Domänendienste**. Klicken Sie im Dialogfeld **Assistent zum Hinzufügen von Rollen und Features** auf **Features hinzufügen**, und klicken Sie auf **Weiter**.  

7. Klicken Sie auf der Seite **Features auswählen** auf **Weiter**.  

8. Lesen Sie die Informationen auf der Seite **AD DS**, und klicken Sie dann auf **Weiter**.  

9. Klicken Sie auf der Seite **Bestätigung** auf **Installieren**. Die Statusanzeige „Featureinstallation“ auf der Seite „Ergebnisse“ zeigt an, dass die Rolle installiert wird.  

10. Stellen Sie auf der Seite **Ergebnisse** sicher, dass die Installation erfolgreich war. Klicken Sie anschließend auf das Warnsymbol mit einem Ausrufezeichen in der oberen rechten Ecke des Bildschirms neben **Verwalten**. Klicken Sie in der Liste „Aufgaben“ auf die Verknüpfung **Server zu einem Domänencontroller heraufstufen**.  

    > [!IMPORTANT]  
    > Wenn Sie den Installations-Assistenten zu diesem Zeitpunkt schließen und nicht auf **Server zu einem Domänencontroller heraufstufen** klicken, können Sie die AD DS-Installation fortsetzen, indem Sie auf **Aufgaben** im Server-Manager klicken.  

11. Klicken Sie auf der Seite **Bereitstellungskonfiguration** auf **Neue Gesamtstruktur hinzufügen**, geben Sie den Namen der Stammdomäne **adatum.com** ein, und klicken Sie dann auf **Weiter**.  

12. Wählen Sie auf der Seite **Domänen Controller Optionen** die Domänen-und Gesamtstruktur Funktionsebenen als Windows Server 2012 aus, geben Sie das DSRM-Kennwort an <strong>pass@word1</strong>und klicken Sie dann auf **weiter**.  

13. Klicken Sie auf der Seite **DNS-Optionen** auf **Weiter**.  

14. Klicken Sie auf der Seite **Zusätzliche Optionen** auf **Weiter**.  

15. Geben Sie auf der Seite **Pfade** die Speicherorte für die Active Directory-Datenbanken, -Protokolldateien und den Ordner „SYSVOL“ an (oder übernehmen Sie die Standardspeicherorte), und klicken Sie dann auf **Weiter**.  

16. Bestätigen Sie auf der Seite **Optionen prüfen** die Einstellungen, und klicken Sie dann auf **Weiter**.  

17. Bestätigen Sie auf der Seite **Voraussetzungsüberprüfung**, dass die Validierung der Voraussetzungen abgeschlossen ist, und klicken Sie dann auf **Installieren**.  

18. Stellen Sie auf der Seite **Ergebnisse** sicher, dass der Server erfolgreich als Domänencontroller konfiguriert wurde, und klicken Sie dann auf **Schließen**.  

19. Starten Sie den Server zum Abschließen der AD DS-Installation neu. (Dies erfolgt standardmäßig automatisch.)  

> [!IMPORTANT]  
> Führen Sie Folgendes aus, um sicherzustellen, dass das Netzwerk nach der Einrichtung beider Gesamtstrukturen ordnungsgemäß konfiguriert ist:  
>   
> -   Melden Sie sich bei „adatum.com“ als „adatum\administrator“ an. Öffnen Sie ein Eingabeaufforderungsfenster, geben Sie **nslookup contoso.com** ein, und drücken Sie dann die EINGABETASTE.  
> -   Melden Sie sich bei „contoso.com“ als „contoso\administrator“ an. Öffnen Sie ein Eingabeaufforderungsfenster, geben Sie **nslookup adatum.com**ein, und drücken Sie dann die EINGABETASTE.  
>   
> Wenn diese Befehle fehlerfrei ausgeführt werden, können die Gesamtstrukturen miteinander kommunizieren. Weitere Informationen über nslookup-Fehler finden Sie im Problembehandlungsabschnitt im Thema [Using NSlookup.exe](https://support.microsoft.com/kb/200525).  

### <a name="BKMK_2.22"></a>Legen Sie contoso.com als vertrauende Gesamtstruktur auf adatum.com fest.  
In diesem Schritt erstellen Sie eine Vertrauensstellung zwischen der Adatum Corporation- und der Contoso, Ltd.-Website.  

##### <a name="to-set-contoso-as-a-trusting-forest-to-adatum"></a>So legen Sie Contoso als eine vertrauenswürdige Gesamtstruktur auf Adatum fest  

1.  Melden Sie sich bei „DC2“ als Administrator an. Geben Sie **domain.msc** auf dem Startbildschirm ein.  

2.  Klicken Sie in der Konsolenstruktur mit der rechten Maustaste auf „adatum.com“, und klicken Sie anschließend auf „Eigenschaften“.  

3.  Klicken Sie auf die Registerkarte **Vertrauensstellungen**, klicken Sie auf **Neue Vertrauensstellung**, und klicken Sie dann auf **Weiter**.  

4.  Geben Sie auf der Seite **Vertrauensstellungsname** **contoso.com**in das Namensfeld „DNS-Server (Domain Name System)“ ein, und klicken Sie dann auf **Weiter**.  

5.  Klicken Sie auf der Seite **Vertrauenstyp** auf **Gesamtstruktur-Vertrauensstellung**, und klicken Sie dann auf **Weiter**.  

6.  Klicken Sie auf der Seite **Richtung der Vertrauensstellung** auf **Bidirektional**.  

7.  Klicken Sie auf der Seite **Vertrauensstellungsseiten** auf **Diese und die angegebene Domäne**, und klicken Sie dann auf **Weiter**.  

8.  Folgen Sie den weiteren Anweisungen des Assistenten.  

### <a name="BKMK_2.4"></a>Erstellen zusätzlicher Benutzer in der Adatum-Gesamtstruktur  
Erstellen Sie den Benutzer Jeff Low mit dem Kennwort <strong>pass@word1</strong>, und weisen Sie das Company-Attribut mit dem Wert **adatum**zu.  

##### <a name="to-create-a-user-with-the-company-attribute"></a>So erstellen Sie einen Benutzer mit dem „Company“-Attribut  

1.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten in Windows PowerShell, und fügen Sie den folgenden Code ein:  

    ```  
    New-ADUser `  
    -SamAccountName jlow `  
    -Name "Jeff Low" `  
    -UserPrincipalName jlow@adatum.com `  
    -AccountPassword (ConvertTo-SecureString `  
    -AsPlainText "pass@word1" -Force) `  
    -Enabled $true `  
    -PasswordNeverExpires $true `  
    -Path 'CN=Users,DC=adatum,DC=com' `  
    -Company Adatum`  

    ```  

### <a name="BKMK_2.5"></a>Erstellen des Anspruchs Typs Company auf adataum.com  

##### <a name="to-create-a-claim-type-by-using-windows-powershell"></a>So erstellen Sie einen Anspruchstyp mithilfe der Windows PowerShell  

1.  Melden Sie sich bei „adatum.com“ als ein Administrator an.  

2.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten in Windows PowerShell, und geben Sie den folgenden Code ein:  

    ```  
    New-ADClaimType `  
    -AppliesToClasses:@('user') `  
    -Description:"Company" `  
    -DisplayName:"Company" `  
    -ID:"ad://ext/Company:ContosoAdatum" `  
    -IsSingleValued:$true `  
    -Server:"adatum.com" `  
    -SourceAttribute:Company `  
    -SuggestedValues:@((New-Object Microsoft.ActiveDirectory.Management.ADSuggestedValueEntry("Contoso", "Contoso", "")), (New-Object Microsoft.ActiveDirectory.Management.ADSuggestedValueEntry("Adatum", "Adatum", ""))) `  

    ```  

### <a name="BKMK_2.55"></a>Aktivieren der Eigenschaft "Unternehmensressourcen" auf contoso.com  

##### <a name="to-enable-the-company-resource-property-on-contosocom"></a>So aktivieren Sie die Ressourceneigenschaft „Company“ auf „contoso.com“  

1.  Melden Sie sich bei „contoso.com“ als ein Administrator an.  

2.  Klicken Sie in Server-Manager auf **Extras** und dann auf **Active Directory-Verwaltungscenter**.  

3.  Klicken Sie im linken Bereich des Active Directory-Verwaltungscenters auf **Strukturansicht**. Klicken Sie im linken Bereich auf **Dynamische Zugriffssteuerung**, und doppelklicken Sie dann auf **Ressourceneigenschaften**.  

4.  Wählen Sie **Unternehmen** aus der Liste **Ressourceneigenschaften** aus, und klicken Sie mit der rechten Maustaste auf **Eigenschaften**, und wählen Sie die Option aus. Klicken Sie im Abschnitt **Vorgeschlagene Werte** auf **Hinzufügen** , um die vorgeschlagenen Werte „Contoso“ und „Adatum“ hinzuzufügen, und klicken Sie dann zweifach auf **OK** .  

5.  Wählen Sie **Unternehmen** aus der Liste **Ressourceneigenschaften** aus, und klicken Sie mit der rechten Maustaste auf **Aktivieren**, und wählen Sie die Option aus.  

### <a name="BKMK_2.6"></a>Dynamische Access Control auf adatum.com aktivieren  

##### <a name="to-enable-dynamic-access-control-for-adatumcom"></a>So aktivieren Sie die dynamische Zugriffssteuerung für „adatum.com“  

1.  Melden Sie sich bei „adatum.com“ als ein Administrator an.  

2.  Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole, klicken Sie auf **adatum.com**, und doppelklicken Sie anschließend auf **Domänencontroller**.  

3.  Klicken Sie mit der rechten Maustaste auf **Standarddomänencontroller-Richtlinie**, und wählen Sie **Bearbeiten**aus.  

4.  Doppelklicken Sie im Fenster „Gruppenrichtlinienverwaltungs-Editor“ auf **Computerkonfiguration**, doppelklicken Sie auf **Richtlinien**, doppelklicken Sie auf **Administrative Vorlagen**, doppelklicken Sie auf **System**, und doppelklicken Sie dann auf **KDC**.  

5.  Doppelklicken Sie auf die Option **KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos Armoring** , und wählen Sie die Option neben **Aktiviert**aus. Sie müssen diese Einstellung aktivieren, um „Zentrale Zugriffsrichtlinien“ verwenden zu können.  

6.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und führen Sie den folgenden Befehl aus:  

    ```  
    gpupdate /force  
    ```  

### <a name="BKMK_2.8"></a>Erstellen des Anspruchs Typs Company auf contoso.com  

##### <a name="to-create-a-claim-type-by-using-windows-powershell"></a>So erstellen Sie einen Anspruchstyp mithilfe der Windows PowerShell  

1.  Melden Sie sich bei „contoso.com“ als ein Administrator an.  

2.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten in Windows PowerShell, und geben Sie dann den folgenden Code ein:  

    ```  
    New-ADClaimType '"SourceTransformPolicy `  
    '"DisplayName 'Company' `  
    '"ID 'ad://ext/Company:ContosoAdatum' `  
    '"IsSingleValued $true `  
    '"ValueType 'string' `  

    ```  

### <a name="BKMK_2.9"></a>Erstellen der zentralen Zugriffs Regel  

##### <a name="to-create-a-central-access-rule"></a>So erstellen Sie eine zentrale Zugriffsregel  

1. Klicken Sie im linken Bereich des Active Directory-Verwaltungscenters auf **Strukturansicht**. Klicken Sie im linken Bereich auf **Dynamische Zugriffssteuerung**, und klicken Sie dann auf **Zentrale Zugriffsregeln**.  

2. Klicken Sie mit der rechten Maustaste auf **Zentrale Zugriffsregeln**, klicken Sie auf **Neu**und dann auf **Zentrale Zugriffsregel**.  

3. Geben Sie in das Feld **Name** **AdatumEmployeeAccessRule** ein.  

4. Wählen Sie im Abschnitt **Berechtigungen** die Option **Folgende Berechtigungen als aktuelle Berechtigungen verwenden** aus, klicken Sie auf **Bearbeiten** und dann auf **Hinzufügen**. Klicken Sie auf die Verknüpfung **Prinzipal auswählen** geben Sie **Authentifizierte Benutzer**ein, und klicken Sie dann auf **OK**.  

5. Klicken Sie im Dialogfeld **Berechtigungseintrag für Berechtigungen** auf **Bedingung hinzufügen**, und geben Sie die folgenden Bedingungen ein: [**User**] [**Company**] [**Equals**] [**Value**] [**Adatum**]. Die Berechtigungen sollten **ändern, lesen und ausführen, lesen und schreiben** lauten.  

6. Klicken Sie auf **OK**.  

7. Klicken Sie dreimal auf **OK** zum Abschließen des Vorgangs, und kehren Sie zum Active Directory-Verwaltungscenter zurück.  

   ![projektmappenanleitung für](media/Appendix-B--Setting-Up-the-Test-Environment/PowerShellLogoSmall.gif)***<em>entsprechende Windows PowerShell-Befehle</em>***  

   Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  

   ```  
   New-ADCentralAccessRule `  
   -CurrentAcl:"O:SYG:SYD:AR(A;;FA;;;OW)(A;;FA;;;BA)(A;;FA;;;SY)(XA;;0x1301bf;;;AU;(@USER.ad://ext/Company:ContosoAdatum == `"Adatum`"))" `  
   -Name:"AdatumEmployeeAccessRule" `  
   -ProposedAcl:$null `  
   -ProtectedFromAccidentalDeletion:$true `  
   -Server:"contoso.com" `  
   ```  

### <a name="BKMK_2.10"></a>Erstellen der zentralen Zugriffs Richtlinie  

##### <a name="to-create-a-central-access-policy"></a>So erstellen Sie eine zentrale Zugriffsrichtlinie  

1.  Melden Sie sich bei „contoso.com“ als ein Administrator an.  

2.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten in der Windows PowerShell, und fügen Sie dann den folgenden Code ein:  

    ```  
    New-ADCentralAccessPolicy "Adatum Only Access Policy"   
    Add-ADCentralAccessPolicyMember "Adatum Only Access Policy" `  
    -Member "AdatumEmployeeAccessRule" `  
    ```  

### <a name="BKMK_2.11"></a>Veröffentlichen der neuen Richtlinie über Gruppenrichtlinie  

##### <a name="to-apply-the-central-access-policy-across-file-servers-through-group-policy"></a>So wenden Sie die zentrale Zugriffsrichtlinie dateiserverübergreifend durch die Gruppenrichtlinie an  

1.  Geben Sie auf dem Startbildschirm**Verwaltung**ein, und klicken Sie auf der Suchleiste auf **Einstellungen**. Klicken Sie in den Ergebnissen für **Einstellungen** auf **Verwaltung**. Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole im Ordner **Verwaltung** .  

    > [!TIP]  
    > Wenn die Einstellung **Verwaltungstools anzeigen** deaktiviert ist, werden der Ordner „Verwaltung“ und sein Inhalt nicht in den Ergebnissen für **Einstellungen** angezeigt.  

2.  Klicken Sie mit der rechten Maustaste auf die Domäne contoso.com, klicken Sie auf Gruppenrichtlinien Objekt **in dieser Domäne erstellen, und verknüpfen Sie es** .  

3.  Geben Sie einen beschreibenden Namen für das Gruppenrichtlinienobjekt wie **AdatumAccessGPO** ein, und klicken Sie dann auf **OK**.  

##### <a name="to-apply-the-central-access-policy-to-the-file-server-through-group-policy"></a>So wenden Sie die zentrale Zugriffsrichtlinie auf den Dateiserver durch die Gruppenrichtlinie an  

1.  Geben Sie **Gruppenrichtlinienverwaltung** auf dem Startbildschirm im Feld **Suche** ein. Öffnen Sie **Gruppenrichtlinienverwaltung** im Ordner „Verwaltung“.  

    > [!TIP]  
    > Wenn die Einstellung **Verwaltungstools anzeigen** deaktiviert ist, werden der Ordner „Verwaltung“ und sein Inhalt nicht in den Ergebnissen für „Einstellungen“ angezeigt.  

2.  Navigieren Sie zu und wählen Sie Contoso wie folgt aus: „Group Policy Management\Forest: contoso.com\Domains\contoso.com“.  

3.  Klicken Sie mit der rechten Maustaste auf die Richtlinie **AdatumAccessGPO** , und wählen Sie **Bearbeiten**aus.  

4.  Klicken Sie im Gruppenrichtlinienverwaltungs-Editor auf **Computerkonfiguration**, erweitern Sie **Richtlinien**, erweitern Sie **Windows-Einstellungen**, und klicken Sie dann auf **Sicherheitseinstellungen**.  

5.  Erweitern Sie **Dateisystem**, klicken Sie mit der rechten Maustaste auf **Zentrale Zugriffsrichtlinie**, und klicken Sie dann auf **Zentrale Zugriffsrichtlinien verwalten**.  

6.  Klicken Sie im Dialogfeld **Konfiguration der zentralen Zugriffsrichtlinien** auf **Hinzufügen**, wählen Sie **Adatum Only Access Policy**aus, und klicken Sie dann auf **OK**.  

7.  Schließen Sie den Gruppenrichtlinienverwaltungs-Editor. Sie haben nun der Gruppenrichtlinie die zentrale Zugriffsrichtlinie hinzugefügt.  

### <a name="BKMK_2.12"></a>Erstellen des Ordners "Ergebnis" auf dem Dateiserver  
Erstellen Sie ein neues NTFS-Volume auf „FILE1“, und erstellen Sie den folgenden Ordner: D:\Ergebnis.  

> [!NOTE]  
> Zentrale Zugriffsrichtlinien sind auf dem System oder Startvolume C: standardmäßig nicht aktiviert.  

### <a name="BKMK_2.13"></a>Festlegen der Klassifizierung und Anwenden der zentralen Zugriffs Richtlinie auf den Ordner "Ergebnis"  

##### <a name="to-assign-the-central-access-policy-on-the-file-server"></a>So weisen Sie die zentrale Zugriffsrichtlinie auf dem Dateiserver zu  

1. Stellen Sie im Hyper-V-Manager eine Verbindung mit dem Server „FILE1“ her. Melden Sie sich mit dem Kennwort <strong>pass@word1</strong>bei dem Server an.  

2. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und geben Sie Folgendes ein: **gpupdate /force**. Dadurch wird sichergestellt, dass Ihre Gruppenrichtlinienänderungen auf Ihrem Server wirksam werden.  

3. Sie müssen auch die globalen Ressourceneigenschaften in Active Directory aktualisieren. Öffnen Sie Windows PowerShell, geben Sie `Update-FSRMClassificationpropertyDefinition`ein, und drücken Sie dann die EINGABETASTE. Schließen Sie Windows PowerShell.  

4. Öffnen Sie den Windows-Explorer, und wechseln Sie zu „D:\ERGEBNIS“. Klicken Sie mit der rechten Maustaste auf den Ordner **Ergebnis** , und klicken Sie auf **Eigenschaften**.  

5. Klicken Sie auf die Registerkarte **Klassifizierung** . Wählen Sie **Unternehmen**aus, und wählen Sie dann **adatum** im Feld **Wert** aus.  

6. Klicken Sie auf **Ändern**, wählen Sie **Adatum Only Access Policy** aus dem Dropdownmenü aus, und klicken Sie dann auf **Übernehmen**.  

7. Klicken Sie auf die Registerkarte **Sicherheit** , klicken Sie auf **erweitert**und dann auf die Registerkarte **zentrale Richtlinie** . Die **adatumemployeeaccessrule** sollte aufgeführt sein. Sie können das Element erweitern, um alle von Ihnen beim Erstellen der Regel in Active Directory festgelegten Berechtigungen anzuzeigen.  

8. Klicken Sie auf **OK**, um zum Windows-Explorer zurückzukehren.  



