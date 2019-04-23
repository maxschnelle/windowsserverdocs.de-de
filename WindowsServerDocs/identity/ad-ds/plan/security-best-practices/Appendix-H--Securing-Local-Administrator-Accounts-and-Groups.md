---
ms.assetid: ea015cbc-dea9-4c72-a9d8-d6c826d07608
title: Anhang H - schützen lokaler Administratorkonten und-Gruppen
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 71eea3f623968172076708dbea34d5bbf4a07684
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858691"
---
# <a name="appendix-h-securing-local-administrator-accounts-and-groups"></a>Anhang H: Schützen lokaler Administratorkonten und-Gruppen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-h-securing-local-administrator-accounts-and-groups"></a>Anhang H: Schützen lokaler Administratorkonten und-Gruppen  
In allen Versionen von Windows, die derzeit in der mainstream-Support ist das lokale Administratorkonto standardmäßig deaktiviert, dadurch wird das Konto nicht vom Pass-the-Hash und anderen Angriffen mit gestohlenen Anmeldeinformationen. Allerdings: in Umgebungen, die ältere Betriebssysteme enthalten oder in der lokale Administratorkonten aktiviert wurden, können diese Konten Gefährdung über MemberServer und Arbeitsstationen verteilt wie oben beschrieben verwendet werden. Jeder lokalen Administratorkontos und Gruppe sollten gesichert werden, wie in den folgenden schrittweisen Anleitungen beschrieben.  

Ausführliche Informationen zu Überlegungen zum Sichern der integrierte Administrator (BA)-Gruppen finden Sie unter [implementieren mit Minimalprivilegien Verwaltungsmodellen](../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md).  

#### <a name="controls-for-local-administrator-accounts"></a>Steuerelemente für die Konten für lokale Administratoren  
Für das lokale Administratorkonto in jeder Domäne in der Gesamtstruktur sollten Sie die folgenden Einstellungen konfigurieren:  

-   Konfigurieren der Gruppenrichtlinienobjekte, um der Domäne-Administratorkonto verwenden, in der Domäne Angehörige Systeme zu beschränken.  
    -   Fügen Sie das Administratorkonto in ein oder mehrere Gruppenrichtlinienobjekte, die Sie erstellen und auf Arbeitsstationen und Mitgliedsservern Server Organisationseinheiten in jeder Domäne verknüpfen, um in der folgenden Benutzerrechte **Computer Computerkonfiguration\Richtlinien\Windows unter Sicherheitseinstellungen\Lokale Policies\ Zuweisen von Benutzerrechten**:  

        -   Zugriff vom Netzwerk auf diesen Computer verweigern  

        -   Anmelden als Batchauftrag verweigern  

        -   Anmelden als Dienst verweigern  

        -   Anmelden über Remotedesktopdienste verweigern  

#### <a name="step-by-step-instructions-to-secure-local-administrators-groups"></a>Schrittweise Anleitungen zum Schützen der lokalen Administratorgruppe  

###### <a name="configuring-gpos-to-restrict-administrator-account-on-domain-joined-systems"></a>Konfigurieren von Gruppenrichtlinienobjekten, um das Administratorkonto auf der Domäne Angehörige Systeme zu beschränken.  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Gruppenrichtlinienverwaltung**.  

2.  Erweitern Sie in der Konsolenstruktur <Forest>\Domains\\<Domain>, und klicken Sie dann **Group Policy Objects** (wo <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, wo Sie möchten, Legen Sie die Gruppenrichtlinie).  

3.  In der Konsolenstruktur mit der Maustaste **Group Policy Objects**, und klicken Sie auf **neu**.  

    ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_101.png)  

4.  In der **neues Gruppenrichtlinienobjekt** (Dialogfeld), Typ **<GPO Name>**, und klicken Sie auf **OK** (, in denen <GPO Name> ist der Name des dieses Gruppenrichtlinienobjekt).  

    ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_102.png)  

5.  Klicken Sie im Detailbereich mit der Maustaste **<GPO Name>**, und klicken Sie auf **bearbeiten**.  

6.  Navigieren Sie zu **Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, und klicken Sie auf **Zuweisen von Benutzerrechten**.  

    ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_103.png)  

7.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das lokale Administratorkonto Zugriff auf Member-Servern und Arbeitsstationen über das Netzwerk wie folgt:  

    1.  Doppelklicken Sie auf **Zugriff vom Netzwerk auf diesen Computer Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen**, geben Sie den Benutzernamen des lokalen Administratorkontos an, und klicken Sie auf **OK**. Dieser Benutzername wird **Administrator**, die Standardeinstellung bei der Installation von Windows.  

        ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_104.png)  

    3.  Klicken Sie auf „OK“.  

        > [!IMPORTANT]  
        > Wenn Sie das Administratorkonto an diesen Einstellungen hinzufügen, geben Sie an, ob Sie zum Konfigurieren eines lokalen Administratorkontos oder eines Domänenadministratorkontos wie Sie die Konten bezeichnen. Hinzufügen der TAILSPINTOYS Domäne Administratorkonto anmelden, um diese Verweigern von Benutzerrechten, die Sie dem Administratorkonto für die Domäne TAILSPINTOYS durchsuchen würde beispielsweise würde die als TAILSPINTOYS\Administrator angezeigt werden. Wenn Sie eingeben **Administrator** in diese Rechte benutzereinstellungen in der Gruppenrichtlinienobjekt-Editor, schränken Sie das lokale Administratorkonto auf jedem Computer, auf das Gruppenrichtlinienobjekt angewendet wird, wie oben beschrieben.  

8.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das lokale Administratorkonto anmelden als Stapelverarbeitungsauftrag wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Batchauftrag verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen**, geben Sie den Benutzernamen des lokalen Administratorkontos an, und klicken Sie auf **OK**. Dieser Benutzername wird **Administrator**, die Standardeinstellung bei der Installation von Windows.  

        ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_105.png)  

    3.  Klicken Sie auf **OK**.  

        > [!IMPORTANT]  
        > Wenn Sie das Administratorkonto an diesen Einstellungen hinzufügen, geben Sie an, ob Sie zum Konfigurieren lokaler Administrator- oder Domänenadministratorkonto wie Sie die Konten bezeichnen. Hinzufügen der TAILSPINTOYS Domäne Administratorkonto anmelden, um diese Verweigern von Benutzerrechten, die Sie dem Administratorkonto für die Domäne TAILSPINTOYS durchsuchen würde beispielsweise würde die als TAILSPINTOYS\Administrator angezeigt werden. Wenn Sie eingeben **Administrator** in diese Rechte benutzereinstellungen in der Gruppenrichtlinienobjekt-Editor, schränken Sie das lokale Administratorkonto auf jedem Computer, auf das Gruppenrichtlinienobjekt angewendet wird, wie oben beschrieben.  

9. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das lokale Administratorkonto anmelden als Dienst wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Dienst verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen**, geben Sie den Benutzernamen des lokalen Administratorkontos an, und klicken Sie auf **OK**. Dieser Benutzername wird **Administrator**, die Standardeinstellung bei der Installation von Windows.  

        ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_106.png)  

    3.  Klicken Sie auf **OK**.  

        > [!IMPORTANT]  
        > Wenn Sie das Administratorkonto an diesen Einstellungen hinzufügen, geben Sie an, ob Sie zum Konfigurieren lokaler Administrator- oder Domänenadministratorkonto wie Sie die Konten bezeichnen. Hinzufügen der TAILSPINTOYS Domäne Administratorkonto anmelden, um diese Verweigern von Benutzerrechten, die Sie dem Administratorkonto für die Domäne TAILSPINTOYS durchsuchen würde beispielsweise würde die als TAILSPINTOYS\Administrator angezeigt werden. Wenn Sie eingeben **Administrator** in diese Rechte benutzereinstellungen in der Gruppenrichtlinienobjekt-Editor, schränken Sie das lokale Administratorkonto auf jedem Computer, auf das Gruppenrichtlinienobjekt angewendet wird, wie oben beschrieben.  

10. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das lokale Administratorkonto Zugriff auf MemberServer und Arbeitsstationen über Remote Desktop Services wie folgt:  

    1.  Doppelklicken Sie auf **anmelden über Remotedesktopdienste Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen**, geben Sie den Benutzernamen des lokalen Administratorkontos an, und klicken Sie auf **OK**. Dieser Benutzername wird **Administrator**, die Standardeinstellung bei der Installation von Windows.  

        ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_107.png)  

    3.  Klicken Sie auf **OK**.  

        > [!IMPORTANT]  
        > Wenn Sie das Administratorkonto an diesen Einstellungen hinzufügen, geben Sie an, ob Sie zum Konfigurieren lokaler Administrator- oder Domänenadministratorkonto wie Sie die Konten bezeichnen. Hinzufügen der TAILSPINTOYS Domäne Administratorkonto anmelden, um diese Verweigern von Benutzerrechten, die Sie dem Administratorkonto für die Domäne TAILSPINTOYS durchsuchen würde beispielsweise würde die als TAILSPINTOYS\Administrator angezeigt werden. Wenn Sie eingeben **Administrator** in diese Rechte benutzereinstellungen in der Gruppenrichtlinienobjekt-Editor, schränken Sie das lokale Administratorkonto auf jedem Computer, auf das Gruppenrichtlinienobjekt angewendet wird, wie oben beschrieben.  

11. Zum Beenden **Gruppenrichtlinienverwaltungs-Editor**, klicken Sie auf **Datei**, und klicken Sie auf **beenden**.  

12. In **Gruppenrichtlinienverwaltung**, verknüpfen Sie das Gruppenrichtlinienobjekt auf dem Mitgliedsserver und die Arbeitsstation Organisationseinheiten wie folgt:  

    1.  Navigieren Sie zu der <Forest>\Domains\\ <Domain> (wobei <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, in dem Sie die Gruppenrichtlinie festlegen möchten).  

    2.  Mit der rechten Maustaste in der Organisationseinheit, die das Gruppenrichtlinienobjekt wird auf angewendet werden, und klicken Sie auf **vorhandenes Gruppenrichtlinienobjekt verknüpfen**.  

        ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_108.png)  

    3.  Wählen Sie das Gruppenrichtlinienobjekt, das Sie erstellt haben, und klicken Sie auf **OK**.  

        ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_109.png)  

    4.  Erstellen Sie Links zu allen anderen Organisationseinheiten, die Arbeitsstationen enthalten.  

    5.  Erstellen Sie Verknüpfungen mit allen anderen Organisationseinheiten, die Member-Server enthalten.  

#### <a name="verification-steps"></a>Überprüfungsschritte  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen für "Zugriff auf diesen Computer vom Netzwerk verweigern"  

Versuchen Sie von jeder Mitgliedsserver oder Arbeitsstation, die durch die GPO-Änderungen (z. B. ein sprungbrettserver) nicht beeinträchtigt ist, auf einem Mitgliedsserver oder Arbeitsstation über das Netzwerk zugreifen, die die GPO-Änderungen betroffen ist. Um die GPO-Einstellungen zu überprüfen, versuchen, auf das Systemlaufwerk Zuordnung von der **NET USE** Befehl.  

1.  Melden Sie sich lokal auf jedem Mitgliedsserver oder Arbeitsstation, die die GPO-Änderungen nicht betroffen ist.  

2.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Eingabeaufforderung**, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen** zu einer mit erhöhten Rechten öffnen. -Eingabeaufforderung.  

4.  Wenn Sie dazu aufgefordert werden, die Erhöhung zustimmen, klicken Sie auf **Ja**.  

    ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_110.png)  

5.  In der **Eingabeaufforderung** geben **net verwenden \\ \\ <Server Name>\c$/User:<Server Name>\Administrator**, wobei <Server Name> ist der Name des Elements Server oder einer Arbeitsstation müssen Sie versuchen, über das Netzwerk zugreifen.  

    > [!NOTE]  
    > Die Anmeldeinformationen des lokalen Administrators müssen vom gleichen System sein, die Sie versuchen, über das Netzwerk zugreifen.  

6.  Der folgende Screenshot zeigt die Fehlermeldung, die angezeigt werden soll.  

    ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_111.png)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Batchauftrag verweigern"  
Melden Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind sich lokal.  

###### <a name="create-a-batch-file"></a>Erstellen Sie eine Datei  

1.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Editor**, und klicken Sie auf **Editor**.  

3.  In **Editor**, Typ **Dir c:**.  

4.  Klicken Sie auf **Datei**, und klicken Sie auf **speichern**.  

5.  In der **Dateiname** geben  **<Filename>bat** (, in denen <Filename> ist der Name der neuen Batchdatei).  

###### <a name="schedule-a-task"></a>Planen einer Aufgabe  

1.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** Feld Geben Sie aufgabenplanung, und klicken Sie auf **Taskplaner**.  

    > [!NOTE]  
    > Auf Computern Windows 8 ausgeführt wird, in der **Suche** geben **Planen von Aufgaben**, und klicken Sie auf **Planen von Aufgaben**.  

3.  Klicken Sie auf **Aktion**, und klicken Sie auf **Create Task**.  

4.  In der **Create Task** (Dialogfeld), Typ **<Task Name>** (, in denen <Task Name> ist der Name der neuen Aufgabe).  

5.  Klicken Sie auf die **Aktionen** Registerkarte, und klicken Sie auf **neu**.  

6.  In der **Aktion** auf **ein Programm starten**.  

7.  In der **Programm/Skript** auf **Durchsuchen**, und wählen Sie die Batchdatei erstellt, der **eine Batchdatei erstellen** aus, und klicken Sie auf **Öffnen**.  

8.  Klicken Sie auf **OK**.  

9. Klicken Sie auf die Registerkarte **Allgemein**.  

10. In der **Sicherheitsoptionen** auf **Benutzer oder Gruppe ändern**.  

11. Geben Sie den Namen des Systems lokalen Administratorkontos an, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

12. Wählen Sie **ausgeführt wird, ob der Benutzer oder nicht angemeldet ist** und **speichern Sie das Kennwort nicht**. Der Task wird nur auf lokale Computerressourcen zugreifen.  

13. Klicken Sie auf **OK**.  

14. Es sollte ein Dialogfeld angezeigt, die Anmeldeinformationen für anfordernden Benutzerkonto zum Ausführen des Tasks.  

15. Klicken Sie nach Eingabe der Anmeldeinformationen an, auf **OK**.  

16. Ein Dialogfeld ähnlich der folgenden sollte angezeigt werden.  

    ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_112.png)  

###### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Dienst verweigern"  

1.  Melden Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind sich lokal.  

2.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Services**, und klicken Sie auf **Services**.  

4.  Doppelklicken Sie auf die **Druckspooler**.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  In **melden Sie sich als** auf **dieses Konto**.  

7.  Klicken Sie auf **Durchsuchen**, geben die Systemvariable lokalen Administratorkonto an, und klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

8.  In der **Kennwort** und **Bestätigungskennwort** Felder, geben Sie das ausgewählte Konto-Kennwort ein, und klicken Sie auf **OK**.  

9. Klicken Sie auf **OK** drei weitere Male.  

10. Mit der rechten Maustaste **Druckspooler** , und klicken Sie auf **Neustart**.  

11. Wenn der Dienst neu gestartet wird, wird ein Dialogfeld ähnlich der folgenden sollte angezeigt werden.  

    ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_113.png)  

###### <a name="revert-changes-to-the-printer-spooler-service"></a>Wiederherstellen von Änderungen an den Druckerwarteschlangendienst  

1.  Melden Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind sich lokal.  

2.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Services**, und klicken Sie auf **Services**.  

4.  Doppelklicken Sie auf die **Druckspooler**.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  In der **melden Sie sich als**: die Option **lokale Einstellungen dem Systemkonto**, und klicken Sie auf **OK**.  

###### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden über Remotedesktopdienste verweigern"  

1.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Remotedesktopverbindung**, und klicken Sie auf **Remotedesktopverbindung**.  

3.  In der **Computer** Feld, geben Sie den Namen des Computers ein, die Sie verwenden möchten, Herstellen einer Verbindung mit, und klicken Sie auf **Connect**. (Sie können auch die IP-Adresse anstelle des Computernamens eingeben.)  

4.  Geben Sie bei Aufforderung Anmeldeinformationen für das System den lokalen **Administrator** Konto.  

5.  Ein Dialogfeld ähnlich der folgenden sollte angezeigt werden.  

    ![Sichere lokale Administratorkonten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_114.png)  
