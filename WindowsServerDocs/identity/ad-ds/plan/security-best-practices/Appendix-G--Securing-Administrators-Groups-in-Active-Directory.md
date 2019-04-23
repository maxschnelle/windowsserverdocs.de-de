---
ms.assetid: 4baefbd3-038f-44c0-85ba-f24e9722b757
title: Anhang G – Schützen von Administratorgruppen in Active Directory
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 2912dfc534d751d4aa121d238dffc36c07562d76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882711"
---
# <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>Anhang G: Schützen von Administratorgruppen in Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>Anhang G: Schützen von Administratorgruppen in Active Directory  
Wie bei der Gruppen Unternehmens-Admins (EA) und Domänen-Admins (DA) der Fall ist, sollte die Mitgliedschaft in der integrierten Gruppe "Administratoren (BA);" nur in Build oder Notfallwiederherstellungsszenarios erforderlich sein. Dürfte keine täglich verwendeten Benutzerkonten in der Gruppe "Administratoren" mit Ausnahme des integrierten Administratorkontos für die Domäne, wenn es wie in beschrieben gesichert wurde [Anhang D: Schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  

Administratoren sind, wird standardmäßig die Besitzer der Großteil der AD DS-Objekte in ihren jeweiligen Domänen. Mitgliedschaft in dieser Gruppe möglicherweise im Build oder Notfallwiederherstellungsszenarios müssen in dem der Besitz oder die Fähigkeit des Besitzes von Objekten erforderlich ist. Darüber hinaus erben DAs und EAs diverse ihre Rechte und Berechtigungen, da ihre Standardmitgliedschaft in der Gruppe "Administratoren". Schachteln von privilegierten Gruppen in Active Directory für die Standardgruppe sollte nicht geändert werden, und jede Domäne in der Gruppe "Administratoren" muss geschützt werden, wie in den folgenden schrittweisen Anleitungen beschrieben.  

Für die Gruppe der Administratoren in jeder Domäne in der Gesamtstruktur:  

1.  Entfernen Sie alle Mitglieder aus der Administratorengruppe, mit Ausnahme des integrierten Administratorkontos für die Domäne, vorausgesetzt sie gesichert wurden unter [Anhang D: Schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  

2.  In Gruppenrichtlinienobjekten, die mit den Organisationseinheiten mit MemberServer und Arbeitsstationen in jeder Domäne verknüpft werden, DA Gruppe hinzugefügt werden sollen in der folgenden Benutzerrechte **Computerkonfiguration\Richtlinien\Windows unter Sicherheitseinstellungen\Lokale Policies\ Benutzerrechte Zuweisung**:  

    -   Zugriff vom Netzwerk auf diesen Computer verweigern  

    -   Anmelden als Batchauftrag verweigern  

    -   Anmelden als Dienst verweigern  

3.  Auf die Organisationseinheit Domain Controllers in jeder Domäne in der Gesamtstruktur sollte auf die Gruppe "Administratoren" die folgenden Berechtigungen erteilt werden:  

    -   Auf diesen Computer vom Netzwerk aus zugreifen.  

    -   Lokale Anmeldung zulassen  

    -   Anmelden über Remotedesktopdienste zulassen  

4.  Überwachung sollte zum Senden von Warnungen, wenn keine Änderungen, auf die Eigenschaften oder die Mitgliedschaft der Gruppe "Administratoren vorgenommen werden" konfiguriert werden.  

#### <a name="step-by-step-instructions-for-removing-all-members-from-the-administrators-group"></a>Schrittweise Anleitungen zum Entfernen aller Elemente aus der Gruppe "Administratoren"  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Active Directory-Benutzer und-Computer**.  

2.  Um alle Elemente aus der Gruppe "Administratoren" zu entfernen, führen Sie die folgenden Schritte aus:  

    1.  Doppelklicken Sie auf die **Administratoren** gruppieren, und klicken Sie auf die **Mitglieder** Registerkarte.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_79.gif)  

    2.  Wählen Sie ein Mitglied der Gruppe aus, klicken Sie auf **entfernen**, klicken Sie auf **Ja**, und klicken Sie auf **OK**.  

3.  Wiederholen Sie Schritt 2, bis alle Mitglieder der Gruppe "Administratoren" entfernt wurden.  

#### <a name="step-by-step-instructions-to-secure-administrators-groups-in-active-directory"></a>Schrittweise Anleitungen zum Schützen von Administratorgruppen in Active Directory  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Gruppenrichtlinienverwaltung**.  

2.  Erweitern Sie in der Konsolenstruktur &lt;Gesamtstruktur&gt;\Domains\\&lt;Domäne&gt;, und klicken Sie dann **Group Policy Objects** (, in denen &lt;Gesamtstruktur&gt; ist die Name der Gesamtstruktur und &lt;Domäne&gt; ist der Name der Domäne, in dem die Gruppenrichtlinie festgelegt werden sollen).  

3.  In der Konsolenstruktur mit der Maustaste **Group Policy Objects**, und klicken Sie auf **neu**.  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_80.gif)  

4.  In der **neues Gruppenrichtlinienobjekt** (Dialogfeld), geben <GPO Name>, und klicken Sie auf **OK** (, in denen *Gruppenrichtlinienobjektname* ist der Name des dieses Gruppenrichtlinienobjekt).  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_81.gif)  

5.  Klicken Sie im Detailbereich mit der Maustaste **<GPO Name>**, und klicken Sie auf **bearbeiten**.  

6.  Navigieren Sie zu **Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, und klicken Sie auf **Zuweisen von Benutzerrechten**.  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_82.gif)  

7.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass die Mitglieder der Gruppe "Administratoren" Zugriff auf MemberServer und Arbeitsstationen über das Netzwerk wie folgt:  

    1.  Doppelklicken Sie auf **Zugriff vom Netzwerk auf diesen Computer Verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administratoren**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_83.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

8.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass die Mitglieder der Gruppe "Administratoren" Anmelden als Stapelverarbeitungsauftrag wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Batchauftrag verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administratoren**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_84.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

9. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass die Mitglieder der Gruppe "Administratoren" Anmelden als Dienst wie folgt:  

    1.  Doppelklicken Sie auf **Anmelden als Dienst verweigern** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administratoren**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_85.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

10. Zum Beenden **Gruppenrichtlinienverwaltungs-Editor**, klicken Sie auf **Datei**, und klicken Sie auf **beenden**.  

11. In **Gruppenrichtlinienverwaltung**, verknüpfen Sie das Gruppenrichtlinienobjekt auf dem Mitgliedsserver und die Arbeitsstation Organisationseinheiten wie folgt:  

    1.  Navigieren Sie zu der &lt;Gesamtstruktur&gt;> \Domains\\&lt;Domäne&gt; (wobei &lt;Gesamtstruktur&gt; ist der Name der Gesamtstruktur und &lt;Domäne&gt; ist der Name für die Domäne, in dem die Gruppenrichtlinie festgelegt werden sollen).  

    2.  Mit der rechten Maustaste in der Organisationseinheit, die das Gruppenrichtlinienobjekt wird auf angewendet werden, und klicken Sie auf **vorhandenes Gruppenrichtlinienobjekt verknüpfen**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_86.gif)  

    3.  Wählen Sie das Gruppenrichtlinienobjekt, das Sie gerade erstellt haben, und klicken Sie auf **OK**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_87.gif)  

    4.  Erstellen Sie Links zu allen anderen Organisationseinheiten, die Arbeitsstationen enthalten.  

    5.  Erstellen Sie Verknüpfungen mit allen anderen Organisationseinheiten, die Member-Server enthalten.  

        > [!IMPORTANT]  
        > Jump-Server zum Verwalten von Domänencontrollern und Active Directory verwendet werden, sicher, dass Jump-Server befinden, in einer Organisationseinheit, zu dem dieser Gruppenrichtlinienobjekte nicht verknüpft ist.  

        > [!NOTE]  
        > Wenn Sie Einschränkungen auf die Gruppe "Administratoren" in Gruppenrichtlinienobjekten implementieren, werden die Einstellungen von Windows auf Mitglieder der lokalen Administratorengruppe des Computers zusätzlich zur Gruppe "Administratoren" der Domäne angewendet. Aus diesem Grund sollten Sie Vorsicht walten, bei der Implementierung von Einschränkungen in der Gruppe "Administratoren". Obwohl das Verbot von Netzwerk, Batch und Dienst-Anmeldungen für Mitglieder der Gruppe "Administratoren" wird empfohlen, ganz egal, wo es möglich, zu implementieren ist, beschränken Sie nicht lokale Anmeldungen oder Anmeldungen über Remote Desktop Services. Blockieren diese Anmeldetypen kann legitime Verwaltung eines Computers von einem Mitglied der lokalen Gruppe "Administratoren" blockieren.  
        >   
        > Der folgende Screenshot zeigt die Konfigurationseinstellungen, die eine unsachgemäße Verwendung des integrierten Blockierung lokalen und Domäne Administratorkonten, zusätzlich zu unsachgemäße Verwendung des integrierten lokalen oder Domänengruppen der Administratoren. Beachten Sie, dass die **anmelden über Remotedesktopdienste Verweigern** Benutzerrecht schließt nicht die Gruppe "Administratoren", da Integrieren der Codekomponente in diese Einstellung auch diese Anmeldungen für Konten blockieren würde, die Elemente des lokalen Computers Gruppe "Administratoren". Wenn Dienste auf dem Computer für die Ausführung im Kontext von alle privilegierten Gruppen in diesem Abschnitt beschriebenen konfiguriert sind, kann implementieren diese Einstellungen Dienste und Anwendungen fehlschlagen. Aus diesem Grund sollten wie bei allen die Empfehlungen in diesem Abschnitt, Sie gründlich Einstellungen für die Anwendbarkeit in Ihrer Umgebung testen.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_88.gif)  

#### <a name="step-by-step-instructions-to-grant-user-rights-to-the-administrators-group"></a>Schrittweise Anweisungen zum Erteilen von Benutzerrechten der Gruppe "Administratoren"  

1.  In **Server-Manager**, klicken Sie auf **Tools**, und klicken Sie auf **Gruppenrichtlinienverwaltung**.  

2.  Erweitern Sie in der Konsolenstruktur <Forest>\Domains\\<Domain>, und klicken Sie dann **Group Policy Objects** (wo <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, wo Sie möchten, Legen Sie die Gruppenrichtlinie).  

3.  In der Konsolenstruktur mit der Maustaste **Group Policy Objects**, und klicken Sie auf **neu**.  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_89.gif)  

4.  In der **neues Gruppenrichtlinienobjekt** (Dialogfeld), Typ <GPO Name>, und klicken Sie auf **OK** (, in denen <GPO Name> ist der Name des dieses Gruppenrichtlinienobjekt).  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_90.gif)  

5.  Klicken Sie im Detailbereich mit der Maustaste **<GPO Name>**, und klicken Sie auf **bearbeiten**.  

6.  Navigieren Sie zu **Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, und klicken Sie auf **Zuweisen von Benutzerrechten**.  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_91.gif)  

7.  Konfigurieren Sie die Benutzerrechte für die Mitglieder der Gruppe "Administratoren" Zugriff Domänencontroller über das Netzwerk zu ermöglichen, wie folgt:  

    1.  Doppelklicken Sie auf **Zugriff auf diesen Computer vom Netzwerk** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_92.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

8.  Konfigurieren Sie die Benutzerrechte zu Mitgliedern der Gruppe "Administratoren" anmelden, die lokal, indem Sie Folgendes tun:  

    1.  Doppelklicken Sie auf **lokal anmelden zulassen** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administratoren**, klicken Sie auf Häkchen **Namen**, und klicken Sie auf **OK**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_93.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

9. Konfigurieren Sie die Benutzerrechte zu Mitgliedern der Gruppe "Administratoren" Anmelden über Remotedesktopdienste wie folgt vorgehen:  

    1.  Doppelklicken Sie auf **anmelden über Remotedesktopdienste zulassen** , und wählen Sie **diese Richtlinieneinstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** , und klicken Sie auf **Durchsuchen**.  

    3.  Typ **Administratoren**, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_94.gif)  

    4.  Klicken Sie auf **OK**, und **OK** erneut aus.  

10. Zum Beenden **Gruppenrichtlinienverwaltungs-Editor**, klicken Sie auf **Datei**, und klicken Sie auf **beenden**.  

11. In **Gruppenrichtlinienverwaltung**, verknüpfen Sie das Gruppenrichtlinienobjekt auf die Organisationseinheit Domain Controllers, folgendermaßen aus:  

    1.  Navigieren Sie zu der <Forest>\Domains\\ <Domain> (wobei <Forest> ist der Name der Gesamtstruktur und <Domain> ist der Name der Domäne, in dem Sie die Gruppenrichtlinie festlegen möchten).  

    2.  Mit der rechten Maustaste in der Domänencontrollern, die Organisationseinheit, und klicken Sie auf **vorhandenes Gruppenrichtlinienobjekt verknüpfen**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_95.gif)  

    3.  Wählen Sie das Gruppenrichtlinienobjekt, das Sie gerade erstellt haben, und klicken Sie auf **OK**.  

        ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_96.gif)  

#### <a name="verification-steps"></a>Überprüfungsschritte  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen für "Zugriff auf diesen Computer vom Netzwerk verweigern"  
Versuchen Sie von jeder Mitgliedsserver oder Arbeitsstation, die durch die GPO-Änderungen (z. B. ein "sprungbrettserver") nicht beeinträchtigt ist, auf einem Mitgliedsserver oder Arbeitsstation über das Netzwerk zugreifen, die die GPO-Änderungen betroffen ist. Um die GPO-Einstellungen zu überprüfen, versuchen, auf das Systemlaufwerk Zuordnung von der **NET USE** Befehl.  

1.  Melden Sie sich lokal mit einem Konto an, die Mitglied der Gruppe "Administratoren" ist.  

2.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Eingabeaufforderung**, mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen** zu einer mit erhöhten Rechten öffnen. -Eingabeaufforderung.  

4.  Wenn Sie dazu aufgefordert werden, die Erhöhung zustimmen, klicken Sie auf **Ja**.  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_97.gif)  

5.  In der **Eingabeaufforderung** geben **net verwenden \\ \\ \<Servernamen\>\c$**, wobei \<Servernamen\> ist die Der Name der Mitgliedsserver oder Arbeitsstation, die Sie versuchen, über das Netzwerk zugreifen.  

6.  Der folgende Screenshot zeigt die Fehlermeldung, die angezeigt werden soll.  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_98.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Batchauftrag verweigern"  
Melden Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind sich lokal.  

###### <a name="create-a-batch-file"></a>Erstellen Sie eine Datei  

1.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Editor**, und klicken Sie auf **Editor**.  

3.  In **Editor**, Typ **Dir c:**.  

4.  Klicken Sie auf **Datei**, und klicken Sie auf **speichern**.  

5.  In der **Dateiname** Feld  **<Filename>bat** (, in denen <Filename> ist der Name der neuen Batchdatei).  

###### <a name="schedule-a-task"></a>Planen einer Aufgabe  

1.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

2.  In der **Suche** geben **Taskplaner**, und klicken Sie auf **Taskplaner**.  

    > [!NOTE]  
    > Klicken Sie auf Computern unter Windows 8, in das Suchfeld Geben Sie die Zeitpläne für Aufgaben, und Planen von Aufgaben auf.  

3.  Klicken Sie auf **Aktion**, und klicken Sie auf **Create Task**.  

4.  In der **Create Task** (Dialogfeld), Typ **<Task Name>** (, in denen <Task Name> ist der Name der neuen Aufgabe).  

5.  Klicken Sie auf die **Aktionen** Registerkarte, und klicken Sie auf **neu**.  

6.  In der **Aktion** die Option **ein Programm starten**.  

7.  In der **Programm/Skript** auf **Durchsuchen**, und wählen Sie die Batchdatei erstellt, der **eine Batchdatei erstellen** aus, und klicken Sie auf **Öffnen**.  

8.  Klicken Sie auf **OK**.  

9. Klicken Sie auf die Registerkarte **Allgemein**.  

10. In der **Sicherheitsoptionen** auf **Benutzer oder Gruppe ändern**.  

11. Geben Sie den Namen eines Kontos, das Mitglied der Gruppe "Administratoren" ist, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

12. Wählen Sie **ausgeführt wird, ob der Benutzer nicht protokollierten Onor ist** und **speichern Sie das Kennwort nicht**. Der Task wird nur auf lokale Computerressourcen zugreifen.  

13. Klicken Sie auf **OK**.  

14. Es sollte ein Dialogfeld angezeigt, die Anmeldeinformationen für anfordernden Benutzerkonto zum Ausführen des Tasks.  

15. Klicken Sie nach Eingabe des Kennworts an, auf **OK**.  

16. Ein Dialogfeld ähnlich der folgenden sollte angezeigt werden.  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_99.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>Überprüfen Sie die GPO-Einstellungen "Anmelden als Dienst verweigern"  

1.  Melden Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind sich lokal.  

2.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Services**, und klicken Sie auf **Services**.  

4.  Doppelklicken Sie auf die **Druckspooler**.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  In der **melden Sie sich als** die Option **dieses Konto**.  

7.  Klicken Sie auf **Durchsuchen**, geben Sie den Namen eines Kontos, das Mitglied der Gruppe "Administratoren" ist, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

8.  In der **Kennwort** und **Bestätigungskennwort** Felder, geben Sie das ausgewählte Konto-Kennwort ein, und klicken Sie auf **OK**.  

9. Klicken Sie auf **OK** drei weitere Male.  

10. Mit der rechten Maustaste **Druckspooler** , und klicken Sie auf **Neustart**.  

11. Wenn der Dienst neu gestartet wird, wird ein Dialogfeld ähnlich der folgenden sollte angezeigt werden.  

    ![Sichere Administratorgruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_100.png)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>Wiederherstellen von Änderungen an den Druckerwarteschlangendienst  

1.  Melden Sie von jeder Mitgliedsserver oder Arbeitsstation, die von der GPO-Änderungen betroffen sind sich lokal.  

2.  Zeigen Sie mit der Maus auf, in der oberen rechten oder unteren rechten Ecke des Bildschirms. Wenn die **Charms** Leiste angezeigt wird, klicken Sie auf **Suche**.  

3.  In der **Suche** geben **Services**, und klicken Sie auf **Services**.  

4.  Doppelklicken Sie auf die **Druckspooler**.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  In der **melden Sie sich als** auf **Lokales System** -Konto, und klicken Sie auf **OK**.  
