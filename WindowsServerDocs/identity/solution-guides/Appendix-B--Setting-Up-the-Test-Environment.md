---
ms.assetid: 82918181-525d-4e93-af96-957dac6aedb6
title: Anhang B zum Einrichten der Testumgebung
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: deb08b0663e5f349df7cce51ddabd4aae7f624c5
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="appendix-b-setting-up-the-test-environment"></a>Anhang B: Einrichten der Testumgebung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema werden die Schritte zum Erstellen eines praktischen Labors zum Testen der dynamischen Zugriffssteuerung. Die Anweisungen dienen zum schrittweise befolgt werden, da es gibt viele Komponenten, die über Abhängigkeiten verfügen.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
**Hardware- und softwareanforderungen**  
  
Anforderungen für das Einrichten der testumgebung:  
  
-   Ein Hostserver unter Windows Server 2008 R2 mit SP1 und Hyper-V  
  
-   Eine Kopie der ISO-Datei von Windows Server 2012  
  
-   Eine Kopie der Windows 8-ISO  
  
-   Microsoft Office 2010  
  
-   Ein Server mit Microsoft Exchange Server 2003 oder höher  
  
Sie müssen die folgenden virtuellen Computer zum Testen der dynamischen Zugriffssteuerung Szenarien erstellen:  
  
-   DC1 (Domänencontroller)  
  
-   DC2 (Domänencontroller)  
  
-   File1 (Dateiserver und Active Directory Rights Management Services)  
  
-   SRV1 (POP3- und SMTP-Server)  
  
-   CLIENT1 (Clientcomputer mit Microsoft Outlook)  
  
Die Kennwörter für die virtuellen Computer sollte wie folgt lauten:  
  
-   BUILTIN\Administrator:pass@word1  
  
-   "Contoso\Administrator" an:pass@word1  
  
-   Alle anderen Konten:pass@word1  
  
## <a name="build-the-test-lab-virtual-machines"></a>Erstellen Sie den Test Lab virtuelle Maschinen  
  
### <a name="install-the-hyper-v-role"></a>Installieren der Hyper-V-Rolle  
Sie müssen die Hyper-V-Rolle auf einem Computer unter Windows Server 2008 R2 mit SP1 zu installieren.  
  
##### <a name="to-install-the-hyper-v-role"></a>So installieren Sie die Hyper-V-Rolle  
  
1.  Klicken Sie auf **starten**, und klicken Sie dann auf Server-Manager.  
  
2.  Klicken Sie im Bereich Rollenübersicht des Server-Manager-Hauptfensters auf **Hinzufügen von Rollen**.  
  
3.  Auf der **Serverrollen auswählen** auf **Hyper-V**.  
  
4.  Auf der **virtuelle Netzwerke erstellen** Seite, klicken Sie auf eine oder mehrere Netzwerkadapter, wenn Sie ihre Netzwerkverbindung für virtuelle Maschinen verfügbar machen möchten.  
  
5.  Auf der **Installationsauswahl bestätigen** auf **installieren**.  
  
6.  Der Computer muss neu gestartet werden, um die Installation abzuschließen. Klicken Sie auf **schließen** beenden Sie den Assistenten, und klicken Sie dann auf **Ja** den Computer neu starten.  
  
7.  Nachdem Sie den Computer neu starten, melden Sie sich mit demselben Konto an, das Sie zum Installieren der Rolle verwendet. Nachdem der Assistent zum Fortsetzen der Konfiguration die Installation abgeschlossen ist, klicken Sie auf **schließen** um den Assistenten zu beenden.  
  
### <a name="create-an-internal-virtual-network"></a>Erstellen Sie ein internes virtuelles Netzwerk  
Nun erstellen Sie ein internes virtuelles Netzwerk ID_AD_Network aufgerufen.  
  
##### <a name="to-create-a-virtual-network"></a>Zum Erstellen eines virtuellen Netzwerks  
  
1.  Hyper-V-Manager zu öffnen.  
  
2.  Von der **Aktionen** Menü klicken Sie auf **Manager für virtuelle Netzwerke**.  
  
3.  Klicken Sie unter **virtuelles Netzwerk erstellen**, wählen die **intern**.  
  
4.  Klicken Sie auf **hinzufügen**. Die **neues virtuelles Netzwerk** Seite wird angezeigt.  
  
5.  Typ **ID_AD_Network** als Namen für das neue Netzwerk. Überprüfen Sie die anderen Eigenschaften, und ggf. zu ändern.  
  
6.  Klicken Sie auf **OK** das virtuelle Netzwerk zu erstellen und Manager für virtuelle Netzwerke zu schließen, oder klicken Sie auf **übernehmen** das virtuelle Netzwerk zu erstellen und weiterhin mit dem virtuellen Netzwerk-Manager.  
  
### <a name="BKMK_Build"></a>Erstellen des Domänencontrollers  
Erstellen Sie einen virtuellen Computer als dem Domänencontroller (DC1) verwendet werden soll. Installieren Sie den virtuellen Computer mit Windows Server 2012 ISO-Datei, und nennen Sie ihn "DC1".  
  
##### <a name="to-install-active-directory-domain-services"></a>So installieren Sie Active Directory-Domänendienste  
  
1.  Schließen Sie die virtuelle Maschine mit "id_ad_network". Melden Sie sich bei DC1 als Administrator mit dem Kennwort ** pass@word1 **.  
  
2.  Klicken Sie im Server-Manager auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**.  
  
3.  Auf der **vor dem Beginn** auf **Weiter**.  
  
4.  Auf der **Installationstyp auswählen** auf **rollenbasierte oder featurebasierte Installation**, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Zielserver auswählen** auf **Weiter**.  
  
6.  Auf der **Serverrollen auswählen** auf **Active Directory Domain Services**. In der **Hinzufügen von Rollen und Features Assistenten** Dialogfeld, klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.  
  
7.  Auf der **Features auswählen** auf **Weiter**.  
  
8.  Auf der **Active Directory Domain Services** Seite, überprüfen Sie die Informationen, und klicken Sie dann auf **Weiter**.  
  
9. Auf der **Installationsauswahl bestätigen** auf **installieren**. Die Statusanzeige des Feature-Installation auf der Seite mit den weist darauf hin, dass die Rolle installiert wird.  
  
10. Auf der **Ergebnisse** sicher, dass die Installation erfolgreich war, und klicken Sie auf **schließen**. Im Server-Manager, klicken Sie auf das Warnsymbol mit einem Ausrufezeichen in der oberen rechten Ecke des Bildschirms neben **verwalten**. Klicken Sie in der Liste "Aufgaben" auf die **Server zu einem Domänencontroller heraufstufen** Link.  
  
11. Auf der **Bereitstellungskonfiguration** auf **Hinzufügen einer neuen Gesamtstruktur**, geben Sie den Namen der Stammdomäne, **"contoso.com"**, und klicken Sie dann auf **Weiter**.  
  
12. Auf der **Domänencontrolleroptionen** Seite die Domänen- und Gesamtstruktur-Funktionsebenen wie Windows Server 2012 aus, geben Sie das DSRM-Kennwort ** pass@word1 **, und klicken Sie dann auf **Weiter**.  
  
13. Auf der **DNS-Optionen** auf **Weiter**.  
  
14. Auf der **zusätzliche Optionen** auf **Weiter**.  
  
15. Auf der **Pfade** Seite, geben Sie die Speicherorte für die Active Directory-Datenbank, Protokolldateien und SYSVOL-Ordner (oder übernehmen Sie die Standardspeicherorte), und klicken Sie dann auf **Weiter**.  
  
16. Auf der **Optionen prüfen** Seite, bestätigen Sie Ihre Auswahl, und klicken Sie dann auf **Weiter**.  
  
17. Auf der **Voraussetzungsüberprüfung** Seite, stellen Sie sicher, dass die Validierung der Voraussetzungen abgeschlossen ist, und klicken Sie dann auf **installieren**.  
  
18. Auf der **Ergebnisse** Seite, stellen Sie sicher, dass der Server erfolgreich als Domänencontroller konfiguriert wurde, und klicken Sie dann auf **schließen**.  
  
19. Starten Sie den Server zum Abschließen der AD DS-Installation. (Standardmäßig geschieht dies automatisch.)  
  
Erstellen Sie die folgenden Benutzer mithilfe von Active Directory-Verwaltungscenter.  
  
##### <a name="create-users-and-groups-on-dc1"></a>Erstellen von Benutzern und Gruppen auf DC1  
  
1.  Melden Sie sich bei "contoso.com" als Administrator. Starten Sie Active Directory-Verwaltungscenter.  
  
2.  Erstellen Sie die folgenden Sicherheitsgruppen:  
  
    |Gruppenname|E-Mail-Adresse|  
    |--------------|-----------------|  
    |FinanceAdmin|financeadmin@contoso.com|  
    |"Financeexception"|financeexception@contoso.com|  
  
3.  Erstellen Sie die folgende Organisationseinheit (OU):  
  
    |Name der Organisationseinheit|Computer|  
    |-----------|-------------|  
    |FileServerOU|"FILE1"|  
  
4.  Erstellen Sie die folgenden Benutzer mit den angegebenen Attributen:  
  
    |Benutzer|Benutzername|E-Mail-Adresse|Abteilung|Gruppe|Land/Region|  
    |--------|------------|-----------------|--------------|---------|-------------------|  
    |Myriam Delesalle|MDelesalle|MDelesalle@contoso.com|Finanzen||UNS|  
    |Miles Reid|MReid|MReid@contoso.com|Finanzen|FinanceAdmin|UNS|  
    |Esther Valle|EValle|EValle@contoso.com|Vorgänge|"Financeexception"|UNS|  
    |Maira Wenzel|MWenzel|MWenzel@contoso.com|HR||UNS|  
    |Jeff Low|JLow|JLow@contoso.com|HR||UNS|  
    |RMS-Server|RMS|rms@contoso.com||||  
  
    Weitere Informationen zum Erstellen von Sicherheitsgruppen finden Sie unter [Erstellen einer neuen Gruppe](https://technet.microsoft.com/library/dd861305.aspx) auf der Windows Server-Website.  
  
##### <a name="to-create-a-group-policy-object"></a>Um ein Gruppenrichtlinienobjekt zu erstellen.  
  
1.  Bewegen Sie den Cursor auf der oberen rechten Ecke des Bildschirms, und klicken Sie auf das Symbol "Suchen". Geben Sie in das Suchfeld **gruppenrichtlinienverwaltung**, und klicken Sie auf **Gruppenrichtlinienverwaltung**.  
  
2.  Erweitern Sie **Gesamtstruktur: contoso.com**, und erweitern Sie dann **Domänen**, navigieren Sie zu **"contoso.com"**, erweitern Sie **(contoso.com)**, und wählen Sie dann **FileServerOU**. Mit der rechten Maustaste **ein Gruppenrichtlinienobjekt in dieser Domäne erstellen und verknüpfen Sie es hier**
  
3.  Geben Sie einen beschreibenden Namen für das Gruppenrichtlinienobjekt, z. B. **FlexibleAccessGPO**, und klicken Sie dann auf **OK**.  
  
##### <a name="to-enable-dynamic-access-control-for-contosocom"></a>So aktivieren Sie die dynamische Zugriffssteuerung für "contoso.com"  
  
1.  Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole, klicken Sie auf **"contoso.com"**, und doppelklicken Sie dann auf **Domänencontroller**.  
  
2.  Mit der rechten Maustaste **Standarddomänencontroller-Richtlinie**, und wählen Sie **bearbeiten**.  
  
3.  Doppelklicken Sie in der Gruppenrichtlinienverwaltungs-Editor-Fenster auf **Computerkonfiguration**, doppelklicken Sie auf **Richtlinien**, doppelklicken Sie auf **Administrative Vorlagen**, doppelklicken Sie auf **System**, und doppelklicken Sie dann auf **KDC**.  
  
4.  Doppelklicken Sie auf **KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos armoring** und wählen Sie die Option neben **aktiviert**. Sie müssen diese Einstellung, um die Verwendung zentraler Zugriffsrichtlinien zu aktivieren.  
  
5.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, und führen Sie den folgenden Befehl:  
  
    ```  
    gpupdate /force  
    ```  
  
### <a name="BKMK_FS1"></a>Erstellen des Dateiservers und AD RMS-Servers (FILE1)  
  
1.  Erstellen einer virtuellen Maschine mit dem Namen "file1" aus der Windows Server 2012-ISO-Datei.  
  
2.  Schließen Sie die virtuelle Maschine mit "id_ad_network".  
  
3.  Fügen Sie den virtuellen Computer der Domäne "contoso.com", und melden Sie sich bei FILE1 als Contoso\administrator mit dem Kennwort ** pass@word1 **.  
  
#### <a name="install-file-services-resource-manager"></a>File Services Resource Manager installieren  
  
###### <a name="to-install-the-file-services-role-and-the-file-server-resource-manager"></a>So installieren Sie die Rolle "Dateidienste" und die File Server Resource Manager  
  
1.  Klicken Sie im Server-Manager auf **Hinzufügen von Rollen und Features**.  
  
2.  Auf der **vor dem Beginn** auf **Weiter**.  
  
3.  Auf der **Installationstyp auswählen** auf **Weiter**.  
  
4.  Auf der **Zielserver auswählen** auf **Weiter**.  
  
5.  Auf der **Serverrollen auswählen** Bereich **Datei- und Speicherdienste**, aktivieren Sie das Kontrollkästchen neben **Datei- und iSCSI-Dienste**, erweitern, und wählen Sie **File Server Resource Manager**.  
  
    Hinzufügen von Rollen und Features-Assistenten, klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **Features auswählen** auf **Weiter**.  
  
7.  Auf der **Installationsauswahl bestätigen** auf **installieren**.  
  
8.  Auf der **Installationsstatus** auf **schließen**.  
  
#### <a name="install-the-microsoft-office-filter-packs-on-the-file-server"></a>Installieren Sie die Microsoft Office Filter Packs auf dem Dateiserver  
Sie sollten die Microsoft Office Filter Packs auf Windows Server 2012, um IFilters für ein größeres Array an Office-Dateien als das standardmäßig bereitgestellte ermöglichen installieren.  Windows Server 2012 hat keine IFilter für Microsoft Office-Dateien, die standardmäßig installiert, und die dateiklassifizierungsinfrastruktur IFilter zum Ausführen der Inhaltsanalyse verwendet.  
  
Zum Herunterladen und Installieren der IFilter finden Sie unter [Microsoft Office 2010 Filter Packs](https://go.microsoft.com/fwlink/?LinkID=234122).  
  
#### <a name="configure-email-notifications-on-file1"></a>Konfigurieren Sie e-Mail-Benachrichtigungen auf FILE1  
Bei der Erstellung von Kontingenten und haben Sie die Möglichkeit, e-Mail-Benachrichtigungen an Benutzer senden, wenn ihre kontingentbegrenzung oder nachdem sie versucht haben, zum Speichern von Dateien, die blockiert wurden. Wenn Sie regelmäßig bestimmte Administratoren Kontingent-und Dateiprüfungsereignisse benachrichtigen möchten, können Sie einen oder mehrere standardmäßige Empfänger konfigurieren. Um diese Benachrichtigungen zu senden, müssen Sie den SMTP-Server verwendet werden, für die Weiterleitung von e-Mail-Nachrichten angeben.  
  
###### <a name="to-configure-email-options-in-file-server-resource-manager"></a>So konfigurieren Sie e-Mail-Optionen in File Server Resource Manager  
  
1.  File Server Resource Manager zu öffnen. File Server Resource Manager zu öffnen, klicken Sie auf **starten**, Typ **Ressourcen-Manager für Dateiserver**, und klicken Sie dann auf **File Server Resource Manager**.  
  
2.  In der Oberfläche File Server Resource Manager, mit der rechten Maustaste **File Server Resource Manager**, und klicken Sie dann auf **Optionen konfigurieren**. Die **File Server Resource Manager Optionen** Dialogfeld wird geöffnet.  
  
3.  Auf der **e-Mail-Benachrichtigungen** Registerkarte unter SMTP-Servername oder IP-Adresse, geben Sie den Hostnamen oder die IP-Adresse des SMTP-Servers, der weiterleiten, werden e-Mail-Benachrichtigungen.  
  
4.  Sollten Sie regelmäßig benachrichtigen bestimmte Administratoren Kontingent- oder Dateiprüfungsereignisse unter **Standardadministratorempfänger**, geben Sie z.B. die E-Mail-Adressen fileadmin@contoso.com. Verwenden Sie das Format account@domain, und verwenden Sie Semikolons zum Trennen mehrerer Konten.  
  
#### <a name="create-groups-on-file1"></a>Erstellen von Gruppen auf FILE1  
  
###### <a name="to-create-security-groups-on-file1"></a>Zum Erstellen von Sicherheitsgruppen auf FILE1  
  
1.  Melden Sie sich bei FILE1 als "Contoso\administrator" mit dem Kennwort: ** pass@word1 **.  
  
2.  NT-AUTORITÄT\Authentifizierte Benutzer zum Hinzufügen der **WinRMRemoteWMIUsers__** Gruppe.  
  
#### <a name="create-files-and-folders-on-file1"></a>Erstellen von Dateien und Ordnern auf FILE1  
  
1.  Erstellen Sie ein neues NTFS-Volume auf FILE1, und erstellen Sie die folgenden Ordner: D:\Finance Documents.  
  
2.  Erstellen Sie die folgenden Dateien mit den angegebenen Details:  
  
    -   **Finance Memo.docx**: Fügen Sie etwas finanztechnischen Text in das Dokument. Z. B. "die Geschäftsregeln darüber, wer auf Finanzdokumente zugreifen können, haben sich geändert. Finanzdokumente werden jetzt nur von Mitgliedern der Gruppe ' financeexpert ' können zugegriffen. Keine anderen Abteilungen oder Gruppen Zugriff haben. " Sie müssen die Auswirkungen dieser Änderung vor der Implementierung in der Umgebung zu bewerten. Stellen Sie sicher, dass in diesem Dokument als Fußzeile auf jeder Seite CONTOSO vertraulich ist.  
  
    -   **Request for Approval to Hire.docx**: Erstellen Sie ein Formular in diesem Dokument, das Bewerberinformationen erfasst. Sie benötigen die folgenden Felder im Dokument: **Name des Bewerbers, Sozialversicherungsnummer, Position, vorgeschlagenes Gehalt, Startdatum, Name des Vorgesetzten, Abteilung**. Fügen Sie einen zusätzlichen Abschnitt in das Dokument mit einem Formular für **Unterschrift des Vorgesetzten, genehmigtes Gehalt, Bestätigung des Angebots**, und **Status des Angebots**.   
        Stellen Sie das Dokument rechteverwaltung.  
  
    -   **Word Document1.docx**: in diesem Dokument einige testinhalte hinzugefügt.  
  
    -   **Word Document2.docx**: Hinzufügen Inhalt für dieses Dokument zu testen.  
  
    -   **Workbook1.xlsx**  
  
    -   **Workbook2.xlsx**  
  
    -   Erstellen Sie einen Ordner auf dem Desktop mit Namen von regulären Ausdrücken. Erstellen Sie ein Textdokument unter dem Ordner **RegEx-SSN**. Geben Sie den folgenden Inhalt in der Datei, und klicken Sie dann speichern Sie und schließen Sie die Datei:   
        ^(?! 000)([0-7]\d{2}|7([0-7]\d|7[012])) ([-]?) (?! 00) \d\d\3 (? 0000) \d {4} $  
  
3.  Geben Sie den Ordner "D:\Finance Documents" als Finanzdokumente, und gewähren Sie jedem über Lese-und Schreibzugriff auf die Freigabe.  
  
> [!NOTE]  
> Zentrale Zugriffsrichtlinien sind nicht standardmäßig aktiviert, auf dem System oder Startvolume C:.  
  
#### <a name="BKMK_CS1"></a>Installieren von Active Directory Rights Management Services  
Fügen Sie die Active Directory Rights Management Services (AD RMS) und alle erforderlichen Features über den Server-Manager. Wählen Sie alle Standardeinstellungen.  
  
###### <a name="to-install-active-directory-rights-management-services"></a>So installieren Sie Active Directory-Rechteverwaltungsdienste  
  
1.  Melden Sie sich bei FILE1 als "Contoso\Administrator" oder als Mitglied der Gruppe "Domänen-Admins".  
  
    > [!IMPORTANT]  
    > Zum Installieren der AD RMS-Serverrolle den Installer müssen Konto (in diesem Fall "Contoso\Administrator") als Mitglied der Gruppe sowohl der lokalen Gruppe Administratoren auf dem Server auf dem AD RMS wird installiert werden auch die Mitgliedschaft in der Gruppe "Organisations-Admins" in Active Directory gewährt werden.  
  
2.  Klicken Sie im Server-Manager auf **Hinzufügen von Rollen und Features**. Hinzufügen von Rollen und Features-Assistent wird angezeigt.  
  
3.  Auf der **Vorbemerkungen** auf **Weiter**.  
  
4.  Auf der **Select Installation Type** auf **Rollen-und Feature-basierte Installation**, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Auswählen der Serverziele** auf **Weiter**.  
  
6.  Auf der **Serverrollen auswählen** Bildschirm, wählen Sie das Kontrollkästchen neben **Active Directory Rights Management Services**, und klicken Sie dann auf **Weiter**.  
  
7.  In der **Hinzufügen von Features, die für Active Directory Rights Management Services erforderlich sind? ** Dialogfeld, klicken Sie auf **Features hinzufügen**.  
  
8.  Auf der **Serverrollen auswählen** auf **Weiter**.  
  
9. Auf der **zu installierende Features auswählen** auf **Weiter**.  
  
10. Auf der **Active Directory Rights Management Services** auf Weiter.  
  
11. Auf der **Rollendienste auswählen** auf **Weiter**.  
  
12. Auf der **Webserverrolle (IIS)** auf **Weiter**.  
  
13. Auf der **Rollendienste auswählen** auf **Weiter**.  
  
14. Auf der **Installationsauswahl bestätigen** auf **installieren**.  
  
15. Nachdem die Installation abgeschlossen ist, auf die **Installationsstatus** auf **zusätzliche Konfiguration durchführen**. Der AD RMS-Konfigurations-Assistent wird angezeigt.  
  
16. Auf der **AD RMS** auf **Weiter**.  
  
17. Auf der **AD RMS-Clusters** wählen **erstellen Sie einen neuen AD RMS-Stammcluster** , und klicken Sie dann auf **Weiter**.  
  
18. Auf der **-Konfigurationsdatenbank** auf **interne Windows-Datenbank auf diesem Server**, und klicken Sie dann auf **Weiter**.  
  
    > [!NOTE]  
    > Für die Verwendung der internen Windows-Datenbank testumgebungen empfohlen, da es nicht mehr als einen Server in den AD RMS-Cluster unterstützt. Produktionsbereitstellungen sollten einen separaten Datenbankserver verwenden.  
  
19. Auf der **Dienstkonto** Bildschirm in **Domänenbenutzerkonto**, klicken Sie auf **angeben** und geben Sie dann den Benutzernamen (**"contoso\rms"**), und das Kennwort (**pass@word1**), und klicken Sie auf **OK**, und klicken Sie dann auf **Weiter**.  
  
20. Auf der **Kryptografiemodus** auf **Kryptografiemodus 2**.  
  
21. Auf der **Clusterschlüsselspeicher** auf **Weiter**.  
  
22. Auf der **Clusterschlüsselkennwort** Bildschirm, in dem **Kennwort** und **Kennwort bestätigen** Dialogfelder, Typ ** pass@word1 **, und klicken Sie dann auf **Weiter**.  
  
23. Auf der **Clusterwebsite** Bildschirm, stellen Sie sicher, dass **Default Web Site** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
24. Auf der **Clusteradresse** wählen die **verwenden eine unverschlüsselte Verbindung** option in der **vollqualifizierter Domänenname** geben **FILE1.contoso.com**, und klicken Sie dann auf **Weiter**.  
  
25. Auf der **Lizenzgeber-Zertifikatname** Bildschirm, übernehmen Sie den Standardnamen (**"file1"**) in das Textfeld ein und klicken Sie dann auf **Weiter**.  
  
26. Auf der **Dienstverbindungspunkt-Registrierung** wählen **Dienstverbindungspunkt jetzt registrieren**, und klicken Sie dann auf **Weiter**.  
  
27. Auf der **Bestätigung** auf **installieren**.  
  
28. Auf der **Ergebnisse** auf **schließen**, und klicken Sie dann auf **schließen** auf **Installationsstatus** Bildschirm. Nach Abschluss des Vorgangs, melden Sie sich ab und melden Sie sich als "contoso\rms" mit dem angegebenen Kennwort (**pass@word1**).  
  
29. Starten Sie die AD RMS-Konsole, und navigieren Sie zu **Vorlagen für Benutzerrechterichtlinien**.  
  
    Klicken Sie zum Öffnen der AD RMS-Konsole im Server-Manager **lokalen Server** klicken Sie dann in der Konsolenstruktur auf **Tools**, und klicken Sie dann auf **Active Directory Rights Management Services**.  
  
30. Klicken Sie auf die **verteilt Benutzerrechterichtlinien erstellen** Vorlage befindet sich im rechten Bereich, klicken Sie auf **hinzufügen**, und wählen Sie die folgende Informationen:  
  
    -   Sprache: Englisch (USA)  
  
    -   Name: Contoso Finance Admin Only  
  
    -   Beschreibung: Contoso Finance Admin Only  
  
    Klicken Sie auf **hinzufügen**, und klicken Sie dann auf **Weiter**.  
  
31. Klicken Sie im Abschnitt Benutzer und Rechte **Benutzer und Rechte**, klicken Sie auf **hinzufügen**, Typ ** financeadmin@contoso.com **, und klicken Sie auf **OK**.  
  
32. Wählen Sie **Vollzugriff**, und lassen Sie **vollständige Steuerung von gestatten Besitzer (Autor) permanenten** ausgewählten.  
  
33. Klicken Sie auf die verbleibenden Registerkarten ohne Änderungen jedoch aus, und klicken Sie dann auf **Fertig stellen**. Melden Sie sich als "Contoso\Administrator" an.  
  
34. Navigieren Sie zum Ordner C:\inetpub\wwwroot\\_wmcs\certification, wählen Sie die Datei "ServerCertification.asmx", und fügen Sie Benutzer authentifiziert, um über Lese- und Schreibberechtigungen für die Datei.  
  
35. Öffnen Sie Windows PowerShell, und führen Sie `Get-FsrmRmsTemplate`. Stellen Sie sicher, dass Sie die RMS-Vorlage finden in den vorherigen Schritten in dieser Prozedur mit diesem Befehl erstellten Verbindung sind.  
  
> [!IMPORTANT]  
> Wenn Sie möchten Ihre Dateiserver unmittelbar geändert werden, damit Sie sie testen können, müssen Sie die folgenden Schritte ausführen:  
>   
> 1.  Klicken Sie auf dem Dateiserver "file1", öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, und führen Sie die folgenden Befehle:  
>   
>     -   Gpupdate/force.  
>     -   NLTEST /SC_RESET:contoso.com  
> 2.  Replizieren Sie auf dem Domänencontroller (DC1) Active Directory.  
>   
>     Weitere Informationen zu den Schritten zum Erzwingen der Replikation von Active Directory finden Sie unter [Active Directory-Replikation](https://technet.microsoft.com/library/cc794809(WS.10).aspx)  
  
Optional, und damit ohne Hinzufügen von Rollen und Features Assistenten im Server-Manager können Sie Windows PowerShell installieren und Konfigurieren der AD RMS-Serverrolle wie im folgenden Verfahren zeigen.  
  
###### <a name="to-install-and-configure-an-ad-rms-cluster-in-windows-server-2012-using-windows-powershell"></a>So installieren und Konfigurieren eines AD RMS-Clusters in Windows Server 2012 mit Windows PowerShell  
  
1.  Melden Sie sich als CONTOSO\Administrator mit dem Kennwort: ** pass@word1 **.  
  
    > [!IMPORTANT]  
    > Zum Installieren der AD RMS-Serverrolle den Installer müssen Konto (in diesem Fall "Contoso\Administrator") als Mitglied der Gruppe sowohl der lokalen Gruppe Administratoren auf dem Server auf dem AD RMS wird installiert werden auch die Mitgliedschaft in der Gruppe "Organisations-Admins" in Active Directory gewährt werden.  
  
2.  Auf den Serverdesktop, klicken Sie das Windows PowerShell-Symbol auf der Taskleiste und wählen **als Administrator ausführen** zu Windows PowerShell-Eingabeaufforderung mit Administratorrechten zu öffnen.  
  
3.  Um den Server-Manager-Cmdlets verwenden, um die AD RMS-Serverrolle installieren, geben Sie Folgendes ein:  
  
    ```  
    Add-WindowsFeature ADRMS '"IncludeAllSubFeature '"IncludeManagementTools  
    ```  
  
4.  Erstellen Sie die Windows PowerShell-Laufwerk auf den AD RMS-Server darstellen, den Sie installieren.  
  
    Geben Sie z. B. zum Erstellen einer Windows PowerShell-Laufwerk mit dem Namen RC zu installieren und konfigurieren den ersten Server in einer AD RMS-Stammcluster:  
  
    ```  
    Import-Module ADRMS  
    New-PSDrive -PSProvider ADRMSInstall -Name RC -Root RootCluster  
    ```  
  
5.  Legen Sie Eigenschaften für Objekte im datenträgernamespace, die erforderliche Konfigurationseinstellungen widerspiegeln.  
  
    Angenommen, um das AD RMS-Dienstkonto in der Windows PowerShell-Befehlszeile festzulegen, geben Sie Folgendes ein:  
  
    ```  
    $svcacct = Get-Credential  
    ```  
  
    Wenn das Dialogfeld "Windows-Sicherheit" angezeigt wird, geben Sie die AD RMS-Dienst-Konto-Domänenbenutzernamen "contoso\rms" und das zugehörige Kennwort ein.  
  
    Um das AD RMS-Dienstkonto den AD RMS-Clustereinstellungen zuzuweisen, geben Sie als Nächstes Folgendes ein:  
  
    ```  
    Set-ItemProperty -Path RC:\ -Name ServiceAccount -Value $svcacct  
    ```  
  
    Zum Festlegen der AD RMS-Server mithilfe von Windows Internal Database, bei der Windows PowerShell-Eingabeaufforderung, geben Sie als Nächstes:  
  
    ```  
    Set-ItemProperty -Path RC:\ClusterDatabase -Name UseWindowsInternalDatabase -Value $true  
    ```  
  
    Geben Sie als Nächstes, um das Clusterschlüsselkennwort in einer Variablen, an der Windows PowerShell-Eingabeaufforderung sicher zu speichern:  
  
    ```  
    $password = Read-Host -AsSecureString -Prompt "Password:"  
    ```  
  
    Geben Sie das Clusterschlüsselkennwort ein, und klicken Sie dann drücken Sie die EINGABETASTE.  
  
    Geben Sie anschließend die AD RMS-Installation an der Windows PowerShell-Eingabeaufforderung das Kennwort zuweisen:  
  
    ```  
    Set-ItemProperty -Path RC:\ClusterKey -Name CentrallyManagedPassword -Value $password  
    ```  
  
    Um die AD RMS-Cluster-Adresse, an der Windows PowerShell-Befehlszeile festzulegen, geben Sie Folgendes ein:  
  
    ```  
    Set-ItemProperty -Path RC:\ -Name ClusterURL -Value "http://file1.contoso.com:80"  
    ```  
  
    Geben Sie anschließend den SLC-Namen für die AD RMS-Installation an der Windows PowerShell-Eingabeaufforderung zuzuweisen:  
  
    ```  
    Set-ItemProperty -Path RC:\ -Name SLCName -Value "FILE1"  
    ```  
  
    Um den Dienstverbindungspunkt (SCP) für den AD RMS-Cluster, in der Windows PowerShell-Befehlszeile festzulegen, geben Sie Folgendes ein:  
  
    ```  
    Set-ItemProperty -Path RC:\ -Name RegisterSCP -Value $true  
    ```  
  
6.  Führen Sie die **Install-ADRMS** Cmdlet. Zusätzlich zu den AD RMS-Serverrolle installieren und Konfigurieren des Servers, installiert dieses Cmdlet auch andere Features von AD RMS, falls erforderlich.  
  
    Ändern Sie in der Windows PowerShell-Laufwerk mit dem Namen RC und installieren und Konfigurieren von AD RMS, beispielsweise Folgendes ein:  
  
    ```  
    Set-Location RC:\  
    Install-ADRMS -Path.  
    ```  
  
    Geben Sie "Y", wenn das Cmdlet zur Bestätigung aufgefordert werden möchten die Installation zu starten.  
  
7.  Melden Sie sich als "Contoso\Administrator" an und melden Sie sich auf als "contoso\rms" mithilfe des angegebenen Kennworts ("pass@word1").  
  
    > [!IMPORTANT]  
    > Zur Verwaltung von AD RMS-Server muss das Konto, Sie sind angemeldet und zum Verwalten des Servers (in diesem Fall "contoso\rms") verwenden Mitgliedschaft in beiden der lokalen Gruppe Administratoren auf dem AD RMS-Servercomputer sowie die Mitgliedschaft in der Gruppe "Organisations-Admins" in Active Directory gewährt werden.  
  
8.  Auf den Serverdesktop, klicken Sie das Windows PowerShell-Symbol auf der Taskleiste und wählen **als Administrator ausführen** zu Windows PowerShell-Eingabeaufforderung mit Administratorrechten zu öffnen.  
  
9. Erstellen Sie die Windows PowerShell-Laufwerk auf den AD RMS-Server darstellen, den Sie konfigurieren.  
  
    Z. B. um ein Windows PowerShell-Laufwerk mit dem Namen RC so konfigurieren Sie die AD RMS-Stammcluster erstellen, geben Sie Folgendes ein:  
  
    ```  
    Import-Module ADRMSAdmin `  
    New-PSDrive -PSProvider ADRMSAdmin -Name RC -Root http://localhost -Force -Scope Global  
    ```  
  
10. So erstellen neue Rechtevorlage für den Contoso-Administrator und weisen diese Benutzerrechte mit Vollzugriff in Ihrer AD RMS-Installation an der Windows PowerShell-Eingabeaufforderung, geben Sie Folgendes ein:  
  
    ```  
    New-Item -Path RC:\RightsPolicyTemplate '"LocaleName en-us -DisplayName "Contoso Finance Admin Only" -Description "Contoso Finance Admin Only" -UserGroup financeadmin@contoso.com  -Right ('FullControl')  
    ```  
  
11. So überprüfen, dass die neue Rechtevorlage für den Contoso-Administrator, der Windows PowerShell-Eingabeaufforderung angezeigt werden können:  
  
    ```  
    Get-FsrmRmsTemplate  
    ```  
  
    Prüfen Sie die Ausgabe dieses Cmdlets, die RMS-Vorlage zu bestätigen, die Sie im vorherigen Schritt erstellt haben, ist vorhanden.  
  
### <a name="build-the-mail-server-srv1"></a>Erstellen Sie e-Mail-Servers (SRV1)  
SRV1 ist der SMTP-/POP3-Mail-Server. Sie müssen es so einrichten, dass Sie als Teil des Szenarios für die Unterstützung nach "Zugriff verweigert" e-Mail-Benachrichtigungen senden können.  
  
Konfigurieren von Microsoft Exchange Server auf diesem Computer. Weitere Informationen finden Sie unter [zum Installieren von Exchange Server](https://go.microsoft.com/fwlink/?prd=12364).  
  
### <a name="build-the-client-virtual-machine-client1"></a>Erstellen des virtuellen Clientcomputers (CLIENT1)  
  
##### <a name="to-build-the-client-virtual-machine"></a>Um den virtuellen Clientcomputer zu erstellen.  
  
1.  Verbinden Sie den CLIENT1 mit "id_ad_network".  
  
2.  Installieren Sie Microsoft Office 2010.  
  
3.  Melden Sie sich als "Contoso\Administrator" an, und verwenden Sie die folgende Informationen zum Konfigurieren von Microsoft Outlook.  
  
    -   Ihr Name: Dateiadministrator  
  
    -   E-Mail-Adresse:fileadmin@contoso.com  
  
    -   Kontotyp: POP3  
  
    -   Eingehender e-Mail-Server: statische IP-Adresse von SRV1  
  
    -   Ausgehender e-Mail-Server: statische IP-Adresse von SRV1  
  
    -   Benutzername:fileadmin@contoso.com  
  
    -   Kennwort speichern: Wählen Sie  
  
4.  Erstellen Sie eine Verknüpfung zu Outlook auf dem Desktop "Contoso\Administrator" an.  
  
5.  Öffnen Sie Outlook, und beheben Sie alle "erstmals gestarteten" Nachrichten.  
  
6.  Löschen Sie jede, die generiert wurden.  
  
7.  Erstellen Sie eine neue Verknüpfung auf dem Desktop für alle Benutzer auf dem virtuellen Clientcomputer, die auf Dokumente \\\FILE1\Finance verweist.  
  
8.  Starten Sie nach Bedarf neu.  
  
##### <a name="enable-access-denied-assistance-on-the-client-virtual-machine"></a>Aktivieren der Unterstützung nach "Zugriff verweigert" auf dem virtuellen Clientcomputer  
  
1.  Registrierungs-Editor zu öffnen, und navigieren Sie zu **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Explorer**.  
  
    -   Legen Sie **EnableShellExecuteFileStreamCheck** auf **1**.  
  
    -   Wert: DWORD-Wert  
  
## <a name="BKMK_CF"></a>Die laboreinrichtung für die Bereitstellung von Ansprüchen über Gesamtstrukturen Szenario  
  
### <a name="BKMK_2.1"></a>Erstellen eines virtuellen Computers für DC2  
  
-   Erstellen eines virtuellen Computers von der Windows Server 2012-ISO-Datei.  
  
-   Name des virtuellen Computers als DC2 zu erstellen.  
  
-   Schließen Sie die virtuelle Maschine mit "id_ad_network".  
  
> [!IMPORTANT]  
> Virtuelle Computer einer Domäne hinzufügen und Bereitstellen von Anspruchstypen in mehreren Gesamtstrukturen erforderlich, dass die virtuellen Computer die FQDNs der relevanten Domänen auflösen können. Möglicherweise wird die DNS-Einstellungen auf den virtuellen Computern zu diesem Zweck manuell konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren eines virtuellen Netzwerks](https://technet.microsoft.com/library/cc732470%28v=ws.10%29.aspx).  
>   
> Alle Abbilder der virtuellen Maschine (Server und Clients) müssen neu konfiguriert werden, um eine statische IP-Version 4 (IPv4) verwenden-Adresse und das Domain Name System (DNS)-Clienteinstellungen. Weitere Informationen finden Sie unter [konfigurieren Sie einen DNS-Client für statische IP-Adresse](https://go.microsoft.com/fwlink/?LinkId=150952).  
  
### <a name="BKMK_2.2"></a>Richten Sie eine neue Gesamtstruktur namens "adatum.com"  
  
##### <a name="to-install-active-directory-domain-services"></a>So installieren Sie Active Directory-Domänendienste  
  
1.  Schließen Sie die virtuelle Maschine mit "id_ad_network". Melden Sie sich bei DC2 als Administrator mit dem Kennwort ** Pass@word1 **.  
  
2.  Klicken Sie im Server-Manager auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**.  
  
3.  Auf der **vor dem Beginn** auf **Weiter**.  
  
4.  Auf der **Select Installation Type** auf **rollenbasierte oder featurebasierte Installation**, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Zielserver auswählen** auf **wählen Sie einen Server aus dem Serverpool**, klicken Sie auf den Namen des Servers, in dem Sie zum Installieren von Active Directory-Domänendienste (AD DS), und klicken Sie dann auf soll **Weiter**.  
  
6.  Auf der **Serverrollen auswählen** auf **Active Directory Domain Services**. In der **Hinzufügen von Rollen und Features Assistenten** Dialogfeld, klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.  
  
7.  Auf der **Features auswählen** auf **Weiter**.  
  
8.  Auf der **AD DS** Seite, überprüfen Sie die Informationen, und klicken Sie dann auf **Weiter**.  
  
9. Auf der **Bestätigung** auf **installieren**. Die Statusanzeige des Feature-Installation auf der Seite mit den weist darauf hin, dass die Rolle installiert wird.  
  
10. Auf der **Ergebnisse** sicher, dass die Installation erfolgreich war, und klicken Sie dann auf das Warnsymbol mit einem Ausrufezeichen in der oberen rechten Ecke des Bildschirms neben **verwalten**. Klicken Sie in der Liste "Aufgaben" auf die **Server zu einem Domänencontroller heraufstufen** Link.  
  
    > [!IMPORTANT]  
    > Wenn Sie den Installations-Assistenten jetzt schließen, sondern klicken Sie auf **Server zu einem Domänencontroller heraufstufen**, Sie können die AD DS-Installation fortsetzen, indem Sie auf **Aufgaben** im Server-Manager.  
  
11. Auf der **Bereitstellungskonfiguration** auf **Hinzufügen einer neuen Gesamtstruktur**, geben Sie den Namen der Stammdomäne, **"adatum.com"**, und klicken Sie dann auf **Weiter**.  
  
12. Auf der **Domänencontrolleroptionen** Seite die Domänen- und Gesamtstruktur-Funktionsebenen wie Windows Server 2012 aus, geben Sie das DSRM-Kennwort ** pass@word1 **, und klicken Sie dann auf **Weiter**.  
  
13. Auf der **DNS-Optionen** auf **Weiter**.  
  
14. Auf der **zusätzliche Optionen** auf **Weiter**.  
  
15. Auf der **Pfade** Seite, geben Sie die Speicherorte für die Active Directory-Datenbank, Protokolldateien und SYSVOL-Ordner (oder übernehmen Sie die Standardspeicherorte), und klicken Sie dann auf **Weiter**.  
  
16. Auf der **Optionen prüfen** Seite, bestätigen Sie Ihre Auswahl, und klicken Sie dann auf **Weiter**.  
  
17. Auf der **Voraussetzungsüberprüfung** Seite, stellen Sie sicher, dass die Validierung der Voraussetzungen abgeschlossen ist, und klicken Sie dann auf **installieren**.  
  
18. Auf der **Ergebnisse** Seite, stellen Sie sicher, dass der Server erfolgreich als Domänencontroller konfiguriert wurde, und klicken Sie dann auf **schließen**.  
  
19. Starten Sie den Server zum Abschließen der AD DS-Installation. (Standardmäßig geschieht dies automatisch.)  
  
> [!IMPORTANT]  
> Um sicherzustellen, dass das Netzwerk ordnungsgemäß konfiguriert ist, nachdem Sie die beiden Gesamtstrukturen eingerichtet haben, müssen Sie die folgenden Schritte ausführen:  
>   
> -   Melden Sie sich bei "adatum.com" als "adatum\administrator" an. Öffnen Sie ein Eingabeaufforderungsfenster, geben **Nslookup contoso.com**, und drücken Sie dann die EINGABETASTE.  
> -   Melden Sie sich bei "contoso.com" als "Contoso\Administrator" an. Öffnen Sie ein Eingabeaufforderungsfenster, geben **Nslookup adatum.com**, und drücken Sie dann die EINGABETASTE.  
>   
> Wenn diese Befehle fehlerfrei ausgeführt werden, können die Gesamtstrukturen miteinander kommunizieren. Weitere Informationen über Nslookup-Fehler finden Sie im Abschnitt zur Problembehandlung im Thema [Verwendung von NSlookup.exe](https://support.microsoft.com/kb/200525)  
  
### <a name="BKMK_2.22"></a>Festlegen von "contoso.com" als eine vertrauenswürdige Gesamtstruktur "adatum.com"  
In diesem Schritterstellen Sie eine Vertrauensstellung zwischen der Adatum Corporation-Website und der Contoso, Ltd.-Website.  
  
##### <a name="to-set-contoso-as-a-trusting-forest-to-adatum"></a>So legen Sie Contoso als eine vertrauenswürdige Gesamtstruktur auf Adatum fest  
  
1.  Melden Sie sich an DC2 als Administrator. Auf der **starten** geben domain.msc.  
  
2.  Klicken Sie in der Konsolenstruktur mit der rechten Maustaste "adatum.com", und klicken Sie dann auf Eigenschaften.  
  
3.  Auf der **Vertrauensstellungen** auf **neue Vertrauensstellung**, und klicken Sie dann auf **Weiter**.  
  
4.  Auf der **Vertrauensstellungsname** geben **"contoso.com"**Namensfeld in Domain Name System (DNS), und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Vertrauenstyp** auf **Gesamtstruktur-Vertrauensstellung**, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **Richtung der Vertrauensstellung** auf **bidirektionale**.  
  
7.  Auf der **Seiten der Vertrauensstellung** auf **für diese Domäne und die angegebene Domäne**, und klicken Sie dann auf **Weiter**.  
  
8.  Fahren Sie mit der Anweisungen im Assistenten.  
  
### <a name="BKMK_2.4"></a>Erstellen Sie zusätzlicher Benutzer in der Adatum-Gesamtstruktur  
Erstellen Sie den Benutzer Jeff Low mit dem Kennwort ** pass@word1 **, und weisen Sie das "Company"-Attribut mit dem Wert **Adatum**.  
  
##### <a name="to-create-a-user-with-the-company-attribute"></a>Zum Erstellen eines Benutzers mit dem "Company"-Attribut  
  
1.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten in Windows PowerShell, und fügen Sie den folgenden Code:  
  
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
  
### <a name="BKMK_2.5"></a>Erstellen Sie den Anspruchstyp Unternehmen auf "adataum.com"  
  
##### <a name="to-create-a-claim-type-by-using-windows-powershell"></a>So erstellen Sie einen Anspruchstyp mithilfe von Windows PowerShell  
  
1.  Melden Sie sich bei "adatum.com" als Administrator.  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten in Windows PowerShell, und geben Sie den folgenden Code:  
  
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
  
### <a name="BKMK_2.55"></a>Aktivieren Sie die Ressourceneigenschaft "Unternehmen" auf "contoso.com"  
  
##### <a name="to-enable-the-company-resource-property-on-contosocom"></a>So aktivieren Sie die Ressourceneigenschaft "Unternehmen" auf "contoso.com"  
  
1.  Melden Sie sich bei "contoso.com" als Administrator.  
  
2.  Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **Active Directory-Verwaltungscenter**.  
  
3.  Klicken Sie im linken Bereich des Active Directory-Verwaltungscenters auf **Strukturansicht**. Klicken Sie im linken Bereich auf **dynamische Zugriffssteuerung**, und doppelklicken Sie dann auf **Ressourceneigenschaften**.  
  
4.  Wählen Sie **Unternehmen** aus der **Ressourceneigenschaften** aufgelistet, mit der rechten Maustaste, und wählen Sie **Eigenschaften**. In der **vorgeschlagene Werte** auf **hinzufügen** die vorgeschlagenen Werte hinzu: Contoso und "Adatum", und klicken Sie dann auf **OK** zweimal.  
  
5.  Wählen Sie **Unternehmen** aus der **Ressourceneigenschaften** aufgelistet, mit der rechten Maustaste, und wählen Sie **aktivieren**.  
  
### <a name="BKMK_2.6"></a>Aktivieren der dynamischen Zugriffssteuerung auf "adatum.com"  
  
##### <a name="to-enable-dynamic-access-control-for-adatumcom"></a>So aktivieren Sie die dynamische Zugriffssteuerung für "adatum.com"  
  
1.  Melden Sie sich bei "adatum.com" als Administrator.  
  
2.  Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole, klicken Sie auf **"adatum.com"**, und doppelklicken Sie dann auf **Domänencontroller**.  
  
3.  Mit der rechten Maustaste **Standarddomänencontroller-Richtlinie**, und wählen Sie **bearbeiten**.  
  
4.  Doppelklicken Sie in der Gruppenrichtlinienverwaltungs-Editor-Fenster auf **Computerkonfiguration**, doppelklicken Sie auf **Richtlinien**, doppelklicken Sie auf **Administrative Vorlagen**, doppelklicken Sie auf **System**, und doppelklicken Sie dann auf **KDC**.  
  
5.  Doppelklicken Sie auf **KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos armoring** und wählen Sie die Option neben **aktiviert**. Sie müssen diese Einstellung, um die Verwendung zentraler Zugriffsrichtlinien zu aktivieren.  
  
6.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, und führen Sie den folgenden Befehl:  
  
    ```  
    gpupdate /force  
    ```  
  
### <a name="BKMK_2.8"></a>Erstellen Sie den Anspruchstyp Unternehmen auf "contoso.com"  
  
##### <a name="to-create-a-claim-type-by-using-windows-powershell"></a>So erstellen Sie einen Anspruchstyp mithilfe von Windows PowerShell  
  
1.  Melden Sie sich bei "contoso.com" als Administrator.  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten in Windows PowerShell, und geben den folgenden Code:  
  
    ```  
    New-ADClaimType '"SourceTransformPolicy `  
    '"DisplayName 'Company' `  
    '"ID 'ad://ext/Company:ContosoAdatum' `  
    '"IsSingleValued $true `  
    '"ValueType 'string' `  
  
    ```  
  
### <a name="BKMK_2.9"></a>Erstellen Sie die zentrale Zugriffsregel  
  
##### <a name="to-create-a-central-access-rule"></a>Erstellen Sie eine zentrale Zugriffsregel  
  
1.  Klicken Sie im linken Bereich des Active Directory-Verwaltungscenters auf **Strukturansicht**. Klicken Sie im linken Bereich auf **dynamische Zugriffssteuerung**, und klicken Sie dann auf **zentrale Zugriffsregeln**.  
  
2.  Mit der rechten Maustaste **zentrale Zugriffsregeln**, klicken Sie auf **neu**, und klicken Sie dann **zentrale Zugriffsregel**.  
  
3.  In den **Namen** geben **AdatumEmployeeAccessRule**.  
  
4.  In der **Berechtigungen** Abschnitt der **folgende Berechtigungen als aktuelle Berechtigungen verwenden** auf **bearbeiten**, und klicken Sie dann auf **hinzufügen**. Klicken Sie auf die **Prinzipal auswählen** verknüpfen, geben Sie **authentifizierte Benutzer**, und klicken Sie dann auf **OK**.  
  
5.  In der **Berechtigungseintrag für Berechtigungen** im Dialogfeld klicken Sie auf **eine Bedingung hinzufügen,**, und geben Sie Folgendes ein: [**Benutzer**] [**Unternehmen**] [**gleich**] [**Wert**] [**Adatum**]. Berechtigungen werden sollten **ändern, lesen und ausführen, lesen, schreiben**.  
  
6.  Klicken Sie auf **OK**.  
  
7.  Klicken Sie auf **OK** dreimal ab, und kehren Sie zu Active Directory-Verwaltungscenter zurück.  
  
    ![Lösungshandbücher](media/Appendix-B--Setting-Up-the-Test-Environment/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
    Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
    ```  
    New-ADCentralAccessRule `  
    -CurrentAcl:"O:SYG:SYD:AR(A;;FA;;;OW)(A;;FA;;;BA)(A;;FA;;;SY)(XA;;0x1301bf;;;AU;(@USER.ad://ext/Company:ContosoAdatum == `"Adatum`"))" `  
    -Name:"AdatumEmployeeAccessRule" `  
    -ProposedAcl:$null `  
    -ProtectedFromAccidentalDeletion:$true `  
    -Server:"contoso.com" `  
    ```  
  
### <a name="BKMK_2.10"></a>Erstellen Sie die zentrale Zugriffsrichtlinie  
  
##### <a name="to-create-a-central-access-policy"></a>Erstellen Sie eine zentrale Zugriffsrichtlinie  
  
1.  Melden Sie sich bei "contoso.com" als Administrator.  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten in Windows PowerShell, und fügen Sie den folgenden Code:  
  
    ```  
    New-ADCentralAccessPolicy "Adatum Only Access Policy"   
    Add-ADCentralAccessPolicyMember "Adatum Only Access Policy" `  
    -Member "AdatumEmployeeAccessRule" `  
    ```  
  
### <a name="BKMK_2.11"></a>Veröffentlichen der neuen Richtlinie mithilfe von Gruppenrichtlinien  
  
##### <a name="to-apply-the-central-access-policy-across-file-servers-through-group-policy"></a>Die zentrale Zugriffsrichtlinie dateiserverübergreifend durch die Gruppenrichtlinie angewendet  
  
1.  Auf der **starten** geben **Verwaltung**, und in der **Suche** , klicken Sie auf **Einstellungen**. In der **Einstellungen** , klicken Sie auf **Verwaltung**. Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole aus der **Verwaltung** Ordner.  
  
    > [!TIP]  
    > Wenn die **Verwaltungstools anzeigen** Einstellung deaktiviert ist, den Ordner "Verwaltung" und dessen Inhalt werden nicht angezeigt, dem **Einstellungen** Ergebnisse.  
  
2.  Mit der rechten Maustaste in der Domäne "contoso.com", klicken Sie auf **ein Gruppenrichtlinienobjekt in dieser Domäne erstellen und verknüpfen Sie es hier**  
  
3.  Geben Sie einen beschreibenden Namen für das Gruppenrichtlinienobjekt, z. B. **AdatumAccessGPO**, und klicken Sie dann auf **OK**.  
  
##### <a name="to-apply-the-central-access-policy-to-the-file-server-through-group-policy"></a>Die zentrale Zugriffsrichtlinie auf den Dateiserver über eine Gruppenrichtlinie angewendet  
  
1.  Auf der **starten** geben **die Gruppenrichtlinien-Verwaltungskonsole**in der **Suche** Feld. Öffnen **Gruppenrichtlinienverwaltung** aus dem Ordner "Verwaltung".  
  
    > [!TIP]  
    > Wenn die **Verwaltungstools anzeigen** Einstellung deaktiviert ist, den Ordner "Verwaltung" und dessen Inhalt werden nicht in den Ergebnissen Einstellungen angezeigt.  
  
2.  Navigieren Sie zu, und wählen Sie Contoso wie folgt aus: Gruppe Group Policy Management\Forest: contoso.com\Domains\contoso.com.  
  
3.  Mit der rechten Maustaste die **AdatumAccessGPO** Richtlinie, und wählen Sie **bearbeiten**.  
  
4.  Im Gruppenrichtlinienverwaltungs-Editor, klicken Sie auf **Computerkonfiguration**, erweitern Sie **Richtlinien**, erweitern Sie **Windows-Einstellungen**, und klicken Sie dann auf **Sicherheitseinstellungen**.  
  
5.  Erweitern Sie **Dateisystem**, mit der rechten Maustaste **zentrale Zugriffsrichtlinie**, und klicken Sie dann auf **zentrale Zugriffsrichtlinien verwalten**.  
  
6.  In der **Konfiguration der zentralen Zugriffsrichtlinien** Dialogfeld, klicken Sie auf **hinzufügen**wählen **Adatum Only Access Policy**, und klicken Sie dann auf **OK**.  
  
7.  Schließen Sie den Gruppenrichtlinienverwaltungs-Editor. Sie haben nun der Gruppenrichtlinie die zentrale Zugriffsrichtlinie hinzugefügt.  
  
### <a name="BKMK_2.12"></a>Erstellen Sie den Ordner "Ergebnis" auf dem Dateiserver  
Erstellen Sie ein neues NTFS-Volume auf FILE1, und erstellen Sie den folgenden Ordner: D:\Earnings.  
  
> [!NOTE]  
> Zentrale Zugriffsrichtlinien sind nicht standardmäßig aktiviert, auf dem System oder Startvolume C:.  
  
### <a name="BKMK_2.13"></a>Legen Sie die Klassifizierung, und wenden Sie die zentrale Zugriffsrichtlinie auf den Ordner "Ergebnis"  
  
##### <a name="to-assign-the-central-access-policy-on-the-file-server"></a>Die zentrale Zugriffsrichtlinie auf dem Dateiserver zugewiesen.  
  
1.  Schließen Sie in Hyper-V-Manager auf Server "file1". Melden Sie sich an den Server mit "Contoso\Administrator" mit dem Kennwort ** pass@word1 **.  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten und Typ: **Gpupdate/force**. Dadurch wird sichergestellt, dass Ihre gruppenrichtlinienänderungen auf Ihrem Server wirksam werden.  
  
3.  Sie müssen auch die globalen Ressourceneigenschaften aus Active Directory zu aktualisieren. Öffnen Sie Windows PowerShell, geben `Update-FSRMClassificationpropertyDefinition`, und drücken Sie dann die EINGABETASTE. Schließen Sie WindowsPowerShell.  
  
4.  Öffnen Sie Windows Explorer, und navigieren Sie zu D:\EARNINGS. Mit der rechten Maustaste die **Einnahmen** Ordner, und klicken Sie dann auf **Eigenschaften**.  
  
5.  Klicken Sie auf die **Klassifizierung** Registerkarte **Unternehmen**, und wählen Sie dann **Adatum** in die **Wert** Feld.  
  
6.  Klicken Sie auf **ändern**Option **Adatum Only Access Policy** aus der Dropdown-Menü, und klicken Sie dann auf **übernehmen**.  
  
7.  Klicken Sie auf die **Security** auf **erweitert**, und klicken Sie dann auf die **zentrale Richtlinie** Registerkarte. Sollte die **AdatumEmployeeAccessRule** aufgeführt. Sie können das Element, um alle Berechtigungen anzeigen, die Sie festlegen, wenn Sie die Regel in Active Directory erstellt erweitern.  
  
8.  Klicken Sie auf **OK** zurückkehren zu Windows-Explorer.  
  


