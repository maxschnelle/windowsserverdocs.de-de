---
ms.assetid: f643099e-f9c6-476f-9378-5a9228c39b33
title: "Anhang E - Schützen von Organisationsadministratorgruppen in Active Directory"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 714bc0ab3fe15d09f4ccabb3f35d9b4519e5459c
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="appendix-e-securing-enterprise-admins-groups-in-active-directory"></a>Anhang E: Schützen von Organisationsadministratorgruppen in Active Directory

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012


## <a name="appendix-e-securing-enterprise-admins-groups-in-active-directory"></a>Anhang E: Schützen von Organisationsadministratorgruppen in Active Directory  
Die Gruppe Organisations-Admins (EA), die in der Gesamtstruktur-Stammdomäne untergebracht ist, sollte keine Benutzer täglich, mit Ausnahme der Administratorkonto der Stammdomäne enthalten, sofern er gesichert ist, siehe [Anhang D: schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  

Organisations-Admins sind standardmäßig Mitglieder der Gruppe "Administratoren" in jeder Domäne in der Gesamtstruktur. Sie sollten nicht die EA-Gruppe aus den Gruppen "Administratoren" in jeder Domäne entfernen, da im Falle einer Gesamtstruktur notfallwiederherstellungs-Szenario EA-Rechte werden wahrscheinlich aufgefordert werden. Organisations-Admins der Gesamtstruktur sollten geschützt werden entsprechend den Details in der schrittweisen Anleitung, die folgen.  

Für die Gruppe "Organisations-Admins" in der Gesamtstruktur:  

1.  Auf Mitgliedsservern und Arbeitsstationen in jeder Domäne mit Organisationseinheiten verknüpften Gruppenrichtlinienobjekten, die Organisations-Admins hinzugefügt werden sollen die folgenden Benutzerrechte in **Computer Computerkonfiguration\Richtlinien\Windows Settings\Security Einstellungen\Sicherheitseinstellungen\Lokale Einstellungen\Benutzername\Lokale Rechte Zuweisungen**:  

    -   Zugriff vom Netzwerk auf diesen Computer verweigern  

    -   Anmelden als Batchauftrag verweigern  

    -   Anmelden als Dienst verweigern  

    -   Lokal anmelden verweigern  

    -   Anmelden über Remotedesktopdienste verweigern  

2.  Konfigurieren der Überwachung, um Warnungen zu senden, wenn Änderungen an die Eigenschaften oder Mitglied der Gruppe "Organisations-Admins" vorgenommen werden.  

### <a name="step-by-step-instructions-for-removing-all-members-from-the-enterprise-admins-group"></a>Eine schrittweise Anleitung zum Entfernen aller Elemente aus der Gruppe Organisations-Admins  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Active Directory-Benutzer und-Computer**.  

2.  Wenn Sie nicht die Stammdomäne für die Gesamtstruktur, in der Konsolenstruktur verwalten mit der rechten Maustaste <Domain>, und klicken Sie dann auf **Domäne ändern** (, in denen <Domain> ist der Name der Domäne haben Sie gerade verwalten).  

    ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_43.gif)  

3.  In der **Domäne ändern** Dialogfeld, klicken Sie auf **Durchsuchen**, auswählen die Stammdomäne der Gesamtstruktur, und klicken Sie auf **OK**.  

    ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_44.gif)  

4.  So entfernen Sie alle Mitglieder aus der EA-Gruppe  

    1.  Doppelklicken Sie auf die **Organisations-Admins** Gruppe, und klicken Sie dann auf die **Mitglieder** Registerkarte.  

        ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_45.gif)  

    2.  Wählen Sie ein Mitglied der Gruppe aus, klicken Sie auf **entfernen**, klicken Sie auf **Ja**, und klicken Sie auf **OK**.  

5.  Wiederholen Sie Schritt 2, bis alle Mitglieder der Gruppe EA entfernt wurden.  

### <a name="step-by-step-instructions-to-secure-enterprise-admins-in-active-directory"></a>Eine schrittweise Anleitung zum Sichern der Organisations-Admins in Active Directory  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Gruppenrichtlinienverwaltung**.  

2.  Erweitern Sie in der Konsolenstruktur <Forest>\Domains\\<Domain>, und klicken Sie dann **Group Policy Objects** (wo <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, in dem Sie die Gruppenrichtlinie festlegen möchten).  

    > [!NOTE]  
    > In einer Gesamtstruktur mit mehreren Domänen, sollte eine ähnliche GPO in jeder Domäne erstellt werden, die erfordert, dass die Gruppe "Organisations-Admins" geschützt werden.  

3.  In der Konsolenstruktur mit der rechten Maustaste **Group Policy Objects**, und klicken Sie auf **neu**.  

    ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_46.gif)  

4.  In der **neues Gruppenrichtlinienobjekt** , geben Sie im Dialogfeld <GPO Name>, und klicken Sie auf **OK** (wo <GPO Name> ist der Name des dieses Gruppenrichtlinienobjekt).  

    ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_47.gif)  

5.  Klicken Sie im Detailbereich mit der rechten Maustaste <GPO Name>, und klicken Sie auf **bearbeiten**.  

6.  Navigieren Sie zu **Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, und klicken Sie auf **Zuweisen von Benutzerrechten**.  

    ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_48.gif)  

7.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe Organisations-Admins den Zugriff auf Mitgliedsservern und Arbeitsstationen über das Netzwerk wie folgt:  

    1.  Doppelklicken Sie auf **Zugriff vom Netzwerk auf diesen Computer Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Organisations-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_49.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

8.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe "Organisations-Admins" Anmelden als Stapelverarbeitungsauftrag wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Batchauftrag verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

        > [!NOTE]  
        > Klicken Sie in einer Gesamtstruktur mit mehreren Domänen, auf **Speicherorte** und auswählen die Stammdomäne der Gesamtstruktur.  

    3.  Typ **Organisations-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_50.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

9. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe der EA Anmelden als Dienst wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Dienst verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie dann auf **Durchsuchen**.  

        > [!NOTE]  
        > Klicken Sie in einer Gesamtstruktur mit mehreren Domänen, auf **Speicherorte** und auswählen die Stammdomäne der Gesamtstruktur.  

    3.  Typ **Organisations-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_51.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

10. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe "Organisations-Admins" lokal anmelden können Mitgliedsservern und Arbeitsstationen, indem Sie Folgendes tun:  

    1.  Doppelklicken Sie auf **lokal anmelden verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie dann auf **Durchsuchen**.  

        > [!NOTE]  
        > Klicken Sie in einer Gesamtstruktur mit mehreren Domänen, auf **Speicherorte** und auswählen die Stammdomäne der Gesamtstruktur.  

    3.  Typ **Organisations-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_52.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

11. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe Organisations-Admins den Zugriff auf Mitgliedsservern und Arbeitsstationen über Remote Desktop Services wie folgt:  

    1.  Doppelklicken Sie auf **anmelden über Remotedesktopdienste Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie dann auf **Durchsuchen**.  

        > [!NOTE]  
        > Klicken Sie in einer Gesamtstruktur mit mehreren Domänen, auf **Speicherorte** und auswählen die Stammdomäne der Gesamtstruktur.  

    3.  Typ **Organisations-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_53.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

12. Zum Beenden **Gruppenrichtlinienverwaltungs-Editor**, klicken Sie auf **Datei**, und klicken Sie auf **beenden**.  

13. In **Gruppenrichtlinienverwaltung**, verknüpfen Sie das Gruppenrichtlinienobjekt auf dem Mitgliedsserver und Arbeitsstation Organisationseinheiten mithilfe der folgenden Schritte:  

    1.  Navigieren Sie zu der <Forest>\Domains\\<Domain> (wobei <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, in dem Sie die Gruppenrichtlinie festlegen möchten).  

    2.  Mit der rechten Maustaste in der Organisationseinheit, die das Gruppenrichtlinienobjekt wird angewendet, und klicken Sie auf **vorhandenes Gruppenrichtlinienobjekt verknüpfen**.  

        ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_54.gif)  

    3.  Wählen Sie das Gruppenrichtlinienobjekt, das Sie gerade erstellt haben, und klicken Sie auf **OK**.  

        ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_55.gif)  

    4.  Erstellen Sie Links zu anderen Organisationseinheiten, die Arbeitsstationen enthalten.  

    5.  Erstellen Sie Links zu allen anderen Organisationseinheiten, Mitgliedsserver enthalten.  

    6.  In einer Gesamtstruktur mit mehreren Domänen, sollte eine ähnliche GPO in jeder Domäne erstellt werden, die erfordert, dass die Gruppe "Organisations-Admins" geschützt werden.  

> [!IMPORTANT]  
> Sprunglisten Server zum Verwalten von Domänencontrollern und Active Directory verwendet werden, sicher, dass sprungbrettservern befinden, in einer Organisationseinheit, mit denen diese Gruppenrichtlinienobjekte nicht verknüpft ist.  

### <a name="verification-steps"></a>Überprüfungsschritte  

#### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Deny Zugriff auf diesen Computer vom Netzwerk aus zugreifen"  
Versuchen Sie von jeder Mitgliedsserver oder einer Arbeitsstation, die durch die GPO-Änderungen (z. B. ein "sprungbrettserver") nicht beeinträchtigt ist auf einem Mitgliedsserver oder einer Arbeitsstation über das Netzwerk zugreifen, die von der GPO-Änderungen betroffen ist. Um die GPO-Einstellungen zu überprüfen, versuchen, das Systemlaufwerk mithilfe der **NET USE** Befehl durch die folgenden Schritte ausführen:  

1.  Melden Sie sich lokal mit einem Konto, das Mitglied der Gruppe EA ist.  

2.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Eingabeaufforderung**, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen** ein Eingabeaufforderungsfenster mit erhöhten Rechten öffnen.  

4.  Wenn Sie aufgefordert werden, die für erhöhte Rechte zu genehmigen, klicken Sie auf **Ja**.  

    ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_56.gif)  

5.  In der **Eingabeaufforderung** geben **net verwenden \\\<Server Name>\c$**, wobei <Server Name> ist der Name der Mitgliedsserver oder einer Arbeitsstation, die Sie versuchen, sich über das Netzwerk zugreifen.  

6.  Der folgende Screenshot zeigt die Fehlermeldung, die angezeigt werden soll.  

    ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_57.gif)  

#### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Batchauftrag verweigern"  

Melden Sie von jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen sich lokal.  

##### <a name="create-a-batch-file"></a>Erstellen Sie eine Datei  

1.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Editor**, und klicken Sie auf **Editor**.  

3.  In **Editor**, Typ **Dir c:**.  

4.  Klicken Sie auf **Datei**, und klicken Sie auf **speichern unter**.  

5.  In der **Datei** , geben Sie Namen im ** <Filename>. bat** (wo <Filename> ist der Name der neuen Batch-Datei).  

##### <a name="schedule-a-task"></a>Planen einer Aufgabe  

1.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Taskplaner**, und klicken Sie auf **Aufgabenplanung**.  

    > [!NOTE]  
    > Auf Computern Windows 8 ausgeführt wird, in der **Suche** geben **Planen von Aufgaben**, und klicken Sie auf **Planen von Aufgaben**.  

3.  Klicken Sie auf **Aktion**, und klicken Sie auf **Task erstellen**.  

4.  In der **Task erstellen** , geben Sie im Dialogfeld ** <Task Name> ** (wobei <Task Name> ist der Name der neuen Aufgabe).  

5.  Klicken Sie auf die **Aktionen** Registerkarte, und klicken Sie auf **neu**.  

6.  In der **Aktion** Feld **Programm starten**.  

7.  Klicken Sie unter **Programm-Skript**, klicken Sie auf **Durchsuchen**suchen und markieren Sie die Batchdatei in erstellt die **erstellen Sie eine Datei** Abschnitt, und klicken Sie auf **öffnen**.  

8.  Klicken Sie auf **OK**.  

9. Klicken Sie auf die **allgemeine** Registerkarte.  

10. In der **Sicherheitsoptionen** auf **Benutzer oder Gruppe ändern**.  

11. Geben Sie den Namen eines Kontos, das Mitglied der Gruppe EAs ist, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

12. Wählen Sie **ausgeführt wird, ob der Benutzer oder nicht angemeldet ist** , und wählen Sie **keine Kennwort speichern**. Die Aufgabe wird nur auf lokale Ressourcen zugreifen.  

13. Klicken Sie auf **OK**.  

14. Es sollte ein Dialogfeld angezeigt, die Anmeldeinformationen für anfordernden Benutzerkonto zum Ausführen der Aufgabe.  

15. Geben Sie die Anmeldeinformationen ein, klicken Sie auf **OK**.  

16. Sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

    ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_58.gif)  

#### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Dienst verweigern"  

1.  Melden Sie von jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen sich lokal.  

2.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Dienste**, und klicken Sie auf **Dienste**.  

4.  Doppelklicken Sie auf **Druckspooler**.  

5.  Klicken Sie auf die **anmelden** Registerkarte.  

6.  Klicken Sie unter **melden Sie sich als**Option **dieses Konto**.  

7.  Klicken Sie auf **Durchsuchen**, geben Sie den Namen eines Kontos, das Mitglied der Gruppe EAs ist, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

8.  Klicken Sie unter **Kennwort:** und **Kennwort bestätigen**, geben Sie das ausgewählte Konto Kennwort ein, und klicken Sie auf **OK**.  

9. Klicken Sie auf **OK** drei Mal.  

10. Mit der rechten Maustaste die **Druckspooler** service, und wählen Sie **neu starten**.  

11. Wenn der Dienst neu gestartet wird, sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

    ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_59.gif)  

#### <a name="revert-changes-to-the-printer-spooler-service"></a>Wiederherstellen von Änderungen an den Druckerwarteschlangendienst  

1.  Melden Sie von jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen sich lokal.  

2.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Dienste**, und klicken Sie auf **Dienste**.  

4.  Doppelklicken Sie auf **Druckspooler**.  

5.  Klicken Sie auf die **anmelden** Registerkarte.  

6.  Klicken Sie unter **melden Sie sich als**, wählen die **Lokales System** Konto, und klicken Sie auf **OK**.  

#### <a name="verify-deny-log-on-locally-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Lokal anmelden verweigern"  

1.  Versuchen Sie von jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen, melden Sie sich lokal mit einem Konto, das Mitglied der Gruppe EA ist. Sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

    ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_60.gif)  

#### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden über Remotedesktopdienste verweigern"  

1.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Remotedesktopverbindung**, und klicken Sie dann auf **Remotedesktopverbindung**.  

3.  In der **Computer** Feld, geben Sie den Namen des Computers, die Sie verwenden möchten, schließen Sie an, und klicken Sie dann auf **verbinden**. (Sie können auch die IP-Adresse anstelle des Computernamens eingeben.)  

4.  Wenn Sie aufgefordert werden, geben Sie Anmeldeinformationen für ein Konto, das Mitglied der Gruppe EA ist.  

5.  Sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

    ![Schützen Sie Unternehmen Administratorgruppen](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_61.gif)  
