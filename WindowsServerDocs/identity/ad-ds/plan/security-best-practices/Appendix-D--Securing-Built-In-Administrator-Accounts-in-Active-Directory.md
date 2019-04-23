---
ms.assetid: 11f36f2b-9981-4da0-9e7c-4eca78035f37
title: Anhang D – schützen integrierter Administratorkonten in Active Directory
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 51e503f55ee0fca1f1a53339de555fd213c69296
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870681"
---
# <a name="appendix-d-securing-built-in-administrator-accounts-in-active-directory"></a>Anhang D: Schützen integrierter Administratorkonten in Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-d-securing-built-in-administrator-accounts-in-active-directory"></a>Anhang D: Schützen integrierter Administratorkonten in Active Directory  
In jeder Domäne in Active Directory ist ein Administratorkonto im Rahmen der Erstellung der Domäne erstellt. Dieses Konto ist standardmäßig ein Mitglied der Gruppen "Domänen-Admins" und "Administratoren" in der Domäne, und die Domäne der Gesamtstruktur-Stammdomäne, das Konto ist auch Mitglied der Gruppe "Organisations-Admins".

Verwendung von einem Domänen Administratorkonto sollte nur für die ersten Build-Aktivitäten und möglicherweise auch Notfallwiederherstellungsszenarien reserviert werden. Um sicherzustellen, dass ein Administratorkonto verwendet werden kann, um Reparaturen Auswirkungen auf den Fall, dass keine anderen Konten verwendet werden können, sollten Sie die Standardmitgliedschaft für das Administratorkonto in einer beliebigen Domäne in der Gesamtstruktur nicht ändern. Stattdessen sollte das Administratorkonto in jeder Domäne in der Gesamtstruktur schützen, wie im folgenden Abschnitt beschrieben und in den schrittweisen Anleitungen beschrieben. 

> [!NOTE]
> Dieses Handbuch verwendet, um wird empfohlen, das Konto deaktivieren. Dies wurde entfernt, als das Whitepaper für Gesamtstruktur-Wiederherstellung verwendet das standardmäßige Administratorkonto. Der Grund ist, sieht das einzige Konto, das Anmeldung ohne globalen Katalogserver ermöglicht.


#### <a name="controls-for-built-in-administrator-accounts"></a>Steuerelemente für integrierter Administratorkonten  
Für das integrierte Administratorkonto in jeder Domäne in der Gesamtstruktur sollten Sie die folgenden Einstellungen konfigurieren:  

-   Aktivieren der **Konto ist vertraulich und kann nicht delegiert werden** Flag für das Konto.  

-   Aktivieren der **Smartcard ist erforderlich, für die interaktive Anmeldung** Flag für das Konto.  

-   Konfigurieren der Gruppenrichtlinienobjekte, um das Administratorkonto verwenden, in der Domäne Angehörige Systeme zu beschränken:  

    -   Fügen Sie in ein oder mehrere Gruppenrichtlinienobjekte, die Sie erstellen und auf Arbeitsstationen und Mitgliedsservern Server Organisationseinheiten in jeder Domäne verknüpfen, einzelnen Domänen Administratorkonto, in der folgenden Benutzerrechte **Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Zuweisen von Richtlinien\Zuweisen von Benutzerrechten**:  

        -   Zugriff vom Netzwerk auf diesen Computer verweigern  

        -   Anmelden als Batchauftrag verweigern  

        -   Anmelden als Dienst verweigern  

        -   Anmelden über Remotedesktopdienste verweigern  

> [!NOTE]  
> Wenn Sie diese Einstellung Konten hinzugefügt haben, müssen Sie angeben, ob Sie lokale Administratorkonten oder Administratorkonten der Domäne konfigurieren. Z. B. hinzufügen, Verweigern der Domäne NWTRADERS Administratorkonto anmelden, um diese Rechte, müssen Sie das Konto als NWTRADERS\Administrator, bzw. Suchen Sie das Administratorkonto für die Domäne NWTRADERS eingeben. Wenn Sie "Administrator" in den diese Rechte benutzereinstellungen in der Gruppenrichtlinienobjekt-Editor eingeben, werden Sie einschränken, das lokale Administratorkonto auf jedem Computer, die das Gruppenrichtlinienobjekt angewendet wird.
>   
> Es wird empfohlen, lokale Administratorkonten auf den Servern und Arbeitsstationen in die gleiche Weise wie Administratorkonten domänenbasierten einschränken. Aus diesem Grund sollten Sie diese Rechte benutzereinstellungen in der Regel das Administratorkonto für jede Domäne in der Gesamtstruktur und das Administratorkonto für die lokalen Computer hinzufügen. Der folgende Screenshot zeigt ein Beispiel zum Konfigurieren dieser Benutzerrechte zum Blockieren von lokalen Administratorkonten und ein Domänenadministratorkonto von der Durchführung von Anmeldungen, die für diese Konten nicht benötigt werden sollte.  


![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_23.gif)  

-   Konfigurieren der Gruppenrichtlinienobjekte, um Administratorkonten auf einem Domänencontroller zu beschränken.  
    -   In jeder Domäne in der Gesamtstruktur, die Standarddomänencontroller-Gruppenrichtlinienobjekt oder eine Richtlinie verknüpft mit den Domänencontrollern, die Organisationseinheit geändert werden, dass die folgenden Berechtigungen in einzelnen Domänen Administratorkonto hinzugefügt **Computer Computerkonfiguration\Richtlinien\Windows Zuweisen von-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten**:   
        -   Zugriff vom Netzwerk auf diesen Computer verweigern  

        -   Anmelden als Batchauftrag verweigern  

        -   Anmelden als Dienst verweigern  

        -   Anmelden über Remotedesktopdienste verweigern  

> [!NOTE]  
> Diese Einstellungen werden sichergestellt, dass integrierte Administratorkonto in der Domäne zur Verbindung mit eines Domänencontrollers verwendet werden kann, obwohl das Konto, wenn aktiviert, lokal an Domänencontrollern anmelden kann. Da dieses Konto sollte nur aktiviert und in Szenarien der notfallwiederherstellung verwendet werden, es wird davon ausgegangen, dass die physischer Zugriff auf mindestens einen Domänencontroller zur Verfügung stehen oder andere Konten mit Berechtigungen für den Remotezugriff auf Domänencontroller werden kann gebraucht.  

-   Konfigurieren der Überwachung von Administratorkonten  

    Wenn Sie jede Domänenadministratorkonto gesichert und deaktiviert werden, sollten Sie konfigurieren, Überwachung, um Änderungen am Konto zu überwachen. Wenn das Konto aktiviert ist, dessen Kennwort zurückgesetzt wird oder alle anderen Änderungen, um das Konto vorgenommen werden, sollten Warnungen an die Benutzer oder Teams, die verantwortlich für die Verwaltung von Active Directory, zusätzlich zur Reaktion auf Vorfälle-Teams in Ihrer Organisation gesendet werden.  

#### <a name="step-by-step-instructions-to-secure-built-in-administrator-accounts-in-active-directory"></a>Schrittweise Anleitungen zum Schützen integrierter Administratorkonten in Active Directory  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Active Directory-Benutzer und-Computer**.  

2.  Um Angriffe zu verhindern, die Delegierung zu verwenden, die Anmeldeinformationen für die auf anderen Systemen zu nutzen, führen Sie die folgenden Schritte aus:  

    1.  Mit der rechten Maustaste die **Administrator** Konto, und klicken Sie auf **Eigenschaften**.  

    2.  Klicken Sie auf die **Konto** Registerkarte.  

    3.  Klicken Sie unter **Kontooptionen**Option **Konto ist vertraulich und kann nicht delegiert werden** kennzeichnen, wie im folgenden Screenshot gezeigt aus, und klicken Sie auf **OK**.  

        ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_24.gif)  

3.  So aktivieren Sie die **Smartcard ist erforderlich, für die interaktive Anmeldung** flag für das Konto, das die folgenden Schritte aus:  

    1.  Mit der rechten Maustaste die **Administrator** Konto, und wählen Sie **Eigenschaften**.  

    2.  Klicken Sie auf die **Konto** Registerkarte.  

    3.  Klicken Sie unter **Konto** Option die **Smartcard ist erforderlich, für die interaktive Anmeldung** kennzeichnen, wie im folgenden Screenshot gezeigt aus, und klicken Sie auf **OK**.  

        ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_25.gif) 

##### <a name="configuring-gpos-to-restrict-administrator-accounts-at-the-domain-level"></a>Konfigurieren von Gruppenrichtlinienobjekten zum Einschränken von Administratorkonten auf der Ebene der Domäne  

> [!WARNING]  
> Dieses Gruppenrichtlinienobjekt sollte nie auf der Ebene der Domäne verbunden sein, da sie das integrierte Administratorkonto kann nicht verwendet werden, auch in Szenarien für die notfallwiederherstellung machen kann.  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Gruppenrichtlinienverwaltung**.  

2.  Erweitern Sie in der Konsolenstruktur <Forest>\Domains\\<Domain>, und klicken Sie dann **Group Policy Objects** (wo <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, wo Sie möchten, Erstellen Sie die Gruppenrichtlinie).  

3.  In der Konsolenstruktur mit der Maustaste **Group Policy Objects**, und klicken Sie auf **neu**.  

    ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_27.gif)  

4.  In der **neues Gruppenrichtlinienobjekt** (Dialogfeld), Typ <GPO Name>, und klicken Sie auf **OK** (, in denen <GPO Name> ist der Name des dieses Gruppenrichtlinienobjekt) wie im folgenden Screenshot gezeigt.  

    ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_28.gif)  

5.  Klicken Sie im Detailbereich mit der Maustaste <GPO Name>, und klicken Sie auf **bearbeiten**.  

6.  Navigieren Sie zu **Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, und klicken Sie auf **Zuweisen von Benutzerrechten**.  

    ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_29.gif)  

7.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das Administratorkonto zugreifen auf Member-Servern und Arbeitsstationen über das Netzwerk wie folgt vorgehen:  

    1.  Doppelklicken Sie auf **Zugriff vom Netzwerk auf diesen Computer Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administrator**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**. Stellen Sie sicher, dass das Konto, im angezeigt wird <DomainName>\Username Format wie im folgenden Screenshot gezeigt.  

        ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_30.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

8.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das Administratorkonto anmelden als Stapelverarbeitungsauftrag wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Batchauftrag verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administrator**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**. Stellen Sie sicher, dass das Konto, im angezeigt wird <DomainName>\Username Format wie im folgenden Screenshot gezeigt.  

        ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_31.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

9. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das Administratorkonto anmelden als Dienst wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Dienst verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administrator**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**. Stellen Sie sicher, dass das Konto, im angezeigt wird <DomainName>\Username Format wie im folgenden Screenshot gezeigt.  

        ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_32.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

10. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass das Konto BA MemberServer und Arbeitsstationen über Remote Desktop Services wie folgt zugreifen:  

    1.  Doppelklicken Sie auf **anmelden über Remotedesktopdienste Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administrator**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**. Stellen Sie sicher, dass das Konto, im angezeigt wird <DomainName>\Username Format wie im folgenden Screenshot gezeigt.  

        ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_33.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

11. Zum Beenden **Gruppenrichtlinienverwaltungs-Editor**, klicken Sie auf **Datei**, und klicken Sie auf **beenden**.  

12. In **Gruppenrichtlinienverwaltung**, verknüpfen Sie das Gruppenrichtlinienobjekt auf dem Mitgliedsserver und die Arbeitsstation Organisationseinheiten wie folgt:  

    1.  Navigieren Sie zu der <Forest>\Domains\\ <Domain> (wobei <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, in dem Sie die Gruppenrichtlinie festlegen möchten).  

    2.  Mit der rechten Maustaste in der Organisationseinheit, die das Gruppenrichtlinienobjekt wird auf angewendet werden, und klicken Sie auf **vorhandenes Gruppenrichtlinienobjekt verknüpfen**.  

        ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_34.gif)  

    3.  Wählen Sie das Gruppenrichtlinienobjekt, das Sie erstellt haben, und klicken Sie auf **OK**.  

        ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_35.gif)  

    4.  Erstellen Sie Links zu allen anderen Organisationseinheiten, die Arbeitsstationen enthalten.  

    5.  Erstellen Sie Verknüpfungen mit allen anderen Organisationseinheiten, die Member-Server enthalten.  

> [!IMPORTANT]  
> Wenn Sie das Administratorkonto an diesen Einstellungen hinzufügen, geben Sie an, ob Sie zum Konfigurieren eines lokalen Administratorkontos oder eines Domänenadministratorkontos wie Sie die Konten bezeichnen. Hinzufügen der TAILSPINTOYS Domäne Administratorkonto anmelden, um diese Verweigern von Benutzerrechten, die Sie dem Administratorkonto für die Domäne TAILSPINTOYS durchsuchen würde beispielsweise würde die als TAILSPINTOYS\Administrator angezeigt werden. Wenn Sie "Administrator" in den diese Rechte benutzereinstellungen in der Gruppenrichtlinienobjekt-Editor eingeben, werden Sie das lokale Administratorkonto auf jedem Computer, auf die das Gruppenrichtlinienobjekt angewendet wird, einschränken, wie oben beschrieben.  

#### <a name="verification-steps"></a>Überprüfungsschritte  
Die hier beschriebenen Überprüfungsschritte gelten für Windows 8 und Windows Server 2012 zur Verfügung.  

##### <a name="verify-smart-card-is-required-for-interactive-logon-account-option"></a>Überprüfen Sie, ob "Smartcard für die interaktive Anmeldung erforderlich" Dienstkonto-Option  

1.  Versuchen Sie von jeder Mitgliedsserver oder Arbeitsstation, die die GPO-Änderungen betroffen interaktiv in die Domäne melden Sie sich mit der Domäne integrierten Administratorkonto an. Nach dem anmelden wollen, sollte ein Dialogfeld ähnlich der folgenden angezeigt werden.  

![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_36.gif)  

##### <a name="verify-account-is-disabled-account-option"></a>Überprüfen Sie, "Konto ist deaktiviert" Dienstkonto-Option  

1.  Versuchen Sie von jeder Mitgliedsserver oder Arbeitsstation, die die GPO-Änderungen betroffen interaktiv in die Domäne melden Sie sich mit der Domäne integrierten Administratorkonto an. Nach dem anmelden wollen, sollte ein Dialogfeld ähnlich der folgenden angezeigt werden.  

![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_37.gif)  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen für "Zugriff auf diesen Computer vom Netzwerk verweigern"  
Versuchen Sie von jeder Mitgliedsserver oder Arbeitsstation, die durch die GPO-Änderungen (z. B. ein sprungbrettserver) nicht beeinträchtigt ist, auf einem Mitgliedsserver oder Arbeitsstation über das Netzwerk zugreifen, die die GPO-Änderungen betroffen ist. Um die GPO-Einstellungen zu überprüfen, versuchen, auf das Systemlaufwerk Zuordnung von der **NET USE** Befehl die folgenden Schritte ausführen:  

1.  Melden Sie sich mit der Domäne, die mit der Domäne integrierten Administratorkonto an.  

2.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Eingabeaufforderung**, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen** zu einer mit erhöhten Rechten öffnen. -Eingabeaufforderung.  

4.  Wenn Sie dazu aufgefordert werden, die Erhöhung zustimmen, klicken Sie auf **Ja**.  

    ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_38.gif)  

5.  In der **Eingabeaufforderung** geben **net verwenden \\ \\ \<Servernamen\>\c$**, wobei \<Servernamen\> ist die Der Name der Mitgliedsserver oder Arbeitsstation, die Sie versuchen, über das Netzwerk zugreifen.  

6.  Der folgende Screenshot zeigt die Fehlermeldung, die angezeigt werden soll.  

    ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_39.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Batchauftrag verweigern"  

Melden Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind sich lokal.  

###### <a name="create-a-batch-file"></a>Erstellen Sie eine Datei  

1.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Editor**, und klicken Sie auf **Editor**.  

3.  In **Editor**, Typ **Dir c:**.  

4.  Klicken Sie auf **Datei** , und klicken Sie auf **speichern**.  

5.  In der **Filename** Feld  **<Filename>bat** (, in denen <Filename> ist der Name der neuen Batchdatei).  

###### <a name="schedule-a-task"></a>Planen einer Aufgabe  

1.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Taskplaner**, und klicken Sie auf **Taskplaner**.  

    > [!NOTE]  
    > Geben Sie auf Computern unter Windows 8, in das Suchfeld **Planen von Aufgaben**, und klicken Sie auf **Planen von Aufgaben**.  

3.  Auf **Taskplaner**, klicken Sie auf **Aktion**, und klicken Sie auf **Create Task**.  

4.  In der **Create Task** (Dialogfeld), Typ **<Task Name>** (, in denen **<Task Name>** ist der Name der neuen Aufgabe).  

5.  Klicken Sie auf die **Aktionen** Registerkarte, und klicken Sie auf **neu**.  

6.  Klicken Sie unter **Aktion:** Option **ein Programm starten**.  

7.  Klicken Sie unter **Programm/Skript:**, klicken Sie auf **Durchsuchen**, suchen und wählen Sie die Batchdatei, die im Abschnitt "Erstellen eines Batch-Datei" erstellt, und klicken Sie auf **öffnen**.  

8.  Klicken Sie auf **OK**.  

9. Klicken Sie auf die Registerkarte **Allgemein**.  

10. Klicken Sie unter **Sicherheit** Optionen klicken Sie auf **Benutzer oder Gruppe ändern**.  

11. Geben Sie den Namen des Kontos, BA auf Domänenebene, **Namen überprüfen**, und klicken Sie auf **OK**.  

12. Wählen Sie **ausgeführt wird, ob der Benutzer oder nicht angemeldet ist** und **speichern Sie das Kennwort nicht**. Der Task wird nur auf lokale Computerressourcen zugreifen.  

13. Klicken Sie auf **OK**.  

14. Es sollte ein Dialogfeld angezeigt, die Anmeldeinformationen für anfordernden Benutzerkonto zum Ausführen des Tasks.  

15. Klicken Sie nach Eingabe der Anmeldeinformationen an, auf **OK**.  

16. Ein Dialogfeld ähnlich der folgenden sollte angezeigt werden.  

    ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_40.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Dienst verweigern"  

1.  Melden Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind sich lokal.  

2.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Services**, und klicken Sie auf **Services**.  

4.  Doppelklicken Sie auf die **Druckspooler**.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  Klicken Sie unter **melden Sie sich als:** Option **dieses Konto**.  

7.  Klicken Sie auf **Durchsuchen**, geben Sie den Namen des Kontos, BA auf der Ebene der Domäne, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

8.  Klicken Sie unter **Kennwort:** und **Kennwort bestätigen:**, geben Sie das Administratorkonto-Kennwort ein, und klicken Sie auf **OK**.  

9. Klicken Sie auf **OK** drei weitere Male.  

10. Mit der rechten Maustaste die **Druckspoolerdienst** , und wählen Sie **Neustart**.  

11. Wenn der Dienst neu gestartet wird, wird ein Dialogfeld ähnlich der folgenden sollte angezeigt werden.  

    ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_41.gif)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>Wiederherstellen von Änderungen an den Druckerwarteschlangendienst  

1.  Melden Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind sich lokal.  

2.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Services**, und klicken Sie auf **Services**.  

4.  Doppelklicken Sie auf die **Druckspooler**.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  Klicken Sie unter **melden Sie sich als:**, wählen die **Lokales System** -Konto, und klicken Sie auf **OK**.  

##### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden über Remotedesktopdienste verweigern"

1.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Remotedesktopverbindung**, und klicken Sie auf **Remotedesktopverbindung**.  

3.  In der **Computer** Feld, geben Sie den Namen des Computers ein, die Sie verwenden möchten, Herstellen einer Verbindung mit, und klicken Sie auf **Connect**. (Sie können auch die IP-Adresse anstelle des Computernamens eingeben.)  

4.  Wenn Sie aufgefordert werden, geben Sie Anmeldeinformationen für den Namen des Kontos BA auf der Ebene der Domäne ein.  

5.  Ein Dialogfeld ähnlich der folgenden sollte angezeigt werden.  

    ![Schützen integrierter Administratorkonten](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_42.gif)  
