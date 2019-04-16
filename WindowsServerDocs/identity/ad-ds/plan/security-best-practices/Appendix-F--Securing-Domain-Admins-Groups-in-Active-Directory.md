---
ms.assetid: 017b88a6-f29b-4787-99b6-b5c8eaf8c3df
title: "Anhang F: Schützen von Domänenadministratorgruppen in Active Directory"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3535714e0df43cb94c7e89c503bc5f875cd49e28
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="appendix-f-securing-domain-admins-groups-in-active-directory"></a>Anhang F: Schützen von Domänenadministratorgruppen in Active Directory

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012


## <a name="appendix-f-securing-domain-admins-groups-in-active-directory"></a>Anhang F: Schützen von Domänenadministratorgruppen in Active Directory  
Wie bei der Gruppe Organisations-Admins (EA) der Fall ist, sollten die Mitgliedschaft in der Gruppe Domänen-Admins (DA) nur in Build oder ein Notfall-Wiederherstellungsszenarien erforderlich sein. Wird keine tägliche Benutzerkonten in der Gruppe DA mit Ausnahme der das integrierte Administratorkonto für die Domäne, wenn es gemäß gesichert wurde [Anhang D: schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  

Domänen-Admins sind standardmäßig Mitglieder der lokalen Administratorgruppe auf allen Servern und Arbeitsstationen in ihren jeweiligen Domänen. Diese Standardeinstellung Schachtelung sollte für Wartungsfreundlichkeit und Wiederherstellung im Notfall nicht geändert werden. Wenn Domänenadministratoren aus der lokalen Administratorgruppe auf dem Mitgliedsserver entfernt wurden, sollte die Gruppe der Gruppe "Administratoren" auf jedem Mitgliedsserver und Arbeitsstationen in der Domäne hinzugefügt werden. Jede Domäne Domänen-Admins sollte gesichert werden, wie in der schrittweisen Anleitung beschrieben.  

Für die Gruppe "Domänen-Admins" in jeder Domäne in der Gesamtstruktur:  

1.  Entfernen Sie alle Mitglieder aus der Gruppe, mit Ausnahme des integrierten Administratorkontos für die Domäne bereitgestellten gesichert wurde gemäß [Anhang D: schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  

2.  Auf Mitgliedsservern und Arbeitsstationen in jeder Domäne mit Organisationseinheiten verknüpften Gruppenrichtlinienobjekten, die DA-Gruppe hinzugefügt werden sollen die folgenden Benutzerrechte in **Computer Computerkonfiguration\Richtlinien\Windows Settings\Security Einstellungen\Sicherheitseinstellungen\Lokale Einstellungen\Benutzername\Lokale Rechte Zuweisungen**:  

    -   Zugriff vom Netzwerk auf diesen Computer verweigern  

    -   Anmelden als Batchauftrag verweigern  

    -   Anmelden als Dienst verweigern  

    -   Lokal anmelden verweigern  

    -   Verweigern Sie anmelden über Remotedesktopdienste Benutzerrechte  

3.  Überwachung sollte konfiguriert werden, um Warnungen zu senden, wenn Änderungen an die Eigenschaften oder die Mitgliedschaft der Gruppe der Domänenadministratoren vorgenommen werden.  

#### <a name="step-by-step-instructions-for-removing-all-members-from-the-domain-admins-group"></a>Eine schrittweise Anleitung zum Entfernen aller Elemente aus der Gruppe Domänen-Admins  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Active Directory-Benutzer und-Computer**.  

2.  Um alle Elemente aus der Directaccess-Gruppe entfernen möchten, führen Sie die folgenden Schritte aus:  

    1.  Doppelklicken Sie auf die **Domänen-Admins** Gruppe, und klicken Sie auf die **Mitglieder** Registerkarte.  

        ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_62.gif)  

    2.  Wählen Sie ein Mitglied der Gruppe aus, klicken Sie auf **entfernen**, klicken Sie auf **Ja**, und klicken Sie auf **OK**.  

3.  Wiederholen Sie Schritt 2, bis alle Mitglieder der Gruppe DA entfernt wurden.  

#### <a name="step-by-step-instructions-to-secure-domain-admins-in-active-directory"></a>Eine schrittweise Anleitung zum Sichern von Domänen-Admins in Active Directory  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Gruppenrichtlinienverwaltung**.  

2.  Erweitern Sie in der Konsolenstruktur \ < Forest\ > \\Domains\\\ < Domäne\ >, und klicken Sie dann **Group Policy Objects** (wobei \ < Forest\ > ist der Name der Gesamtstruktur und \ < Domäne\ > ist der Name der Domäne, in dem Sie die Gruppenrichtlinie festlegen möchten).  

3.  In der Konsolenstruktur mit der rechten Maustaste **Group Policy Objects**, und klicken Sie auf **neu**.  

    ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_63.gif)  

4.  In der **Gruppenrichtlinienobjekt** , geben Sie im Dialogfeld \ < GPO Tokentypen >, und klicken Sie auf **OK** (, in denen \ < GPO Tokentypen > ist der Name des dieses Gruppenrichtlinienobjekt).  

    ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_64.gif)  

5.  Klicken Sie im Detailbereich mit der rechten Maustaste \ < GPO Tokentypen >, und klicken Sie auf **bearbeiten**.  

6.  Navigieren Sie zu **Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, und klicken Sie auf **Zuweisen von Benutzerrechten**.  

    ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_65.gif)  

7.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe Domänen-Admins den Zugriff auf Member Servern und Arbeitsstationen über das Netzwerk wie folgt:  

    1.  Doppelklicken Sie auf **Zugriff vom Netzwerk auf diesen Computer Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Domänen-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_66.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

8.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe "DA" Anmelden als Stapelverarbeitungsauftrag wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Batchauftrag verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Domänen-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_67.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

9. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe "DA" Anmelden als Dienst wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Dienst verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Domänen-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_68.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

10. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe "Domänen-Admins" lokal anmelden können Mitgliedsservern und Arbeitsstationen, indem Sie Folgendes tun:  

    1.  Doppelklicken Sie auf **lokal anmelden verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Domänen-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_69.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

11. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe Domänen-Admins den Zugriff auf Mitgliedsservern und Arbeitsstationen über Remote Desktop Services wie folgt:  

    1.  Doppelklicken Sie auf **anmelden über Remotedesktopdienste Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Domänen-Admins**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_70.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

12. Zum Beenden **Gruppenrichtlinienverwaltungs-Editor**, klicken Sie auf **Datei**, und klicken Sie auf **beenden**.  

13. Verknüpfen Sie das Gruppenrichtlinienobjekt in der Gruppenrichtlinien-Verwaltungskonsole auf dem Mitgliedsserver und Arbeitsstation Organisationseinheiten wie folgt:  

    1.  Navigieren Sie zu der \ < Forest\ > \Domains\\\ < Domäne\ > (wobei \ < Forest\ > ist der Name der Gesamtstruktur und \ < Domäne\ > ist der Name der Domäne, in dem Sie die Gruppenrichtlinie festlegen möchten).  

    2.  Mit der rechten Maustaste in der Organisationseinheit, die das Gruppenrichtlinienobjekt wird angewendet, und klicken Sie auf **vorhandenes Gruppenrichtlinienobjekt verknüpfen**.  

        ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_71.gif)  

    3.  Wählen Sie das Gruppenrichtlinienobjekt, das Sie gerade erstellt haben, und klicken Sie auf **OK**.  

        ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_72.gif)  

    4.  Erstellen Sie Links zu anderen Organisationseinheiten, die Arbeitsstationen enthalten.  

    5.  Erstellen Sie Links zu allen anderen Organisationseinheiten, Mitgliedsserver enthalten.  

        > [!IMPORTANT]  
        > Sprunglisten Server zum Verwalten von Domänencontrollern und Active Directory verwendet werden, sicher, dass sprungbrettservern befinden, in einer Organisationseinheit, mit denen diese Gruppenrichtlinienobjekte nicht verknüpft ist.  

#### <a name="verification-steps"></a>Überprüfungsschritte  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Deny Zugriff auf diesen Computer vom Netzwerk aus zugreifen"  
Versuchen Sie von jeder Mitgliedsserver oder einer Arbeitsstation, die durch die GPO-Änderungen (z. B. ein "sprungbrettserver") nicht beeinträchtigt ist auf einem Mitgliedsserver oder einer Arbeitsstation über das Netzwerk zugreifen, die von der GPO-Änderungen betroffen ist. Um die GPO-Einstellungen zu überprüfen, versuchen, das Systemlaufwerk mithilfe der **NET USE** Befehl.  

1.  Melden Sie sich lokal mit einem Konto, das Mitglied der Gruppe Domänen-Admins ist.  

2.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Eingabeaufforderung**, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen** ein Eingabeaufforderungsfenster mit erhöhten Rechten öffnen.  

4.  Wenn Sie aufgefordert werden, die für erhöhte Rechte zu genehmigen, klicken Sie auf **Ja**.  

    ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_73.gif)  

5.  In der **Eingabeaufforderung** geben **net verwenden \\\ < Server Tokentypen > \c$**, wobei \ < Server Tokentypen > ist der Name der Mitgliedsserver oder einer Arbeitsstation, die Sie versuchen, sich über das Netzwerk zugreifen.  

6.  Der folgende Screenshot zeigt die Fehlermeldung, die angezeigt werden soll.  

    ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_74.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Batchauftrag verweigern"  

Melden Sie von jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen sich lokal.  

###### <a name="create-a-batch-file"></a>Erstellen Sie eine Datei  

1.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Editor**, und klicken Sie auf **Editor**.  

3.  In **Editor**, Typ **Dir c:**.  

4.  Klicken Sie auf **Datei**, und klicken Sie auf **speichern unter**.  

5.  In der **Datei** Namensfeld, Typ **\ < Filename\ >. bat** (wo \ < Filename\ > ist der Name der neuen Batch-Datei).  

###### <a name="schedule-a-task"></a>Planen einer Aufgabe  

1.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Taskplaner**, und klicken Sie auf **Aufgabenplanung**.  

    > [!NOTE]  
    > Auf Computern Windows 8 ausgeführt wird, in der **Suche** geben **Planen von Aufgaben**, und klicken Sie auf **Planen von Aufgaben**.  

3.  In der **Taskplaner** Menüleiste, klicken Sie auf **Aktion**, und klicken Sie auf **Task erstellen**.  

4.  In der **Task erstellen** , geben Sie im Dialogfeld **\ < Task Tokentypen >** (wobei \ < Task Tokentypen > ist der Name der neuen Aufgabe).  

5.  Klicken Sie auf die **Aktionen** Registerkarte, und klicken Sie auf **neu**.  

6.  In der **Aktion** Feld **Programm starten**.  

7.  Klicken Sie unter **Programm-Skript**, klicken Sie auf **Durchsuchen**suchen und markieren Sie die Batchdatei in erstellt die **erstellen Sie eine Datei** Abschnitt, und klicken Sie auf **öffnen**.  

8.  Klicken Sie auf **OK**.  

9. Klicken Sie auf die **allgemeine** Registerkarte.  

10. Klicken Sie unter **Security** Optionen, klicken Sie auf **Benutzer oder Gruppe ändern**.  

11. Geben Sie den Namen eines Kontos, das Mitglied der Gruppe Domänen-Admins ist, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

12. Wählen Sie **ausgeführt wird, ob der Benutzer oder nicht angemeldet ist** , und wählen Sie **keine Kennwort speichern**. Die Aufgabe wird nur auf lokale Ressourcen zugreifen.  

13. Klicken Sie auf **OK**.  

14. Es sollte ein Dialogfeld angezeigt, die Anmeldeinformationen für anfordernden Benutzerkonto zum Ausführen der Aufgabe.  

15. Geben Sie die Anmeldeinformationen ein, klicken Sie auf **OK**.  

16. Sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

    ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_75.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Dienst verweigern"  

1.  Melden Sie von jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen sich lokal.  

2.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Dienste**, und klicken Sie auf **Dienste**.  

4.  Doppelklicken Sie auf **Druckspooler**.  

5.  Klicken Sie auf die **anmelden** Registerkarte.  

6.  Klicken Sie unter **melden Sie sich als**, wählen die **dieses Konto** Option.  

7.  Klicken Sie auf **Durchsuchen**, geben Sie den Namen eines Kontos, das Mitglied der Gruppe Domänen-Admins ist, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

8.  Klicken Sie unter **Kennwort** und **Kennwort bestätigen**, geben Sie das ausgewählte Konto Kennwort ein, und klicken Sie auf **OK**.  

9. Klicken Sie auf **OK** drei Mal.  

10. Mit der rechten Maustaste **Druckspooler** , und klicken Sie auf **neu starten**.  

11. Wenn der Dienst neu gestartet wird, sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

    ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_76.gif)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>Wiederherstellen von Änderungen an den Druckerwarteschlangendienst  

1.  Melden Sie von jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen sich lokal.  

2.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Dienste**, und klicken Sie auf **Dienste**.  

4.  Doppelklicken Sie auf **Druckspooler**.  

5.  Klicken Sie auf die **anmelden** Registerkarte.  

6.  Klicken Sie unter **melden Sie sich als**, wählen die **Lokales System** Konto, und klicken Sie auf **OK**.  

##### <a name="verify-deny-log-on-locally-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Lokal anmelden verweigern"  

1.  Versuchen Sie von jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen, melden Sie sich lokal mit einem Konto, das Mitglied der Gruppe Domänen-Admins ist. Sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

    ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_77.gif)  

##### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden über Remotedesktopdienste verweigern"    
1.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Remotedesktopverbindung**, und klicken Sie auf **Remotedesktopverbindung**.  

3.  In der **Computer** Feld, geben Sie den Namen des Computers, die Sie verwenden möchten, schließen Sie an, und klicken Sie auf **verbinden**. (Sie können auch die IP-Adresse anstelle des Computernamens eingeben.)  

4.  Wenn Sie aufgefordert werden, geben Sie Anmeldeinformationen für ein Konto, das Mitglied der Gruppe Domänen-Admins ist.  

5.  Sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

    ![Sichere Domäne Administratorgruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_78.gif)  
