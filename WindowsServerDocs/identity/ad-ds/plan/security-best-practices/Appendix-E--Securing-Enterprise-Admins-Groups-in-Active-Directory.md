---
ms.assetid: f643099e-f9c6-476f-9378-5a9228c39b33
title: 'Anhang E: Sichern von Organisations-Admins-Gruppen in Active Directory'
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 5294be945ce4a93ffeb1c27cffa8a82470920e7b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80821633"
---
# <a name="appendix-e-securing-enterprise-admins-groups-in-active-directory"></a>Anhang E: Schützen von Organisationsadministratorgruppen in Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-e-securing-enterprise-admins-groups-in-active-directory"></a>Anhang E: Schützen von Organisationsadministratorgruppen in Active Directory  
Die Enterprise Admins-Gruppe (EA), die in der Stamm Domäne der Gesamtstruktur enthalten ist, sollte täglich keine Benutzer enthalten, mit der Ausnahme, dass das Administrator Konto der Stamm Domäne verfügbar ist, vorausgesetzt, Sie ist wie in [Anhang D: sichern integrierter Administrator Konten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)beschrieben geschützt.  

Organisations-Admins sind standardmäßig Mitglieder der Gruppe "Administratoren" in jeder Domäne in der Gesamtstruktur. Sie sollten die EA-Gruppe nicht aus den Administratoren Gruppen in jeder Domäne entfernen, da im Falle eines Notfall Wiederherstellungs Szenarios wahrscheinlich EA-Rechte erforderlich sind. Die Gruppe "Organisations-Admins" der Gesamtstruktur sollte wie in den folgenden Schritt-für-Schritt-Anweisungen beschrieben geschützt werden.  

Für die Gruppe "Organisations-Admins" in der Gesamtstruktur:  

1.  In Gruppenrichtlinien Objekten, die mit Organisationseinheiten verknüpft sind, die Mitglieds Server und Arbeitsstationen in jeder Domäne enthalten, sollte die Gruppe Organisations-Admins den folgenden Benutzerrechten in **Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten**  

    -   Zugriff vom Netzwerk auf diesen Computer verweigern  

    -   Anmelden als Batchauftrag verweigern  

    -   Anmelden als Dienst verweigern  

    -   Lokal anmelden verweigern  

    -   Anmelden über Remotedesktopdienste verweigern  

2.  Konfigurieren Sie die Überwachung so, dass Warnungen gesendet werden, wenn Änderungen an den Eigenschaften oder an der Mitgliedschaft in der Gruppe Organisations-Admins vorgenommen werden.  

### <a name="step-by-step-instructions-for-removing-all-members-from-the-enterprise-admins-group"></a>Schritt-für-Schritt-Anleitung zum Entfernen aller Mitglieder aus der Gruppe "Organisations-Admins"  

1.  Klicken **Server Manager**Sie in Server-Manager **auf Extras, und**klicken Sie dann auf **Active Directory Benutzer und Computer**.  

2.  Wenn Sie die Stamm Domäne für die Gesamtstruktur nicht verwalten, klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf <Domain>, und klicken Sie dann auf **Domäne ändern** (wobei <Domain> der Name der Domäne ist, die Sie gerade verwalten).  

    ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_43.gif)  

3.  Klicken Sie im Dialogfeld **Domäne ändern** auf **Durchsuchen**, wählen Sie die Stamm Domäne für die Gesamtstruktur aus, und klicken Sie auf **OK**.  

    ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_44.gif)  

4.  So entfernen Sie alle Mitglieder aus der EA-Gruppe:  

    1.  Doppelklicken Sie auf die Gruppe Organisations- **Admins** , und klicken Sie dann auf die Registerkarte **Mitglieder** .  

        ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_45.gif)  

    2.  Wählen Sie ein Mitglied der Gruppe aus, klicken Sie auf **Entfernen**, klicken Sie auf **Ja**, und klicken Sie auf **OK**.  

5.  Wiederholen Sie Schritt 2, bis alle Mitglieder der EA-Gruppe entfernt wurden.  

### <a name="step-by-step-instructions-to-secure-enterprise-admins-in-active-directory"></a>Schritt-für-Schritt-Anleitungen zum Schützen von Organisations-Admins in Active Directory  

1.  Klicken **Server Manager**Sie in Server-Manager **auf Extras, und**klicken Sie auf **Gruppenrichtlinie Verwaltung**.  

2.  Erweitern Sie in der Konsolen Struktur <Forest>\domains\\<Domain>, und klicken Sie dann auf **Gruppenrichtlinie Objekte** (wobei <Forest> der Name der Gesamtstruktur und <Domain> der Name der Domäne ist, in der Sie die Gruppenrichtlinie festlegen möchten).  

    > [!NOTE]  
    > In einer Gesamtstruktur, die mehrere Domänen enthält, sollte in jeder Domäne ein ähnliches GPO erstellt werden, in dem die Gruppe Organisations-Admins gesichert werden muss.  

3.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Gruppenrichtlinie Objekte**, und klicken Sie dann auf **neu**.  

    ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_46.gif)  

4.  Geben Sie im Dialogfeld **Neues** Gruppenrichtlinien Objekt <GPO Name>ein, und klicken Sie auf **OK** (wobei <GPO Name> der Name dieses Gruppenrichtlinien Objekts ist).  

    ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_47.gif)  

5.  Klicken Sie im Detailfenster mit der rechten Maustaste auf <GPO Name>, und klicken Sie dann auf **Bearbeiten**.  

6.  Navigieren Sie zu **Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, **und klicken Sie**auf Zuweisen von  

    ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_48.gif)  

7.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe Organisations-Admins auf Mitglieds Server und Arbeitsstationen über das Netzwerk zugreifen, indem Sie die folgenden Schritte ausführen:  

    1.  Doppelklicken Sie **auf Zugriff vom Netzwerk auf diesen Computer verweigern,** und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

    3.  Geben Sie **Enterprise Admins**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**.  

        ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_49.gif)  

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .  

8.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass sich Mitglieder der Gruppe "Organisations-Admins" als Batch Auftrag anmelden. gehen Sie hierzu wie folgt vor:  

    1.  Doppelklicken Sie auf **Anmelden als Batch Auftrag verweigern** , und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

        > [!NOTE]  
        > Klicken Sie in einer Gesamtstruktur, die mehrere Domänen enthält, auf **Standorte** , und wählen Sie die Stamm Domäne der Gesamtstruktur aus.  

    3.  Geben Sie **Enterprise Admins**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**.  

        ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_50.gif)  

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .  

9. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der EA-Gruppe sich als Dienst anmelden. gehen Sie hierzu wie folgt vor:  

    1.  Doppelklicken Sie auf **Protokoll als Dienst verweigern** , und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

        > [!NOTE]  
        > Klicken Sie in einer Gesamtstruktur, die mehrere Domänen enthält, auf **Standorte** , und wählen Sie die Stamm Domäne der Gesamtstruktur aus.  

    3.  Geben Sie **Enterprise Admins**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**.  

        ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_51.gif)  

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .  

10. Konfigurieren Sie Benutzerrechte, um zu verhindern, dass sich Mitglieder der Gruppe "Organisations-Admins" lokal bei Mitglieds Servern und Arbeitsstationen anmelden, indem Sie folgende Schritte ausführen:  

    1.  Doppelklicken Sie auf **Lokal anmelden verweigern** , und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

        > [!NOTE]  
        > Klicken Sie in einer Gesamtstruktur, die mehrere Domänen enthält, auf **Standorte** , und wählen Sie die Stamm Domäne der Gesamtstruktur aus.  

    3.  Geben Sie **Enterprise Admins**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**.  

        ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_52.gif)  

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .  

11. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe Organisations-Admins über Remotedesktopdienste auf Mitglieds Server und Arbeitsstationen zugreifen, indem Sie die folgenden Schritte ausführen:  

    1.  Doppelklicken Sie auf **Anmelden über Remotedesktopdienste verweigern** , und wählen Sie **die Option Diese Richtlinien Einstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

        > [!NOTE]  
        > Klicken Sie in einer Gesamtstruktur, die mehrere Domänen enthält, auf **Standorte** , und wählen Sie die Stamm Domäne der Gesamtstruktur aus.  

    3.  Geben Sie **Enterprise Admins**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**.  

        ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_53.gif)  

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .  

12. Um **Gruppenrichtlinienverwaltungs-Editor**zu beenden, klicken Sie auf **Datei**und dann auf **Beenden**.  

13. Verknüpfen Sie das Gruppenrichtlinien Objekt in **Gruppenrichtlinie Management**mit dem Mitglieds Server und Arbeitsstations Organisationseinheiten, indem Sie die folgenden Schritte ausführen:  

    1.  Navigieren Sie zum <Forest>\domains\\<Domain> (wobei <Forest> der Name der Gesamtstruktur und <Domain> der Name der Domäne ist, in der Sie die Gruppenrichtlinie festlegen möchten).  

    2.  Klicken Sie mit der rechten Maustaste auf die Organisationseinheit, auf die das Gruppenrichtlinien Objekt angewendet wird, und klicken Sie auf **vorhandenes GPO verknüpfen**  

        ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_54.gif)  

    3.  Wählen Sie das soeben erstellte Gruppenrichtlinien Objekt aus, und klicken Sie auf **OK**.  

        ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_55.gif)  

    4.  Erstellen Sie Links zu allen anderen Organisationseinheiten, die Arbeitsstationen enthalten.  

    5.  Erstellen Sie Links zu allen anderen Organisationseinheiten, die Mitglieds Server enthalten.  

    6.  In einer Gesamtstruktur, die mehrere Domänen enthält, sollte in jeder Domäne ein ähnliches GPO erstellt werden, in dem die Gruppe Organisations-Admins gesichert werden muss.  

> [!IMPORTANT]  
> Wenn für die Verwaltung von Domänen Controllern und Active Directory Jump-Server verwendet werden, stellen Sie sicher, dass sich die jumpserver in einer Organisationseinheit befinden, mit der diese GPOs nicht verknüpft sind  

### <a name="verification-steps"></a>Überprüfungsschritte  

#### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>GPO-Einstellungen "Zugriff auf diesen Computer über das Netzwerk verweigern"  
Versuchen Sie auf einem Mitglieds Server oder einer Arbeitsstation, der nicht von den GPO-Änderungen (z. b. einem "Sprung Server") betroffen ist, auf einen Mitglieds Server oder eine Arbeitsstation über das Netzwerk zuzugreifen, das von den GPO-Änderungen betroffen ist. Um die GPO-Einstellungen zu überprüfen, versuchen Sie, das Systemlaufwerk mithilfe des **net use** -Befehls zuzuordnen, indem Sie die folgenden Schritte ausführen:  

1.  Melden Sie sich lokal mit einem Konto an, das Mitglied der EA-Gruppe ist.  

2.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

3.  Geben Sie im **Suchfeld** **Eingabeaufforderung**ein, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen** , um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen.  

4.  Wenn Sie aufgefordert werden, die Höhe zu genehmigen, klicken Sie auf **Ja**.  

    ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_56.gif)  

5.  Geben Sie im **Eingabe** Aufforderungs Fenster **net use \\\\\<Server Name\>\c $** ein, wobei \<Servername\> der Name des Mitglieds Servers oder der Arbeitsstation ist, auf den Sie über das Netzwerk zuzugreifen versuchen.  

6.  Der folgende Screenshot zeigt die Fehlermeldung, die angezeigt werden soll.  

    ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_57.gif)  

#### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>"Anmelden als Batch Auftrag verweigern"-GPO-Einstellungen überprüfen  

Melden Sie sich lokal bei allen Mitglieds Servern oder Arbeitsstationen an, die von den GPO-Änderungen betroffen sind.  

##### <a name="create-a-batch-file"></a>Erstellen einer Batch Datei  

1.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

2.  Geben Sie im **Suchfeld den Suchbegriff** **Editor**ein, und klicken Sie auf **Editor**.  

3.  Geben **Sie im Editor**den Befehl **dir c:** ein.  

4.  Klicken Sie auf **Datei**und dann auf **Speichern**unter.  

5.  Geben Sie **File** im Feld Dateiname **<Filename>. bat** ein (wobei <Filename> der Name der neuen Batchdatei ist).  

##### <a name="schedule-a-task"></a>Planen einer Aufgabe  

1.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

2.  Geben Sie im **Suchfeld** den Text **Task Scheduler**ein, und klicken Sie auf **Taskplaner**.  

    > [!NOTE]  
    > Geben Sie auf Computern, auf denen Windows 8 ausgeführt wird, im **Suchfeld** **Schedule Tasks**ein, und klicken Sie auf **Aufgaben planen**.  

3.  Klicken Sie auf **Aktion**, und klicken Sie auf **Task erstellen**.  

4.  Geben Sie im Dialogfeld **Task erstellen** **<Task Name>** ein (wobei <Task Name> der Name der neuen Aufgabe ist).  

5.  Klicken Sie auf die Registerkarte **Aktionen** , und klicken Sie auf **neu**.  

6.  Wählen Sie im Feld **Aktion** die Option **Programm starten**aus.  

7.  Klicken Sie unter **Programm/Skript**auf **Durchsuchen**, suchen Sie die Batchdatei, die Sie im Abschnitt **Erstellen einer Batchdatei** erstellt haben, und klicken Sie auf **Öffnen**.  

8.  Klicken Sie auf **OK**.  

9. Klicken Sie auf die Registerkarte **Allgemein**.  

10. Klicken Sie im Feld **Sicherheitsoptionen** auf **Benutzer oder Gruppe ändern**.  

11. Geben Sie den Namen eines Kontos ein, das Mitglied der EAS-Gruppe ist, klicken Sie auf **Namen überprüfen**, und klicken Sie dann auf **OK**.  

12. Wählen Sie **Ausführen aus, ob der Benutzer angemeldet ist oder nicht** , und wählen Sie **Kennwort nicht speichern**aus. Der Task hat nur Zugriff auf lokale Computerressourcen.  

13. Klicken Sie auf **OK**.  

14. Es wird ein Dialogfeld angezeigt, in dem die Anmelde Informationen des Benutzerkontos zum Ausführen des Tasks angefordert werden.  

15. Klicken Sie nach Eingabe der Anmelde Informationen auf **OK**.  

16. Ein Dialogfeld ähnlich dem folgenden sollte angezeigt werden.  

    ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_58.gif)  

#### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>GPO-Einstellungen "Anmelden als Dienst verweigern" überprüfen  

1.  Melden Sie sich lokal bei allen Mitglieds Servern oder Arbeitsstationen an, die von den GPO-Änderungen betroffen sind.  

2.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

3.  Geben Sie im **Suchfeld den Suchbegriff** **Dienste**ein, und klicken Sie auf **Dienste**.  

4.  Suchen Sie den **Druck Spooler**, und doppelklicken Sie darauf.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  Wählen Sie unter **Anmelden als** **das Konto**aus.  

7.  Klicken Sie auf **Durchsuchen**, geben Sie den Namen eines Kontos ein, das Mitglied der EAS-Gruppe ist, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

8.  Geben Sie unter **Kennwort:** und **Kennwort bestätigen**das Kennwort des ausgewählten Kontos ein, und klicken Sie auf **OK**.  

9. Klicken Sie drei weitere Male auf **OK** .  

10. Klicken Sie mit der rechten Maustaste auf den **Druckspoolerdienst** , und wählen Sie **neu starten**  

11. Wenn der Dienst neu gestartet wird, sollte ein Dialogfeld ähnlich dem folgenden angezeigt werden.  

    ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_59.gif)  

#### <a name="revert-changes-to-the-printer-spooler-service"></a>Änderungen am Druckerspoolerdienst zurücksetzen  

1.  Melden Sie sich lokal bei allen Mitglieds Servern oder Arbeitsstationen an, die von den GPO-Änderungen betroffen sind.  

2.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

3.  Geben Sie im **Suchfeld den Suchbegriff** **Dienste**ein, und klicken Sie auf **Dienste**.  

4.  Suchen Sie den **Druck Spooler**, und doppelklicken Sie darauf.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  Wählen Sie unter **Anmelden als**das Konto **Lokales System** aus, und klicken Sie auf **OK**.  

#### <a name="verify-deny-log-on-locally-gpo-settings"></a>GPO-Einstellungen "Lokal anmelden verweigern"  

1.  Versuchen Sie, sich lokal mithilfe eines Kontos, das Mitglied der EA-Gruppe ist, von einem von den GPO-Änderungen betroffenen Mitglieds Server oder Arbeitsplatz anzumelden. Ein Dialogfeld ähnlich dem folgenden sollte angezeigt werden.  

    ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_60.gif)  

#### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>Überprüfen der GPO-Einstellungen "Anmelden über Remotedesktopdienste verweigern"  

1.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

2.  Geben Sie im **Suchfeld als Suchbegriff** **Remote Desktop Verbindung**ein, und klicken Sie dann auf **Remotedesktopverbindung**.  

3.  Geben Sie im Feld **Computer** den Namen des Computers ein, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **verbinden**. (Sie können auch die IP-Adresse anstelle des Computer namens eingeben.)  

4.  Wenn Sie dazu aufgefordert werden, geben Sie die Anmelde Informationen für ein Konto an, das Mitglied der EA-Gruppe ist.  

5.  Ein Dialogfeld ähnlich dem folgenden sollte angezeigt werden.  

    ![sichere Unternehmens Administratoren Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_61.gif)  
