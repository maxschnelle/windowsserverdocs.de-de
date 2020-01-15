---
ms.assetid: 13fe87d9-75cf-45bc-a954-ef75d4423839
title: 'Anhang I: Erstellen von Verwaltungs Konten für geschützte Konten und Gruppen in Active Directory'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 834aa2611ff2b965c9184524fa6782fb4477a4cd
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949137"
---
# <a name="appendix-i-creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>Anhang I: Erstellen von Verwaltungskonten für geschützte Konten und Gruppen in Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Eine der Herausforderungen bei der Implementierung eines Active Directory Modells, das sich nicht auf die permanente Mitgliedschaft in sehr privilegierten Gruppen stützt, besteht darin, dass es einen Mechanismus zum Auffüllen dieser Gruppen geben muss, wenn eine temporäre Mitgliedschaft in den Gruppen erforderlich ist. Einige privilegierte Identitäts Verwaltungslösungen erfordern, dass den Dienst Konten der Software permanente Mitgliedschaft in Gruppen wie z. b. da oder Administratoren in jeder Domäne in der Gesamtstruktur gewährt wird. Es ist jedoch technisch nicht erforderlich, dass Privileged Identity Management (PIM)-Lösungen ihre Dienste in solch hoch privilegierten Kontexten ausführen.  
  
Dieser Anhang enthält Informationen, die Sie für nativ implementierte oder Drittanbieter-PIM-Lösungen zum Erstellen von Konten mit eingeschränkten Berechtigungen verwenden können. Sie können jedoch auch mit der stringdirektionellen Kontrolle verwendet werden. Sie können jedoch auch zum Auffüllen privilegierter Gruppen in Active Directory verwendet werden. eine temporäre Erhöhung ist erforderlich. Wenn Sie PIM als systemeigene Lösung implementieren, können diese Konten von Administratoren verwendet werden, um die temporäre Gruppen Population durchzuführen. Wenn Sie PIM über Software von Drittanbietern implementieren, können Sie diese Konten möglicherweise an die Funktion als Dienst anpassen. Buchhaltungs.  
  
> [!NOTE]  
> Die in diesem Anhang beschriebenen Verfahren bieten einen Ansatz für die Verwaltung von Gruppen mit hohen Berechtigungen in Active Directory. Sie können diese Prozeduren an Ihre Anforderungen anpassen, zusätzliche Einschränkungen hinzufügen oder einige der hier beschriebenen Einschränkungen weglassen.  
  
## <a name="creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>Erstellen von Verwaltungs Konten für geschützte Konten und Gruppen in Active Directory

Das Erstellen von Konten, die zum Verwalten der Mitgliedschaft privilegierter Gruppen verwendet werden können, ohne dass die Verwaltungs Konten übermäßige Rechte und Berechtigungen verfügen müssen, besteht aus vier allgemeinen Aktivitäten, die in den Schritt-für-Schritt-Anweisungen beschrieben werden. Führen Sie  
  
1.  Zuerst sollten Sie eine Gruppe erstellen, die die Konten verwaltet, da diese Konten von einer begrenzten Anzahl vertrauenswürdiger Benutzer verwaltet werden sollen. Wenn Sie nicht bereits über eine OE-Struktur verfügen, die das Trennen privilegierter und geschützter Konten und Systeme von der allgemeinen Einwohnerzahl in der Domäne unterscheidet, sollten Sie eine erstellen. Obwohl in diesem Anhang keine speziellen Anweisungen bereitgestellt werden, zeigen Screenshots ein Beispiel für eine solche Organisationseinheiten Hierarchie an.  
  
2.  Erstellen Sie die Verwaltungs Konten. Diese Konten sollten als "reguläre" Benutzerkonten erstellt werden, und es sind keine Benutzerrechte mehr vorhanden, die über diejenigen hinausgehen, die Benutzern standardmäßig bereits erteilt wurden.  
  
3.  Implementieren Sie Einschränkungen für die Verwaltungs Konten, die Sie nur für den speziellen Zweck verwenden, für den Sie erstellt wurden. Außerdem können Sie steuern, wer die Konten aktivieren und verwenden darf (die Gruppe, die Sie im ersten Schritt erstellt haben).  
  
4.  Konfigurieren Sie die Berechtigungen für das AdminSDHolder-Objekt in jeder Domäne, damit die Verwaltungs Konten die Mitgliedschaft der privilegierten Gruppen in der Domäne ändern können.  
  
Sie sollten alle diese Prozeduren gründlich testen und Sie nach Bedarf für Ihre Umgebung ändern, bevor Sie Sie in einer Produktionsumgebung implementieren. Sie sollten außerdem überprüfen, ob alle Einstellungen erwartungsgemäß funktionieren (einige Testverfahren werden in diesem Anhang bereitgestellt), und Sie sollten ein Notfall Wiederherstellungs Szenario testen, in dem die Verwaltungs Konten nicht zur Verwendung zum Auffüllen geschützter Gruppen für die Wiederherstellung verfügbar sind. verwendet. Weitere Informationen zum Sichern und Wiederherstellen Active Directory finden Sie in der [schrittweisen Anleitung zur AD DS Sicherung und](https://technet.microsoft.com/library/cc771290(v=ws.10).aspx)Wiederherstellung.  
  
> [!NOTE]  
> Durch die Implementierung der in diesem Anhang beschriebenen Schritte erstellen Sie Konten, die in der Lage sind, die Mitgliedschaft aller geschützten Gruppen in den einzelnen Domänen zu verwalten, nicht nur die Active Directory Gruppen mit den höchsten Berechtigungen wie EAS, das und Bas. Weitere Informationen zu geschützten Gruppen in Active Directory finden Sie unter [Anhang C: geschützte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md).  
  
### <a name="step-by-step-instructions-for-creating-management-accounts-for-protected-groups"></a>Schritt-für-Schritt-Anleitung zum Erstellen von Verwaltungs Konten für geschützte Gruppen  
  
#### <a name="creating-a-group-to-enable-and-disable-management-accounts"></a>Erstellen einer Gruppe zum Aktivieren und Deaktivieren von Verwaltungs Konten

Die Kenn Wörter der Verwaltungs Konten sollten bei jeder Verwendung zurückgesetzt werden und sollten deaktiviert werden, wenn die Aktivitäten, die Sie benötigen, fertiggestellt werden Obwohl Sie ggf. auch die Implementierung von Smartcard-Anmelde Anforderungen für diese Konten in Erwägung gezogen haben, handelt es sich um eine optionale Konfiguration. diese Anweisungen gehen davon aus, dass die Verwaltungs Konten mit einem Benutzernamen und einem langen, komplexen Kennwort konfiguriert werden. Steuerelemente. In diesem Schritt erstellen Sie eine Gruppe, die über die Berechtigung zum Zurücksetzen des Kennworts für die Verwaltungs Konten und zum Aktivieren und Deaktivieren der Konten verfügt.  
  
Führen Sie die folgenden Schritte aus, um eine Gruppe zum Aktivieren und Deaktivieren von Verwaltungs Konten zu erstellen:  
  
1.  Klicken Sie in der OE-Struktur, in der Sie die Verwaltungs Konten einrichten werden, mit der rechten Maustaste auf die Organisationseinheit, in der Sie die Gruppe erstellen möchten, klicken Sie auf **neu** und dann auf **Gruppe**  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_115.png)  
  
2.  Geben Sie im Dialogfeld **Neues Objekt-Gruppe** einen Namen für die Gruppe ein. Wenn Sie beabsichtigen, diese Gruppe zu verwenden, um alle Verwaltungs Konten in Ihrer Gesamtstruktur zu aktivieren, legen Sie Sie als universelle Sicherheitsgruppe fest. Wenn Sie über eine Gesamtstruktur mit einer einzelnen Domäne verfügen oder beabsichtigen, eine Gruppe in jeder Domäne zu erstellen, können Sie eine globale Sicherheitsgruppe erstellen. Klicken Sie auf **OK** , um die Gruppe zu erstellen.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_116.png)  
  
3.  Klicken Sie mit der rechten Maustaste auf die soeben erstellte Gruppe, klicken Sie auf **Eigenschaften**und dann auf die Registerkarte **Objekt** . Wählen Sie im Dialogfeld **Objekt Eigenschaft** der Gruppe die Option **Objekt vor versehentlichem Löschen schützen**aus, was nicht nur verhindert, dass anderweitig autorisierte Benutzer die Gruppe löschen, sondern auch, dass Sie in eine andere Organisationseinheit verschoben wird, es sei denn, das Attribut wird zuerst deaktiviert.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_117.png)  
  
    > [!NOTE]  
    > Wenn Sie bereits Berechtigungen für die übergeordnete Organisationseinheiten der Gruppe konfiguriert haben, um die Verwaltung auf eine begrenzte Anzahl von Benutzern zu beschränken, müssen Sie möglicherweise nicht die folgenden Schritte ausführen. Sie werden hier bereitgestellt, damit Sie selbst dann, wenn Sie noch keine eingeschränkte administrative Kontrolle über die Struktur der Organisationseinheit implementiert haben, in der Sie diese Gruppe erstellt haben, die Gruppe vor Änderungen durch nicht autorisierte Benutzer sichern können.  
  
4.  Klicken Sie auf die Registerkarte **Mitglieder** , und fügen Sie die Konten für Mitglieder Ihres Teams hinzu, die für das Aktivieren von Verwaltungs Konten oder das Auffüllen geschützter Gruppen bei Bedarf verantwortlich sein werden.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_118.png)  
  
5.  Wenn Sie dies noch nicht getan haben, klicken Sie in der Konsole **Active Directory-Benutzer und-Computer** auf **anzeigen** , und wählen Sie **Erweiterte Features**aus. Klicken Sie mit der rechten Maustaste auf die soeben erstellte Gruppe, klicken Sie auf **Eigenschaften**und dann auf die Registerkarte **Sicherheit** . Klicken Sie auf der Registerkarte **Sicherheit** auf **erweitert**.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_119.png)  
  
6.  Klicken Sie im Dialogfeld **Erweiterte Sicherheitseinstellungen für [Gruppe]** auf **Vererbung deaktivieren**. Wenn Sie dazu aufgefordert werden, klicken Sie **auf geerbte Berechtigungen in explizite Berechtigungen für dieses Objekt konvertieren**, und klicken Sie auf **OK** , um zum Dialogfeld **Sicherheit** der Gruppe zurückzukehren.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_120.png)  
  
7.  Entfernen Sie auf der Registerkarte **Sicherheit** Gruppen, denen der Zugriff auf diese Gruppe nicht gestattet werden soll. Wenn Sie z. b. nicht möchten, dass authentifizierte Benutzer den Namen der Gruppe und allgemeine Eigenschaften lesen können, können Sie diesen ACE entfernen. Sie können auch ACEs entfernen, wie z. b. Konten für Konto-und Windows Server-kompatible Zugriffe vor Windows 2000. Sie sollten jedoch einen minimalen Satz von Objekt Berechtigungen überlassen. Behalten Sie die folgenden ACEs bei:  
  
    -   SELBST  
  
    -   SYSTEM  
  
    -   Domänen-Admins  
  
    -   Organisations-Admins  
  
    -   Administratoren  
  
    -   Windows-Autorisierungs Zugriffs Gruppe (falls zutreffend)  
  
    -   DOMÄNENCONTROLLER DER ORGANISATION  
  
    Obwohl es möglicherweise intuitiv erscheint, dass die Gruppen mit den höchsten Berechtigungen in Active Directory diese Gruppe verwalten können, besteht das Ziel der Implementierung dieser Einstellungen nicht darin, dass Mitglieder dieser Gruppen autorisierte Änderungen vornehmen. Vielmehr soll sichergestellt werden, dass bei einer Zeit, in der eine sehr hohe Berechtigungsstufe erforderlich ist, autorisierte Änderungen erfolgreich ausgeführt werden. Der Grund hierfür ist, dass das Ändern der standardmäßigen privilegierten Gruppen Schachtelung, der Rechte und der Berechtigungen in diesem Dokument nicht empfehlenswert ist. Wenn Sie die Standard Strukturen intakt lassen und die Mitgliedschaft der Gruppen mit den höchsten Berechtigungen im Verzeichnis leeren, können Sie eine sicherere Umgebung erstellen, die weiterhin erwartungsgemäß funktioniert.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_121.png)  
  
    > [!NOTE]  
    > Wenn Sie die Überwachungs Richtlinien für die Objekte in der OE-Struktur, in der Sie diese Gruppe erstellt haben, noch nicht konfiguriert haben, sollten Sie die Überwachung so konfigurieren, dass diese Gruppe Änderungen protokolliert.  
  
8.  Sie haben die Konfiguration der Gruppe abgeschlossen, die verwendet wird, um die Verwaltungs Konten bei Bedarf zu überprüfen und die Konten einzuchecken, wenn ihre Aktivitäten abgeschlossen sind.  
  
#### <a name="creating-the-management-accounts"></a>Erstellen der Verwaltungs Konten

Sie sollten mindestens ein Konto erstellen, das zum Verwalten der Mitgliedschaft privilegierter Gruppen in der Active Directory-Installation verwendet wird, vorzugsweise ein zweites Konto, das als Sicherungskopie dienen soll. Unabhängig davon, ob Sie die Verwaltungs Konten in einer einzelnen Domäne in der Gesamtstruktur erstellen und Ihnen Verwaltungsfunktionen für die geschützten Gruppen der Domänen gewähren oder ob Sie Verwaltungs Konten in jeder Domäne in der Gesamtstruktur implementieren möchten, werden die Prozeduren effektiv identisch.  
  
> [!NOTE]  
> Bei den Schritten in diesem Dokument wird davon ausgegangen, dass Sie noch keine rollenbasierten Zugriffs Steuerungen und privilegierte Identitätsverwaltung für Active Directory implementiert haben. Daher müssen einige Prozeduren von einem Benutzer ausgeführt werden, dessen Konto Mitglied der Gruppe "Domänen-Admins" für die betreffende Domäne ist.  
>   
> Wenn Sie ein Konto mit-Berechtigungen verwenden, können Sie sich bei einem Domänen Controller anmelden, um die Konfigurations Aktivitäten auszuführen. Schritte, die keine da-Berechtigungen erfordern, können von Konten mit weniger Berechtigungen ausgeführt werden, die bei administrativen Arbeitsstationen angemeldet sind. Bildschirmaufnahmen, die Dialogfelder anzeigen, die an der helleren blauen Farbe Grenzen, repräsentieren Aktivitäten, die auf einem Domänen Controller ausgeführt werden können. Screenshots, die Dialogfelder in der dunkleren blauen Farbe anzeigen, stellen Aktivitäten dar, die auf administrativen Arbeitsstationen mit Konten mit eingeschränkten Berechtigungen ausgeführt werden können.  
  
Führen Sie die folgenden Schritte aus, um die Verwaltungs Konten zu erstellen:  
  
1. Melden Sie sich bei einem Domänen Controller mit einem Konto an, das Mitglied der Gruppe "da" der Domäne ist.  

2. Starten Sie **Active Directory Benutzer und Computer** , und navigieren Sie zu der Organisationseinheit, in der Sie das Verwaltungskonto erstellen werden.  

3. Klicken Sie mit der rechten Maustaste auf die Organisationseinheit, und klicken Sie **dann auf** **neu** und  

4. Geben Sie im Dialogfeld **Neues Objekt-Benutzer** die gewünschten Benennungs Informationen für das Konto ein, und klicken Sie auf **weiter**.  

   ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_122.png)  
  
5. Geben Sie ein erstes Kennwort für das Benutzerkonto an, deaktivieren Sie **Benutzer muss Kennwort bei der nächsten Anmeldung ändern**, wählen Sie **Benutzer kann Kennwort nicht ändern** , **Konto ist deaktiviert**, und klicken Sie auf **weiter**.  

   ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_123.png)  

6. Vergewissern Sie sich, dass die Konto Details richtig sind, und klicken Sie auf **Fertig**  

7. Klicken Sie mit der rechten Maustaste auf das soeben erstellte Benutzerobjekt, und klicken Sie auf **Eigenschaften**.  

8. Klicken Sie auf die Registerkarte **Konto**.  

9. Wählen Sie im Feld **Konto Optionen** das Flag **Konto ist vertraulich und kann nicht delegiert werden** aus, wählen Sie das **Konto unterstützt Kerberos AES 128 Bit Encryption** und/oder das kennflag **dieses Konto unterstützt Kerberos AES 256 encryption** aus, und klicken Sie auf **OK**.  

   ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_124.png)  

   > [!NOTE]  
   > Da dieses Konto, wie andere Konten, eine begrenzte, aber leistungsstarke Funktion haben, sollte das Konto nur auf sicheren administrativen Hosts verwendet werden. Für alle sicheren administrativen Hosts in Ihrer Umgebung sollten Sie die Implementierung der Gruppenrichtlinie Einstellung **Netzwerksicherheit: Konfigurieren von Verschlüsselungstypen, die für Kerberos zulässig** sind, in Erwägung gezogen werden, um nur die sichersten Verschlüsselungstypen zuzulassen, die für sichere Hosts implementiert werden können.  
   >
   > Obwohl das Implementieren von sichereren Verschlüsselungstypen für die Hosts keine Angriffe auf Diebstahl von Anmelde Informationen durchführt, erfolgt die geeignete Verwendung und Konfiguration der sicheren Hosts. Das Festlegen stärkerer Verschlüsselungstypen für Hosts, die nur von privilegierten Konten verwendet werden, reduziert einfach die Gesamt Angriffsfläche der Computer.  
   >
   > Weitere Informationen zum Konfigurieren von Verschlüsselungstypen für Systeme und Konten finden Sie [unter Windows-Konfigurationen für den von Kerberos unterstützten Verschlüsselungstyp](https://blogs.msdn.com/b/openspecification/archive/2011/05/31/windows-configurations-for-kerberos-supported-encryption-type.aspx).  
   >
   > Diese Einstellungen werden nur auf Computern unterstützt, auf denen Windows Server 2012, Windows Server 2008 R2, Windows 8 oder Windows 7 ausgeführt wird.  
  
10. Wählen Sie auf der Registerkarte **Objekt** die Option **Objekt vor zufälligem Löschen schützen aus**. Dadurch wird nicht nur verhindert, dass das Objekt gelöscht wird (selbst bei autorisierten Benutzern), sondern verhindert, dass es in eine andere Organisationseinheit in der AD DS Hierarchie verschoben wird, es sei denn, das Kontrollkästchen wird zuerst von einem Benutzer mit der Berechtigung zum Ändern des Attributs gelöscht.  

    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_125.png)  

11. Klicken Sie auf die Registerkarte **Remote Steuerung** .  

12. Deaktivieren Sie das Flag zum **Aktivieren der Remote Steuerung** . Es sollte nie erforderlich sein, dass Supportmitarbeiter eine Verbindung zu den Sitzungen dieses Kontos herstellen, um Korrekturen zu implementieren.  

    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_126.png)  

    > [!NOTE]  
    > Jedes Objekt in Active Directory sollte über einen designierten IT-Besitzer und einen designierten Geschäfts Besitzer verfügen, wie in [Planen](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)der Gefährdung beschrieben. Wenn Sie den Besitz von AD DS Objekten in Active Directory (im Gegensatz zu einer externen Datenbank) nachverfolgen, sollten Sie die entsprechenden Besitzer Informationen in den Eigenschaften dieses Objekts eingeben.  
    >
    > In diesem Fall ist der Geschäftsinhaber höchstwahrscheinlich eine IT-Abteilung, und es besteht kein Verbot für Geschäftsinhaber, die auch als IT-Besitzer fungieren. Der Besitz von Objekten besteht darin, dass Sie Kontakte identifizieren können, wenn Änderungen an den Objekten vorgenommen werden müssen, vielleicht Jahre nach der anfänglichen Erstellung.  

13. Klicken Sie auf die Registerkarte **Organisation** .  

14. Geben Sie alle Informationen ein, die für die AD DS-Objekt Standards erforderlich sind.  

    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_127.png)  

15. Klicken Sie auf die Registerkarte **Einwählen** .  

16. Wählen Sie im Feld **Netzwerk Zugriffsberechtigung** die Option **Zugriff verweigern**aus. Dieses Konto sollte nie über eine Remote Verbindung eine Verbindung herstellen müssen.  

    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_128.png)  

    > [!NOTE]  
    > Es ist unwahrscheinlich, dass dieses Konto für die Anmeldung bei schreibgeschützten Domänen Controllern (Read-Only Domain Controllers, RODCs) in Ihrer Umgebung verwendet wird. Sollte es jedoch erforderlich sein, dass sich das Konto bei einem RODC anmelden muss, sollten Sie dieses Konto der abgelehnten RODC-Kenn Wort Replikations Gruppe hinzufügen, damit das zugehörige Kennwort nicht auf dem RODC zwischengespeichert wird.  
    >
    > Obwohl das Kennwort des Kontos nach jeder Verwendung zurückgesetzt werden sollte und das Konto deaktiviert werden soll, hat die Implementierung dieser Einstellung keine Auswirkungen auf das Konto, und es kann hilfreich sein, wenn ein Administrator das Zurücksetzen des Kontos vergisst. Kennwort und deaktivieren.  

17. Klicken Sie auf die Registerkarte **Mitglied von**.  

18. Klicken Sie auf **Add**.  

19. Geben Sie im Dialogfeld **Benutzer, Kontakte und Computer auswählen** die Option **verweigerte RODC-Kenn Wort Replikations Gruppe ein** , und klicken Sie auf **Namen** Wenn der Name der Gruppe in der Objektauswahl unterstrichen ist, klicken Sie auf **OK** , und überprüfen Sie, ob das Konto nun Mitglied der beiden Gruppen ist, die im folgenden Screenshot angezeigt werden. Fügen Sie das Konto nicht zu geschützten Gruppen hinzu.  

20. Klicken Sie auf **OK**.  

    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_129.png)  

21. Klicken Sie auf die Registerkarte **Sicherheit** und dann auf **erweitert**.  

22. Klicken Sie im Dialogfeld **Erweiterte Sicherheitseinstellungen** auf **Vererbung deaktivieren** , kopieren Sie die geerbten Berechtigungen als explizite Berechtigungen, und klicken Sie auf **Hinzufügen**.  

    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_130.png)  

23. Klicken Sie im Dialogfeld **Berechtigungs Eintrag für [Konto]** auf **Prinzipal auswählen** , und fügen Sie die Gruppe hinzu, die Sie im vorherigen Verfahren erstellt haben. Scrollen Sie zum unteren Rand des Dialog Felds, und klicken Sie auf **Alle löschen** , um alle Standard Berechtigungen zu entfernen.  

    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_131.png)  

24. Scrollen Sie nach oben im Dialogfeld **Berechtigungs Eintrag** . Stellen Sie sicher, dass die Dropdown Liste **Typ** auf **zulassen**festgelegt ist, und wählen Sie in der Dropdown Liste **gilt für** **nur dieses Objekt**aus.  

25. Wählen Sie im Feld **Berechtigungen** die Option **alle Eigenschaften lesen**, **Berechtigungen Lesen**und **Kennwort zurücksetzen**aus.  

    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_132.png)  

26. Wählen Sie im Feld **Eigenschaften** die Option **userAccountControl lesen** aus, und **schreiben Sie userAccountControl**.  

27. Klicken Sie im Dialogfeld **Erweiterte Sicherheitseinstellungen** **erneut auf** **OK**.  

    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_133.png)  

    > [!NOTE]  
    > Das **userAccountControl** -Attribut steuert mehrere Konto Konfigurationsoptionen. Sie können keine Berechtigung erteilen, um nur einige der Konfigurationsoptionen zu ändern, wenn Sie dem Attribut Schreibberechtigungen erteilen.  

28. Entfernen Sie im Feld **Gruppen-oder Benutzernamen** der Registerkarte **Sicherheit** alle Gruppen, die nicht für den Zugriff auf das Konto berechtigt sind. Entfernen Sie keine Gruppen, die mit deny-ACEs konfiguriert wurden, z. b. die Gruppe Jeder und das selbst berechnete Konto (dieser ACE wurde festgelegt, wenn der Benutzer das Kenn **Wort Kennwort nicht ändern** während der Erstellung des Kontos aktiviert war. Entfernen Sie außerdem nicht die soeben hinzugefügte Gruppe, das System Konto oder die Gruppen, z. b. EA, da, BA oder die Windows-Autorisierungs Zugriffs Gruppe.  

    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_134.png)  

29. Klicken Sie auf **erweitert** , und überprüfen Sie, ob das Dialogfeld Erweiterte Sicherheitseinstellungen dem folgenden Screenshot ähnelt.  

30. Klicken Sie auf **OK**und dann erneut auf **OK** , um das Eigenschaften Dialogfeld des Kontos zu schließen.  

    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_135.png)  

31. Das erste Verwaltungskonto ist nun fertiggestellt. Sie werden das Konto in einem späteren Verfahren testen.  

##### <a name="creating-additional-management-accounts"></a>Erstellen zusätzlicher Verwaltungs Konten

Sie können zusätzliche Verwaltungs Konten erstellen, indem Sie die vorherigen Schritte wiederholen, indem Sie das soeben erstellte Konto kopieren oder ein Skript erstellen, um Konten mit den gewünschten Konfigurationseinstellungen zu erstellen. Beachten Sie jedoch Folgendes: Wenn Sie das soeben erstellte Konto kopieren, werden viele der angepassten Einstellungen und ACLs nicht in das neue Konto kopiert, und Sie müssen die meisten Konfigurationsschritte wiederholen.  
  
Stattdessen können Sie eine Gruppe erstellen, der Sie Rechte zum Auffüllen und Auffüllen geschützter Gruppen delegieren, aber Sie müssen die Gruppe und die Konten, die Sie darin platzieren, sichern. Da in Ihrem Verzeichnis nur wenige Konten vorhanden sein sollten, denen die Verwaltung der Mitglieder geschützter Gruppen gewährt werden kann, ist das Erstellen einzelner Konten möglicherweise der einfachste Ansatz.  
  
Unabhängig davon, wie Sie eine Gruppe erstellen, in die Sie die Verwaltungs Konten platzieren, sollten Sie sicherstellen, dass jedes Konto wie zuvor beschrieben geschützt wird. Sie sollten auch die Implementierung von GPO-Einschränkungen in Erwägung gezogen, ähnlich wie in [Anhang D: sichern integrierter Administrator Konten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  
  
##### <a name="auditing-management-accounts"></a>Überwachen von Verwaltungs Konten

Sie sollten die Überwachung für das Konto so konfigurieren, dass mindestens alle Schreibvorgänge in das Konto protokolliert werden. Auf diese Weise können Sie nicht nur die erfolgreiche Aktivierung des Kontos und das Zurücksetzen des Kennworts während der autorisierten Verwendung ermitteln, sondern auch Versuche von nicht autorisierten Benutzern, das Konto zu manipulieren. Fehlerhafte Schreibvorgänge für das Konto sollten in Ihrem Siem-System (Security Information and Event Monitoring, Sicherheits-und Ereignisüberwachung) aufgezeichnet werden. Außerdem sollten Warnungen ausgegeben werden, die die Mitarbeiter informieren, die für die Untersuchung potenzieller Kompromisse verantwortlich sind.  
  
Siem-Lösungen nehmen Ereignis Informationen aus den beteiligten Sicherheitsquellen (z. b. Ereignisprotokolle, Anwendungsdaten, Netzwerkstreams, antischadsoftwareprodukte und Quellen zum Erkennen von Eindring Versuchen), sortieren die Daten und versuchen, intelligente Ansichten und proaktive Aktionen zu erstellen . Es gibt viele kommerzielle Siem-Lösungen, und viele Unternehmen erstellen private Implementierungen. Eine gut entworfene und ordnungsgemäß implementierte Siem-Lösung kann die Sicherheitsüberwachung und die Reaktionsfähigkeit von Vorfällen erheblich verbessern Die Funktionen und die Genauigkeit variieren jedoch sehr stark zwischen den Lösungen. Siems geht über den Rahmen dieses Artikels hinaus, aber die spezifischen Ereignis Empfehlungen sollten von jeder Siem-Implementierung berücksichtigt werden.  
  
Weitere Informationen zu empfohlenen Überwachungs Konfigurationseinstellungen für Domänen Controller finden Sie unter [Monitoring Active Directory for Anzeichen of Kompromittierung](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md). Domänen Controller spezifische Konfigurationseinstellungen werden im [Überwachungs Active Directory für Anzeichen einer](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)Gefährdung bereitgestellt.  
  
#### <a name="enabling-management-accounts-to-modify-the-membership-of-protected-groups"></a>Aktivieren von Verwaltungs Konten zum Ändern der Mitgliedschaft geschützter Gruppen

In diesem Verfahren konfigurieren Sie die Berechtigungen für das AdminSDHolder-Objekt der Domäne, damit die neu erstellten Verwaltungs Konten die Mitgliedschaft geschützter Gruppen in der Domäne ändern können. Dieses Verfahren kann nicht über eine grafische Benutzeroberfläche (GUI) ausgeführt werden.  
  
Wie in [Anhang C: geschützte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)erläutert, wird die ACL für das AdminSDHolder-Objekt einer Domäne beim Ausführen der SDPROP-Aufgabe effektiv in geschützte Objekte kopiert. Geschützte Gruppen und Konten erben nicht Ihre Berechtigungen vom AdminSDHolder-Objekt. Ihre Berechtigungen werden explizit so festgelegt, dass Sie mit den Berechtigungen im AdminSDHolder-Objekt übereinstimmen. Wenn Sie also Berechtigungen für das AdminSDHolder-Objekt ändern, müssen Sie diese für Attribute ändern, die für den Typ des geschützten Objekts geeignet sind, das Sie als Ziel haben.  
  
In diesem Fall erteilen Sie die neu erstellten Verwaltungs Konten, damit Sie das Members-Attribut für Gruppen Objekte lesen und schreiben können. Das AdminSDHolder-Objekt ist jedoch kein Gruppen Objekt, und Gruppen Attribute werden im grafischen ACL-Editor nicht verfügbar gemacht. Aus diesem Grund müssen Sie die Berechtigungs Änderungen über das Befehlszeilen-Hilfsprogramm DSACLS implementieren. Führen Sie die folgenden Schritte aus, um den (deaktivierten) Verwaltungs Konten Berechtigungen zum Ändern der Mitgliedschaft geschützter Gruppen zu erteilen:  
  
1. Melden Sie sich bei einem Domänen Controller an, vorzugsweise bei dem Domänen Controller mit der PDC-Emulator-Rolle (PDCE) mit den Anmelde Informationen eines Benutzerkontos, das Mitglied der Gruppe "da" in der Domäne ist.  
  
   ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_136.png)  
  
2. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung** klicken und **als Administrator ausführen**klicken  
  
   ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_137.gif)  
  
3. Wenn Sie aufgefordert werden, die Höhe zu genehmigen, klicken Sie auf **Ja**.  
  
   ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_138.gif)  
  
   > [!NOTE]  
   > Weitere Informationen über die Rechte Erweiterung und die Benutzerkontensteuerung (User Account Control, UAC) in Windows finden Sie auf der TechNet-Website unter [UAC-Prozesse und-Interaktionen](https://technet.microsoft.com/library/dd835561(v=WS.10).aspx) .  
  
4. Geben Sie an der Eingabeaufforderung (durch Ihre domänenspezifischen Informationen) **DSACLS [Distinguished Name des AdminSDHolder-Objekts in Ihrer Domäne]/G [Administrator Konto-UPN]: rpwp; Mitglied**ein.  
  
   ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_139.gif)  
  
   Der vorherige Befehl (bei dem die Groß-/Kleinschreibung nicht beachtet wird) funktioniert wie folgt:  
  
   - DSACLS legt ACEs in Verzeichnis Objekten fest oder zeigt diese an.  
  
   - CN = AdminSDHolder, CN = System, DC = tailspintoys, DC = msft identifiziert das zu ändernde Objekt.  
  
   - /G gibt an, dass ein Grant-ACE konfiguriert wird.  
  
   - PIM001@tailspintoys.msft ist der Benutzer Prinzipal Name (User Principal Name, UPN) des Sicherheits Prinzipals, dem die ACEs erteilt werden.  
  
   - Rpwp erteilt Berechtigungen für Lese-und Schreib Eigenschaften  
  
   - Member ist der Name der Eigenschaft (Attribut), für die die Berechtigungen festgelegt werden.  
  
   Weitere Informationen zur Verwendung von **DSACLS**erhalten Sie, wenn Sie an einer Eingabeaufforderung DSACLS ohne Parameter eingeben.  
  
   Wenn Sie mehrere Verwaltungs Konten für die Domäne erstellt haben, sollten Sie für jedes Konto den DSACLS-Befehl ausführen. Wenn Sie die ACL-Konfiguration für das AdminSDHolder-Objekt abgeschlossen haben, sollten Sie die Ausführung von SDPROP erzwingen oder warten, bis die geplante Ausführung abgeschlossen ist. Informationen zum Erzwingen der Ausführung von SDPROP finden Sie unter "Manuelles Ausführen von SDPROP" in [Anhang C: geschützte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md).  
  
   Wenn SDPROP ausgeführt wurde, können Sie überprüfen, ob die Änderungen, die Sie am AdminSDHolder-Objekt vorgenommen haben, auf geschützte Gruppen in der Domäne angewendet wurden. Sie können dies nicht überprüfen, indem Sie die ACL für das AdminSDHolder-Objekt aus den oben beschriebenen Gründen anzeigen, aber Sie können überprüfen, ob die Berechtigungen angewendet wurden, indem Sie die ACLs für geschützte Gruppen anzeigen.  
  
5. Vergewissern Sie sich unter **Active Directory Benutzer und Computer**, dass Sie **Erweiterte Features**aktiviert haben. Klicken Sie hierzu auf **anzeigen**, suchen Sie die Gruppe **Domänen-Admins** , klicken Sie mit der rechten Maustaste auf die Gruppe, und klicken Sie auf **Eigenschaften**.  
  
6. Klicken Sie auf die Registerkarte **Sicherheit** und dann auf **erweitert** , um das Dialogfeld **Erweiterte Sicherheitseinstellungen für Domänen-Admins** zu öffnen.  
  
   ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_140.gif)  
  
7. Wählen Sie **ACE für das Verwaltungskonto zulassen aus** , und klicken Sie auf **Bearbeiten**. Stellen Sie sicher, dass dem Konto nur die Berechtigungen **Mitglieder lesen** und **Mitglieder schreiben** für die Gruppe da erteilt wurden, und klicken Sie auf **OK**.  
  
8. Klicken Sie im Dialogfeld **Erweiterte Sicherheitseinstellungen** auf **OK** , und klicken Sie erneut auf **OK** , um das Eigenschaften Dialogfeld für die Gruppe da zu schließen.  
  
   ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_141.gif)  
  
9. Sie können die vorherigen Schritte für andere geschützte Gruppen in der Domäne wiederholen. die Berechtigungen sollten für alle geschützten Gruppen identisch sein. Sie haben nun die Erstellung und Konfiguration der Verwaltungs Konten für die geschützten Gruppen in dieser Domäne abgeschlossen.  
  
    > [!NOTE]  
    > Jedes Konto, das über die Berechtigung zum Schreiben der Mitgliedschaft einer Gruppe in Active Directory verfügt, kann sich auch selbst zur Gruppe hinzufügen. Dieses Verhalten ist Entwurfs bedingt und kann nicht deaktiviert werden. Aus diesem Grund sollten Sie die Verwaltungs Konten immer deaktiviert lassen, wenn Sie nicht verwendet werden, und sollten die Konten genau überwachen, wenn Sie deaktiviert sind und wenn Sie verwendet werden.  
  
#### <a name="verifying-group-and-account-configuration-settings"></a>Überprüfen der Konfigurationseinstellungen für Gruppen und Konten

Nachdem Sie nun Verwaltungs Konten erstellt und konfiguriert haben, mit denen die Mitgliedschaft geschützter Gruppen in der Domäne geändert werden kann (einschließlich der am stärksten privilegierten EA-, da-und BA-Gruppen), sollten Sie überprüfen, ob die Konten und deren Verwaltungsgruppe ordnungsgemäß erstellt. Die Überprüfung besteht aus diesen allgemeinen Aufgaben:  
  
1.  Testen Sie die Gruppe, die Verwaltungs Konten aktivieren und deaktivieren kann, um zu überprüfen, ob Mitglieder der Gruppe die Konten aktivieren und deaktivieren und ihre Kenn Wörter zurücksetzen können, aber keine anderen administrativen Aktivitäten auf den Verwaltungs Konten ausführen können.  
  
2.  Testen Sie die Verwaltungs Konten, um sicherzustellen, dass Sie Mitglieder zu geschützten Gruppen in der Domäne hinzufügen und daraus entfernen können, aber keine anderen Eigenschaften geschützter Konten und Gruppen ändern können.  
  
##### <a name="test-the-group-that-will-enable-and-disable-management-accounts"></a>Testen Sie die Gruppe, die Verwaltungs Konten aktivieren und deaktivieren soll.
  
1.  Wenn Sie das Aktivieren eines Verwaltungs Kontos und das Zurücksetzen des Kennworts testen möchten, melden Sie sich bei einer sicheren administrativen Arbeitsstation mit einem Konto an, das Mitglied der Gruppe ist, die Sie in [Anhang I: Erstellen von Verwaltungs Konten für geschützte Konten und Gruppen in Active Directory](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)erstellt haben.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_142.gif)  
  
2.  Öffnen Sie **Active Directory Benutzer und Computer**, klicken Sie mit der rechten Maustaste auf das Verwaltungskonto, und klicken Sie auf **Konto aktivieren**.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_143.gif)  
  
3.  Es sollte ein Dialogfeld angezeigt werden, in dem bestätigt wird, dass das Konto aktiviert wurde.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_144.gif)  
  
4.  Legen Sie als nächstes das Kennwort für das Verwaltungskonto zurück. Klicken Sie hierzu mit der rechten Maustaste erneut auf das Konto, und klicken Sie dann auf **Kennwort zurücksetzen**.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_145.gif)  
  
5.  Geben Sie in die Felder **Neues Kennwort** und **Kennwort bestätigen** ein neues Kennwort für das Konto ein, und klicken Sie auf **OK**.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_146.gif)  
  
6.  Es wird ein Dialogfeld angezeigt, in dem bestätigt wird, dass das Kennwort für das Konto zurückgesetzt wurde.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_147.gif)  
  
7.  Versuchen Sie jetzt, zusätzliche Eigenschaften des Verwaltungs Kontos zu ändern. Klicken Sie mit der rechten Maustaste auf das Konto, und klicken Sie auf **Eigenschaften**und auf die Registerkarte **Remote Steuerung** .  
  
8.  Wählen Sie **Remote Steuerung aktivieren** und **dann**übernehmen aus. Der Vorgang sollte fehlschlagen, und die Fehlermeldung " **Zugriff verweigert** " sollte angezeigt werden.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_148.gif)  
  
9. Klicken Sie auf die Registerkarte **Konto** für das Konto, und versuchen Sie, den Namen des Kontos, die Anmeldezeiten oder die Anmelde Arbeitsstationen zu ändern. Alle sollten fehlschlagen, und Konto Optionen, die nicht durch das **userAccountControl** -Attribut gesteuert werden, sollten abgeblendet und nicht zur Änderung verfügbar sein.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_149.gif)  
  
10. Versuchen Sie, die Verwaltungsgruppe einer geschützten Gruppe, z. b. der Gruppe "da", hinzuzufügen. Wenn Sie auf **OK**klicken, wird eine Meldung angezeigt, in der Sie darüber informiert werden, dass Sie nicht über die Berechtigung zum Ändern der Gruppe verfügen.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_150.gif)  
  
11. Führen Sie nach Bedarf weitere Tests durch, um zu überprüfen, ob Sie mit Ausnahme von **userAccountControl** -Einstellungen und Zurücksetzen von Kenn Wörtern eine Konfiguration für das Verwaltungskonto  
  
    > [!NOTE]  
    > Das **userAccountControl** -Attribut steuert mehrere Konto Konfigurationsoptionen. Sie können keine Berechtigung erteilen, um nur einige der Konfigurationsoptionen zu ändern, wenn Sie dem Attribut Schreibberechtigungen erteilen.  
  
##### <a name="test-the-management-accounts"></a>Testen der Verwaltungs Konten

Nachdem Sie ein oder mehrere Konten aktiviert haben, die die Mitgliedschaft geschützter Gruppen ändern können, können Sie die Konten testen, um sicherzustellen, dass Sie die geschützte Gruppenmitgliedschaft ändern, aber keine anderen Änderungen an geschützten Konten und Gruppen ausführen können.  
  
1.  Melden Sie sich als erstes Verwaltungskonto bei einem sicheren administrativen Host an.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_151.gif)  
  
2.  Starten Sie **Active Directory Benutzer und Computer** , und suchen Sie nach der **Gruppe Domänen-Admins**.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Gruppe **Domänen-Admins** , **und klicken Sie**  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_152.gif)  
  
4.  Klicken Sie in den **Eigenschaften der Domänen Administratoren**auf die Registerkarte **Mitglieder** , und **Klicken Sie auf** hinzufügen. Geben Sie den Namen eines Kontos ein, dem temporäre Domänen-Admins-Berechtigungen erteilt werden, und klicken Sie auf **Namen überprüfen**. Wenn der Name des Kontos unterstrichen ist, klicken Sie auf **OK** , um zur Registerkarte **Mitglieder** zurückzukehren.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_153.gif)  
  
5.  Klicken Sie im Dialogfeld **Eigenschaften von Domänen-Admins** auf der Registerkarte **Mitglieder** auf **anwenden**. Nachdem Sie auf " **anwenden**" geklickt haben, sollte das Konto Mitglied der Gruppe "da" bleiben, und Sie sollten keine Fehlermeldungen erhalten.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_154.gif)  
  
6.  Klicken Sie im Dialogfeld Eigenschaften von **Domänen-Admins** auf die Registerkarte **verwaltet von** , und vergewissern Sie sich, dass Sie keinen Text in Felder eingeben können und alle Schaltflächen ausgegraut sind.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_155.gif)  
  
7.  Klicken Sie im Dialogfeld **Eigenschaften von Domänen-Admins** auf die Registerkarte **Allgemein** , und vergewissern Sie sich, dass Sie die Informationen zu dieser Registerkarte nicht ändern können.  
  
    ![Erstellen von Verwaltungs Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_156.gif)  
  
8.  Wiederholen Sie diese Schritte für weitere geschützte Gruppen nach Bedarf. Melden Sie sich nach Abschluss des Vorgangs an einem sicheren administrativen Host mit einem Konto an, das Mitglied der Gruppe ist, die Sie zum Aktivieren und Deaktivieren der Verwaltungs Konten erstellt haben. Setzen Sie dann das Kennwort des soeben getesteten Verwaltungs Kontos zurück, und deaktivieren Sie das Konto. Sie haben die Einrichtung der Verwaltungs Konten und der Gruppe abgeschlossen, die für das Aktivieren und Deaktivieren der Konten zuständig ist.  
