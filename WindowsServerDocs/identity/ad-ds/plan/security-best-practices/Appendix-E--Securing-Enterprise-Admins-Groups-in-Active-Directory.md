---
ms.assetid: f643099e-f9c6-476f-9378-5a9228c39b33
title: Anhang E – Schützen von Organisationsadministratorgruppen in Active Directory
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 976eb8c7159c8349b72bee05a5248b5cc116d96b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856721"
---
# <a name="appendix-e-securing-enterprise-admins-groups-in-active-directory"></a>Anhang E: Schützen von Organisationsadministratorgruppen in Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-e-securing-enterprise-admins-groups-in-active-directory"></a>Anhang E: Schützen von Organisationsadministratorgruppen in Active Directory  
Enterprise-Administratoren (EA) enthält die Gruppe, die Stammdomäne der Gesamtstruktur ausgeführt wird, sollten keine Benutzer für den täglichen, mit Ausnahme des Administratorkontos für die Stammdomäne, vorausgesetzt es geschützt ist, wie in beschrieben [Anhang D: Schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  

Organisations-Admins sind standardmäßig Mitglieder der Gruppe "Administratoren" in jeder Domäne in der Gesamtstruktur. Sie sollten der Gruppe "EA" nicht aus der Gruppe "Administratoren" in jeder Domäne entfernen, da bei einem Notfallwiederherstellungsszenario für die Gesamtstruktur, EA-Rechte wahrscheinlich benötigt werden. Die Gesamtstruktur der Organisations-Admins muss geschützt werden, finden Sie in den schrittweisen Anleitungen.  

Für die Organisations-Admins-Gruppe in der Gesamtstruktur:  

1.  In Gruppenrichtlinienobjekten, die mit den Organisationseinheiten mit MemberServer und Arbeitsstationen in jeder Domäne verknüpft ist, der Gruppe Organisations-Admins hinzugefügt werden sollen in der folgenden Benutzerrechte **Computer Computerkonfiguration\Richtlinien\Windows unter Sicherheitseinstellungen\Lokale Policies\ Zuweisen von Benutzerrechten**:  

    -   Zugriff vom Netzwerk auf diesen Computer verweigern  

    -   Anmelden als Batchauftrag verweigern  

    -   Anmelden als Dienst verweigern  

    -   Lokal anmelden verweigern  

    -   Anmelden über Remotedesktopdienste verweigern  

2.  Konfigurieren der Überwachung, die zum Senden von Warnungen, wenn keine Änderungen, um die Eigenschaften oder die Mitgliedschaft der Gruppe "Organisations-Admins vorgenommen werden".  

### <a name="step-by-step-instructions-for-removing-all-members-from-the-enterprise-admins-group"></a>Schrittweise Anleitungen zum Entfernen aller Elemente aus der Enterprise-Administratoren-Gruppe  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Active Directory-Benutzer und-Computer**.  

2.  Wenn Sie nicht die Stammdomäne für die Gesamtstruktur, in der Konsolenstruktur verwalten mit der rechten Maustaste <Domain>, und klicken Sie dann auf **Domäne ändern** (, in denen <Domain> ist der Name der Domäne sind Sie gerade verwalten).  

    ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_43.gif)  

3.  In der **Domäne ändern** Dialogfeld klicken Sie auf **Durchsuchen**, wählen Sie die für die Gesamtstruktur-Stammdomäne, und klicken Sie auf **OK**.  

    ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_44.gif)  

4.  So entfernen alle Elemente aus der Gruppe "EA":  

    1.  Doppelklicken Sie auf die **Organisations-Admins** gruppieren, und klicken Sie dann auf die **Mitglieder** Registerkarte.  

        ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_45.gif)  

    2.  Wählen Sie ein Mitglied der Gruppe aus, klicken Sie auf **entfernen**, klicken Sie auf **Ja**, und klicken Sie auf **OK**.  

5.  Wiederholen Sie Schritt 2, bis alle Mitglieder der Gruppe "EA" entfernt wurden.  

### <a name="step-by-step-instructions-to-secure-enterprise-admins-in-active-directory"></a>Schrittweise Anweisungen zum Sichern der Organisations-Admins in Active Directory  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Gruppenrichtlinienverwaltung**.  

2.  Erweitern Sie in der Konsolenstruktur <Forest>\Domains\\<Domain>, und klicken Sie dann **Group Policy Objects** (wo <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, wo Sie möchten, Legen Sie die Gruppenrichtlinie).  

    > [!NOTE]  
    > In einer Gesamtstruktur, die mehrere Domänen enthält, sollte eine ähnliche GPO in jeder Domäne erstellt werden, die erfordert, dass die Gruppe "Unternehmensadministratoren" gesichert werden.  

3.  In der Konsolenstruktur mit der Maustaste **Group Policy Objects**, und klicken Sie auf **neu**.  

    ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_46.gif)  

4.  In der **neues Gruppenrichtlinienobjekt** (Dialogfeld), Typ <GPO Name>, und klicken Sie auf **OK** (, in denen <GPO Name> ist der Name des dieses Gruppenrichtlinienobjekt).  

    ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_47.gif)  

5.  Klicken Sie im Detailbereich mit der Maustaste <GPO Name>, und klicken Sie auf **bearbeiten**.  

6.  Navigieren Sie zu **Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, und klicken Sie auf **Zuweisen von Benutzerrechten**.  

    ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_48.gif)  

7.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass die Mitglieder der Gruppe "Organisations-Admins" MemberServer und Arbeitsstationen über das Netzwerk zugreifen, wie folgt:  

    1.  Doppelklicken Sie auf **Zugriff vom Netzwerk auf diesen Computer Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Organisations-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_49.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

8.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass die Mitglieder der Gruppe "Organisations-Admins" Anmelden als Stapelverarbeitungsauftrag wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Batchauftrag verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

        > [!NOTE]  
        > In einer Gesamtstruktur, die mehrere Domänen enthält, klicken Sie auf **Speicherorte** , und wählen Sie die Stammdomäne der Gesamtstruktur.  

    3.  Typ **Organisations-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_50.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

9. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass die Mitglieder der Gruppe "EA" Anmelden als Dienst wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Dienst verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie dann auf **Durchsuchen**.  

        > [!NOTE]  
        > In einer Gesamtstruktur, die mehrere Domänen enthält, klicken Sie auf **Speicherorte** , und wählen Sie die Stammdomäne der Gesamtstruktur.  

    3.  Typ **Organisations-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_51.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

10. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass die Mitglieder der Gruppe "Organisations-Admins" lokal anmelden können MemberServer und Arbeitsstationen wie folgt:  

    1.  Doppelklicken Sie auf **lokal anmelden verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie dann auf **Durchsuchen**.  

        > [!NOTE]  
        > In einer Gesamtstruktur, die mehrere Domänen enthält, klicken Sie auf **Speicherorte** , und wählen Sie die Stammdomäne der Gesamtstruktur.  

    3.  Typ **Organisations-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_52.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

11. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass die Mitglieder der Gruppe "Organisations-Admins" zugreifen auf MemberServer und Arbeitsstationen über Remote Desktop Services wie folgt vorgehen:  

    1.  Doppelklicken Sie auf **anmelden über Remotedesktopdienste Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie dann auf **Durchsuchen**.  

        > [!NOTE]  
        > In einer Gesamtstruktur, die mehrere Domänen enthält, klicken Sie auf **Speicherorte** , und wählen Sie die Stammdomäne der Gesamtstruktur.  

    3.  Typ **Organisations-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_53.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

12. Zum Beenden **Gruppenrichtlinienverwaltungs-Editor**, klicken Sie auf **Datei**, und klicken Sie auf **beenden**.  

13. In **Gruppenrichtlinienverwaltung**, verknüpfen Sie das Gruppenrichtlinienobjekt auf dem Mitgliedsserver und die Arbeitsstation Organisationseinheiten wie folgt:  

    1.  Navigieren Sie zu der <Forest>\Domains\\ <Domain> (wobei <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, in dem Sie die Gruppenrichtlinie festlegen möchten).  

    2.  Mit der rechten Maustaste in der Organisationseinheit, die das Gruppenrichtlinienobjekt wird auf angewendet werden, und klicken Sie auf **vorhandenes Gruppenrichtlinienobjekt verknüpfen**.  

        ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_54.gif)  

    3.  Wählen Sie das Gruppenrichtlinienobjekt, das Sie gerade erstellt haben, und klicken Sie auf **OK**.  

        ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_55.gif)  

    4.  Erstellen Sie Links zu allen anderen Organisationseinheiten, die Arbeitsstationen enthalten.  

    5.  Erstellen Sie Verknüpfungen mit allen anderen Organisationseinheiten, die Member-Server enthalten.  

    6.  In einer Gesamtstruktur, die mehrere Domänen enthält, sollte eine ähnliche GPO in jeder Domäne erstellt werden, die erfordert, dass die Gruppe "Unternehmensadministratoren" gesichert werden.  

> [!IMPORTANT]  
> Jump-Server zum Verwalten von Domänencontrollern und Active Directory verwendet werden, sicher, dass Jump-Server befinden, in einer Organisationseinheit, zu dem dieser Gruppenrichtlinienobjekte nicht verknüpft ist.  

### <a name="verification-steps"></a>Überprüfungsschritte  

#### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen für "Zugriff auf diesen Computer vom Netzwerk verweigern"  
Versuchen Sie von jeder Mitgliedsserver oder Arbeitsstation, die durch die GPO-Änderungen (z. B. ein "sprungbrettserver") nicht beeinträchtigt ist, auf einem Mitgliedsserver oder Arbeitsstation über das Netzwerk zugreifen, die die GPO-Änderungen betroffen ist. Um die GPO-Einstellungen zu überprüfen, versuchen, auf das Systemlaufwerk Zuordnung von der **NET USE** Befehl die folgenden Schritte ausführen:  

1.  Melden Sie sich lokal mit einem Konto an, die ein Mitglied der Gruppe "EA" ist.  

2.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Eingabeaufforderung**, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen** zu einer mit erhöhten Rechten öffnen. -Eingabeaufforderung.  

4.  Wenn Sie dazu aufgefordert werden, die Erhöhung zustimmen, klicken Sie auf **Ja**.  

    ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_56.gif)  

5.  In der **Eingabeaufforderung** geben **net verwenden \\ \\ \<Servernamen\>\c$**, wobei \<Servernamen\> ist die Der Name der Mitgliedsserver oder Arbeitsstation, die Sie versuchen, über das Netzwerk zugreifen.  

6.  Der folgende Screenshot zeigt die Fehlermeldung, die angezeigt werden soll.  

    ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_57.gif)  

#### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Batchauftrag verweigern"  

Melden Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind sich lokal.  

##### <a name="create-a-batch-file"></a>Erstellen Sie eine Datei  

1.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Editor**, und klicken Sie auf **Editor**.  

3.  In **Editor**, Typ **Dir c:**.  

4.  Klicken Sie auf **Datei**, und klicken Sie auf **speichern**.  

5.  In der **Datei** , geben Sie Namen im  **<Filename>bat** (wobei <Filename> ist der Name der neuen Batchdatei).  

##### <a name="schedule-a-task"></a>Planen einer Aufgabe  

1.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Taskplaner**, und klicken Sie auf **Taskplaner**.  

    > [!NOTE]  
    > Auf Computern Windows 8 ausgeführt wird, in der **Suche** geben **Planen von Aufgaben**, und klicken Sie auf **Planen von Aufgaben**.  

3.  Klicken Sie auf **Aktion**, und klicken Sie auf **Create Task**.  

4.  In der **Create Task** (Dialogfeld), Typ **<Task Name>** (, in denen <Task Name> ist der Name der neuen Aufgabe).  

5.  Klicken Sie auf die **Aktionen** Registerkarte, und klicken Sie auf **neu**.  

6.  In der **Aktion** die Option **ein Programm starten**.  

7.  Unter **Programm/Skript**, klicken Sie auf **Durchsuchen**, und wählen Sie die Batchdatei erstellt, der **eine Batchdatei erstellen** aus, und klicken Sie auf **öffnen**.  

8.  Klicken Sie auf **OK**.  

9. Klicken Sie auf die Registerkarte **Allgemein**.  

10. In der **Sicherheitsoptionen** auf **Benutzer oder Gruppe ändern**.  

11. Geben Sie den Namen eines Kontos, das ein Mitglied der EAs-Gruppe ist, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

12. Wählen Sie **ausgeführt wird, ob der Benutzer oder nicht angemeldet ist** , und wählen Sie **speichern Sie das Kennwort nicht**. Der Task wird nur auf lokale Computerressourcen zugreifen.  

13. Klicken Sie auf **OK**.  

14. Es sollte ein Dialogfeld angezeigt, die Anmeldeinformationen für anfordernden Benutzerkonto zum Ausführen des Tasks.  

15. Klicken Sie nach Eingabe der Anmeldeinformationen an, auf **OK**.  

16. Ein Dialogfeld ähnlich der folgenden sollte angezeigt werden.  

    ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_58.gif)  

#### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Dienst verweigern"  

1.  Melden Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind sich lokal.  

2.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Services**, und klicken Sie auf **Services**.  

4.  Doppelklicken Sie auf die **Druckspooler**.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  Klicken Sie unter **melden Sie sich als**Option **dieses Konto**.  

7.  Klicken Sie auf **Durchsuchen**, geben Sie den Namen eines Kontos, das ein Mitglied der EAs-Gruppe ist, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

8.  Klicken Sie unter **Kennwort:** und **Bestätigungskennwort**, geben Sie das ausgewählte Konto-Kennwort ein, und klicken Sie auf **OK**.  

9. Klicken Sie auf **OK** drei weitere Male.  

10. Mit der rechten Maustaste die **Druckspooler** service, und wählen Sie **Neustart**.  

11. Wenn der Dienst neu gestartet wird, wird ein Dialogfeld ähnlich der folgenden sollte angezeigt werden.  

    ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_59.gif)  

#### <a name="revert-changes-to-the-printer-spooler-service"></a>Wiederherstellen von Änderungen an den Druckerwarteschlangendienst  

1.  Melden Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind sich lokal.  

2.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Services**, und klicken Sie auf **Services**.  

4.  Doppelklicken Sie auf die **Druckspooler**.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  Klicken Sie unter **melden Sie sich als**, wählen die **Lokales System** -Konto, und klicken Sie auf **OK**.  

#### <a name="verify-deny-log-on-locally-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Lokal anmelden verweigern"  

1.  Versuchen Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind melden Sie sich lokal mit einem Konto, ein Mitglied der Gruppe "EA" ist. Ein Dialogfeld ähnlich der folgenden sollte angezeigt werden.  

    ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_60.gif)  

#### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden über Remotedesktopdienste verweigern"  

1.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Remotedesktopverbindung**, und klicken Sie dann auf **Remotedesktopverbindung**.  

3.  In der **Computer** Feld, geben Sie den Namen des Computers ein, die Sie verwenden möchten, Herstellen einer Verbindung mit, und klicken Sie dann auf **Connect**. (Sie können auch die IP-Adresse anstelle des Computernamens eingeben.)  

4.  Wenn Sie aufgefordert werden, geben Sie Anmeldeinformationen für ein Konto, das ein Mitglied der Gruppe "EA" ist ein.  

5.  Ein Dialogfeld ähnlich der folgenden sollte angezeigt werden.  

    ![Sichern von Enterprise-Gruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_61.gif)  
