---
ms.assetid: 11f36f2b-9981-4da0-9e7c-4eca78035f37
title: "Anhang D – schützen integrierter Administratorkonten in Active Directory"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 2878e661e1bb93fcdc3161c46b73d8e4baec76d2
ms.sourcegitcommit: 2782a80a916f8432c030af76e860a72f08481899
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/13/2018
---
# <a name="appendix-d-securing-built-in-administrator-accounts-in-active-directory"></a>Anhang D: schützen integrierter Administratorkonten in Active Directory

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012


## <a name="appendix-d-securing-built-in-administrator-accounts-in-active-directory"></a>Anhang D: schützen integrierter Administratorkonten in Active Directory  
In jeder Domäne in Active Directory wird ein Administratorkonto im Rahmen der Erstellung der Domäne erstellt. Dieses Konto ist standardmäßig ein Mitglied der Gruppen Domänen-Admins und Administratoren in der Domäne, und die Domäne der Gesamtstruktur-Stammdomäne, das Konto ist auch ein Mitglied der Gruppe "Organisations-Admins".

Verwendung von einem Domänen Administratorkonto sollte nur für Aktivitäten der ersten Erstellung und möglicherweise auch Notfall-Wiederherstellungsszenarien reserviert werden. Um sicherzustellen, dass ein Administratorkonto verwendet werden kann, um Reparaturen wirksam, wenn keine anderen Konten verwendet werden können, sollten Sie die Standardmitgliedschaft des Administratorkontos in einer beliebigen Domäne in der Gesamtstruktur nicht ändern. Stattdessen wird das Administratorkonto in jeder Domäne in der Gesamtstruktur müssen gesichert werden, wie im folgenden Abschnitt beschrieben und detaillierte in der schrittweisen Anleitung, die folgen. 

> [!NOTE]
> Dieses Handbuch verwendet, wird empfohlen, das Konto deaktivieren. Dies wurde als der Gesamtstruktur Recovery-Whitepaper entfernt wird, verwendet das standardmäßige Administratorkonto. Der Grund ist dies das einzige Konto ist, das Anmeldung ohne globalen Katalogserver ermöglicht.


#### <a name="controls-for-built-in-administrator-accounts"></a>Steuerelemente für integrierter Administratorkonten  
Für das integrierte Administratorkonto in jeder Domäne in der Gesamtstruktur sollten Sie die folgenden Einstellungen konfigurieren:  

-   Aktivieren der **Konto ist vertraulich und kann nicht delegiert werden** Flag für das Konto.  

-   Aktivieren der **Smartcard ist erforderlich für die interaktive Anmeldung** Flag für das Konto.  

-   Konfigurieren Sie Gruppenrichtlinienobjekte, um das Administratorkonto verwenden, auf die Domäne Angehörige Systeme zu beschränken:  

    -   Fügen Sie in ein oder mehrere Gruppenrichtlinienobjekte, die Sie erstellen und auf Arbeitsstationen und Server in jeder Domäne Organisationseinheiten verknüpfen, Administratorkonto für jede Domäne auf die folgenden Benutzerrechte in **Computer Computerkonfiguration\Richtlinien\Windows Settings\Security Einstellungen\Sicherheitseinstellungen\Lokale Einstellungen\Benutzername\Lokale Rechte Zuweisungen**:  

        -   Zugriff vom Netzwerk auf diesen Computer verweigern  

        -   Anmelden als Batchauftrag verweigern  

        -   Anmelden als Dienst verweigern  

        -   Anmelden über Remotedesktopdienste verweigern  

> [!NOTE]  
> Wenn Sie diese Einstellung Konten hinzufügen, müssen Sie angeben, ob Sie lokale Administratorkonten oder Domänenadministratorkonten konfigurieren. Z. B. Rechte der Domäne NWTRADERS Administratorkonto anmelden, um diese verweigert, hinzufügen, müssen Sie das Konto als NWTRADERS\Administrator oder Durchsuchen, um das Administratorkonto für die Domäne NWTRADERS eingeben. Wenn Sie diese Benutzer Rechte Einstellungen im Gruppenrichtlinienobjekt-Editor "Administrator" eingeben, wird das lokale Administratorkonto auf jedem Computer eingeschränkt werden, für die das Gruppenrichtlinienobjekt angewendet wird.
>   
> Es wird empfohlen, lokale Administratorkonten auf Mitgliedsservern und Arbeitsstationen in die gleiche Weise wie Administratorkonten domänenbasierten einschränken. Aus diesem Grund sollten Sie diese Benutzer Rechte Einstellungen in der Regel das Administratorkonto für jede Domäne in der Gesamtstruktur und das Administratorkonto für den lokalen Computer hinzufügen. Der folgende Screenshot zeigt ein Beispiel für das Blockieren von lokalen Administratorkonten und ein Domänenadministratorkonto ausführt, Anmeldungen, die für diese Konten nicht erforderlich, sollte die Benutzerrechte konfigurieren.  


![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_23.gif)  

-   Konfigurieren von Gruppenrichtlinienobjekten zum Einschränken von Administratorkonten auf Domänencontrollern  
    -   In jeder Domäne in der Gesamtstruktur, die Standarddomänencontroller-Gruppenrichtlinienobjekt oder eine Richtlinie verknüpft auf die Organisationseinheit modifiziert werden, dass das Administratorkonto für jede Domäne in die folgenden Benutzerrechte hinzufügen Domänencontroller **Computer Computerkonfiguration\Richtlinien\Windows Settings\Security Einstellungen\Sicherheitseinstellungen\Lokale Einstellungen\Benutzername\Lokale Rechte Zuweisungen**:   
        -   Zugriff vom Netzwerk auf diesen Computer verweigern  

        -   Anmelden als Batchauftrag verweigern  

        -   Anmelden als Dienst verweigern  

        -   Anmelden über Remotedesktopdienste verweigern  

> [!NOTE]  
> Diese Einstellung werden sichergestellt, dass das integrierte Administratorkonto in der Domäne für die Verbindung zu einem Domänencontroller verwendet werden kann, auch wenn das Konto, wenn aktiviert, lokal auf Domänencontrollern anmelden kann. Da dieses Konto sollte nur aktiviert und im Notfall-Wiederherstellungsszenarien verwendet werden, es wird davon ausgegangen, dass die physischer Zugriff auf mindestens ein Domänencontroller verfügbar ist oder andere Konten mit Berechtigungen für den Remotezugriff auf den Domänencontrollern verwendet werden können.  

-   Konfigurieren Sie die Überwachung von Administratorkonten  

    Wenn Sie gesicherte Administratorkonto für jede Domäne und er deaktiviert haben, sollten Sie die Überwachung zum Überwachen von Änderungen für das Konto konfigurieren. Wenn das Konto aktiviert ist, dessen Kennwort zurückgesetzt wird oder andere Änderungen werden an das Konto vorgenommen, sollten Warnungen an die Benutzer oder Teams, die für die Verwaltung von Active Directory, zusätzlich zur Reaktion auf Sicherheitsvorfälle Teams in Ihrer Organisation gesendet werden.  

#### <a name="step-by-step-instructions-to-secure-built-in-administrator-accounts-in-active-directory"></a>Schrittweise Anleitung zum Schützen integrierter Administratorkonten in Active Directory  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Active Directory-Benutzer und-Computer**.  

2.  Um Angriffe zu verhindern, die Delegierung auf die Anmeldeinformationen des Kontos auf anderen Systemen verwenden nutzen, können führen Sie die folgenden Schritte aus:  

    1.  Mit der rechten Maustaste die **Administrator** Konto, und klicken Sie auf **Eigenschaften**.  

    2.  Klicken Sie auf die **Konto** Registerkarte.  

    3.  Unter **Konto Optionen**Option **Konto ist vertraulich und kann nicht delegiert werden** kennzeichnen, wie im folgenden Screenshot dargestellt, und klicken Sie auf **OK**.  

        ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_24.gif)  

3.  So aktivieren Sie die **Smartcard ist erforderlich für die interaktive Anmeldung** flag für das Konto, führen Sie die folgenden Schritte aus:  

    1.  Mit der rechten Maustaste die **Administrator** Konto, und wählen Sie **Eigenschaften**.  

    2.  Klicken Sie auf die **Konto** Registerkarte.  

    3.  Klicken Sie unter **Konto** anzuzeigen, wählen die **Smartcard ist erforderlich für die interaktive Anmeldung** kennzeichnen, wie im folgenden Screenshot dargestellt, und klicken Sie auf **OK**.  

        ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_25.gif) 

##### <a name="configuring-gpos-to-restrict-administrator-accounts-at-the-domain-level"></a>Konfigurieren von Gruppenrichtlinienobjekten Administratorkonten auf der Domänenebene einschränken  

> [!WARNING]  
> Dieses Gruppenrichtlinienobjekt sollte nie auf der Domänenebene verknüpft werden, da sie das integrierte Administratorkonto nicht verwendbar, auch im Notfall-Wiederherstellungsszenarien machen kann.  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Gruppenrichtlinienverwaltung**.  

2.  Erweitern Sie in der Konsolenstruktur <Forest>\Domains\\<Domain>, und klicken Sie dann **Group Policy Objects** (wobei <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, in dem Sie die Gruppenrichtlinie erstellen möchten).  

3.  In der Konsolenstruktur mit der rechten Maustaste **Group Policy Objects**, und klicken Sie auf **neu**.  

    ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_27.gif)  

4.  In der **Gruppenrichtlinienobjekt** , geben Sie im Dialogfeld <GPO Name>, und klicken Sie auf **OK** (, in denen <GPO Name> ist der Name des dieses Gruppenrichtlinienobjekt) wie im folgenden Screenshot dargestellt.  

    ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_28.gif)  

5.  Klicken Sie im Detailbereich mit der rechten Maustaste <GPO Name>, und klicken Sie auf **bearbeiten**.  

6.  Navigieren Sie zu **Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, und klicken Sie auf **Zuweisen von Benutzerrechten**.  

    ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_29.gif)  

7.  Konfigurieren Sie die Benutzerrechte für das Administratorkonto zu verhindern, dass den Zugriff auf Member Servern und Arbeitsstationen über das Netzwerk wie folgt vorgehen:  

    1.  Doppelklicken Sie auf **Zugriff vom Netzwerk auf diesen Computer Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administrator**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**. Stellen Sie sicher, dass das Konto, in angezeigt wird <DomainName>\Username Format wie im folgenden Screenshot dargestellt.  

        ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_30.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

8.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das Administratorkonto anmelden als Stapelverarbeitungsauftrag wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Batchauftrag verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administrator**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**. Stellen Sie sicher, dass das Konto, in angezeigt wird <DomainName>\Username Format wie im folgenden Screenshot dargestellt.  

        ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_31.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

9. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das Administratorkonto anmelden als Dienst wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Dienst verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administrator**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**. Stellen Sie sicher, dass das Konto, in angezeigt wird <DomainName>\Username Format wie im folgenden Screenshot dargestellt.  

        ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_32.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

10. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das Konto BA zugreifen auf Mitgliedsservern und Arbeitsstationen über Remote Desktop Services wie folgt vorgehen:  

    1.  Doppelklicken Sie auf **anmelden über Remotedesktopdienste Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administrator**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**. Stellen Sie sicher, dass das Konto, in angezeigt wird <DomainName>\Username Format wie im folgenden Screenshot dargestellt.  

        ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_33.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut.  

11. Zum Beenden **Gruppenrichtlinienverwaltungs-Editor**, klicken Sie auf **Datei**, und klicken Sie auf **beenden**.  

12. In **Gruppenrichtlinienverwaltung**, verknüpfen Sie das Gruppenrichtlinienobjekt auf dem Mitgliedsserver und Arbeitsstation Organisationseinheiten mithilfe der folgenden Schritte:  

    1.  Navigieren Sie zu der <Forest>\Domains\\<Domain> (wobei <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, in dem Sie die Gruppenrichtlinie festlegen möchten).  

    2.  Mit der rechten Maustaste in der Organisationseinheit, die das Gruppenrichtlinienobjekt wird angewendet, und klicken Sie auf **vorhandenes Gruppenrichtlinienobjekt verknüpfen**.  

        ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_34.gif)  

    3.  Wählen Sie das Gruppenrichtlinienobjekt, das Sie erstellt haben, und klicken Sie auf **OK**.  

        ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_35.gif)  

    4.  Erstellen Sie Links zu anderen Organisationseinheiten, die Arbeitsstationen enthalten.  

    5.  Erstellen Sie Links zu allen anderen Organisationseinheiten, Mitgliedsserver enthalten.  

> [!IMPORTANT]  
> Wenn Sie das Administratorkonto an diesen Einstellungen hinzufügen, geben Sie an, ob Sie ein lokales Administratorkonto oder ein Domänenadministratorkonto durch Konfigurieren wie Sie die Konten Bezeichnung. Z. B. zum Hinzufügen der TAILSPINTOYS Domäne Administratorkonto anmelden, um diese Verweigern von Benutzerrechten, würden Sie navigieren Sie zu dem Administratorkonto für die Domäne TAILSPINTOYS würde die als TAILSPINTOYS\Administrator angezeigt werden. Wenn Sie diese Benutzer Rechte Einstellungen im Gruppenrichtlinienobjekt-Editor "Administrator" eingeben, wird das lokale Administratorkonto auf jedem Computer, auf denen das Gruppenrichtlinienobjekt angewendet wird, eingeschränkt werden, wie zuvor beschrieben.  

#### <a name="verification-steps"></a>Überprüfungsschritte  
Die hier beschriebenen Schritte sind spezifisch für Windows 8 und Windows Server 2012.  

##### <a name="verify-smart-card-is-required-for-interactive-logon-account-option"></a>Überprüfen Sie, ob "Smartcard für die interaktive Anmeldung erforderlich" Wenn Sie die Option  

1.  Versuchen Sie aus jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen interaktiv mit der Domäne anmelden mit integrierten Administratorkonto der Domäne. Nach dem Versuch, sich anzumelden, sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_36.gif)  

##### <a name="verify-account-is-disabled-account-option"></a>Überprüfen Sie, ob "Konto ist deaktiviert" Wenn Sie die Option  

1.  Versuchen Sie aus jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen interaktiv mit der Domäne anmelden mit integrierten Administratorkonto der Domäne. Nach dem Versuch, sich anzumelden, sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_37.gif)  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Deny Zugriff auf diesen Computer vom Netzwerk aus zugreifen"  
Versuchen Sie von jeder Mitgliedsserver oder einer Arbeitsstation, die durch die GPO-Änderungen (z. B. ein sprungbrettserver) nicht beeinträchtigt ist auf einem Mitgliedsserver oder einer Arbeitsstation über das Netzwerk zugreifen, die von der GPO-Änderungen betroffen ist. Um die GPO-Einstellungen zu überprüfen, versuchen, das Systemlaufwerk mithilfe der **NET USE** Befehl durch die folgenden Schritte ausführen:  

1.  Melden Sie sich auf die Domäne, die Domäne integrierten Administratorkonto an.  

2.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Eingabeaufforderung**, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen** ein Eingabeaufforderungsfenster mit erhöhten Rechten öffnen.  

4.  Wenn Sie aufgefordert werden, die für erhöhte Rechte zu genehmigen, klicken Sie auf **Ja**.  

    ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_38.gif)  

5.  In der **Eingabeaufforderung** geben **net verwenden \\\<Server Name>\c$**, wobei <Server Name> ist der Name der Mitgliedsserver oder einer Arbeitsstation, die Sie versuchen, über das Netzwerk zugreifen.  

6.  Der folgende Screenshot zeigt die Fehlermeldung, die angezeigt werden soll.  

    ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_39.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Batchauftrag verweigern"  

Melden Sie von jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen sich lokal.  

###### <a name="create-a-batch-file"></a>Erstellen Sie eine Datei  

1.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Editor**, und klicken Sie auf **Editor**.  

3.  In **Editor**, Typ **Dir c:**.  

4.  Klicken Sie auf **Datei** , und klicken Sie auf **speichern unter**.  

5.  In der **Dateiname** geben ** <Filename>. bat** (wo <Filename> ist der Name der neuen Batch-Datei).  

###### <a name="schedule-a-task"></a>Planen einer Aufgabe  

1.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Taskplaner**, und klicken Sie auf **Aufgabenplanung**.  

    > [!NOTE]  
    > Geben Sie auf Computern unter Windows 8, in das Suchfeld **Planen von Aufgaben**, und klicken Sie auf **Planen von Aufgaben**.  

3.  Auf **Aufgabenplanung**, klicken Sie auf **Aktion**, und klicken Sie auf **Task erstellen**.  

4.  In der **Task erstellen** , geben Sie im Dialogfeld ** <Task Name> ** (wobei ** <Task Name> ** ist der Name der neuen Aufgabe).  

5.  Klicken Sie auf die **Aktionen** Registerkarte, und klicken Sie auf **neu**.  

6.  Klicken Sie unter **Aktion:**Option **Programm starten**.  

7.  Klicken Sie unter **Programm-Skript:**, klicken Sie auf **Durchsuchen**, suchen und wählen Sie die Batchdatei, die im Abschnitt "Erstellen einer Batchdatei" erstellt, und klicken Sie auf **öffnen**.  

8.  Klicken Sie auf **OK**.  

9. Klicken Sie auf die **allgemeine** Registerkarte.  

10. Klicken Sie unter **Security** Optionen, klicken Sie auf **Benutzer oder Gruppe ändern**.  

11. Geben Sie den Namen des Kontos BA auf Domänenebene, **Namen überprüfen**, und klicken Sie auf **OK**.  

12. Wählen Sie **ausgeführt wird, ob der Benutzer oder nicht angemeldet ist** und **keine Kennwort speichern**. Die Aufgabe wird nur auf lokale Ressourcen zugreifen.  

13. Klicken Sie auf **OK**.  

14. Es sollte ein Dialogfeld angezeigt, die Anmeldeinformationen für anfordernden Benutzerkonto zum Ausführen der Aufgabe.  

15. Geben Sie die Anmeldeinformationen ein, klicken Sie auf **OK**.  

16. Sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

    ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_40.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Dienst verweigern"  

1.  Melden Sie von jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen sich lokal.  

2.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Dienste**, und klicken Sie auf **Dienste**.  

4.  Doppelklicken Sie auf **Druckspooler**.  

5.  Klicken Sie auf die **anmelden** Registerkarte.  

6.  Klicken Sie unter **melden Sie sich als:**Option **dieses Konto**.  

7.  Klicken Sie auf **Durchsuchen**, geben Sie den Namen des Kontos BA auf der Domänenebene, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

8.  Klicken Sie unter **Kennwort:** und **Kennwort bestätigen:**, geben Sie das Administratorkonto ein, und klicken Sie auf **OK**.  

9. Klicken Sie auf **OK** drei Mal.  

10. Mit der rechten Maustaste die **Druckspoolerdienst** , und wählen Sie **neu starten**.  

11. Wenn der Dienst neu gestartet wird, sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

    ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_41.gif)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>Wiederherstellen von Änderungen an den Druckerwarteschlangendienst  

1.  Melden Sie von jeder Mitgliedsserver oder eine Arbeitsstation, die von der GPO-Änderungen betroffen sich lokal.  

2.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Dienste**, und klicken Sie auf **Dienste**.  

4.  Doppelklicken Sie auf **Druckspooler**.  

5.  Klicken Sie auf die **anmelden** Registerkarte.  

6.  Klicken Sie unter **melden Sie sich als:**, wählen die **Lokales System** Konto, und klicken Sie auf **OK**.  

##### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden über Remotedesktopdienste verweigern"

1.  Mit der Maus den Mauszeiger in die obere oder untere rechte Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Remotedesktopverbindung**, und klicken Sie auf **Remotedesktopverbindung**.  

3.  In der **Computer** Feld, geben Sie den Namen des Computers, die Sie verwenden möchten, schließen Sie an, und klicken Sie auf **verbinden**. (Sie können auch die IP-Adresse anstelle des Computernamens eingeben.)  

4.  Wenn Sie dazu aufgefordert werden, geben Sie Anmeldeinformationen für den Namen des Kontos BA auf der Domänenebene.  

5.  Sollte etwa wie folgt ein Dialogfeld angezeigt werden.  

    ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_42.gif)  
