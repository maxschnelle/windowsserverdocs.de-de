---
ms.assetid: ea015cbc-dea9-4c72-a9d8-d6c826d07608
title: 'Anhang H: Sichern von lokalen Administrator Konten und-Gruppen'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 7e0cff62851250009d8af6ec7d87ec8191dcaec0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408631"
---
# <a name="appendix-h-securing-local-administrator-accounts-and-groups"></a>Anhang H: Schützen lokaler Administratorkonten und -gruppen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-h-securing-local-administrator-accounts-and-groups"></a>Anhang H: Schützen lokaler Administratorkonten und -gruppen  
In allen Versionen von Windows, die derzeit unterstützt werden, ist das lokale Administrator Konto standardmäßig deaktiviert, wodurch das Konto für Pass-the-Hash-Angriffe und andere Angriffe auf Anmelde Informationen unbrauchbar wird. In Umgebungen, die ältere Betriebssysteme enthalten oder für die lokale Administrator Konten aktiviert wurden, können diese Konten jedoch wie zuvor beschrieben verwendet werden, um die Kompromittierung über Mitglieds Server und Arbeitsstationen hinweg weiterzugeben. Jedes lokale Administrator Konto und jede Gruppe sollten wie in den folgenden schrittweisen Anleitungen beschrieben gesichert werden.  

Ausführliche Informationen zu den Überlegungen bei der Sicherung integrierter Administrator Gruppen finden Sie unter Implementieren von [Verwaltungs Modellen mit geringsten Rechten](../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md).  

#### <a name="controls-for-local-administrator-accounts"></a>Steuerelemente für lokale Administrator Konten  
Für das lokale Administrator Konto in jeder Domäne in der Gesamtstruktur sollten Sie die folgenden Einstellungen konfigurieren:  

-   Konfigurieren von Gruppenrichtlinien Objekten, um die Verwendung des Administrator Kontos der Domäne auf in die Domäne eingebundenen Systemen einzuschränken  
    -   Fügen Sie in jeder Domäne in mindestens einem Gruppenrichtlinien Objekt, das Sie erstellen und mit der Arbeitsstation und den Mitglieds Server Organisationseinheiten verknüpft sind, das Administrator Konto den folgenden Benutzerrechten in **Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale**Richtlinien\Zuweisen von Benutzerrechten  

        -   Zugriff vom Netzwerk auf diesen Computer verweigern  

        -   Anmelden als Batchauftrag verweigern  

        -   Anmelden als Dienst verweigern  

        -   Anmelden über Remotedesktopdienste verweigern  

#### <a name="step-by-step-instructions-to-secure-local-administrators-groups"></a>Schritt-für-Schritt-Anleitung zum Sichern von lokalen Administratoren Gruppen  

###### <a name="configuring-gpos-to-restrict-administrator-account-on-domain-joined-systems"></a>Konfigurieren von GPOs, um das Administrator Konto auf in die Domäne eingebundenen Systemen einzuschränken  

1.  KlickenSie in Server-Manager **auf Extras, und**klicken Sie auf **Gruppenrichtlinie Verwaltung**.  

2.  Erweitern Sie in der Konsolen Struktur <Forest>\domains\\<Domain>, und klicken Sie dann auf **Gruppenrichtlinie Objekte** (wobei <Forest> der Name der Gesamtstruktur und <Domain> der Name der Domäne ist, in der Sie die Gruppenrichtlinie festlegen möchten).  

3.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Gruppenrichtlinie Objekte**, und klicken Sie dann auf **neu**.  

    ![sichere lokale Administrator Konten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_101.png)  

4.  Geben Sie im Dialogfeld **Neues** Gruppenrichtlinien Objekt **<GPO Name>** ein, und klicken Sie auf **OK** (wobei <GPO Name> der Name dieses Gruppenrichtlinien Objekts ist).  

    ![sichere lokale Administrator Konten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_102.png)  

5.  Klicken Sie im Detailfenster mit der rechten Maustaste auf **<GPO Name>** , und klicken Sie dann auf **Bearbeiten**.  

6.  Navigieren Sie zu **Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, **und klicken Sie**auf Zuweisen von  

    ![sichere lokale Administrator Konten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_103.png)  

7.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das lokale Administrator Konto auf Mitglieder Server und Arbeitsstationen über das Netzwerk zugreift:  

    1.  Doppelklicken Sie **auf Zugriff vom Netzwerk auf diesen Computer verweigern,** und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen**, geben Sie den Benutzernamen für das lokale Administrator Konto ein, und klicken Sie auf **OK**. Dieser Benutzername ist **Administrator**, der Standard bei der Installation von Windows.  

        ![sichere lokale Administrator Konten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_104.png)  

    3.  Klicken Sie auf „OK“.  

        > [!IMPORTANT]  
        > Wenn Sie diesem Einstellungen das Administrator Konto hinzufügen, geben Sie an, ob Sie ein lokales Administrator Konto oder ein Domänen Administrator Konto konfigurieren, indem Sie die Bezeichnung der Konten angeben. Wenn Sie z. b. das Administrator Konto der tailspintoys-Domäne diesen Ablehnungs rechten hinzufügen möchten, navigieren Sie zum Administrator Konto für die tailspintoys-Domäne, die als TAILSPINTOYS\Administrator. angezeigt wird. Wenn Sie in der Gruppenrichtlinienobjekt-Editor in diese Benutzerrechte Einstellungen **Administrator** eingeben, beschränken Sie das lokale Administrator Konto auf jedem Computer, auf den das Gruppenrichtlinien Objekt angewendet wird, wie zuvor beschrieben.  

8.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass sich das lokale Administrator Konto als Batch Auftrag anmeldet. gehen Sie hierzu wie folgt vor:  

    1.  Doppelklicken Sie auf **Anmelden als Batch Auftrag verweigern** , und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen**, geben Sie den Benutzernamen für das lokale Administrator Konto ein, und klicken Sie auf **OK**. Dieser Benutzername ist **Administrator**, der Standard bei der Installation von Windows.  

        ![sichere lokale Administrator Konten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_105.png)  

    3.  Klicken Sie auf **OK**.  

        > [!IMPORTANT]  
        > Wenn Sie diesem Einstellungen das Administrator Konto hinzufügen, geben Sie an, ob Sie das lokale Administrator Konto oder das Domänen Administrator Konto konfigurieren, indem Sie die Bezeichnung der Konten angeben. Wenn Sie z. b. das Administrator Konto der tailspintoys-Domäne diesen Ablehnungs rechten hinzufügen möchten, navigieren Sie zum Administrator Konto für die tailspintoys-Domäne, die als TAILSPINTOYS\Administrator. angezeigt wird. Wenn Sie in der Gruppenrichtlinienobjekt-Editor in diese Benutzerrechte Einstellungen **Administrator** eingeben, beschränken Sie das lokale Administrator Konto auf jedem Computer, auf den das Gruppenrichtlinien Objekt angewendet wird, wie zuvor beschrieben.  

9. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass sich das lokale Administrator Konto als Dienst anmeldet. gehen Sie hierzu wie folgt vor:  

    1.  Doppelklicken Sie auf **Anmelden als Dienst verweigern** , und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen**, geben Sie den Benutzernamen für das lokale Administrator Konto ein, und klicken Sie auf **OK**. Dieser Benutzername ist **Administrator**, der Standard bei der Installation von Windows.  

        ![sichere lokale Administrator Konten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_106.png)  

    3.  Klicken Sie auf **OK**.  

        > [!IMPORTANT]  
        > Wenn Sie diesem Einstellungen das Administrator Konto hinzufügen, geben Sie an, ob Sie das lokale Administrator Konto oder das Domänen Administrator Konto konfigurieren, indem Sie die Bezeichnung der Konten angeben. Wenn Sie z. b. das Administrator Konto der tailspintoys-Domäne diesen Ablehnungs rechten hinzufügen möchten, navigieren Sie zum Administrator Konto für die tailspintoys-Domäne, die als TAILSPINTOYS\Administrator. angezeigt wird. Wenn Sie in der Gruppenrichtlinienobjekt-Editor in diese Benutzerrechte Einstellungen **Administrator** eingeben, beschränken Sie das lokale Administrator Konto auf jedem Computer, auf den das Gruppenrichtlinien Objekt angewendet wird, wie zuvor beschrieben.  

10. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das lokale Administrator Konto über Remotedesktopdienste auf Mitglieds Server und Arbeitsstationen zugreift, indem Sie folgende Schritte ausführen:  

    1.  Doppelklicken Sie auf **Anmelden über Remotedesktopdienste verweigern** , und wählen Sie **die Option Diese Richtlinien Einstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen**, geben Sie den Benutzernamen für das lokale Administrator Konto ein, und klicken Sie auf **OK**. Dieser Benutzername ist **Administrator**, der Standard bei der Installation von Windows.  

        ![sichere lokale Administrator Konten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_107.png)  

    3.  Klicken Sie auf **OK**.  

        > [!IMPORTANT]  
        > Wenn Sie diesem Einstellungen das Administrator Konto hinzufügen, geben Sie an, ob Sie das lokale Administrator Konto oder das Domänen Administrator Konto konfigurieren, indem Sie die Bezeichnung der Konten angeben. Wenn Sie z. b. das Administrator Konto der tailspintoys-Domäne diesen Ablehnungs rechten hinzufügen möchten, navigieren Sie zum Administrator Konto für die tailspintoys-Domäne, die als TAILSPINTOYS\Administrator. angezeigt wird. Wenn Sie in der Gruppenrichtlinienobjekt-Editor in diese Benutzerrechte Einstellungen **Administrator** eingeben, beschränken Sie das lokale Administrator Konto auf jedem Computer, auf den das Gruppenrichtlinien Objekt angewendet wird, wie zuvor beschrieben.  

11. Um **Gruppenrichtlinienverwaltungs-Editor**zu beenden, klicken Sie auf **Datei**und dann auf **Beenden**.  

12. Verknüpfen Sie das Gruppenrichtlinien Objekt in **Gruppenrichtlinie Management**mit dem Mitglieds Server und Arbeitsstations Organisationseinheiten, indem Sie die folgenden Schritte ausführen:  

    1.  Navigieren Sie zum <Forest>\domains\\<Domain> (wobei <Forest> der Name der Gesamtstruktur und <Domain> der Name der Domäne ist, in der Sie die Gruppenrichtlinie festlegen möchten).  

    2.  Klicken Sie mit der rechten Maustaste auf die Organisationseinheit, auf die das Gruppenrichtlinien Objekt angewendet wird, und klicken Sie auf **vorhandenes GPO verknüpfen**  

        ![sichere lokale Administrator Konten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_108.png)  

    3.  Wählen Sie das von Ihnen erstellte GPO aus, und klicken Sie auf **OK**.  

        ![sichere lokale Administrator Konten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_109.png)  

    4.  Erstellen Sie Links zu allen anderen Organisationseinheiten, die Arbeitsstationen enthalten.  

    5.  Erstellen Sie Links zu allen anderen Organisationseinheiten, die Mitglieds Server enthalten.  

#### <a name="verification-steps"></a>Überprüfungs Schritte  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>GPO-Einstellungen "Zugriff auf diesen Computer über das Netzwerk verweigern"  

Versuchen Sie auf einem Mitglieds Server oder einer Arbeitsstation, der nicht von den GPO-Änderungen (z. b. einem Sprung Server) betroffen ist, auf einen Mitglieds Server oder eine Arbeitsstation über das Netzwerk zuzugreifen, das von den GPO-Änderungen betroffen ist. Um die GPO-Einstellungen zu überprüfen, versuchen Sie, das Systemlaufwerk mithilfe des Befehls **net use** zuzuordnen.  

1.  Melden Sie sich lokal bei einem Mitglieds Server oder einer Arbeitsstation an, der nicht von den GPO-Änderungen betroffen ist.  

2.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

3.  Geben Sie im **Suchfeld** **Eingabeaufforderung**ein, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen** , um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen.  

4.  Wenn Sie aufgefordert werden, die Höhe zu genehmigen, klicken Sie auf **Ja**.  

    ![sichere lokale Administrator Konten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_110.png)  

5.  Geben Sie im **Eingabe** Aufforderungs Fenster **net use \\\\<Server Name>\c $/User:<Server Name>\administrator**ein, wobei <Server Name> der Name des Mitglieds Servers oder der Arbeitsstation ist, auf den Sie über das Netzwerk zuzugreifen versuchen.  

    > [!NOTE]  
    > Die Anmelde Informationen des lokalen Administrators müssen sich vom gleichen System befinden, auf das Sie über das Netzwerk zugreifen.  

6.  Der folgende Screenshot zeigt die Fehlermeldung, die angezeigt werden soll.  

    ![sichere lokale Administrator Konten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_111.png)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>"Anmelden als Batch Auftrag verweigern"-GPO-Einstellungen überprüfen  
Melden Sie sich lokal bei allen Mitglieds Servern oder Arbeitsstationen an, die von den GPO-Änderungen betroffen sind.  

###### <a name="create-a-batch-file"></a>Erstellen einer Batch Datei  

1.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

2.  Geben Sie im **Suchfeld den Suchbegriff** **Editor**ein, und klicken Sie auf **Editor**.  

3.  Geben **Sie im Editor**den Befehl **dir c:** ein.  

4.  Klicken Sie auf **Datei**und dann auf **Speichern**unter.  

5.  Geben Sie im Feld **Dateiname** **<Filename>. bat** ein (wobei <Filename> der Name der neuen Batchdatei ist).  

###### <a name="schedule-a-task"></a>Planen einer Aufgabe  

1.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

2.  Geben Sie im **Suchfeld den Text** Task Scheduler ein, und klicken Sie auf **Taskplaner**.  

    > [!NOTE]  
    > Geben Sie auf Computern, auf denen Windows 8 ausgeführt wird, im **Suchfeld** **Schedule Tasks**ein, und klicken Sie auf **Aufgaben planen**.  

3.  Klicken Sie auf **Aktion**, und klicken Sie auf **Task erstellen**.  

4.  Geben Sie im Dialogfeld **Task erstellen** **<Task Name>** ein (wobei <Task Name> der Name der neuen Aufgabe ist).  

5.  Klicken Sie auf die Registerkarte **Aktionen** , und klicken Sie auf **neu**.  

6.  Klicken Sie im Feld **Aktion** auf **Programm starten**.  

7.  Klicken Sie im Feld **Programm/Skript** auf **Durchsuchen**, suchen Sie die Batchdatei, die Sie im Abschnitt **Erstellen einer Batchdatei** erstellt haben, und klicken Sie auf **Öffnen**.  

8.  Klicken Sie auf **OK**.  

9. Klicken Sie auf die Registerkarte **Allgemein**.  

10. Klicken Sie im Feld **Sicherheitsoptionen** auf **Benutzer oder Gruppe ändern**.  

11. Geben Sie den Namen des lokalen Administrator Kontos des Systems ein, klicken Sie auf **Namen überprüfen**, und klicken Sie dann auf **OK**.  

12. Wählen Sie **Ausführen aus, ob der Benutzer angemeldet ist oder nicht** , und speichern Sie das **Kennwort**nicht. Der Task hat nur Zugriff auf lokale Computerressourcen.  

13. Klicken Sie auf **OK**.  

14. Es wird ein Dialogfeld angezeigt, in dem die Anmelde Informationen des Benutzerkontos zum Ausführen des Tasks angefordert werden.  

15. Klicken Sie nach Eingabe der Anmelde Informationen auf **OK**.  

16. Ein Dialogfeld ähnlich dem folgenden sollte angezeigt werden.  

    ![sichere lokale Administrator Konten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_112.png)  

###### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>GPO-Einstellungen "Anmelden als Dienst verweigern" überprüfen  

1.  Melden Sie sich lokal bei allen Mitglieds Servern oder Arbeitsstationen an, die von den GPO-Änderungen betroffen sind.  

2.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

3.  Geben Sie im **Suchfeld den Suchbegriff** **Dienste**ein, und klicken Sie auf **Dienste**.  

4.  Suchen Sie den **Druck Spooler**, und doppelklicken Sie darauf.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  Klicken Sie im Feld **Anmelden als** auf **dieses Konto**.  

7.  Klicken Sie auf **Durchsuchen**, geben Sie das lokale Administrator Konto des Systems ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**.  

8.  Geben Sie in die Felder **Kennwort** und **Kennwort bestätigen** das Kennwort für das ausgewählte Konto ein, und klicken Sie auf **OK**.  

9. Klicken Sie drei weitere Male auf **OK** .  

10. Klicken Sie mit der rechten Maustaste auf **Druck Spooler** , und klicken **Sie auf**  

11. Wenn der Dienst neu gestartet wird, sollte ein Dialogfeld ähnlich dem folgenden angezeigt werden.  

    ![sichere lokale Administrator Konten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_113.png)  

###### <a name="revert-changes-to-the-printer-spooler-service"></a>Änderungen am Druckerspoolerdienst zurücksetzen  

1.  Melden Sie sich lokal bei allen Mitglieds Servern oder Arbeitsstationen an, die von den GPO-Änderungen betroffen sind.  

2.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

3.  Geben Sie im **Suchfeld den Suchbegriff** **Dienste**ein, und klicken Sie auf **Dienste**.  

4.  Suchen Sie den **Druck Spooler**, und doppelklicken Sie darauf.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  Wählen Sie im Feld **Anmelden als**: die Option **Lokales Systemkonto**aus, und klicken Sie auf **OK**.  

###### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>Überprüfen der GPO-Einstellungen "Anmelden über Remotedesktopdienste verweigern"  

1.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

2.  Geben Sie im **Suchfeld als Suchbegriff** **Remote Desktop Verbindung**ein, und klicken Sie auf **Remotedesktopverbindung**.  

3.  Geben Sie im Feld **Computer** den Namen des Computers ein, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie auf **verbinden**. (Sie können auch die IP-Adresse anstelle des Computer namens eingeben.)  

4.  Wenn Sie dazu aufgefordert werden, geben Sie Anmelde Informationen für das lokale **Administrator** Konto des Systems an.  

5.  Ein Dialogfeld ähnlich dem folgenden sollte angezeigt werden.  

    ![sichere lokale Administrator Konten und-Gruppen](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_114.png)  
