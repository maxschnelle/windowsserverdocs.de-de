---
ms.assetid: 017b88a6-f29b-4787-99b6-b5c8eaf8c3df
title: 'Anhang F: Sichern von Domänen-Admins-Gruppen in Active Directory'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 4f453aa9f076b0272821849840106dae0c52fbbc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408695"
---
# <a name="appendix-f-securing-domain-admins-groups-in-active-directory"></a>Anhang F: Sichern von Domänen-Admins-Gruppen in Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-f-securing-domain-admins-groups-in-active-directory"></a>Anhang F: Sichern von Domänen-Admins-Gruppen in Active Directory  
Wie bei der Gruppe der Organisations-Admins (Enterprise Admins, EA) sollte die Mitgliedschaft in der Gruppe Domänen-Admins (da) nur bei Build-oder Notfall Wiederherstellungs Szenarios erforderlich sein. Es dürfen keine alltäglichen Benutzerkonten in der Gruppe "da" vorhanden sein, mit Ausnahme des integrierten Administrator Kontos für die Domäne, sofern Sie wie in [anhang D beschrieben gesichert wurde: Sichern integrierter Administrator Konten in Active Directory @ no__t-0.  

Domänen-Admins sind standardmäßig Mitglieder der lokalen Administratoren Gruppen auf allen Mitglieds Servern und Arbeitsstationen in ihren jeweiligen Domänen. Diese Standard Schachtelung sollte nicht für Unterstützungs-und Notfall Wiederherstellungs Zwecke geändert werden. Wenn Domänen-Admins aus den lokalen Administratoren Gruppen auf dem Mitglieds Server entfernt wurden, sollte die Gruppe der Gruppe "Administratoren" auf jedem Mitglieds Server und jeder Arbeitsstation in der Domäne hinzugefügt werden. Die Gruppe "Domänen-Admins" jeder Domäne sollte wie in den folgenden Schritt-für-Schritt-Anweisungen beschrieben gesichert werden.  

Für die Gruppe "Domänen-Admins" in jeder Domäne in der Gesamtstruktur:  

1.  Entfernen Sie alle Mitglieder aus der Gruppe, mit der Ausnahme, dass das integrierte Administrator Konto für die Domäne verfügbar ist, vorausgesetzt, dass Sie wie in [anhang D beschrieben gesichert wurde: Sichern integrierter Administrator Konten in Active Directory @ no__t-0.  

2.  In Gruppenrichtlinien Objekten, die mit Organisationseinheiten verknüpft sind, die Mitglieds Server und Arbeitsstationen in jeder Domäne enthalten, sollte die Gruppe "da" den folgenden Benutzerrechten in **Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale richtlinien\benutzer** :  

    -   Zugriff vom Netzwerk auf diesen Computer verweigern  

    -   Anmelden als Batchauftrag verweigern  

    -   Anmelden als Dienst verweigern  

    -   Lokal anmelden verweigern  

    -   Anmelden über Remotedesktopdienste Benutzerrechte verweigern  

3.  Die Überwachung sollte so konfiguriert werden, dass Warnungen gesendet werden, wenn Änderungen an den Eigenschaften oder der Mitgliedschaft der Gruppe "Domänen-Admins" vorgenommen werden.  

#### <a name="step-by-step-instructions-for-removing-all-members-from-the-domain-admins-group"></a>Schritt-für-Schritt-Anleitung zum Entfernen aller Mitglieder aus der Gruppe "Domänen-Admins"  

1.  KlickenSie in Server-Manager **auf Extras, und**klicken Sie dann auf **Active Directory Benutzer und Computer**.  

2.  Um alle Mitglieder aus der Gruppe "da" zu entfernen, führen Sie die folgenden Schritte aus:  

    1.  Doppelklicken Sie auf die Gruppe **Domänen-Admins** und dann auf die Registerkarte **Mitglieder** .  

        ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_62.gif)  

    2.  Wählen Sie ein Mitglied der Gruppe aus, klicken Sie auf **Entfernen**, klicken Sie auf **Ja**, und klicken Sie auf **OK**.  

3.  Wiederholen Sie Schritt 2, bis alle Mitglieder der Gruppe "da" entfernt wurden.  

#### <a name="step-by-step-instructions-to-secure-domain-admins-in-active-directory"></a>Schritt-für-Schritt-Anleitung zum Sichern von Domänen Administratoren in Active Directory  

1.  KlickenSie in Server-Manager **auf Extras, und**klicken Sie auf **Gruppenrichtlinie Verwaltung**.  

2.  Erweitern Sie in der Konsolen Struktur \<forest @ no__t-1 @ no__t-2domains @ no__t-3 @ no__t-4domain @ no__t-5, und **Gruppenrichtlinie Objekte** (wobei \<forest @ no__t-8 der Name der Gesamtstruktur und \<domäne @ no__t-10 der Name der Domäne ist, in der Sie möchten den Gruppenrichtlinie festlegen).  

3.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Gruppenrichtlinie Objekte**, und klicken Sie dann auf **neu**.  

    ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_63.gif)  

4.  Geben Sie im Dialogfeld **Neues** Gruppenrichtlinien Objekt \<gpo-Name @ no__t-2 ein, und klicken Sie auf **OK** (wobei \<gpo-Name @ no__t-5 der Name dieses Gruppenrichtlinien Objekts ist).  

    ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_64.gif)  

5.  Klicken Sie im Detailfenster mit der rechten Maustaste auf \<gpo Name @ no__t-1, und klicken Sie dann auf **Bearbeiten**.  

6.  Navigieren Sie zu **Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien**, **und klicken Sie**auf Zuweisen von  

    ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_65.gif)  

7.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe "Domänen-Admins" auf Mitglieder Server und Arbeitsstationen über das Netzwerk zugreifen  

    1.  Doppelklicken Sie **auf Zugriff vom Netzwerk auf diesen Computer verweigern,** und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

    3.  Geben Sie **Domain Admins**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**.  

        ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_66.gif)  

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .  

8.  Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass sich Mitglieder der Gruppe "da" wie folgt anmelden:  

    1.  Doppelklicken Sie auf **Anmelden als Batch Auftrag verweigern** , und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

    3.  Geben Sie **Domain Admins**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**.  

        ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_67.gif)  

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .  

9. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass sich Mitglieder der Gruppe "da" wie folgt anmelden:  

    1.  Doppelklicken Sie auf **Anmelden als Dienst verweigern** , und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

    3.  Geben Sie **Domain Admins**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**.  

        ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_68.gif)  

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .  

10. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass sich Mitglieder der Gruppe "Domänen-Admins" lokal bei Mitglieds Servern und Arbeitsstationen anmelden, indem Sie Folgendes ausführen:  

    1.  Doppelklicken Sie auf **Lokal anmelden verweigern** , und wählen Sie **Diese Richtlinien Einstellungen definieren**aus.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

    3.  Geben Sie **Domain Admins**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**.  

        ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_69.gif)  

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .  

11. Konfigurieren Sie die Benutzerrechte, um zu verhindern, dass Mitglieder der Gruppe "Domänen-Admins" über Remotedesktopdienste auf Mitglieds Server und Arbeitsstationen zugreifen:  

    1.  Doppelklicken Sie auf **Anmelden über Remotedesktopdienste verweigern** , und wählen Sie **die Option Diese Richtlinien Einstellungen definieren**.  

    2.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen** und dann auf **Durchsuchen**.  

    3.  Geben Sie **Domain Admins**ein, klicken Sie auf **Namen überprüfen**und dann auf **OK**.  

        ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_70.gif)  

    4.  Klicken Sie erneut auf **OK**und dann auf **OK** .  

12. Um **Gruppenrichtlinienverwaltungs-Editor**zu beenden, klicken Sie auf **Datei**und dann auf **Beenden**.  

13. Verknüpfen Sie das Gruppenrichtlinien Objekt in Gruppenrichtlinie Management mit dem Mitglieds Server und Arbeitsstations Organisationseinheiten, indem Sie die folgenden Schritte ausführen:  

    1.  Navigieren Sie zum \<forest @ no__t-1\Domains @ no__t-2 @ no__t-3domain @ no__t-4 (wobei \<forest @ no__t-6 der Name der Gesamtstruktur und \<domäne @ no__t-8 der Name der Domäne ist, in der Sie die Gruppenrichtlinie festlegen möchten).  

    2.  Klicken Sie mit der rechten Maustaste auf die Organisationseinheit, auf die das Gruppenrichtlinien Objekt angewendet wird, und klicken Sie auf **vorhandenes GPO verknüpfen**  

        ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_71.gif)  

    3.  Wählen Sie das soeben erstellte Gruppenrichtlinien Objekt aus, und klicken Sie auf **OK**.  

        ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_72.gif)  

    4.  Erstellen Sie Links zu allen anderen Organisationseinheiten, die Arbeitsstationen enthalten.  

    5.  Erstellen Sie Links zu allen anderen Organisationseinheiten, die Mitglieds Server enthalten.  

        > [!IMPORTANT]  
        > Wenn für die Verwaltung von Domänen Controllern und Active Directory Jump-Server verwendet werden, stellen Sie sicher, dass sich die jumpserver in einer Organisationseinheit befinden, mit der diese GPOs nicht verknüpft sind  

#### <a name="verification-steps"></a>Überprüfungs Schritte  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>GPO-Einstellungen "Zugriff auf diesen Computer über das Netzwerk verweigern"  
Versuchen Sie auf einem Mitglieds Server oder einer Arbeitsstation, der nicht von den GPO-Änderungen (z. b. einem "Sprung Server") betroffen ist, auf einen Mitglieds Server oder eine Arbeitsstation über das Netzwerk zuzugreifen, das von den GPO-Änderungen betroffen ist. Um die GPO-Einstellungen zu überprüfen, versuchen Sie, das Systemlaufwerk mithilfe des Befehls **net use** zuzuordnen.  

1.  Melden Sie sich lokal mit einem Konto an, das Mitglied der Gruppe "Domänen-Admins" ist.  

2.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

3.  Geben Sie im **Suchfeld** **Eingabeaufforderung**ein, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen** , um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen.  

4.  Wenn Sie aufgefordert werden, die Höhe zu genehmigen, klicken Sie auf **Ja**.  

    ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_73.gif)  

5.  Geben Sie im **Eingabe** Aufforderungs Fenster **net use \\ @ no__t-3 @ no__t-4server Name @ no__t-5\c $** ein, wobei \<server Name @ no__t-7 der Name des Mitglieds Servers oder der Arbeitsstation ist, auf den Sie über das Netzwerk zuzugreifen versuchen.  

6.  Der folgende Screenshot zeigt die Fehlermeldung, die angezeigt werden soll.  

    ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_74.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>"Anmelden als Batch Auftrag verweigern"-GPO-Einstellungen überprüfen  

Melden Sie sich lokal bei allen Mitglieds Servern oder Arbeitsstationen an, die von den GPO-Änderungen betroffen sind.  

###### <a name="create-a-batch-file"></a>Erstellen einer Batch Datei  

1.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

2.  Geben Sie im **Suchfeld den Suchbegriff** **Editor**ein, und klicken Sie auf **Editor**.  

3.  Geben **Sie im Editor**den Befehl **dir c:** ein.  

4.  Klicken Sie auf **Datei**und dann auf **Speichern**unter.  

5.  Geben Sie im Feld Dateiname **@no__t -2Filename\>.bat** ein (wobei \<filename @ no__t-5 der Name der neuen Batchdatei ist).  

###### <a name="schedule-a-task"></a>Planen einer Aufgabe  

1.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

2.  Geben Sie im **Suchfeld** den Text **Task Scheduler**ein, und klicken Sie auf **Taskplaner**.  

    > [!NOTE]  
    > Geben Sie auf Computern, auf denen Windows 8 ausgeführt wird, im **Suchfeld** **Schedule Tasks**ein, und klicken Sie auf **Aufgaben planen**.  

3.  Klicken Sie in der Menüleiste **Taskplaner** auf **Aktion**, und klicken Sie auf **Task erstellen**.  

4.  Geben Sie im Dialogfeld **Task erstellen** **\<task Name @ no__t-3** ein (wobei \<task Name @ no__t-5 der Name der neuen Aufgabe ist).  

5.  Klicken Sie auf die Registerkarte **Aktionen** , und klicken Sie auf **neu**.  

6.  Wählen Sie im Feld **Aktion** die Option **Programm starten**aus.  

7.  Klicken Sie unter **Programm/Skript**auf **Durchsuchen**, suchen Sie die Batchdatei, die Sie im Abschnitt **Erstellen einer Batchdatei** erstellt haben, und klicken Sie auf **Öffnen**.  

8.  Klicken Sie auf **OK**.  

9. Klicken Sie auf die Registerkarte **Allgemein**.  

10. Klicken Sie unter **Sicherheits** Optionen auf **Benutzer oder Gruppe ändern**.  

11. Geben Sie den Namen eines Kontos ein, das Mitglied der Gruppe Domänen-Admins ist, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

12. Wählen Sie **Ausführen aus, ob der Benutzer angemeldet ist oder nicht** , und wählen Sie **Kennwort nicht speichern**aus. Der Task hat nur Zugriff auf lokale Computerressourcen.  

13. Klicken Sie auf **OK**.  

14. Es wird ein Dialogfeld angezeigt, in dem die Anmelde Informationen des Benutzerkontos zum Ausführen des Tasks angefordert werden.  

15. Klicken Sie nach Eingabe der Anmelde Informationen auf **OK**.  

16. Ein Dialogfeld ähnlich dem folgenden sollte angezeigt werden.  

    ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_75.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>GPO-Einstellungen "Anmelden als Dienst verweigern" überprüfen  

1.  Melden Sie sich lokal bei allen Mitglieds Servern oder Arbeitsstationen an, die von den GPO-Änderungen betroffen sind.  

2.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

3.  Geben Sie im **Suchfeld den Suchbegriff** **Dienste**ein, und klicken Sie auf **Dienste**.  

4.  Suchen Sie den **Druck Spooler**, und doppelklicken Sie darauf.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  Wählen Sie unter **Anmelden als**die Option **dieses Konto** aus.  

7.  Klicken Sie auf **Durchsuchen**, geben Sie den Namen eines Kontos ein, das Mitglied der Gruppe Domänen-Admins ist, klicken Sie auf **Namen überprüfen**, und klicken Sie auf **OK**.  

8.  Geben Sie unter **Kennwort** und **Kennwort bestätigen**das Kennwort des ausgewählten Kontos ein, und klicken Sie auf **OK**.  

9. Klicken Sie drei weitere Male auf **OK** .  

10. Klicken Sie mit der rechten Maustaste auf **Druck Spooler** , und klicken **Sie auf**  

11. Wenn der Dienst neu gestartet wird, sollte ein Dialogfeld ähnlich dem folgenden angezeigt werden.  

    ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_76.gif)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>Änderungen am Druckerspoolerdienst zurücksetzen  

1.  Melden Sie sich lokal bei allen Mitglieds Servern oder Arbeitsstationen an, die von den GPO-Änderungen betroffen sind.  

2.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

3.  Geben Sie im **Suchfeld den Suchbegriff** **Dienste**ein, und klicken Sie auf **Dienste**.  

4.  Suchen Sie den **Druck Spooler**, und doppelklicken Sie darauf.  

5.  Klicken Sie auf die Registerkarte **Anmelden**.  

6.  Wählen Sie unter **Anmelden als**das Konto **Lokales System** aus, und klicken Sie auf **OK**.  

##### <a name="verify-deny-log-on-locally-gpo-settings"></a>GPO-Einstellungen "Lokal anmelden verweigern"  

1.  Versuchen Sie, sich lokal mithilfe eines Kontos, das Mitglied der Gruppe "Domänen-Admins" ist, von einem beliebigen Mitglieds Server oder einer Arbeitsstation anzumelden, der von den GPO-Änderungen betroffen ist. Ein Dialogfeld ähnlich dem folgenden sollte angezeigt werden.  

    ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_77.gif)  

##### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>Überprüfen der GPO-Einstellungen "Anmelden über Remotedesktopdienste verweigern"    
1.  Bewegen Sie den Mauszeiger mit der Maus in die obere rechte Ecke des Bildschirms. Wenn die Leiste **Charms** angezeigt wird, klicken Sie auf **Suchen**.  

2.  Geben Sie im **Suchfeld als Suchbegriff** **Remote Desktop Verbindung**ein, und klicken Sie auf **Remotedesktopverbindung**.  

3.  Geben Sie im Feld **Computer** den Namen des Computers ein, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie auf **verbinden**. (Sie können auch die IP-Adresse anstelle des Computer namens eingeben.)  

4.  Wenn Sie dazu aufgefordert werden, geben Sie die Anmelde Informationen für ein Konto an, das Mitglied der Gruppe Domänen-Admins ist.  

5.  Ein Dialogfeld ähnlich dem folgenden sollte angezeigt werden.  

    ![sichere Domänen Administrator Gruppen](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_78.gif)  
