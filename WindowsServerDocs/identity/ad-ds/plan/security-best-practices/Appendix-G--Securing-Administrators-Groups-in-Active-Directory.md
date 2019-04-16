---
ms.assetid: 4baefbd3-038f-44c0-85ba-f24e9722b757
title: "Anhang G - Schützen von Administratorgruppen in Active Directory"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4cf89f7bf31ce848de384778b0213d0ddc822158
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>Anhang G: Schützen von Administratorgruppen in Active Directory

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012


## <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>Anhang G: Schützen von Administratorgruppen in Active Directory  
Wie bei der Gruppen Organisations-Admins (EA) und Domänen-Admins (DA) der Fall ist, sollten die Mitgliedschaft in der integrierten Gruppe Administratoren (BA) nur in Build oder ein Notfall-Wiederherstellungsszenarien erforderlich sein. Wird keine tägliche Benutzerkonten in der Gruppe "Administratoren" mit Ausnahme des integrierten Administratorkontos für die Domäne, wenn sie wie unter gesichert wurden [Anhang D: schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  

Administratoren sind, werden standardmäßig die Besitzer der Großteil der AD DS-Objekte in den jeweiligen Domänen. Mitgliedschaft in dieser Gruppe kann in Build oder ein Notfall-Wiederherstellungsszenarien erforderlich sein, in dem Besitz oder die Fähigkeit des Besitzes von Objekten erforderlich ist. Darüber hinaus erben DAs und EAs zahlreiche ihre Rechte und Berechtigungen durch ihre Standardmitgliedschaft in der Gruppe "Administratoren". Standardgruppe von privilegierten Gruppen in Active Directory Schachtelung sollte nicht geändert werden, und jede Domäne in der Gruppe "Administratoren" sollte gesichert werden, wie in der schrittweisen Anleitung beschrieben.  

Für die Gruppe "Administratoren" in jeder Domäne in der Gesamtstruktur:  

1.  Entfernen Sie alle Mitglieder aus der Gruppe "Administratoren" mit Ausnahme des integrierten Administratorkontos für die Domäne bereitgestellten gesichert wurde gemäß [Anhang D: schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  

2.  Auf Mitgliedsservern und Arbeitsstationen in jeder Domäne mit Organisationseinheiten verknüpften Gruppenrichtlinienobjekten, die DA-Gruppe hinzugefügt werden sollen die folgenden Benutzerrechte in **Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Policies\ Benutzer Benutzerrechten**:  

    -   Zugriff vom Netzwerk auf diesen Computer verweigern  

    -   Anmelden als Batchauftrag verweigern  

    -   Anmelden als Dienst verweigern  

3.  Klicken Sie auf die Organisationseinheit Domain Controllers in jeder Domäne in der Gesamtstruktur sollte der Gruppe "Administratoren" die folgenden Berechtigungen gewährt werden:  

    -   Auf diesen Computer vom Netzwerk aus zugreifen.  

    -   Lokal anmelden zulassen  

    -   Anmelden über Remotedesktopdienste zulassen  

4.  Überwachung sollte konfiguriert werden, um Warnungen zu senden, wenn Änderungen an die Eigenschaften oder Mitglied der Gruppe "Administratoren" vorgenommen werden.  

#### <a name="step-by-step-instructions-for-removing-all-members-from-the-administrators-group"></a>Eine schrittweise Anleitung für alle Mitglieder der Gruppe "Administratoren" entfernen  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Active Directory-Benutzer und-Computer**.  

2.  Um alle Elemente aus der Gruppe "Administratoren" zu entfernen, führen Sie die folgenden Schritte aus:  

    1.  Doppelklicken Sie auf die **Administratoren** Gruppe, und klicken Sie auf die **Mitglieder** Registerkarte.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_79.gif)  

    2.  Wählen Sie ein Mitglied der Gruppe aus, klicken Sie auf **entfernen**, klicken Sie auf **Ja**, und klicken Sie auf **OK**.  

3.  Wiederholen Sie Schritt 2, bis alle Mitglieder der Gruppe "Administratoren" entfernt wurden.  

#### <a name="step-by-step-instructions-to-secure-administrators-groups-in-active-directory"></a>Schrittweise Anleitung zum Schützen von Administratorgruppen in Active Directory  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Gruppenrichtlinienverwaltung**.  

2.  Erweitern Sie in der Konsolenstruktur <Forest>\Domains\\<Domain>, und klicken Sie dann **Group Policy Objects** (wo <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, in dem Sie die Gruppenrichtlinie festlegen möchten).  

3.  In der Konsolenstruktur mit der rechten Maustaste **Group Policy Objects**, und klicken Sie auf **neu**.  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_80.gif)  

4.  In der **neues Gruppenrichtlinienobjekt** , geben Sie im Dialogfeld <GPO Name>, und klicken Sie auf **OK** (wo *GPO-Name* ist der Name des dieses Gruppenrichtlinienobjekt).  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_81.gif)  

5.  Klicken Sie im Detailbereich mit der rechten Maustaste ** <GPO Name> **, und klicken Sie auf **bearbeiten**.  

6.  Navigieren Sie zu **Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, und klicken Sie auf **Zuweisen von Benutzerrechten**.  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_82.gif)  

7.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe "Administratoren" auf Mitgliedsservern und Arbeitsstationen über das Netzwerk wie folgt:  

    1.  Doppelklicken Sie auf **Zugriff vom Netzwerk auf diesen Computer Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administratoren**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_83.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

8.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe "Administratoren" Anmelden als Stapelverarbeitungsauftrag wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Batchauftrag verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administratoren**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_84.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

9. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe "Administratoren" Anmelden als Dienst wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Dienst verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administratoren**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_85.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

10. Zum Beenden **Gruppenrichtlinienverwaltungs-Editor**, klicken Sie auf **Datei**, und klicken Sie auf **beenden**.  

11. In **Gruppenrichtlinienverwaltung**, verknüpfen Sie das Gruppenrichtlinienobjekt auf dem Mitgliedsserver und Arbeitsstation Organisationseinheiten mithilfe der folgenden Schritte:  

    1.  Navigieren Sie zu der <Forest>\Domains\\<Domain> (wobei <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, in dem Sie die Gruppenrichtlinie festlegen möchten).  

    2.  Mit der rechten Maustaste in der Organisationseinheit, die das Gruppenrichtlinienobjekt wird angewendet, und klicken Sie auf **vorhandenes Gruppenrichtlinienobjekt verknüpfen**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_86.gif)  

    3.  Wählen Sie das Gruppenrichtlinienobjekt, das Sie gerade erstellt haben, und klicken Sie auf **OK**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_87.gif)  

    4.  Erstellen Sie Links zu anderen Organisationseinheiten, die Arbeitsstationen enthalten.  

    5.  Erstellen Sie Links zu allen anderen Organisationseinheiten, Mitgliedsserver enthalten.  

        > [!IMPORTANT]  
        > Sprunglisten Server zum Verwalten von Domänencontrollern und Active Directory verwendet werden, sicher, dass sprungbrettservern befinden, in einer Organisationseinheit, mit denen diese Gruppenrichtlinienobjekte nicht verknüpft ist.  

        > [!NOTE]  
        > Beim Implementieren von Einschränkungen für die Gruppe "Administratoren" in Gruppenrichtlinienobjekten, wendet Windows die Einstellungen auf Mitglieder der lokalen Administratorengruppe des Computers zusätzlich zu der Domäne der Gruppe "Administratoren". Sie sollten daher Vorsicht walten, bei der Implementierung von Einschränkungen in der Gruppe "Administratoren". Obwohl das Verbot von Netzwerk-Stapel und Dienst Anmeldungen für Mitglieder der Gruppe "Administratoren" ist empfehlenswert, wo es implementiert werden, nicht schränken Sie lokale Anmeldung oder Anmeldung über Remotedesktopdienste ein. Blockieren diese Anmeldetypen können legitime Verwaltung eines Computers von Mitgliedern der lokalen Gruppe "Administratoren" blockiert werden.  
        >   
        > Der folgende Screenshot zeigt Konfigurationseinstellungen, die die blockieren unsachgemäße Verwendung des integrierten lokalen und Domäne Administratorkonten, zusätzlich zu den Missbrauch der integrierten Gruppe der lokalen oder Administratoren. Beachten Sie, dass die **anmelden über Remotedesktopdienste Verweigern** Benutzerrecht nicht der Gruppe "Administratoren" enthalten, da in dieser Einstellung Standardstylesheet auch diese Anmeldungen für Konten blockieren würde, die Mitglieder der Administratorgruppe des lokalen Computers befinden. Dienste auf Computern für die Ausführung im Kontext einer privilegierten Gruppen in diesem Abschnitt beschriebenen konfiguriert sind, kann diese Einstellungen implementieren Dienste und Anwendungen zu Fehlern führen. Aus diesem Grund sollten wie bei allen die Empfehlungen in diesem Abschnitt können Sie gründlich Einstellungen für die Anwendbarkeit in Ihrer Umgebung testen.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_88.gif)  

#### <a name="step-by-step-instructions-to-grant-user-rights-to-the-administrators-group"></a>Schrittweise Anleitung zum Erteilen von Benutzerrechten der Gruppe "Administratoren"  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Gruppenrichtlinienverwaltung**.  

2.  Erweitern Sie in der Konsolenstruktur <Forest>\Domains\\<Domain>, und klicken Sie dann **Group Policy Objects** (wo <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, in dem Sie die Gruppenrichtlinie festlegen möchten).  

3.  In der Konsolenstruktur mit der rechten Maustaste **Group Policy Objects**, und klicken Sie auf **neu**.  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_89.gif)  

4.  In der **neues Gruppenrichtlinienobjekt** , geben Sie im Dialogfeld <GPO Name>, und klicken Sie auf **OK** (wo <GPO Name> ist der Name des dieses Gruppenrichtlinienobjekt).  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_90.gif)  

5.  Klicken Sie im Detailbereich mit der rechten Maustaste ** <GPO Name> **, und klicken Sie auf **bearbeiten**.  

6.  Navigieren Sie zu **Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, und klicken Sie auf **Zuweisen von Benutzerrechten**.  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_91.gif)  

7.  Konfigurieren Sie die Benutzerberechtigungen für Mitglieder der Gruppe "Administratoren" auf Domänencontrollern für den Zugriff über das Netzwerk zu ermöglichen, indem Sie wie folgt vorgehen:  

    1.  Doppelklicken Sie auf **Zugriff auf diesen Computer vom Netzwerk** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_92.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

8.  Konfigurieren Sie die Benutzerrechte zu Mitgliedern der Gruppe "Administratoren", melden Sie sich lokal wie folgt vorgehen:  

    1.  Doppelklicken Sie auf **lokal anmelden zulassen** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administratoren**, klicken Sie auf **Namen**, und klicken Sie auf **OK**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_93.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

9. Konfigurieren Sie die Benutzerrechte zu Mitgliedern der Gruppe "Administratoren" Anmelden über Remotedesktopdienste wie folgt vorgehen:  

    1.  Doppelklicken Sie auf **anmelden über Remotedesktopdienste zulassen** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administratoren**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_94.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

10. Zum Beenden **Gruppenrichtlinienverwaltungs-Editor**, klicken Sie auf **Datei**, und klicken Sie auf **beenden**.  

11. In **Gruppenrichtlinienverwaltung**, verknüpfen Sie das Gruppenrichtlinienobjekt mit der Organisationseinheit Domain Controllers, mithilfe der folgenden Schritte:  

    1.  Navigieren Sie zu der <Forest>\Domains\\<Domain> (wobei <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, in dem Sie die Gruppenrichtlinie festlegen möchten).  

    2.  Mit der rechten Maustaste die Domänencontroller, die Organisationseinheit, und klicken Sie dann auf **vorhandenes Gruppenrichtlinienobjekt verknüpfen**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_95.gif)  

    3.  Wählen Sie das Gruppenrichtlinienobjekt, das Sie gerade erstellt haben, und klicken Sie auf **OK**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_96.gif)  

#### <a name="verification-steps"></a>Überprüfungsschritte  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Deny Zugriff auf diesen Computer vom Netzwerk aus zugreifen"  
Versuchen Sie von jeder Mitgliedsserver oder einer Arbeitsstation, die durch die GPO-Änderungen (z. B. ein "sprungbrettserver") nicht beeinträchtigt ist auf einem Mitgliedsserver oder einer Arbeitsstation über das Netzwerk zugreifen, die von der GPO-Änderungen betroffen ist. Um die GPO-Einstellungen zu überprüfen, versuchen, das Systemlaufwerk mithilfe der **NET USE** Befehl.  

1.  Melden Sie sich lokal mit einem Konto, das Mitglied der Gruppe "Administratoren" ist.  

2.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Eingabeaufforderung**, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen** ein Eingabeaufforderungsfenster mit erhöhten Rechten öffnen.  

4.  Wenn Sie aufgefordert werden, die für erhöhte Rechte zu genehmigen, klicken Sie auf **Ja**.  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_97.gif)  

5.  In der **Eingabeaufforderung** geben **net verwenden \\\<Server Name>\c$**, wobei <Server Name> ist der Name der Mitgliedsserver oder einer Arbeitsstation, die Sie versuchen, sich über das Netzwerk zugreifen.  

6.  Der folgende Screenshot zeigt die Fehlermeldung, die angezeigt werden soll.  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_98.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Batchauftrag verweigern"  
Melden Sie von jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen sich lokal.  

###### <a name="create-a-batch-file"></a>Erstellen Sie eine Datei  

1.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Editor**, und klicken Sie auf **Editor**.  

3.  In **Editor**, Typ **Dir c:**.  

4.  Klicken Sie auf **Datei**, und klicken Sie auf **speichern unter**.  

5.  In der **Dateinamen** geben ** <Filename>. bat** (wo <Filename> ist der Name der neuen Batch-Datei).  

###### <a name="schedule-a-task"></a>Planen einer Aufgabe  

1.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Taskplaner**, und klicken Sie auf **Aufgabenplanung**.  

    > [!NOTE]  
    > Geben Sie auf Computern unter Windows 8, in das Suchfeld Aufgaben planen, und klicken Sie dann auf Tasks planen.  

3.  Klicken Sie auf **Aktion**, und klicken Sie auf **Task erstellen**.  

4.  In der **Task erstellen** , geben Sie im Dialogfeld ** <Task Name> ** (wobei <Task Name> ist der Name der neuen Aufgabe).  

5.  Klicken Sie auf die **Aktionen** Registerkarte, und klicken Sie auf **neu**.  

6.  In der **Aktion** Feld **Programm starten**.  

7.  In der **Programm-Skript** auf **Durchsuchen**suchen und markieren Sie die Batchdatei in erstellt die **erstellen Sie eine Datei** Abschnitt, und klicken Sie auf **öffnen**.  

8.  Klicken Sie auf **OK**.  

9. Klicken Sie auf die **allgemeine** Registerkarte.  

10. In der **Sicherheitsoptionen** auf **Benutzer oder Gruppe ändern**.  

11. Geben Sie den Namen eines Kontos, das Mitglied der Gruppe "Administratoren" ist, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

12. Wählen Sie **ausgeführt wird, ob der Benutzer nicht angemeldet Onor ist** und **keine Kennwort speichern**. Die Aufgabe wird nur auf lokale Ressourcen zugreifen.  

13. Klicken Sie auf **OK**.  

14. Es sollte ein Dialogfeld angezeigt, die Anmeldeinformationen für anfordernden Benutzerkonto zum Ausführen der Aufgabe.  

15. Geben Sie das Kennwort ein, klicken Sie auf **OK**.  

16. Sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_99.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Dienst verweigern"  

1.  Melden Sie von jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen sich lokal.  

2.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Dienste**, und klicken Sie auf **Dienste**.  

4.  Doppelklicken Sie auf **Druckspooler**.  

5.  Klicken Sie auf die **anmelden** Registerkarte.  

6.  In der **melden Sie sich als** Feld **dieses Konto**.  

7.  Klicken Sie auf **Durchsuchen**, geben Sie den Namen eines Kontos, das Mitglied der Gruppe "Administratoren" ist, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

8.  In der **Kennwort** und **Kennwort bestätigen** Felder, geben Sie das ausgewählte Konto Kennwort ein, und klicken Sie auf **OK**.  

9. Klicken Sie auf **OK** drei Mal.  

10. Mit der rechten Maustaste **Druckspooler** , und klicken Sie auf **neu starten**.  

11. Wenn der Dienst neu gestartet wird, sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_100.png)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>Wiederherstellen von Änderungen an den Druckerwarteschlangendienst  

1.  Melden Sie von jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen sich lokal.  

2.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Dienste**, und klicken Sie auf **Dienste**.  

4.  Doppelklicken Sie auf **Druckspooler**.  

5.  Klicken Sie auf die **anmelden** Registerkarte.  

6.  In der **melden Sie sich als** auf **Lokales System** Konto, und klicken Sie auf **OK**.  
