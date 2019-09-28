---
ms.assetid: 4baefbd3-038f-44c0-85ba-f24e9722b757
title: 'Anhang G: Sichern von Administratoren Gruppen in Active Directory'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: cdea04e211b1873ff51c4bc3dc9ff24e746ead69
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408641"
---
# <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>Anhang G: Sichern von Administratoren Gruppen in Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>Anhang G: Sichern von Administratoren Gruppen in Active Directory  
Wie bei den Gruppen Organisations-Admins (Enterprise Admins, EA) und Domänen-Admins muss die Mitgliedschaft in der Gruppe integrierte Administratoren (BA) nur in Build-oder Notfall Wiederherstellungs Szenarios erforderlich sein. Es dürfen keine alltäglichen Benutzerkonten in der Gruppe "Administratoren" vorhanden sein, mit Ausnahme des integrierten Administrator Kontos für die Domäne, sofern Sie wie in [anhang D beschrieben gesichert wurde: Sichern integrierter Administrator Konten in Active Directory @ no__t-0.  

Administratoren sind standardmäßig Besitzer der meisten AD DS Objekte in ihren jeweiligen Domänen. Die Mitgliedschaft in dieser Gruppe ist möglicherweise in Build-oder Notfall Wiederherstellungs Szenarien erforderlich, in denen der Besitz oder die Fähigkeit, Objekte zu übernehmen, erforderlich ist. Außerdem erben das und EAS aufgrund der Standardmitgliedschaft in der Gruppe "Administratoren" eine Reihe ihrer Rechte und Berechtigungen. Die Standard Gruppen Schachtelung für privilegierte Gruppen in Active Directory sollte nicht geändert werden, und die Administratoren Gruppe jeder Domäne sollte wie in den folgenden Schritt-für-Schritt-Anweisungen beschrieben gesichert werden.  

Für die Gruppe "Administratoren" in jeder Domäne in der Gesamtstruktur:  

1.  Entfernen Sie alle Mitglieder aus der Gruppe Administratoren, mit der Ausnahme, dass das integrierte Administrator Konto für die Domäne verfügbar ist, vorausgesetzt, dass Sie wie in [anhang D beschrieben gesichert wurde: Sichern integrierter Administrator Konten in Active Directory @ no__t-0.  

2.  In GPOs, die mit Organisationseinheiten verknüpft sind, die Mitglieds Server und Arbeitsstationen in jeder Domäne enthalten, sollte die BA-Gruppe den folgenden Benutzerrechten in **Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien \ Zuweisen von Benutzerrechten**  

    -   Zugriff vom Netzwerk auf diesen Computer verweigern  

    -   Anmelden als Batchauftrag verweigern  

    -   Anmelden als Dienst verweigern  

3.  Bei der Organisationseinheit "Domänen Controller" in jeder Domäne in der Gesamtstruktur sollten der Gruppe "Administratoren" die folgenden Benutzerrechte erteilt werden:  

    -   Auf diesen Computer vom Netzwerk aus zugreifen.  

    -   Lokale Anmeldung zulassen  

    -   Anmelden über Remotedesktopdienste zulassen  

4.  Die Überwachung sollte so konfiguriert werden, dass Warnungen gesendet werden, wenn Änderungen an den Eigenschaften oder der Gruppe "Administratoren" vorgenommen werden.  

#### <a name="step-by-step-instructions-for-removing-all-members-from-the-administrators-group"></a>Schritt-für-Schritt-Anleitung zum Entfernen aller Mitglieder aus der Gruppe "Administratoren"  

1.  KlickenSie in Server-Manager **auf Extras, und**klicken Sie dann auf **Active Directory Benutzer und Computer**.  

2.  Um alle Mitglieder aus der Gruppe "Administratoren" zu entfernen, führen Sie die folgenden Schritte aus:  

    1.  Doppelklicken Sie auf die Gruppe **Administratoren** , und klicken Sie auf die Registerkarte **Mitglieder** .  

        ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_79.gif)  

    2.  Wählen Sie ein Mitglied der Gruppe aus, klicken Sie auf **Entfernen**, klicken Sie auf **Ja**, und klicken Sie auf **OK**.  

3.  Wiederholen Sie Schritt 2, bis alle Mitglieder der Gruppe "Administratoren" entfernt wurden.  

#### <a name="step-by-step-instructions-to-secure-administrators-groups-in-active-directory"></a>Schritt-für-Schritt-Anleitung zum Sichern von Administratoren Gruppen in Active Directory  

1.  KlickenSie in Server-Manager **auf Extras, und**klicken Sie auf **Gruppenrichtlinie Verwaltung**.  

2.  Erweitern Sie in der Konsolen Struktur &lt;forest @ no__t-1\Domains @ no__t-2 @ no__t-3domain @ no__t-4, und **Gruppenrichtlinie Objekte** (wobei &lt;forest @ no__t-7 der Name der Gesamtstruktur und &lt;domäne @ no__t-9 der Name der Domäne ist, in der Sie Legen Sie den Gruppenrichtlinie) fest.  

3.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Gruppenrichtlinie Objekte**, und klicken Sie dann auf **neu**.  

    ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_80.gif)  

4.  Geben Sie im Dialogfeld **Neues** Gruppenrichtlinien Objekt <GPO Name> ein, und klicken Sie auf **OK** (wobei *GPO-Name* der Name dieses GPO ist).  

    ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_81.gif)  

5.  Klicken Sie im Detailfenster mit der rechten Maustaste auf **<GPO Name>** , und klicken Sie dann auf **Bearbeiten**.  

6.  Navigieren Sie zu **Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, **und klicken Sie**auf Zuweisen von  

    ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_82.gif)  

7.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Administratoren Gruppe über das Netzwerk auf Mitglieds Server und Arbeitsstationen zugreifen können. gehen Sie hierzu wie folgt vor:  

    1.  Doppelklicken Sie **auf Zugriff vom Netzwerk auf diesen Computer verweigern,** und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

    3.  Geben Sie **Administratoren**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**.  

        ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_83.gif)  

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .  

8.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass sich Mitglieder der Gruppe "Administratoren" als Batch Auftrag anmelden. gehen Sie hierzu wie folgt vor:  

    1.  Doppelklicken Sie auf **Anmelden als Batch Auftrag verweigern** , und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

    3.  Geben Sie **Administratoren**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**.  

        ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_84.gif)  

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .  

9. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass sich Mitglieder der Gruppe "Administratoren" als Dienst anmelden. gehen Sie hierzu wie folgt vor:  

    1.  Doppelklicken Sie auf **Anmelden als Dienst verweigern** , und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

    3.  Geben Sie **Administratoren**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**.  

        ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_85.gif)  

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .  

10. Um **Gruppenrichtlinienverwaltungs-Editor**zu beenden, klicken Sie auf **Datei**und dann auf **Beenden**.  

11. Verknüpfen Sie das Gruppenrichtlinien Objekt in **Gruppenrichtlinie Management**mit dem Mitglieds Server und Arbeitsstations Organisationseinheiten, indem Sie die folgenden Schritte ausführen:  

    1.  Navigieren Sie zum &lt;forest @ no__t-1 > \domains @ no__t-2 @ no__t-3domain @ no__t-4 (wobei &lt;forest @ no__t-6 der Name der Gesamtstruktur und &lt;domäne @ no__t-8 der Name der Domäne ist, in der Sie die Gruppenrichtlinie festlegen möchten).  

    2.  Klicken Sie mit der rechten Maustaste auf die Organisationseinheit, auf die das Gruppenrichtlinien Objekt angewendet wird, und klicken Sie auf **vorhandenes GPO verknüpfen**  

        ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_86.gif)  

    3.  Wählen Sie das soeben erstellte Gruppenrichtlinien Objekt aus, und klicken Sie auf **OK**.  

        ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_87.gif)  

    4.  Erstellen Sie Links zu allen anderen Organisationseinheiten, die Arbeitsstationen enthalten.  

    5.  Erstellen Sie Links zu allen anderen Organisationseinheiten, die Mitglieds Server enthalten.  

        > [!IMPORTANT]  
        > Wenn für die Verwaltung von Domänen Controllern und Active Directory Jump-Server verwendet werden, stellen Sie sicher, dass sich die jumpserver in einer Organisationseinheit befinden, mit der diese GPOs nicht verknüpft sind  

        > [!NOTE]  
        > Wenn Sie Einschränkungen für die Administratoren Gruppe in GPOs implementieren, wendet Windows die Einstellungen zusätzlich zur Administrator Gruppe der Domäne auf Mitglieder der lokalen Administratoren Gruppe eines Computers an. Daher sollten Sie bei der Implementierung von Einschränkungen in der Gruppe "Administratoren" Vorsicht walten lassen. Obwohl das Verweigern von Netzwerk-, Batch-und Dienst Anmeldungen für Mitglieder der Gruppe "Administratoren" empfohlen wird, wenn es möglich ist, lokale Anmeldungen oder Anmeldungen nicht über Remotedesktopdienste einzuschränken. Durch das Blockieren dieser Anmelde Typen kann die legitime Verwaltung eines Computers durch Mitglieder der lokalen Administrator Gruppe blockiert werden.  
        >   
        > Der folgende Screenshot zeigt die Konfigurationseinstellungen, die den Missbrauch von integrierten lokalen Konten und Domänen Administrator Konten blockieren, sowie die Verwendung integrierter lokaler oder Domänen Administratoren Gruppen. Beachten Sie, dass das Benutzerrecht zum **Verweigern von Anmeldungen über Remotedesktopdienste** die Gruppe "Administratoren" nicht einschließt, da diese Anmeldungen auch für Konten blockiert werden, die Mitglieder der Gruppe "Administratoren" des lokalen Computers sind, wenn Sie in diese Einstellung eingeschlossen werden. Wenn Dienste auf Computern für die Ausführung im Zusammenhang mit einer der in diesem Abschnitt beschriebenen privilegierten Gruppen konfiguriert sind, kann das Implementieren dieser Einstellungen zu Fehlern bei Diensten und Anwendungen führen. Daher sollten Sie wie alle Empfehlungen in diesem Abschnitt die Einstellungen für die Anwendbarkeit in Ihrer Umgebung gründlich testen.  

        ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_88.gif)  

#### <a name="step-by-step-instructions-to-grant-user-rights-to-the-administrators-group"></a>Schritt-für-Schritt-Anleitung zum Erteilen von Benutzerrechten für die Administratoren Gruppe  

1.  KlickenSie in Server-Manager **auf Extras, und**klicken Sie auf **Gruppenrichtlinie Verwaltung**.  

2.  Erweitern Sie in der Konsolen Struktur <Forest> \ Domänen @ no__t-1 @ no__t-2, und **Gruppenrichtlinie** Sie dann Objekte (wobei <Forest> der Name der Gesamtstruktur und <Domain> der Name der Domäne ist, in der Sie die Gruppenrichtlinie festlegen möchten).  

3.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Gruppenrichtlinie Objekte**, und klicken Sie dann auf **neu**.  

    ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_89.gif)  

4.  Geben Sie im Dialogfeld **Neues** Gruppenrichtlinien Objekt <GPO Name> ein, und klicken Sie auf **OK** (wobei <GPO Name> der Name dieses GPO ist).  

    ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_90.gif)  

5.  Klicken Sie im Detailfenster mit der rechten Maustaste auf **<GPO Name>** , und klicken Sie dann auf **Bearbeiten**.  

6.  Navigieren Sie zu **Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, **und klicken Sie**auf Zuweisen von  

    ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_91.gif)  

7.  Konfigurieren Sie die Benutzerrechte, damit Mitglieder der Gruppe "Administratoren" über das Netzwerk auf Domänen Controller zugreifen können. gehen Sie hierzu wie folgt vor:  

    1.  Doppelklicken Sie **auf Zugriff auf diesen Computer vom Netzwerk aus,** und wählen Sie **die Option Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

    3.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

        ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_92.gif)  

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .  

8.  Konfigurieren Sie die Benutzerrechte, damit Mitglieder der Gruppe "Administratoren" sich lokal anmelden können, indem Sie Folgendes ausführen:  

    1.  Doppelklicken Sie auf **Lokal anmelden zulassen** , und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

    3.  Geben Sie **Administratoren**ein, klicken Sie auf **Namen**überprüfen und dann auf **OK**.  

        ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_93.gif)  

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .  

9. Konfigurieren Sie die Benutzerrechte, damit sich Mitglieder der Gruppe "Administratoren" über Remotedesktopdienste anmelden können. gehen Sie hierzu wie folgt vor:  

    1.  Doppelklicken Sie **auf Anmelden über Remotedesktopdienste zulassen** , und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

    3.  Geben Sie **Administratoren**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**.  

        ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_94.gif)  

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .  

10. Um **Gruppenrichtlinienverwaltungs-Editor**zu beenden, klicken Sie auf **Datei**und dann auf **Beenden**.  

11. Verknüpfen Sie das Gruppenrichtlinien Objekt in **Gruppenrichtlinie Management**mit der Organisationseinheit Domänen Controller, indem Sie die folgenden Schritte ausführen:  

    1.  Navigieren Sie zum <Forest> \ Domänen @ no__t-1 @ no__t-2 (wobei <Forest> der Name der Gesamtstruktur und <Domain> der Name der Domäne ist, in der Sie die Gruppenrichtlinie festlegen möchten).  

    2.  Klicken Sie mit der rechten Maustaste auf die Organisationseinheit Domänen Controller, und klicken Sie auf **vorhandenes GPO**  

        ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_95.gif)  

    3.  Wählen Sie das soeben erstellte Gruppenrichtlinien Objekt aus, und klicken Sie auf **OK**.  

        ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_96.gif)  

#### <a name="verification-steps"></a>Überprüfungs Schritte  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>GPO-Einstellungen "Zugriff auf diesen Computer über das Netzwerk verweigern"  
Versuchen Sie auf einem Mitglieds Server oder einer Arbeitsstation, der nicht von den GPO-Änderungen (z. b. einem "Sprung Server") betroffen ist, auf einen Mitglieds Server oder eine Arbeitsstation über das Netzwerk zuzugreifen, das von den GPO-Änderungen betroffen ist. Um die GPO-Einstellungen zu überprüfen, versuchen Sie, das Systemlaufwerk mithilfe des Befehls **net use** zuzuordnen.  

1.  Melden Sie sich lokal mit einem Konto an, das Mitglied der Gruppe "Administratoren" ist.  

2.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

3.  Geben Sie im **Suchfeld** **Eingabeaufforderung**ein, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen** , um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen.  

4.  Wenn Sie aufgefordert werden, die Höhe zu genehmigen, klicken Sie auf **Ja**.  

    ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_97.gif)  

5.  Geben Sie im **Eingabe** Aufforderungs Fenster **net use \\ @ no__t-3 @ no__t-4server Name @ no__t-5\c $** ein, wobei \<server Name @ no__t-7 der Name des Mitglieds Servers oder der Arbeitsstation ist, auf den Sie über das Netzwerk zuzugreifen versuchen.  

6.  Der folgende Screenshot zeigt die Fehlermeldung, die angezeigt werden soll.  

    ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_98.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>"Anmelden als Batch Auftrag verweigern"-GPO-Einstellungen überprüfen  
Melden Sie sich lokal bei allen Mitglieds Servern oder Arbeitsstationen an, die von den GPO-Änderungen betroffen sind.  

###### <a name="create-a-batch-file"></a>Erstellen einer Batch Datei  

1.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

2.  Geben Sie im **Suchfeld den Suchbegriff** **Editor**ein, und klicken Sie auf **Editor**.  

3.  Geben **Sie im Editor**den Befehl **dir c:** ein.  

4.  Klicken Sie auf **Datei**und dann auf **Speichern**unter.  

5.  Geben Sie im Feld **Dateiname** **@no__t -2. bat** ein (wobei <Filename> der Name der neuen Batchdatei ist).  

###### <a name="schedule-a-task"></a>Planen einer Aufgabe  

1.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

2.  Geben Sie im **Suchfeld** den Text **Task Scheduler**ein, und klicken Sie auf **Taskplaner**.  

    > [!NOTE]  
    > Geben Sie auf Computern, auf denen Windows 8 ausgeführt wird, im Suchfeld Schedule Tasks ein, und klicken Sie auf Aufgaben planen.  

3.  Klicken Sie auf **Aktion**, und klicken Sie auf **Task erstellen**.  

4.  Geben Sie im Dialogfeld **Task erstellen** **<Task Name>** ein (wobei <Task Name> der Name der neuen Aufgabe ist).  

5.  Klicken Sie auf die Registerkarte **Aktionen** , und klicken Sie auf **neu**.  

6.  Wählen Sie im Feld **Aktion** die Option **Programm starten**aus.  

7.  Klicken Sie im Feld **Programm/Skript** auf **Durchsuchen**, suchen Sie die Batchdatei, die Sie im Abschnitt **Erstellen einer Batchdatei** erstellt haben, und klicken Sie auf **Öffnen**.  

8.  Klicken Sie auf **OK**.  

9. Klicken Sie auf die Registerkarte **Allgemein**.  

10. Klicken Sie im Feld **Sicherheitsoptionen** auf **Benutzer oder Gruppe ändern**.  

11. Geben Sie den Namen eines Kontos ein, das Mitglied der Gruppe "Administratoren" ist, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

12. Wählen Sie ausführen aus, **ob der Benutzer nicht angemeldet ist** , und speichern Sie das **Kennwort**nicht. Der Task hat nur Zugriff auf lokale Computerressourcen.  

13. Klicken Sie auf **OK**.  

14. Es wird ein Dialogfeld angezeigt, in dem die Anmelde Informationen des Benutzerkontos zum Ausführen des Tasks angefordert werden.  

15. Klicken Sie nach der Eingabe des Kennworts auf **OK**.  

16. Ein Dialogfeld ähnlich dem folgenden sollte angezeigt werden.  

    ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_99.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>GPO-Einstellungen "Anmelden als Dienst verweigern" überprüfen  

1.  Melden Sie sich lokal bei allen Mitglieds Servern oder Arbeitsstationen an, die von den GPO-Änderungen betroffen sind.  

2.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

3.  Geben Sie im **Suchfeld den Suchbegriff** **Dienste**ein, und klicken Sie auf **Dienste**.  

4.  Suchen Sie den **Druck Spooler**, und doppelklicken Sie darauf.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  Wählen Sie im Feld **Anmelden als** **das Konto**aus.  

7.  Klicken Sie auf **Durchsuchen**, geben Sie den Namen eines Kontos ein, das Mitglied der Gruppe Administratoren ist, klicken Sie auf **Namen überprüfen**, und klicken Sie dann auf **OK**.  

8.  Geben Sie in die Felder **Kennwort** und **Kennwort bestätigen** das Kennwort für das ausgewählte Konto ein, und klicken Sie auf **OK**.  

9. Klicken Sie drei weitere Male auf **OK** .  

10. Klicken Sie mit der rechten Maustaste auf **Druck Spooler** , und klicken **Sie auf**  

11. Wenn der Dienst neu gestartet wird, sollte ein Dialogfeld ähnlich dem folgenden angezeigt werden.  

    ![sichere Administrator Gruppen](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_100.png)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>Änderungen am Druckerspoolerdienst zurücksetzen  

1.  Melden Sie sich lokal bei allen Mitglieds Servern oder Arbeitsstationen an, die von den GPO-Änderungen betroffen sind.  

2.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

3.  Geben Sie im **Suchfeld den Suchbegriff** **Dienste**ein, und klicken Sie auf **Dienste**.  

4.  Suchen Sie den **Druck Spooler**, und doppelklicken Sie darauf.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  Klicken Sie im Feld **Anmelden als** auf **Lokales System** Konto, und klicken Sie dann auf **OK**.  
