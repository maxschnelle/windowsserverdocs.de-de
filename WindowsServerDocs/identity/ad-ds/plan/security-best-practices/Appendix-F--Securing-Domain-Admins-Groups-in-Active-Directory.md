---
ms.assetid: 017b88a6-f29b-4787-99b6-b5c8eaf8c3df
title: 'Anhang F: Schützen von Domänenadministratorgruppen in Active Directory'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1f35503d1f02d616255c067fbc1750a0cab974cc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880141"
---
# <a name="appendix-f-securing-domain-admins-groups-in-active-directory"></a>Anhang F: Schützen von Domänenadministratorgruppen in Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-f-securing-domain-admins-groups-in-active-directory"></a>Anhang F: Schützen von Domänenadministratorgruppen in Active Directory  
Wie bei der Gruppe Unternehmens-Admins (EA) der Fall ist, sollte die Mitgliedschaft in der Gruppe Domänen-Admins (DA) nur in Build oder Notfallwiederherstellungsszenarios erforderlich sein. Dürfte keine täglich verwendeten Benutzerkonten in der Gruppe "Daten" mit Ausnahme von dem integrierten Administratorkonto an, für die Domäne, wenn sie gesichert wurde wie in beschrieben [Anhang D: Schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  

Domänen-Admins sind standardmäßig Mitglieder der lokalen Administratorengruppe auf allen Servern und Arbeitsstationen in ihren jeweiligen Domänen. Diese Standard-Schachtelung sollte für unterstützbarkeit und notfallwiederherstellung nicht geändert werden. Wenn Domänen-Admins aus der lokalen Administratorengruppe auf dem Mitgliedsserver entfernt wurden, sollte die Gruppe "Administratoren" auf jedem Mitgliedsserver und die Arbeitsstation in der Domäne die Gruppe hinzugefügt werden. Jede Domäne in der Gruppe "Domänenadministratoren" sollten gesichert werden, wie in den folgenden schrittweisen Anleitungen beschrieben.  

Für die Gruppe "Domänenadministratoren" in jeder Domäne in der Gesamtstruktur:  

1.  Entfernen Sie alle Mitglieder aus der Gruppe mit Ausnahme des integrierten Administratorkontos für die Domäne, vorausgesetzt sie gesichert wurden unter [Anhang D: Schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  

2.  In Gruppenrichtlinienobjekten, die mit den Organisationseinheiten mit MemberServer und Arbeitsstationen in jeder Domäne verknüpft werden, DA Gruppe hinzugefügt werden sollen in der folgenden Benutzerrechte **Computer Computerkonfiguration\Richtlinien\Windows unter Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten Zuweisungen**:  

    -   Zugriff vom Netzwerk auf diesen Computer verweigern  

    -   Anmelden als Batchauftrag verweigern  

    -   Anmelden als Dienst verweigern  

    -   Lokal anmelden verweigern  

    -   Verweigern Sie anmelden über Remotedesktopdienste Benutzerrechte  

3.  Überwachung muss konfiguriert werden, um Warnungen zu senden, wenn keine Änderungen, um die Eigenschaften oder die Mitgliedschaft der Gruppe "Domänen-Admins vorgenommen werden".  

#### <a name="step-by-step-instructions-for-removing-all-members-from-the-domain-admins-group"></a>Schrittweise Anleitungen zum Entfernen aller Elemente aus der Gruppe der Domänen-Admins  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Active Directory-Benutzer und-Computer**.  

2.  Um alle Elemente aus der Gruppe "Daten" zu entfernen, führen Sie die folgenden Schritte aus:  

    1.  Doppelklicken Sie auf die **Domänen-Admins** gruppieren, und klicken Sie auf die **Mitglieder** Registerkarte.  

        ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_62.gif)  

    2.  Wählen Sie ein Mitglied der Gruppe aus, klicken Sie auf **entfernen**, klicken Sie auf **Ja**, und klicken Sie auf **OK**.  

3.  Wiederholen Sie Schritt 2, bis alle Mitglieder der Gruppe "Daten" entfernt wurden.  

#### <a name="step-by-step-instructions-to-secure-domain-admins-in-active-directory"></a>Schrittweise Anweisungen zum Sichern der Domänen-Admins in Active Directory  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Gruppenrichtlinienverwaltung**.  

2.  Erweitern Sie in der Konsolenstruktur \<Gesamtstruktur\>\\Domänen\\\<Domäne\>, und klicken Sie dann **Group Policy Objects** (wobei \<Gesamtstruktur\> ist der Name der Gesamtstruktur und \<Domäne\> ist der Name der Domäne, in dem die Gruppenrichtlinie festgelegt werden sollen).  

3.  In der Konsolenstruktur mit der Maustaste **Group Policy Objects**, und klicken Sie auf **neu**.  

    ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_63.gif)  

4.  In der **neues Gruppenrichtlinienobjekt** (Dialogfeld), geben \<Gruppenrichtlinienobjektname\>, und klicken Sie auf **OK** (, in denen \<GPO-Name\> ist der Name des dieses Gruppenrichtlinienobjekt).  

    ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_64.gif)  

5.  Klicken Sie im Detailbereich mit der Maustaste \<Gruppenrichtlinienobjektname\>, und klicken Sie auf **bearbeiten**.  

6.  Navigieren Sie zu **Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, und klicken Sie auf **Zuweisen von Benutzerrechten**.  

    ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_65.gif)  

7.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass die Mitglieder der Gruppe "Domänen-Admins" zugreifen auf Member-Servern und Arbeitsstationen über das Netzwerk wie folgt vorgehen:  

    1.  Doppelklicken Sie auf **Zugriff vom Netzwerk auf diesen Computer Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Domänen-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_66.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

8.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass die Mitglieder der Gruppe "Daten" Anmelden als Stapelverarbeitungsauftrag wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Batchauftrag verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Domänen-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_67.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

9. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass die Mitglieder der Gruppe "Daten" Anmelden als Dienst wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Dienst verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Domänen-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_68.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

10. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass die Mitglieder der Gruppe "Domänen-Admins" lokal anmelden können MemberServer und Arbeitsstationen wie folgt:  

    1.  Doppelklicken Sie auf **lokal anmelden verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Domänen-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_69.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

11. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass die Mitglieder der Gruppe "Domänen-Admins" zugreifen auf MemberServer und Arbeitsstationen über Remote Desktop Services wie folgt vorgehen:  

    1.  Doppelklicken Sie auf **anmelden über Remotedesktopdienste Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Domänen-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_70.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

12. Zum Beenden **Gruppenrichtlinienverwaltungs-Editor**, klicken Sie auf **Datei**, und klicken Sie auf **beenden**.  

13. Verknüpfen Sie das Gruppenrichtlinienobjekt in der Gruppenrichtlinien-Verwaltungskonsole auf die Member-Server und Arbeitsstation Organisationseinheiten wie folgt:  

    1.  Navigieren Sie zu der \<Gesamtstruktur\>\Domains\\\<Domäne\> (wo \<Gesamtstruktur\> ist der Name der Gesamtstruktur und \<Domäne\> ist der Name des die Domäne, in dem die Gruppenrichtlinie festgelegt werden sollen).  

    2.  Mit der rechten Maustaste in der Organisationseinheit, die das Gruppenrichtlinienobjekt wird auf angewendet werden, und klicken Sie auf **vorhandenes Gruppenrichtlinienobjekt verknüpfen**.  

        ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_71.gif)  

    3.  Wählen Sie das Gruppenrichtlinienobjekt, das Sie gerade erstellt haben, und klicken Sie auf **OK**.  

        ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_72.gif)  

    4.  Erstellen Sie Links zu allen anderen Organisationseinheiten, die Arbeitsstationen enthalten.  

    5.  Erstellen Sie Verknüpfungen mit allen anderen Organisationseinheiten, die Member-Server enthalten.  

        > [!IMPORTANT]  
        > Jump-Server zum Verwalten von Domänencontrollern und Active Directory verwendet werden, sicher, dass Jump-Server befinden, in einer Organisationseinheit, zu dem dieser Gruppenrichtlinienobjekte nicht verknüpft ist.  

#### <a name="verification-steps"></a>Überprüfungsschritte  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen für "Zugriff auf diesen Computer vom Netzwerk verweigern"  
Versuchen Sie von jeder Mitgliedsserver oder Arbeitsstation, die durch die GPO-Änderungen (z. B. ein "sprungbrettserver") nicht beeinträchtigt ist, auf einem Mitgliedsserver oder Arbeitsstation über das Netzwerk zugreifen, die die GPO-Änderungen betroffen ist. Um die GPO-Einstellungen zu überprüfen, versuchen, auf das Systemlaufwerk Zuordnung von der **NET USE** Befehl.  

1.  Melden Sie sich lokal mit einem Konto an, das Mitglied der Gruppe "Domänen-Admins" ist.  

2.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Eingabeaufforderung**, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen** zu einer mit erhöhten Rechten öffnen. -Eingabeaufforderung.  

4.  Wenn Sie dazu aufgefordert werden, die Erhöhung zustimmen, klicken Sie auf **Ja**.  

    ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_73.gif)  

5.  In der **Eingabeaufforderung** geben **net verwenden \\ \\ \<Servernamen\>\c$**, wobei \<Servernamen\> ist die Der Name der Mitgliedsserver oder Arbeitsstation, die Sie versuchen, über das Netzwerk zugreifen.  

6.  Der folgende Screenshot zeigt die Fehlermeldung, die angezeigt werden soll.  

    ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_74.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Batchauftrag verweigern"  

Melden Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind sich lokal.  

###### <a name="create-a-batch-file"></a>Erstellen Sie eine Datei  

1.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Editor**, und klicken Sie auf **Editor**.  

3.  In **Editor**, Typ **Dir c:**.  

4.  Klicken Sie auf **Datei**, und klicken Sie auf **speichern**.  

5.  In der **Datei** Feld "Name", Typ  **\<Filename\>bat** (, in denen \<Filename\> ist der Name der neuen Batchdatei).  

###### <a name="schedule-a-task"></a>Planen einer Aufgabe  

1.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Taskplaner**, und klicken Sie auf **Taskplaner**.  

    > [!NOTE]  
    > Auf Computern Windows 8 ausgeführt wird, in der **Suche** geben **Planen von Aufgaben**, und klicken Sie auf **Planen von Aufgaben**.  

3.  In der **Taskplaner** Menüleiste, klicken Sie auf **Aktion**, und klicken Sie auf **Create Task**.  

4.  In der **Task erstellen** (Dialogfeld), Typ **\<Taskname\>** (, in dem \<Taskname\> ist der Name der neuen Aufgabe).  

5.  Klicken Sie auf die **Aktionen** Registerkarte, und klicken Sie auf **neu**.  

6.  In der **Aktion** die Option **ein Programm starten**.  

7.  Unter **Programm/Skript**, klicken Sie auf **Durchsuchen**, und wählen Sie die Batchdatei erstellt, der **eine Batchdatei erstellen** aus, und klicken Sie auf **öffnen**.  

8.  Klicken Sie auf **OK**.  

9. Klicken Sie auf die Registerkarte **Allgemein**.  

10. Klicken Sie unter **Sicherheit** Optionen klicken Sie auf **Benutzer oder Gruppe ändern**.  

11. Geben Sie den Namen eines Kontos, das Mitglied der Gruppe "Domänen-Admins" ist, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

12. Wählen Sie **ausgeführt wird, ob der Benutzer oder nicht angemeldet ist** , und wählen Sie **speichern Sie das Kennwort nicht**. Der Task wird nur auf lokale Computerressourcen zugreifen.  

13. Klicken Sie auf **OK**.  

14. Es sollte ein Dialogfeld angezeigt, die Anmeldeinformationen für anfordernden Benutzerkonto zum Ausführen des Tasks.  

15. Klicken Sie nach Eingabe der Anmeldeinformationen an, auf **OK**.  

16. Ein Dialogfeld ähnlich der folgenden sollte angezeigt werden.  

    ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_75.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Dienst verweigern"  

1.  Melden Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind sich lokal.  

2.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Services**, und klicken Sie auf **Services**.  

4.  Doppelklicken Sie auf die **Druckspooler**.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  Klicken Sie unter **melden Sie sich als**, wählen die **dieses Konto** Option.  

7.  Klicken Sie auf **Durchsuchen**, geben Sie den Namen eines Kontos, das Mitglied der Gruppe "Domänen-Admins" ist, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

8.  Klicken Sie unter **Kennwort** und **Bestätigungskennwort**, geben Sie das ausgewählte Konto-Kennwort ein, und klicken Sie auf **OK**.  

9. Klicken Sie auf **OK** drei weitere Male.  

10. Mit der rechten Maustaste **Druckspooler** , und klicken Sie auf **Neustart**.  

11. Wenn der Dienst neu gestartet wird, wird ein Dialogfeld ähnlich der folgenden sollte angezeigt werden.  

    ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_76.gif)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>Wiederherstellen von Änderungen an den Druckerwarteschlangendienst  

1.  Melden Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind sich lokal.  

2.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Services**, und klicken Sie auf **Services**.  

4.  Doppelklicken Sie auf die **Druckspooler**.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  Klicken Sie unter **melden Sie sich als**, wählen die **Lokales System** -Konto, und klicken Sie auf **OK**.  

##### <a name="verify-deny-log-on-locally-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Lokal anmelden verweigern"  

1.  Versuchen Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind melden Sie sich lokal mit einem Konto an, das Mitglied der Gruppe "Domänen-Admins" ist. Ein Dialogfeld ähnlich der folgenden sollte angezeigt werden.  

    ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_77.gif)  

##### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden über Remotedesktopdienste verweigern"    
1.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Remotedesktopverbindung**, und klicken Sie auf **Remotedesktopverbindung**.  

3.  In der **Computer** Feld, geben Sie den Namen des Computers ein, die Sie verwenden möchten, Herstellen einer Verbindung mit, und klicken Sie auf **Connect**. (Sie können auch die IP-Adresse anstelle des Computernamens eingeben.)  

4.  Wenn Sie aufgefordert werden, geben Sie Anmeldeinformationen für ein Konto, das Mitglied der Gruppe "Domänen-Admins" ist ein.  

5.  Ein Dialogfeld ähnlich der folgenden sollte angezeigt werden.  

    ![Secure Admin-Domänengruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_78.gif)  
