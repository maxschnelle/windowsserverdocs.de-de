---
ms.assetid: 11f36f2b-9981-4da0-9e7c-4eca78035f37
title: 'Anhang D: sichern integrierter Administrator Konten in Active Directory'
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 6b2dd9fdfc40a7dc29943ffc36559f3533a5dac9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963414"
---
# <a name="appendix-d-securing-built-in-administrator-accounts-in-active-directory"></a>Anhang D: Schützen integrierter Administratorkonten in Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-d-securing-built-in-administrator-accounts-in-active-directory"></a>Anhang D: Schützen integrierter Administratorkonten in Active Directory
In jeder Domäne in Active Directory wird ein Administrator Konto im Rahmen der Erstellung der Domäne erstellt. Dieses Konto ist standardmäßig Mitglied der Gruppe "Domänen-Admins" und "Administratoren" in der Domäne. wenn es sich bei der Domäne um die Stamm Domäne der Gesamtstruktur handelt, ist das Konto auch Mitglied der Gruppe "Organisations-Admins".

Die Verwendung des Administrator Kontos einer Domäne sollte nur für anfängliche buildaktivitäten und möglicherweise für Notfall Wiederherstellungs Szenarien reserviert werden. Um sicherzustellen, dass ein Administrator Konto verwendet werden kann, um Reparaturen zu beeinflussen, wenn keine anderen Konten verwendet werden können, sollten Sie die Standardmitgliedschaft des Administrator Kontos in keiner Domäne in der Gesamtstruktur ändern. Stattdessen sollten Sie das Administrator Konto in jeder Domäne in der Gesamtstruktur schützen, wie im folgenden Abschnitt beschrieben und in den folgenden Schritt-für-Schritt-Anleitungen ausführlich erläutert.

> [!NOTE]
> In dieser Anleitung wird empfohlen, das Konto zu deaktivieren. Dies wurde entfernt, da das-Whitepaper zur Gesamtstruktur Wiederherstellung das Standard Administrator Konto verwendet. Der Grund hierfür ist, dass dies das einzige Konto ist, das die Anmeldung ohne globalen Katalog Server ermöglicht.


#### <a name="controls-for-built-in-administrator-accounts"></a>Steuerelemente für integrierte Administrator Konten
Für das integrierte Administrator Konto in jeder Domäne in der Gesamtstruktur sollten Sie die folgenden Einstellungen konfigurieren:

-   Aktivieren Sie das **Konto ist vertraulich und kann für das Konto nicht delegiert werden** .

-   Aktivieren Sie die **Smartcard ist für das interaktive Logon** -Flag für das Konto erforderlich.

-   Konfigurieren Sie Gruppenrichtlinien Objekte, um die Verwendung des Administrator Kontos für mit der Domäne verbundene Systeme einzuschränken:

    -   Fügen Sie in einer oder mehreren Gruppenrichtlinien Objekten, die Sie erstellen und mit der Arbeitsstation und dem Mitglieds Server Organisationseinheiten verknüpft sind, in jeder Domäne das Administrator Konto jeder Domäne den folgenden Benutzerrechten in **Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale**Richtlinien\Zuweisen von Benutzer

        -   Zugriff vom Netzwerk auf diesen Computer verweigern

        -   Anmelden als Batchauftrag verweigern

        -   Anmelden als Dienst verweigern

        -   Anmelden über Remotedesktopdienste verweigern

> [!NOTE]
> Wenn Sie dieser Einstellung Konten hinzufügen, müssen Sie angeben, ob Sie lokale Administrator Konten oder Domänen Administrator Konten konfigurieren möchten. Wenn Sie z. b. das Administrator Konto der Domäne nwtraders zu diesen Verweigerungs rechten hinzufügen möchten, müssen Sie das Konto als NWTRADERS\Administrator eingeben oder zum Administrator Konto für die Domäne nwtraders wechseln. Wenn Sie in den Gruppenrichtlinienobjekt-Editor "Administrator" in den Einstellungen für Benutzerrechte eingeben, schränken Sie das lokale Administrator Konto auf allen Computern ein, auf die das Gruppenrichtlinien Objekt angewendet wird.
>
> Es wird empfohlen, lokale Administrator Konten auf Mitglieds Servern und Arbeitsstationen auf die gleiche Weise wie Domänen basierte Administrator Konten zu beschränken. Daher sollten Sie in der Regel das Administrator Konto für jede Domäne in der Gesamtstruktur und das Administrator Konto für die lokalen Computer zu diesen Benutzerrechten Einstellungen hinzufügen. Der folgende Screenshot zeigt ein Beispiel für die Konfiguration dieser Benutzerrechte, um lokale Administrator Konten und das Administrator Konto einer Domäne für die Ausführung von Anmeldungen zu blockieren, die für diese Konten nicht benötigt werden.


![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_23.gif)

-   Konfigurieren von Gruppenrichtlinien Objekten zum Einschränken von Administrator Konten auf Domänen Controllern
    -   In jeder Domäne in der Gesamtstruktur sollte das Standard Domänen Controller-Gruppenrichtlinien Objekt oder eine Richtlinie, die mit der Domänen Controller-Organisationseinheit verknüpft ist, geändert werden, um das Administrator Konto jeder Domäne den folgenden Benutzerrechten in **Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale**Richtlinien\Zuweisen
        -   Zugriff vom Netzwerk auf diesen Computer verweigern

        -   Anmelden als Batchauftrag verweigern

        -   Anmelden als Dienst verweigern

        -   Anmelden über Remotedesktopdienste verweigern

> [!NOTE]
> Mit diesen Einstellungen wird sichergestellt, dass das integrierte Administrator Konto der Domäne nicht zum Herstellen einer Verbindung mit einem Domänen Controller verwendet werden kann, obwohl sich das Konto, wenn es aktiviert ist, lokal bei Domänen Controllern anmelden kann. Da dieses Konto nur aktiviert und in Notfall Wiederherstellungs Szenarien verwendet werden sollte, wird davon abgerechnet, dass der physische Zugriff auf mindestens einen Domänen Controller verfügbar ist oder dass andere Konten verwendet werden können, die über Berechtigungen für den Remote Zugriff auf Domänen Controller verfügen.

-   Konfigurieren der Überwachung von Administrator Konten

    Wenn Sie das Administrator Konto jeder Domäne gesichert und deaktiviert haben, sollten Sie die Überwachung so konfigurieren, dass Änderungen am Konto überwacht werden. Wenn das Konto aktiviert ist, sein Kennwort zurückgesetzt wird oder andere Änderungen am Konto vorgenommen werden, sollten Warnungen an die Benutzer oder Teams gesendet werden, die für die Verwaltung von Active Directory verantwortlich sind, zusätzlich zu den Teams für die Reaktion auf Vorfälle in Ihrer Organisation.

#### <a name="step-by-step-instructions-to-secure-built-in-administrator-accounts-in-active-directory"></a>Schritt-für-Schritt-Anleitung zum Sichern integrierter Administrator Konten in Active Directory

1.  Klicken **Server Manager**Sie in Server-Manager **auf Extras, und**klicken Sie dann auf **Active Directory Benutzer und Computer**.

2.  Führen Sie die folgenden Schritte aus, um zu verhindern, dass Angriffe, die die Delegierung nutzen, die Anmelde Informationen des Kontos auf anderen Systemen verwenden

    1.  Klicken Sie mit der rechten Maustaste auf das **Administrator** Konto und dann auf **Eigenschaften**.

    2.  Klicken Sie auf die Registerkarte **Konto**.

    3.  Wählen Sie unter " **Konto Optionen**" die Option **Konto ist vertraulich und kann nicht delegiert werden** aus, wie im folgenden Screenshot gezeigt, und klicken Sie auf **OK**.

        ![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_24.gif)

3.  Um die **Smartcard für das interaktive** Anmeldungs Kennzeichen für das Konto zu aktivieren, führen Sie die folgenden Schritte aus:

    1.  Klicken Sie mit der rechten Maustaste auf das **Administrator** Konto, und wählen Sie **Eigenschaften**

    2.  Klicken Sie auf die Registerkarte **Konto**.

    3.  Wählen Sie unter " **Konto** Optionen" das Flag " **Smartcard ist für die interaktive Anmeldung erforderlich" aus** , wie im folgenden Screenshot zu sehen, und klicken Sie auf **OK**.

        ![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_25.gif)

##### <a name="configuring-gpos-to-restrict-administrator-accounts-at-the-domain-level"></a>Konfigurieren von GPOs zum Einschränken von Administrator Konten auf Domänen Ebene

> [!WARNING]
> Dieses GPO sollte nie auf Domänen Ebene verknüpft werden, da es das integrierte Administrator Konto auch in Notfall Wiederherstellungs Szenarien unbrauchbar machen kann.

1.  Klicken **Server Manager**Sie in Server-Manager **auf Extras, und**klicken Sie auf **Gruppenrichtlinie Verwaltung**.

2.  Erweitern Sie in der Konsolen Struktur den Eintrag <Forest> \domains \\ <Domain> , und **Gruppenrichtlinie Objekte** (wobei der Name der Gesamtstruktur <Forest> und <Domain> der Name der Domäne ist, in der Sie die Gruppenrichtlinie erstellen möchten).

3.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Gruppenrichtlinie Objekte**, und klicken Sie dann auf **neu**.

    ![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_27.gif)

4.  Geben Sie im Dialogfeld **Neues** Gruppenrichtlinien Objekt ein <GPO Name> , und klicken Sie auf **OK** (wobei <GPO Name> der Name dieses GPO ist), wie im folgenden Screenshot zu sehen.

    ![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_28.gif)

5.  Klicken Sie im Detailfenster mit der rechten Maustaste auf <GPO Name> , und klicken Sie dann auf **Bearbeiten**.

6.  Navigieren Sie zu **Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, **und klicken Sie**auf Zuweisen von

    ![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_29.gif)

7.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das Administrator Konto auf Mitglieder Server und Arbeitsstationen über das Netzwerk zugreift

    1.  Doppelklicken Sie **auf Zugriff vom Netzwerk auf diesen Computer verweigern,** und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.

    3.  Geben Sie **Administrator**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**. Stellen Sie sicher, dass das Konto im Format "\UserName" angezeigt wird, <DomainName> wie im folgenden Screenshot gezeigt.

        ![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_30.gif)

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .

8.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass sich das Administrator Konto als Batch Auftrag anmeldet. gehen Sie hierzu wie folgt vor:

    1.  Doppelklicken Sie auf **Anmelden als Batch Auftrag verweigern** , und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.

    3.  Geben Sie **Administrator**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**. Stellen Sie sicher, dass das Konto im Format "\UserName" angezeigt wird, <DomainName> wie im folgenden Screenshot gezeigt.

        ![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_31.gif)

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .

9. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass sich das Administrator Konto als Dienst anmeldet. gehen Sie hierzu wie folgt vor:

    1.  Doppelklicken Sie auf **Anmelden als Dienst verweigern** , und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.

    3.  Geben Sie **Administrator**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**. Stellen Sie sicher, dass das Konto im Format "\UserName" angezeigt wird, <DomainName> wie im folgenden Screenshot gezeigt.

        ![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_32.gif)

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .

10. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das BA-Konto über Remotedesktopdienste auf Mitglieds Server und Arbeitsstationen zugreift:

    1.  Doppelklicken Sie auf **Anmelden über Remotedesktopdienste verweigern** , und wählen Sie **die Option Diese Richtlinien Einstellungen definieren**.

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.

    3.  Geben Sie **Administrator**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**. Stellen Sie sicher, dass das Konto im Format "\UserName" angezeigt wird, <DomainName> wie im folgenden Screenshot gezeigt.

        ![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_33.gif)

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .

11. Um **Gruppenrichtlinienverwaltungs-Editor**zu beenden, klicken Sie auf **Datei**und dann auf **Beenden**.

12. Verknüpfen Sie das Gruppenrichtlinien Objekt in **Gruppenrichtlinie Management**mit dem Mitglieds Server und Arbeitsstations Organisationseinheiten, indem Sie die folgenden Schritte ausführen:

    1.  Navigieren Sie zu " <Forest> \domains" \\ <Domain> (wobei der Name der Gesamtstruktur <Forest> und <Domain> der Name der Domäne ist, in der Sie die Gruppenrichtlinie festlegen möchten).

    2.  Klicken Sie mit der rechten Maustaste auf die Organisationseinheit, auf die das Gruppenrichtlinien Objekt angewendet wird, und klicken Sie auf **vorhandenes GPO verknüpfen**

        ![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_34.gif)

    3.  Wählen Sie das von Ihnen erstellte GPO aus, und klicken Sie auf **OK**.

        ![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_35.gif)

    4.  Erstellen Sie Links zu allen anderen Organisationseinheiten, die Arbeitsstationen enthalten.

    5.  Erstellen Sie Links zu allen anderen Organisationseinheiten, die Mitglieds Server enthalten.

> [!IMPORTANT]
> Wenn Sie diesem Einstellungen das Administrator Konto hinzufügen, geben Sie an, ob Sie ein lokales Administrator Konto oder ein Domänen Administrator Konto konfigurieren, indem Sie die Bezeichnung der Konten angeben. Wenn Sie z. b. das Administrator Konto der tailspintoys-Domäne diesen Ablehnungs rechten hinzufügen möchten, navigieren Sie zum Administrator Konto für die tailspintoys-Domäne, die als TAILSPINTOYS\Administrator. angezeigt wird. Wenn Sie in den Gruppenrichtlinienobjekt-Editor "Administrator" in den Einstellungen für Benutzerrechte eingeben, schränken Sie das lokale Administrator Konto auf allen Computern ein, auf die das Gruppenrichtlinien Objekt angewendet wird, wie zuvor beschrieben.

#### <a name="verification-steps"></a>Überprüfungsschritte
Die hier beschriebenen Überprüfungs Schritte gelten speziell für Windows 8 und Windows Server 2012.

##### <a name="verify-smart-card-is-required-for-interactive-logon-account-option"></a>Überprüfen Sie die Konto Option "Smartcard ist für die interaktive Anmeldung erforderlich".

1.  Versuchen Sie, sich über das integrierte Administrator Konto der Domäne interaktiv bei der Domäne anzumelden, wenn Sie von einem Mitglieds Server oder einer Arbeitsstation betroffen sind, die von den GPO-Änderungen betroffen sind. Nachdem Sie versucht haben, sich anzumelden, sollte ein Dialogfeld ähnlich dem folgenden angezeigt werden.

![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_36.gif)

##### <a name="verify-account-is-disabled-account-option"></a>Konto Option "Konto ist deaktiviert" überprüfen

1.  Versuchen Sie, sich über das integrierte Administrator Konto der Domäne interaktiv bei der Domäne anzumelden, wenn Sie von einem Mitglieds Server oder einer Arbeitsstation betroffen sind, die von den GPO-Änderungen betroffen sind. Nachdem Sie versucht haben, sich anzumelden, sollte ein Dialogfeld ähnlich dem folgenden angezeigt werden.

![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_37.gif)

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>GPO-Einstellungen "Zugriff auf diesen Computer über das Netzwerk verweigern"
Versuchen Sie auf einem Mitglieds Server oder einer Arbeitsstation, der nicht von den GPO-Änderungen (z. b. einem Sprung Server) betroffen ist, auf einen Mitglieds Server oder eine Arbeitsstation über das Netzwerk zuzugreifen, das von den GPO-Änderungen betroffen ist. Um die GPO-Einstellungen zu überprüfen, versuchen Sie, das Systemlaufwerk mithilfe des **net use** -Befehls zuzuordnen, indem Sie die folgenden Schritte ausführen:

1.  Melden Sie sich mit dem integrierten Administrator Konto der Domäne bei der Domäne an.

2.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.

3.  Geben Sie im **Suchfeld** **Eingabeaufforderung**ein, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen** , um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen.

4.  Wenn Sie aufgefordert werden, die Höhe zu genehmigen, klicken Sie auf **Ja**.

    ![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_38.gif)

5.  Geben Sie im **Eingabe** Aufforderungs Fenster **net use \\ \\ \<Server Name\> \c $** ein, wobei \<Server Name\> der Name des Mitglieds Servers oder der Arbeitsstation ist, auf den Sie über das Netzwerk zuzugreifen versuchen.

6.  Der folgende Screenshot zeigt die Fehlermeldung, die angezeigt werden soll.

    ![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_39.gif)

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>"Anmelden als Batch Auftrag verweigern"-GPO-Einstellungen überprüfen

Melden Sie sich lokal bei allen Mitglieds Servern oder Arbeitsstationen an, die von den GPO-Änderungen betroffen sind.

###### <a name="create-a-batch-file"></a>Erstellen einer Batch Datei

1.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.

2.  Geben Sie im **Suchfeld den Suchbegriff** **Editor**ein, und klicken Sie auf **Editor**.

3.  Geben **Sie im Editor**den Befehl **dir c:** ein.

4.  Klicken Sie auf **Datei** und dann auf **Speichern**unter.

5.  Geben Sie im Feld **Dateiname** den Namen ** <Filename> . bat** ein (wobei <Filename> der Name der neuen Batchdatei ist).

###### <a name="schedule-a-task"></a>Planen einer Aufgabe

1.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.

2.  Geben Sie im **Suchfeld** den Text **Task Scheduler**ein, und klicken Sie auf **Taskplaner**.

    > [!NOTE]
    > Geben Sie auf Computern, auf denen Windows 8 ausgeführt wird, im Suchfeld **Schedule Tasks**ein, und klicken Sie auf **Aufgaben planen**.

3.  Klicken Sie auf **Taskplaner**auf **Aktion**, und klicken Sie auf **Task erstellen**.

4.  Geben Sie im Dialogfeld **Task erstellen** **<Task Name>** (wobei **<Task Name>** der Name der neuen Aufgabe ist) ein.

5.  Klicken Sie auf die Registerkarte **Aktionen** , und klicken Sie auf **neu**.

6.  Wählen Sie unter **Aktion**die Option **Programm starten**aus.

7.  Klicken Sie unter **Programm/Skript:** auf **Durchsuchen**, suchen Sie die Batchdatei, die Sie im Abschnitt "Erstellen einer Batchdatei" erstellt haben, und klicken Sie auf **Öffnen**.

8.  Klicken Sie auf **OK**.

9. Klicken Sie auf die Registerkarte **Allgemein**.

10. Klicken Sie unter **Sicherheits** Optionen auf **Benutzer oder Gruppe ändern**.

11. Geben Sie den Namen des BA-Kontos auf Domänen Ebene ein, klicken Sie auf **Namen überprüfen**, und klicken Sie dann auf **OK**.

12. Wählen Sie **Ausführen aus, ob der Benutzer angemeldet ist oder nicht** , und speichern Sie das **Kennwort**nicht. Der Task hat nur Zugriff auf lokale Computerressourcen.

13. Klicken Sie auf **OK**.

14. Es wird ein Dialogfeld angezeigt, in dem die Anmelde Informationen des Benutzerkontos zum Ausführen des Tasks angefordert werden.

15. Klicken Sie nach Eingabe der Anmelde Informationen auf **OK**.

16. Ein Dialogfeld ähnlich dem folgenden sollte angezeigt werden.

    ![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_40.gif)

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>GPO-Einstellungen "Anmelden als Dienst verweigern" überprüfen

1.  Melden Sie sich lokal bei allen Mitglieds Servern oder Arbeitsstationen an, die von den GPO-Änderungen betroffen sind.

2.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.

3.  Geben Sie im **Suchfeld den Suchbegriff** **Dienste**ein, und klicken Sie auf **Dienste**.

4.  Suchen Sie den **Druck Spooler**, und doppelklicken Sie darauf.

5.  Klicken Sie auf die Registerkarte **Anmelden**.

6.  Wählen Sie unter **Anmelden als:** **dieses Konto**aus.

7.  Klicken Sie auf **Durchsuchen**, geben Sie den Namen des Bas-Kontos auf Domänen Ebene ein, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.

8.  Geben Sie unter **Kennwort:** und **Kennwort bestätigen:** das Kennwort des Administrator Kontos ein, und klicken Sie auf **OK**.

9. Klicken Sie drei weitere Male auf **OK** .

10. Klicken Sie mit der rechten Maustaste auf den **Druckspoolerdienst** , und wählen Sie **neu starten**

11. Wenn der Dienst neu gestartet wird, sollte ein Dialogfeld ähnlich dem folgenden angezeigt werden.

    ![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_41.gif)

##### <a name="revert-changes-to-the-printer-spooler-service"></a>Änderungen am Druckerspoolerdienst zurücksetzen

1.  Melden Sie sich lokal bei allen Mitglieds Servern oder Arbeitsstationen an, die von den GPO-Änderungen betroffen sind.

2.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.

3.  Geben Sie im **Suchfeld den Suchbegriff** **Dienste**ein, und klicken Sie auf **Dienste**.

4.  Suchen Sie den **Druck Spooler**, und doppelklicken Sie darauf.

5.  Klicken Sie auf die Registerkarte **Anmelden**.

6.  Wählen Sie unter **Anmelden als:** das Konto **Lokales System** aus, und klicken Sie auf **OK**.

##### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>Überprüfen der GPO-Einstellungen "Anmelden über Remotedesktopdienste verweigern"

1.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.

2.  Geben Sie im **Suchfeld als Suchbegriff** **Remote Desktop Verbindung**ein, und klicken Sie auf **Remotedesktopverbindung**.

3.  Geben Sie im Feld **Computer** den Namen des Computers ein, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie auf **verbinden**. (Sie können auch die IP-Adresse anstelle des Computer namens eingeben.)

4.  Wenn Sie dazu aufgefordert werden, geben Sie die Anmelde Informationen für den Namen des BA-Kontos auf Domänen Ebene an.

5.  Ein Dialogfeld ähnlich dem folgenden sollte angezeigt werden.

    ![Sichern integrierter Administrator Konten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_42.gif)
