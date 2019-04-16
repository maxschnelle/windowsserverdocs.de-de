---
ms.assetid: ea015cbc-dea9-4c72-a9d8-d6c826d07608
title: Anhang H - Sichern von lokalen Administratorkonten und-Gruppen
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 222e6725456bb76267240467469e97c5b64fc888
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="appendix-h-securing-local-administrator-accounts-and-groups"></a>Anhang H: schützen lokaler Administratorkonten und-Gruppen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012


## <a name="appendix-h-securing-local-administrator-accounts-and-groups"></a>Anhang H: schützen lokaler Administratorkonten und-Gruppen  
Für alle Versionen von Windows derzeit im grundlegenden Support enthalten wird das lokale Administratorkonto standardmäßig deaktiviert, dadurch wird das Konto für Pass-the-Hash und anderen Methoden des anmeldeinformationsdiebstahls unbrauchbar. Jedoch: in Umgebungen mit älteren Betriebssystemen oder in der lokale Administratorkonten aktiviert wurden, können diese Konten auf Mitgliedsservern und Arbeitsstationen Gefährdung verteilt wie zuvor beschrieben verwendet werden. Jeder lokalen Administratorkontos und der Gruppe sollte gesichert werden, wie in der schrittweisen Anleitung beschrieben.  

Ausführliche Informationen zu Überlegungen zum Sichern der integrierten Administrator (BA)-Gruppen finden Sie unter [implementieren geringsten Verwaltungsmodellen](../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md).  

#### <a name="controls-for-local-administrator-accounts"></a>Steuerelemente für die lokale Administratorkonten  
Für das lokale Administratorkonto in jeder Domäne in der Gesamtstruktur sollten Sie die folgenden Einstellungen konfigurieren:  

-   Konfigurieren von Gruppenrichtlinienobjekten zum Einschränken der Domänen-Administratorkonto verwenden, auf die Domäne Angehörige Systeme  
    -   Fügen Sie das Administratorkonto in ein oder mehrere Gruppenrichtlinienobjekte, die Sie erstellen und auf Arbeitsstationen und Server in jeder Domäne Organisationseinheiten verknüpfen, um die folgenden Benutzerrechte in **Computer Computerkonfiguration\Richtlinien\Windows Settings\Security Einstellungen\Sicherheitseinstellungen\Lokale Einstellungen\Benutzername\Lokale Rechte Zuweisungen**:  

        -   Zugriff vom Netzwerk auf diesen Computer verweigern  

        -   Anmelden als Batchauftrag verweigern  

        -   Anmelden als Dienst verweigern  

        -   Anmelden über Remotedesktopdienste verweigern  

#### <a name="step-by-step-instructions-to-secure-local-administrators-groups"></a>Eine schrittweise Anleitung zum Sichern der lokalen Administratorgruppe  

###### <a name="configuring-gpos-to-restrict-administrator-account-on-domain-joined-systems"></a>Konfigurieren von Gruppenrichtlinienobjekten zum Administratorkonto auf Domäne Angehörige Systeme zu beschränken  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Gruppenrichtlinienverwaltung**.  

2.  Erweitern Sie in der Konsolenstruktur <Forest>\Domains\\<Domain>, und klicken Sie dann **Group Policy Objects** (wo <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, in dem Sie die Gruppenrichtlinie festlegen möchten).  

3.  In der Konsolenstruktur mit der rechten Maustaste **Group Policy Objects**, und klicken Sie auf **neu**.  

    ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_101.png)  

4.  In der **neues Gruppenrichtlinienobjekt** , geben Sie im Dialogfeld ** <GPO Name> **, und klicken Sie auf **OK** (wo <GPO Name> ist der Name des dieses Gruppenrichtlinienobjekt).  

    ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_102.png)  

5.  Klicken Sie im Detailbereich mit der rechten Maustaste ** <GPO Name> **, und klicken Sie auf **bearbeiten**.  

6.  Navigieren Sie zu **Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, und klicken Sie auf **Zuweisen von Benutzerrechten**.  

    ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_103.png)  

7.  Konfigurieren Sie die Benutzerrechte für das lokale Administratorkonto zu verhindern, dass den Zugriff auf Member Servern und Arbeitsstationen über das Netzwerk wie folgt vorgehen:  

    1.  Doppelklicken Sie auf **Zugriff vom Netzwerk auf diesen Computer Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen**, geben Sie den Benutzernamen für das lokale Administratorkonto an, und klicken Sie auf **OK**. Dieser Benutzername wird **Administrator**, die bei der Installation von Windows standardmäßig.  

        ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_104.png)  

    3.  Klicken Sie auf OK.  

        > [!IMPORTANT]  
        > Wenn Sie das Administratorkonto an diesen Einstellungen hinzufügen, geben Sie an, ob Sie ein lokales Administratorkonto oder ein Domänenadministratorkonto durch Konfigurieren wie Sie die Konten Bezeichnung. Z. B. zum Hinzufügen der TAILSPINTOYS Domäne Administratorkonto anmelden, um diese Verweigern von Benutzerrechten, würden Sie navigieren Sie zu dem Administratorkonto für die Domäne TAILSPINTOYS würde die als TAILSPINTOYS\Administrator angezeigt werden. Bei der Eingabe **Administrator** in den Einstellungen im Gruppenrichtlinienobjekt-Editor für diese Benutzer Rechte schränken Sie das lokale Administratorkonto auf jedem Computer, auf die das Gruppenrichtlinienobjekt angewendet wird, wie zuvor beschrieben.  

8.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das lokale Administratorkonto anmelden als Stapelverarbeitungsauftrag wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Batchauftrag verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen**, geben Sie den Benutzernamen für das lokale Administratorkonto an, und klicken Sie auf **OK**. Dieser Benutzername wird **Administrator**, die bei der Installation von Windows standardmäßig.  

        ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_105.png)  

    3.  Klicken Sie auf **OK**.  

        > [!IMPORTANT]  
        > Wenn Sie das Administratorkonto an diesen Einstellungen hinzufügen, geben Sie an, ob Sie zum Konfigurieren lokales Administratorkonto oder Domänen-Administratorkonto wie Sie die Konten Bezeichnung. Z. B. zum Hinzufügen der TAILSPINTOYS Domäne Administratorkonto anmelden, um diese Verweigern von Benutzerrechten, würden Sie navigieren Sie zu dem Administratorkonto für die Domäne TAILSPINTOYS würde die als TAILSPINTOYS\Administrator angezeigt werden. Bei der Eingabe **Administrator** in den Einstellungen im Gruppenrichtlinienobjekt-Editor für diese Benutzer Rechte schränken Sie das lokale Administratorkonto auf jedem Computer, auf die das Gruppenrichtlinienobjekt angewendet wird, wie zuvor beschrieben.  

9. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das lokale Administratorkonto anmelden als Dienst wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Dienst verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen**, geben Sie den Benutzernamen für das lokale Administratorkonto an, und klicken Sie auf **OK**. Dieser Benutzername wird **Administrator**, die bei der Installation von Windows standardmäßig.  

        ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_106.png)  

    3.  Klicken Sie auf **OK**.  

        > [!IMPORTANT]  
        > Wenn Sie das Administratorkonto an diesen Einstellungen hinzufügen, geben Sie an, ob Sie zum Konfigurieren lokales Administratorkonto oder Domänen-Administratorkonto wie Sie die Konten Bezeichnung. Z. B. zum Hinzufügen der TAILSPINTOYS Domäne Administratorkonto anmelden, um diese Verweigern von Benutzerrechten, würden Sie navigieren Sie zu dem Administratorkonto für die Domäne TAILSPINTOYS würde die als TAILSPINTOYS\Administrator angezeigt werden. Bei der Eingabe **Administrator** in den Einstellungen im Gruppenrichtlinienobjekt-Editor für diese Benutzer Rechte schränken Sie das lokale Administratorkonto auf jedem Computer, auf die das Gruppenrichtlinienobjekt angewendet wird, wie zuvor beschrieben.  

10. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das lokale Administratorkonto zugreifen auf Mitgliedsservern und Arbeitsstationen über Remote Desktop Services wie folgt vorgehen:  

    1.  Doppelklicken Sie auf **anmelden über Remotedesktopdienste Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen**, geben Sie den Benutzernamen für das lokale Administratorkonto an, und klicken Sie auf **OK**. Dieser Benutzername wird **Administrator**, die bei der Installation von Windows standardmäßig.  

        ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_107.png)  

    3.  Klicken Sie auf **OK**.  

        > [!IMPORTANT]  
        > Wenn Sie das Administratorkonto an diesen Einstellungen hinzufügen, geben Sie an, ob Sie zum Konfigurieren lokales Administratorkonto oder Domänen-Administratorkonto wie Sie die Konten Bezeichnung. Z. B. zum Hinzufügen der TAILSPINTOYS Domäne Administratorkonto anmelden, um diese Verweigern von Benutzerrechten, würden Sie navigieren Sie zu dem Administratorkonto für die Domäne TAILSPINTOYS würde die als TAILSPINTOYS\Administrator angezeigt werden. Bei der Eingabe **Administrator** in den Einstellungen im Gruppenrichtlinienobjekt-Editor für diese Benutzer Rechte schränken Sie das lokale Administratorkonto auf jedem Computer, auf die das Gruppenrichtlinienobjekt angewendet wird, wie zuvor beschrieben.  

11. Zum Beenden **Gruppenrichtlinienverwaltungs-Editor**, klicken Sie auf **Datei**, und klicken Sie auf **beenden**.  

12. In **Gruppenrichtlinienverwaltung**, verknüpfen Sie das Gruppenrichtlinienobjekt auf dem Mitgliedsserver und Arbeitsstation Organisationseinheiten mithilfe der folgenden Schritte:  

    1.  Navigieren Sie zu der <Forest>\Domains\\<Domain> (wobei <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, in dem Sie die Gruppenrichtlinie festlegen möchten).  

    2.  Mit der rechten Maustaste in der Organisationseinheit, die das Gruppenrichtlinienobjekt wird angewendet, und klicken Sie auf **vorhandenes Gruppenrichtlinienobjekt verknüpfen**.  

        ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_108.png)  

    3.  Wählen Sie das Gruppenrichtlinienobjekt, das Sie erstellt haben, und klicken Sie auf **OK**.  

        ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_109.png)  

    4.  Erstellen Sie Links zu anderen Organisationseinheiten, die Arbeitsstationen enthalten.  

    5.  Erstellen Sie Links zu allen anderen Organisationseinheiten, Mitgliedsserver enthalten.  

#### <a name="verification-steps"></a>Überprüfungsschritte  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Deny Zugriff auf diesen Computer vom Netzwerk aus zugreifen"  

Versuchen Sie von jeder Mitgliedsserver oder einer Arbeitsstation, die durch die GPO-Änderungen (z. B. ein sprungbrettserver) nicht beeinträchtigt ist auf einem Mitgliedsserver oder einer Arbeitsstation über das Netzwerk zugreifen, die von der GPO-Änderungen betroffen ist. Um die GPO-Einstellungen zu überprüfen, versuchen, das Systemlaufwerk mithilfe der **NET USE** Befehl.  

1.  Melden Sie sich lokal auf jeder Mitgliedsserver oder einer Arbeitsstation, die durch die GPO-Änderungen nicht beeinträchtigt ist.  

2.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Eingabeaufforderung**, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen** ein Eingabeaufforderungsfenster mit erhöhten Rechten öffnen.  

4.  Wenn Sie aufgefordert werden, die für erhöhte Rechte zu genehmigen, klicken Sie auf **Ja**.  

    ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_110.png)  

5.  In der **Eingabeaufforderung** geben **net verwenden \\\<Server Name>\c$/User:<Server Name>\Administrator**, wobei <Server Name> ist der Name der Mitgliedsserver oder einer Arbeitsstation, die Sie versuchen, sich über das Netzwerk zugreifen.  

    > [!NOTE]  
    > Die Anmeldeinformationen des lokalen Administrators müssen vom gleichen System sein, die Sie über das Netzwerk zugreifen.  

6.  Der folgende Screenshot zeigt die Fehlermeldung, die angezeigt werden soll.  

    ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_111.png)  

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

2.  In der **Suche** Feld, geben Sie den Taskplaner, und klicken Sie auf **Aufgabenplanung**.  

    > [!NOTE]  
    > Auf Computern Windows 8 ausgeführt wird, in der **Suche** geben **Planen von Aufgaben**, und klicken Sie auf **Planen von Aufgaben**.  

3.  Klicken Sie auf **Aktion**, und klicken Sie auf **Task erstellen**.  

4.  In der **Task erstellen** , geben Sie im Dialogfeld ** <Task Name> ** (wobei <Task Name> ist der Name der neuen Aufgabe).  

5.  Klicken Sie auf die **Aktionen** Registerkarte, und klicken Sie auf **neu**.  

6.  In der **Aktion** auf **Programm starten**.  

7.  In der **Programm-Skript** auf **Durchsuchen**suchen und markieren Sie die Batchdatei in erstellt die **erstellen Sie eine Datei** Abschnitt, und klicken Sie auf **öffnen**.  

8.  Klicken Sie auf **OK**.  

9. Klicken Sie auf die **allgemeine** Registerkarte.  

10. In der **Sicherheitsoptionen** auf **Benutzer oder Gruppe ändern**.  

11. Geben Sie den Namen des lokalen Administratorkontos des Systems, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

12. Wählen Sie **ausgeführt wird, ob der Benutzer oder nicht angemeldet ist** und **keine Kennwort speichern**. Die Aufgabe wird nur auf lokale Ressourcen zugreifen.  

13. Klicken Sie auf **OK**.  

14. Es sollte ein Dialogfeld angezeigt, die Anmeldeinformationen für anfordernden Benutzerkonto zum Ausführen der Aufgabe.  

15. Geben Sie die Anmeldeinformationen ein, klicken Sie auf **OK**.  

16. Sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

    ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_112.png)  

###### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Dienst verweigern"  

1.  Melden Sie von jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen sich lokal.  

2.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Dienste**, und klicken Sie auf **Dienste**.  

4.  Doppelklicken Sie auf **Druckspooler**.  

5.  Klicken Sie auf die **anmelden** Registerkarte.  

6.  In **melden Sie sich als** auf **dieses Konto**.  

7.  Klicken Sie auf **Durchsuchen**, geben Sie das System lokalen Administratorkonto an, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

8.  In der **Kennwort** und **Kennwort bestätigen** Felder, geben Sie das ausgewählte Konto Kennwort ein, und klicken Sie auf **OK**.  

9. Klicken Sie auf **OK** drei Mal.  

10. Mit der rechten Maustaste **Druckspooler** , und klicken Sie auf **neu starten**.  

11. Wenn der Dienst neu gestartet wird, sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

    ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_113.png)  

###### <a name="revert-changes-to-the-printer-spooler-service"></a>Wiederherstellen von Änderungen an den Druckerwarteschlangendienst  

1.  Melden Sie von jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen sich lokal.  

2.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Dienste**, und klicken Sie auf **Dienste**.  

4.  Doppelklicken Sie auf **Druckspooler**.  

5.  Klicken Sie auf die **anmelden** Registerkarte.  

6.  In der **melden Sie sich als**: Feld **lokalen Systemaccount**, und klicken Sie auf **OK**.  

###### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden über Remotedesktopdienste verweigern"  

1.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Remotedesktopverbindung**, und klicken Sie auf **Remotedesktopverbindung**.  

3.  In der **Computer** Feld, geben Sie den Namen des Computers, die Sie verwenden möchten, schließen Sie an, und klicken Sie auf **verbinden**. (Sie können auch die IP-Adresse anstelle des Computernamens eingeben.)  

4.  Wenn Sie aufgefordert werden, geben Sie Anmeldeinformationen für das System den lokalen's **Administrator** Konto.  

5.  Sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

    ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_114.png)  
