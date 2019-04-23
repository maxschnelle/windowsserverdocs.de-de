---
ms.assetid: 13fe87d9-75cf-45bc-a954-ef75d4423839
title: Anhang I - Verwaltungskonten für geschützte Konten und Gruppen in Active Directory erstellen
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c71b96f6c44cfc2b14b4c5d203f876e55cc728ec
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855631"
---
# <a name="appendix-i-creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>Anhang I: Erstellen von Verwaltungskonten für geschützte Konten und Gruppen in Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Eine der Herausforderungen bei der Implementierung eines Active Directory-Modells, das nicht auf permanente Mitgliedschaft in sehr privilegierten Gruppen basiert ist, dass es muss ein Mechanismus, um diese Gruppen auffüllen, wenn eine temporäre Mitgliedschaft in den Gruppen erforderlich ist. Einige Lösungen für die privilegierte identitätsverwaltung erfordern, dass es sich bei der Software-Dienstkonten permanente Mitgliedschaft in Gruppen wie z. B. Daten oder Administratoren in jeder Domäne in der Gesamtstruktur erteilt werden. Allerdings ist es technisch nicht erforderlich für Privileged Identity Management (PIM)-Lösungen für ihre Dienste in einem solchen hoch privilegierten Kontext ausgeführt.  
  
Dieser Anhang enthält Informationen, die Sie für PIM-Lösungen durch systemeigene Funktionen implementiert oder von Drittanbietern verwenden können, um Konten zu erstellen, die über eingeschränkte Berechtigungen und repräsentative Motoröltemperatur gesteuert werden können, jedoch können verwendet werden, um privilegierten Gruppen in Active Directory Auffüllen bei temporäre Erweiterung ist erforderlich. Wenn Sie PIM als native Lösung implementieren, können diese Konten von Administrationsmitarbeiter verwendet werden, bei der temporären Gruppe Auffüllung und, wenn Sie über Drittanbieter-Software PIM implementieren, ist Sie möglicherweise diese Konten für die Funktion als Dienst anpassen Konten.  
  
> [!NOTE]  
> Die in diesem Anhang beschriebenen Verfahren geben Sie einen Ansatz für die Verwaltung von sehr privilegierten Gruppen in Active Directory. Sie können diese Schritte Ihren Bedürfnissen, weitere Einschränkungen hinzufügen, anpassen oder weglassen, einige der Einschränkungen, die hier beschrieben werden.  
  
## <a name="creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>Erstellen von Verwaltungskonten für geschützte Konten und Gruppen in Active Directory

Erstellen von Konten, kann verwendet werden, um die Mitgliedschaft der privilegierten Gruppen zu verwalten, ohne die Verwaltungskonten auf zu viele Rechte und Berechtigungen erteilt werden müssen vier allgemeine Aktivitäten besteht, die in den folgenden schrittweisen Anleitungen beschrieben werden, Gehen Sie folgendermaßen vor:  
  
1.  Zunächst sollten Sie eine Gruppe, die die Konten verwalten erstellen, da diese Konten durch eine begrenzte Anzahl vertrauenswürdiger Benutzer verwaltet werden sollen. Wenn Sie nicht bereits eine OU-Struktur, die durch GALs privilegierten und geschützte Konten und Systeme die allgemeine Population in der Domäne verfügt verfügen, sollten Sie eine erstellen. Screenshots können zwar spezifische Anweisungen in diesem Anhang nicht bereitgestellt werden, ein Beispiel für solche einer Hierarchie von Organisationseinheiten angezeigt.  
  
2.  Erstellen Sie die Management-Konten. Diese Konten als "regular" Benutzerkonten erstellt und keine Benutzer Berechtigungen hinausgehen, die bereits in der Standardeinstellung für Benutzer gewährt werden.  
  
3.  Implementieren Sie Einschränkungen für die Management-Konten, die sie nur für den speziellen Zweck verwendbar machen für die sie erstellt wurden zusätzlich zu steuern, wer zu aktivieren und verwenden Sie die Konten (die Gruppe, die Sie im ersten Schritt erstellt haben) kann.  
  
4.  Konfigurieren Sie Berechtigungen für das Objekt "AdminSDHolder" in jeder Domäne, um die Verwaltungskonten so ändern Sie die Mitgliedschaft der privilegierten Gruppen in der Domäne zu ermöglichen.  
  
Sie sollten gründlich testen alle diese Verfahren und je nach Bedarf für Ihre Umgebung vor der Implementierung in einer produktionsumgebung zu ändern. Sie sollten auch überprüfen, dass alle Einstellungen wie erwartet funktionieren (einige testen Prozeduren werden in diesem Anhang bereitgestellt), und Sie sollten testen, einem Notfallwiederherstellungsszenario, in dem der Management-Konten sind nicht verfügbar, die zum Auffüllen der geschützter Gruppen, die für die Wiederherstellung verwendet werden, Zwecke. Weitere Informationen zum Sichern und Wiederherstellen von Active Directory finden Sie unter den [AD DS-Sicherung und Wiederherstellung schrittweise Anleitung für](https://technet.microsoft.com/library/cc771290(v=ws.10).aspx).  
  
> [!NOTE]  
> Implementieren Sie die Schritte in diesem Anhang, erstellen Sie Konten, die die Mitgliedschaft aller geschützten Gruppen, die in jeder Domäne, nicht nur den höchsten Berechtigungen Active Directory-Gruppen wie EAs, DAs und BAs verwalten kann. Weitere Informationen zu geschützten Gruppen in Active Directory, finden Sie unter [Anhang C: Geschützte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md).  
  
### <a name="step-by-step-instructions-for-creating-management-accounts-for-protected-groups"></a>Schrittweise Anleitungen zum Erstellen von Verwaltungskonten für geschützte Gruppen  
  
#### <a name="creating-a-group-to-enable-and-disable-management-accounts"></a>Erstellen einer Gruppe zum Aktivieren und Deaktivieren von Konten

Management-Konten müssen ihre Kennwörter zurücksetzen jede Verwendung und sollte deaktiviert werden, wenn Aktivitäten, dass diese abgeschlossen sind. Obwohl Sie auch erwägen, Smartcard-Anmeldung Anforderungen für diese Konten zu implementieren, es ist eine optionale Konfiguration, und diese Anweisungen setzen voraus, dass die Verwaltungskonten mit einen Benutzernamen und ein langes, komplexes Kennwort mit mindestens konfiguriert werden -Steuerelemente. In diesem Schritt erstellen Sie eine Gruppe, die über Berechtigungen zum Zurücksetzen des Kennworts auf den Management-Konten und zum Aktivieren und deaktivieren die Konten verfügt.  
  
Um eine Gruppe zum Aktivieren und Deaktivieren von Konten zu erstellen, führen Sie die folgenden Schritte aus:  
  
1.  In der OE-Struktur, in dem Sie werden die Verwaltungskonten speichern werden, mit der Maustaste der Organisationseinheit, in dem Sie die Gruppe erstellen möchten, klicken Sie auf **neu** , und klicken Sie auf **Gruppe**.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_115.png)  
  
2.  In der **neues Objekt – Gruppe** Dialogfeld Geben Sie einen Namen für die Gruppe. Wenn Sie dieser Gruppe auf "alle Verwaltungskonten in Ihrer Gesamtstruktur aktivieren" verwenden möchten, stellen sie eine universelle Sicherheitsgruppe. Wenn Sie die Gesamtstruktur mit eine einzelnen Domäne verfügen, oder wenn Sie planen, erstellen eine Gruppe in jeder Domäne, können Sie eine globale Sicherheitsgruppe erstellen. Klicken Sie auf **OK**, um die Gruppe zu erstellen.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_116.png)  
  
3.  Klicken Sie mit der rechten Maustaste auf die Gruppe, die Sie gerade erstellt haben, klicken Sie auf **Eigenschaften**, und klicken Sie dann auf die Registerkarte **Objekt** . In der Gruppennamens **-Objekteigenschaft** wählen Sie im Dialogfeld **schützen Objekt vor zufälligem Löschen**, die nicht nur verhindert, dass anderweitig autorisierte Benutzer die Gruppe löschen, sondern auch verschiebt es in eine andere, wenn das Attribut der erste ist die Auswahl aufgehoben Organisationseinheit.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_117.png)  
  
    > [!NOTE]  
    > Wenn Sie auf der Gruppe übergeordneten Organisationseinheiten zum Einschränken von Verwaltung, um eine begrenzte Anzahl von Benutzern bereits Berechtigungen konfiguriert haben, müssen Sie möglicherweise nicht die folgenden Schritte ausführen. Sie werden hier bereitgestellt, damit auch, wenn Sie noch nicht eingeschränkte Kontrolle zur Verwaltung von der OE-Struktur implementiert haben in denen Sie diese Gruppe erstellt haben, können Sie die Gruppe vor Änderungen sichern durch nicht autorisierte Benutzer.  
  
4.  Klicken Sie auf die **Mitglieder** Registerkarte, und fügen Sie die Konten für Mitglieder Ihres Teams, die verantwortlich für das Aktivieren von Verwaltungskonten, oder füllen sind Gruppen bei Bedarf geschützt.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_118.png)  
  
5.  Wenn Sie nicht bereits in geschehen die **Active Directory-Benutzer und-Computer** auf **Ansicht** , und wählen Sie **erweiterte Features**. Mit der rechten Maustaste in der Gruppe, die Sie gerade erstellt haben, klicken Sie auf **Eigenschaften**, und klicken Sie auf die **Sicherheit** Registerkarte. Klicken Sie auf der Registerkarte **Sicherheit** auf **Erweitert**.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_119.png)  
  
6.  In der **erweiterte Sicherheitseinstellungen für [-Gruppe]** Dialogfeld klicken Sie auf **Vererbung deaktivieren**. Wenn Sie dazu aufgefordert werden, klicken Sie auf **vererbte Berechtigungen in explizite Berechtigungen für dieses Objekt konvertieren**, und klicken Sie auf **OK** in der Gruppennamens die zurückzugebenden **Sicherheit** im Dialogfeld.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_120.png)  
  
7.  Auf der **Sicherheit** Registerkarte verwenden, entfernen Sie Gruppen, die auf diese Gruppe keinen Zugriff haben sollte. Wenn Sie nicht, dass authentifizierte Benutzer, um die Namen und den allgemeinen Eigenschaften der Gruppennamens lesen zu können möchten, können Sie z. B. dieser ACE entfernen. Sie können auch ACEs, etwa solche für Operatoren und Prä-Windows 2000 Server kompatible Kontozugriff entfernen. Sie sollten jedoch einen minimalen Satz von Objektberechtigungen behalten. Lassen Sie die folgenden ACEs intakt:  
  
    -   SELF  
  
    -   SYSTEM  
  
    -   Domänen-Admins  
  
    -   Organisations-Admins  
  
    -   Administratoren  
  
    -   Windows-Autorisierungszugriffsgruppe (falls zutreffend)  
  
    -   DOMÄNENCONTROLLER DER ORGANISATION  
  
    Es mag nicht besonders intuitiv, um die höchste privilegierten Gruppen in Active Directory zur Verwaltung dieser Gruppe zu ermöglichen, ist Ihr Ziel bei der Implementierung von diesen Einstellungen nicht verhindern, dass die Mitglieder dieser Gruppen autorisierte Änderungen vornehmen. Das Ziel ist, stellen Sie sicher, dass bei Anlass, sehr hohe Berechtigungsebene erforderlich, autorisierte Änderungen erfolgreich ist. Aus diesem Grund, dass das Ändern der standardmäßigen privilegierte gruppenverschachtelung, Rechte und Berechtigungen sind in diesem Dokument nicht empfehlenswert ist. Beibehalten von Standardstrukturen und leeren der Mitgliedschaft in den höchsten Berechtigungen Gruppen im Verzeichnis, können Sie eine sicherere Umgebung erstellen, die immer noch wie erwartet funktioniert.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_121.png)  
  
    > [!NOTE]  
    > Wenn Sie nicht bereits Überwachungsrichtlinien für die Objekte in der OE-Struktur konfiguriert haben, in dem Sie diese Gruppe erstellt haben, sollten Sie die Überwachung konfigurieren zum Protokollieren der Änderungen dieser Gruppe.  
  
8.  Sie haben die Konfiguration der Gruppe, die verwendet wird, um "Auschecken" Management-Konten, wenn sie benötigt werden, und "Einchecken" die Konten bei ihrer Aktivitäten abgeschlossen wurden.  
  
#### <a name="creating-the-management-accounts"></a>Erstellen der Management-Konten

Erstellen Sie mindestens ein Konto an, die zum Verwalten der Mitgliedschaft in privilegierten Gruppen in Ihrer Active Directory-Installation verwendet werden, vorzugsweise ein zweites Konto, als Sicherung dient. Gibt an, ob Sie die Management-Konten in einer einzelnen Domäne in der Gesamtstruktur erstellen, und gewähren diese Verwaltungsfunktionen für alle Domänen auch Gruppen protected "oder", ob Sie entscheiden, Management-Konten in jeder Domäne in der Gesamtstruktur zu implementieren, werden die Prozeduren identisch.  
  
> [!NOTE]  
> Die Schritte in diesem Dokument wird davon ausgegangen, dass Sie rollenbasierte zugriffssteuerungen und privileged Identitätsmanagement für Active Directory noch nicht implementiert haben. Aus diesem Grund müssen einige Verfahren von einem Benutzer ausgeführt werden, dessen Konto Mitglied der Gruppe "Domänen-Admins" für die jeweilige Domäne modelliert ist.  
>   
> Wenn Sie ein Konto mit Berechtigungen für Daten verwenden, können Sie zu einem Domänencontroller die Konfigurationsaufgaben ausführen anmelden. Schritte, die keine Berechtigungen für Daten erfordern, können mit weniger privilegierten Konten ausgeführt werden, die auf Arbeitsstationen für Administratoren angemeldet sind. Screenshots, die Dialogfelder umrandet, in der blauen helleren Farbe angezeigt darstellen, Aktivitäten, die auf einem Domänencontroller ausgeführt werden können. Screenshots, die Dialogfelder in das dunklere blau angezeigt stellen die Aktivitäten, die auf administrativen Arbeitsstationen mit Konten ausgeführt werden können, die über Berechtigungen eingeschränkte dar.  
  
Um die Management-Konten zu erstellen, führen Sie die folgenden Schritte aus:  
  
1. Melden Sie sich auf einen Domänencontroller mit einem Konto an, das Mitglied der Gruppe "Daten" der Domäne ist.  

2. Starten Sie **Active Directory-Benutzer und-Computer** und navigieren Sie zu der Organisationseinheit, in denen erstellen Sie das Managementkonto.  

3. Mit der rechten Maustaste in der Organisationseinheit, und klicken Sie auf **neu** , und klicken Sie auf **Benutzer**.  

4. In der **neues Objekt – Benutzer** Dialogfeld, geben Sie Ihre gewünschten Benennungskonventionen für das Konto, und auf **Weiter**.  

   ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_122.png)  
  
5. Geben Sie ein anfängliches Kennwort für das Benutzerkonto, klarer **Benutzer muss Kennwort bei der nächsten Anmeldung ändern**Option **Benutzer kann Kennwort nicht ändern** und **Konto ist deaktiviert**, und Klicken Sie auf **Weiter**.  

   ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_123.png)  

6. Stellen Sie sicher, dass die Kontodetails richtig sind, und klicken Sie auf **Fertig stellen**.  

7. Mit der rechten Maustaste in des User-Objekts, das Sie gerade erstellt haben, und klicken Sie auf **Eigenschaften**.  

8. Klicken Sie auf die **Konto** Registerkarte.  

9. In der **Kontooptionen** die Option der **Konto ist vertraulich und kann nicht delegiert werden** Flag, wählen die **dieses Konto unterstützt Kerberos-AES-128-Bit-Verschlüsselung** und/oder die **dieses Konto unterstützt Kerberos-AES-256-Verschlüsselung** kennzeichnen, und klicken Sie auf **OK**.  

   ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_124.png)  

   > [!NOTE]  
   > Da dieses Konto ein, z. B. andere Konten eine begrenzte, aber leistungsstarke Funktion verfügt, sollte das Konto nur für sichere administrative Hosts verwendet werden. Für alle sichere administrative Hosts in Ihrer Umgebung, sollten Sie erwägen, implementieren die gruppenrichtlinieneinstellung **Netzwerksicherheit: Für Kerberos zulässige Verschlüsselungstypen konfigurieren** um nur die sichersten Verschlüsselungstypen zu ermöglichen, die Sie für sichere Hosts implementieren können.  
   >
   > Obwohl implementieren sicherere Verschlüsselungstypen für die Hosts nicht Angriffen mit gestohlenen Anmeldeinformationen verringern, verfügt die entsprechende Verwendung und Konfiguration der sicheren Hosts. Festlegen von sichereren Verschlüsselungsarten für Hosts, die nur von privilegierten Konten verwendet werden wird einfach die Gesamtangriffsfläche Computer reduziert.  
   >
   > Weitere Informationen zum Konfigurieren von Verschlüsselungstypen auf Systeme und Konten finden Sie unter [Windows-Konfigurationen für die Kerberos-Verschlüsselungstyp unterstützt](http://blogs.msdn.com/b/openspecification/archive/2011/05/31/windows-configurations-for-kerberos-supported-encryption-type.aspx).  
   >
   > Diese Einstellungen werden nur auf Computern unter Windows Server 2012, Windows Server 2008 R2, Windows 8 oder Windows 7 unterstützt.  
  
10. Auf der **Objekt** Registerkarte **schützen Objekt vor zufälligem Löschen**. Dies wird nicht nur verhindert, dass das Objekt (sogar von autorisierten Benutzern) gelöscht wird, aber es wird verhindert, dass es verschoben wird, in eine andere Organisationseinheit in Ihrer AD DS-Hierarchie, es sei denn, die von einem Benutzer mit Berechtigung zum Ändern des Attributs zuerst das Kontrollkästchen deaktiviert ist.  

   ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_125.png)  

11. Klicken Sie auf die **Remotesteuerung** Registerkarte.  

12. Deaktivieren der **Aktivieren der Remotesteuerung** Flag. Es sollte nie für die Supportmitarbeiter für die Verbindung an dieses Konto-Sitzungen zum Implementieren von Fehlerbehebungen erforderlich sein.  

   ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_126.png)  

   > [!NOTE]  
   > Jedes Objekt in Active Directory müssen einen bestimmten IT-Besitzer und einer entsprechenden zuständigen-Besitzer, siehe [Planen der Gefährdung](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md). Wenn Sie den Besitz von AD DS-Objekte in Active Directory (im Gegensatz zu einer externen Datenbank) verfolgen, sollten Sie geeignete ownershipinformationen in die Eigenschaften dieses Objekts eingeben.  
   >
   > In diesem Fall der Geschäftseigentümer ist sehr wahrscheinlich ein IT-Abteilung, Andthere ist keine Ablehnung von Geschäftsinhaber wird auch IT-Besitzer. Der Punkt der Einrichtung des Besitzes von Objekten ist es Ihnen ermöglichen, die Kontakte zu identifizieren, wenn Änderungen an den Objekten, z. B. Jahre nach ihrer anfänglichen Erstellung vorgenommen werden müssen.  

13. Klicken Sie auf die **Organisation** Registerkarte.  

14. Geben Sie alle erforderlichen Informationen in Ihren AD DS-Objekt-Standards ein.  

   ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_127.png)  

15. Klicken Sie auf die **einwählen** Registerkarte.  

16. In der **Netzwerk Zugriffsberechtigung** die Option **Verweigern des Zugriffs**. Dieses Konto sollte nie über eine Remoteverbindung eine Verbindung herstellen müssen.  

   ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_128.png)  

   > [!NOTE]  
   > Es ist unwahrscheinlich, dass dieses Konto zur Anmeldung beim schreibgeschützten Domänencontrollern (RODCs in Ihrer Umgebung) verwendet werden. Sollte Situation je erfordern jedoch das Konto aus, melden Sie sich bei einem RODC, Sie sollten dieses Konto hinzufügen verweigert RODC-Kennwortreplikationsgruppe, damit das Kennwort nicht auf dem RODC zwischengespeichert werden.  
   >
   > Obwohl das Kennwort des Kontos nach jeder Verwendung zurückgesetzt werden soll, und das Konto deaktiviert werden sollte, implementieren diese Einstellung keine zeitliche für das Konto, und es vielleicht hilfreich in Situationen, in denen ein Administrator, zum Zurücksetzen des Kontos vergisst das Kennwort, und deaktivieren.  

17. Klicken Sie auf die Registerkarte **Mitglied von**.  

18. Klicken Sie auf **Hinzufügen**.  

19. Typ **verweigert RODC-Kennwortreplikationsgruppe** in die **Auswahl von Benutzern, Kontakten, Computern** Dialogfeld und klicken Sie auf **Namen überprüfen**. Wenn Sie der Namen der Gruppe in der Objektauswahl unterstrichen ist, klicken Sie auf **OK** und stellen Sie sicher, dass das Konto jetzt Mitglied von zwei Gruppen angezeigt, die im folgenden Screenshot ist. Fügen Sie das Konto nicht geschützte Gruppen.  

20. Klicken Sie auf **OK**.  

   ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_129.png)  

21. Klicken Sie auf die **Sicherheit** Registerkarte, und klicken Sie auf **erweitert**.  

22. In der **Advanced Security Settings** Dialogfeld klicken Sie auf **Vererbung deaktivieren** und kopieren Sie die geerbten Berechtigungen als explizite Berechtigungen, und klicken Sie auf **hinzufügen**.  

   ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_130.png)  

23. In der **Berechtigungseintrag für [Konto]** Dialogfeld klicken Sie auf **Prinzipal auswählen** und fügen Sie die Gruppe, die Sie im vorherigen Verfahren erstellt haben. Scrollen Sie zum unteren Rand des Dialogfelds, und klicken Sie auf **deaktivieren Sie alle** alle Standardberechtigungen entfernen.  

   ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_131.png)  

24. Führen Sie einen Bildlauf an den Anfang der **Berechtigungseintrag** Dialogfeld. Sicherstellen, dass die **Typ** Dropdown-Listenfeld nastaven NA hodnotu **zulassen**, und klicken Sie in der **gilt für** Dropdown-Liste **nur dieses Objekt**.  

25. In der **Berechtigungen** die Option **alle Eigenschaften lesen**, **Leseberechtigungen**, und **Zurücksetzen des Kennworts**.  

   ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_132.png)  

26. In der **Eigenschaften** die Option **lesen "UserAccountControl"** und **schreiben "UserAccountControl"**.  

27. Klicken Sie auf **OK**, **OK** erneut in die **Advanced Security Settings** Dialogfeld.  

   ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_133.png)  

   > [!NOTE]  
   > Die **"UserAccountControl"** Attribut steuert die Optionen für die Konfiguration mehrerer Konten. Sie können keine Berechtigung, um nur einige der Konfigurationsoptionen ändern, wenn Sie über die Schreibberechtigung für das Attribut gewähren, gewähren.  

28. In der **Gruppen-oder Benutzernamen** Feld der **Sicherheit** Registerkarte, entfernen Sie alle Gruppen, die zum Abrufen oder verwalten das Konto keinen Zugriff haben sollte. Entfernen Sie alle Gruppen, die mit Verweigern-ACEs konfiguriert wurden nicht auf, wie z. B. die Gruppe "Jeder" und der eigenen Konto berechnet (ACE wurde festgelegt, wenn die **Benutzer kann Kennwort nicht ändern** Kennzeichen für den während der Erstellung des Kontos aktiviert wurde. Entfernen Sie auch nicht die Gruppe, die Sie gerade hinzugefügt haben, die SYSTEM-Konto oder Gruppen wie z. B. Enterprise Agreement, DA, BA oder der Windows-Autorisierungszugriffsgruppe.  

   ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_134.png)  

29. Klicken Sie auf **erweitert** und stellen Sie sicher, dass das Dialogfeld "Erweiterte Sicherheitseinstellungen" ähnlich wie im folgenden Screenshot aussieht.  

30. Klicken Sie auf **OK**, und **OK** erneut aus, um die im Eigenschaftendialogfeld des Kontos zu schließen.  

   ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_135.png)  

31. Einrichten des Kontos für die erste ist nun abgeschlossen. Testen Sie das Konto in einer späteren Prozedur.  

##### <a name="creating-additional-management-accounts"></a>Erstellen zusätzliche Management-Konten

Sie können zusätzliche Management-Konten erstellen, durch die vorherigen Schritte wiederholen, kopieren das Konto, das Sie gerade erstellt haben, oder erstellen ein Skript zum Erstellen von Konten mit den gewünschten Konfigurationseinstellungen. Beachten Sie jedoch, dass wenn Sie das Konto, die, das Sie gerade erstellt haben kopieren, viele der benutzerdefinierten Einstellungen und ACLs nicht in das neue Konto kopiert werden und die meisten Konfigurationsschritte wiederholt werden soll müssen.  
  
Sie können stattdessen erstellen Sie eine Gruppe, zu der delegieren Sie Rechte zum Auffüllen und unpopulate geschützte Gruppen, die, aber Sie benötigen zum Sichern der Gruppe und die Konten, die Sie darin zu platzieren. Da nur sehr wenige Konten in Ihrem Verzeichnis, die die Möglichkeit zum Verwalten der Mitgliedschaft einer geschützten Gruppe gewährt werden muss, möglicherweise die einzelne Konten erstellen, dass der einfachste Ansatz.  
  
Unabhängig davon, wie Sie eine Gruppe zu erstellen, in der Sie die Management-Konten platzieren, möchten, sollten Sie sicherstellen, dass jedes Konto gesichert ist, wie oben beschrieben. Sie sollten auch berücksichtigen, implementieren die GPO-Einschränkungen ähnlich jenen in [Anhang D: Schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  
  
##### <a name="auditing-management-accounts"></a>Überwachung von Management-Konten

Konfigurieren Sie die Überwachung für das Konto mindestens alle Schreibvorgänge an das Konto anmelden. Dies ermöglicht, dass Sie nicht nur identifizieren, erfolgreiche Aktivierung des Kontos und der sein Kennwort zurücksetzen, während der genehmigten Verwendungen, sondern auch erkennen, nicht autorisierte Benutzer das Konto zu bearbeiten versuchen. Fehlgeschlagene Schreibvorgänge für das Konto in Ihrem System Security Information and Event Monitoring (SIEM) (falls zutreffend) erfasst werden sollen, und Warnungen, die Benachrichtigungen an die Mitarbeiter, die verantwortlich für die Untersuchung potenzieller gefährdungen auslösen sollte.  
  
SIEM-Lösungen nutzen Ereignisinformationen von Beteiligten Security-Quellen (z. B. Ereignisprotokolle, Anwendungsdaten, Netzwerk-Datenströme, Antischadsoftware-Produkte und Intrusion Detection Quellen), sortieren die Daten und intelligente Ansichten und proaktive Aktionen vorgenommen . Es gibt viele kommerzielle SIEM-Lösungen, und private Implementierungen für viele Unternehmen erstellen. Die sicherheitsüberwachung und Reaktion auf Vorfälle Funktionen kann eine gut durchdachte und ordnungsgemäß implementierte SIEM erheblich gesteigert werden. Jedoch unterschiedlich Funktionen und die Genauigkeit erheblich Lösungen. SIEMs sprengen den Rahmen dieses Artikels, aber die Ereignis-Empfehlungen enthalten sollte durch alle SIEM-Implementierung berücksichtigt werden.  
  
Weitere Informationen zu empfohlenen Konfiguration überwachungseinstellungen für Domänencontroller, finden Sie unter [Überwachen von Active Directory signiert der Gefährdung](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md). Domain Controller-spezifische Konfigurationseinstellungen finden Sie unter [Überwachen von Active Directory signiert der Gefährdung](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md).  
  
#### <a name="enabling-management-accounts-to-modify-the-membership-of-protected-groups"></a>Management-Konten, zum Ändern der Mitgliedschaft einer geschützten Gruppe aktivieren

In diesem Verfahren konfigurieren Sie Berechtigungen auf der Domäne AdminSDHolder-Objekt, um die neu erstellte Verwaltungskonten so ändern Sie die Mitgliedschaft der geschützten Gruppen, die in der Domäne zu ermöglichen. Dieses Verfahren kann nicht über eine grafische Benutzeroberfläche (GUI) nicht ausgeführt werden.  
  
Siehe [Anhang C: Geschützte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md), die ACL auf einer Domäne AdminSDHolder-Objekt wird effektiv "kopiert" auf geschützten Objekte beim Ausführen des Tasks SDProp. Geschützte Gruppen und Konten erben nicht die Berechtigungen aus dem AdminSDHolder-Objekt; Ihre Berechtigungen werden explizit festgelegt, mit denen auf das AdminSDHolder-Objekt übereinstimmen. Aus diesem Grund, wenn Sie Berechtigungen für das AdminSDHolder-Objekt ändern, müssen Sie sie für Attribute ändern, die in den Typ des geschützten Objekts geeignet sind, die Sie verwenden möchten.  
  
In diesem Fall werden Sie gewähren der neu erstellte Management-Konten, damit sie lesen und schreiben, die die Member-Attribut für Gruppenobjekte. Allerdings das AdminSDHolder-Objekt ist kein Group-Objekt, und Gruppieren von Attributen werden nicht in der grafischen ACL-Editor verfügbar gemacht. Es ist deshalb, dass Sie die berechtigungsänderungen über das Dsacls-Befehlszeilen-Hilfsprogramm implementieren. Um die Verwaltung (deaktiviert) Berechtigungen zum Ändern der Mitgliedschaft einer geschützten Gruppe gewähren, führen Sie die folgenden Schritte aus:  
  
1.  Melden Sie sich auf einen Domänencontroller, vorzugsweise für den Domänencontroller, die mit der Rolle PDC-Emulator (PDCE) mit den Anmeldeinformationen eines Benutzerkontos an, die ein Mitglied der Gruppe "Daten" in der Domäne vorgenommen wurde.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_136.png)  
  
2.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, indem Sie mit der rechten Maustaste **Eingabeaufforderung** , und klicken Sie auf **als Administrator ausführen**.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_137.gif)  
  
3.  Wenn Sie dazu aufgefordert werden, die Erhöhung zustimmen, klicken Sie auf **Ja**.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_138.gif)  
  
    > [!NOTE]  
    > Weitere Informationen zur Erhöhung der Rechte und Benutzer Benutzerkontensteuerung (UAC) in Windows finden Sie unter [UAC-Prozesse und-Interaktionen](https://technet.microsoft.com/library/dd835561(v=WS.10).aspx) auf der TechNet-Website.  
  
4.  An der Eingabeaufforderung den Befehl (ersetzen Ihre Informationen mit Domänenspezifischer) **Dsacls [distinguished Name der das Objekt "AdminSDHolder" in Ihrer Domäne] / g [Verwaltungskonto UPN]: RPWP; Member**.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_139.gif)  
  
    Der vorherige Befehl (bei dem Groß-und Kleinschreibung nicht beachtet) funktioniert wie folgt aus:  
  
    -   DSACLS legt fest oder zeigt ACEs für Verzeichnisobjekte  
  
    -   CN = AdminSDHolder, CN = System, DC = TailSpinToys, DC = Msft identifiziert das Objekt geändert werden  
  
    -   / G gibt an, dass eine Zuweisung ACE konfiguriert wird  
  
    -   PIM001@tailspintoys.msft wird der Benutzer Benutzerprinzipalname (UPN) des Sicherheitsprinzipals, der die ACEs gewährt wird  
  
    -   Diese Berechtigung gewährt RPWP-Eigenschaft lesen und Schreibberechtigungen für die Eigenschaft  
  
    -   Member ist der Name der Eigenschaft (Attribut) auf dem die Berechtigungen festgelegt wird  
  
    Weitere Informationen zur Verwendung von **Dsacls**, Dsacls ohne Parameter an einer Eingabeaufforderung eingeben.  
  
    Wenn Sie mehrere Verwaltungskonten für die Domäne erstellt haben, sollten Sie auf den der Befehl für jedes Konto ausführen. Wenn Sie die ACL-Konfiguration für das AdminSDHolder-Objekt abgeschlossen haben, sollten Sie SDProp ausführen, oder warten Sie bis zum Abschluss der geplanten Ausführung erzwingen. Weitere Informationen zum Erzwingen von SDProp ausführen, finden Sie unter "Manually SDProp ausführen" in [Anhang C: Geschützte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md).  
  
    Wenn SDProp ausgeführt wurde, können Sie überprüfen, die an das AdminSDHolder-Objekt vorgenommenen Änderungen zu geschützten Gruppen, die in der Domäne angewendet wurden. Sie können nicht dies überprüfen, indem Sie die ACL für das AdminSDHolder-Objekt anzeigen, die zuvor beschriebenen Gründen, aber zu überprüfen, ob die Berechtigungen angewendet wurden, indem Sie die ACLs in geschützten Gruppen, die anzeigen.  
  
5.  In **Active Directory-Benutzer und-Computer**, stellen Sie sicher, dass Sie aktiviert haben **erweiterte Features**. Zu diesem Zweck klicken Sie auf **Ansicht**, suchen Sie die **Domänen-Admins** gruppieren, mit der rechten Maustaste in der Gruppe aus, und klicken Sie auf **Eigenschaften**.  
  
6.  Klicken Sie auf die **Sicherheit** Registerkarte, und klicken Sie auf **erweitert** zum Öffnen der **erweiterte Sicherheitseinstellungen für Domänen-Admins** Dialogfeld.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_140.gif)  
  
7.  Wählen Sie **ermöglichen ACE für das Verwaltungskonto** , und klicken Sie auf **bearbeiten**. Stellen Sie sicher, dass das Konto nur erteilt wurde **Lesemitglieder** und **Mitglieder schreiben** Berechtigungen für die Gruppe von Daten, und klicken Sie auf **OK**.  
  
8.  Klicken Sie auf **OK** in die **Advanced Security Settings** (Dialogfeld), und klicken Sie auf **OK** erneut aus, um das Eigenschaftendialogfeld für die Gruppe von Daten zu schließen.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_141.gif)  
  
9. Sie können die vorherigen Schritte für andere geschützte Gruppen in der Domäne wiederholen; die Berechtigungen sollten für alle geschützten Gruppen, die identisch sein. Sie haben jetzt die Erstellung und Konfiguration von der Management-Konten für die geschützten Gruppen, die in dieser Domäne abgeschlossen.  
  
    > [!NOTE]  
    > Jedes Konto, das berechtigt ist, schreiben die Mitgliedschaft einer Gruppe in Active Directory kann auch selbst zur Gruppe hinzufügen. Dieses Verhalten ist beabsichtigt und kann nicht deaktiviert werden. Aus diesem Grund sollten Sie eine sorgfältige Management-Konten, die bei Nichtverwendung deaktiviert, und die Konten sollten genau überwachen, wenn sie deaktiviert sind und sie in Verwendung kommen.  
  
#### <a name="verifying-group-and-account-configuration-settings"></a>Überprüfen, Gruppe und Konfigurationseinstellungen

Nun, dass Sie erstellt und Management-Konten, die die Mitgliedschaft der geschützten Gruppen, die in der Domäne ändern können (einschließlich der meisten sehr privilegierten Gruppen für EA, DA und BA) konfiguriert haben, sollten Sie sicherstellen, dass die Konten und die Verwaltungsgruppe wurde ordnungsgemäß erstellt. Überprüfung besteht diese allgemeinen Aufgaben aus:  
  
1.  Testen Sie die Gruppe, die aktivieren und deaktivieren die Management-Konten, um sicherzustellen, dass die Mitglieder der Gruppe können aktivieren und deaktivieren die Konten und ihre Kennwörter zurücksetzen, aber andere administrativen Aktivitäten können nicht ausgeführt werden, auf die Verwaltungskonten kann.  
  
2.  Testen Sie die Management-Konten, um sicherzustellen, dass sie hinzufügen können, und Entfernen von Mitgliedern zu Gruppen in der Domäne geschützt, aber andere Eigenschaften der geschützte Konten und Gruppen können nicht geändert werden.  
  
##### <a name="test-the-group-that-will-enable-and-disable-management-accounts"></a>Testen Sie die Gruppe, die zu aktivieren und Deaktivieren von Konten
  
1.  Um ein Konto für die Aktivierung und die kennwortzurücksetzung zu testen, melden Sie sich bei einer sicheren Verwaltungsarbeitsstation mit einem Konto an, das ein Mitglied der Gruppe im erstellten [Anhang I: Erstellen von Verwaltungskonten für geschützte Konten und Gruppen in Active Directory](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md).  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_142.gif)  
  
2.  Open **Active Directory-Benutzer und-Computer**mit der rechten Maustaste auf das Konto, und klicken Sie auf **Enable Account**.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_143.gif)  
  
3.  Ein Dialogfeld sollte bestätigen, dass das Konto aktiviert wurde, angezeigt.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_144.gif)  
  
4.  Als Nächstes Zurücksetzen des Kennworts für das Managementkonto. Zu diesem Zweck mit der rechten Maustaste erneut auf des Kontos, und klicken Sie auf **Kennwort zurücksetzen**.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_145.gif)  
  
5.  Geben Sie ein neues Kennwort für das Konto in der **neues Kennwort** und **Bestätigungskennwort** Felder, und klicken Sie auf **OK**.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_146.gif)  
  
6.  Ein Dialogfeld sollte angezeigt werden, bestätigt, dass das Kennwort für das Konto zurückgesetzt wurde.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_147.gif)  
  
7.  Nun versucht, um zusätzliche Eigenschaften des Kontos für die zu ändern. Mit der rechten Maustaste in des Kontos, und klicken Sie auf **Eigenschaften**, und klicken Sie auf die **Remotesteuerung** Registerkarte.  
  
8.  Wählen Sie **Aktivieren der Remotesteuerung** , und klicken Sie auf **übernehmen**. Der Vorgang sollte fehlschlagen und eine **Zugriff verweigert** Fehlermeldung sollte angezeigt werden.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_148.gif)  
  
9. Klicken Sie auf die **Konto** Registerkarte für das Konto, und versuchen, den Namen des Kontos, den Anmeldezeiten oder Anmeldearbeitsstationen ändern. Alle fehlschlagen soll, und berücksichtigen Sie die Optionen, die nicht von kontrolliert werden die **"UserAccountControl"** Attribut sollte abgeblendet werden, und für die Änderung nicht verfügbar.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_149.gif)  
  
10. Versuchen Sie, wie z. B. die Gruppe von Daten einer geschützten Gruppe die Verwaltungsgruppe hinzufügen. Beim Klicken auf **OK**, eine Meldung angezeigt, in der Sie darüber informiert werden, dass Sie nicht über Berechtigungen zum Ändern der Gruppe verfügen.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_150.gif)  
  
11. Zusätzliche Tests ausgeführt werden, da erforderlich, um sicherzustellen, dass Sie nicht alles auf dem Managementkonto, mit Ausnahme von konfigurieren **"UserAccountControl"** Einstellungen und das Zurücksetzen von Kennwörtern.  
  
    > [!NOTE]  
    > Die **"UserAccountControl"** Attribut steuert die Optionen für die Konfiguration mehrerer Konten. Sie können keine Berechtigung, um nur einige der Konfigurationsoptionen ändern, wenn Sie über die Schreibberechtigung für das Attribut gewähren, gewähren.  
  
##### <a name="test-the-management-accounts"></a>Testen Sie die Management-Konten

Nun, dass Sie ein oder mehrere Konten aktiviert haben, die die Mitgliedschaft einer geschützten Gruppe ändern können, können Sie die Konten, um sicherzustellen, dass sie können geschützte Gruppenmitgliedschaft ändern, aber andere Änderungen nicht werden, auf geschützte Konten und Gruppen ausgeführt können testen.  
  
1.  Melden Sie sich an sicheren administrative Host wie das erste Managementkonto an.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_151.gif)  
  
2.  Starten Sie **Active Directory-Benutzer und-Computer** und suchen Sie nach der **Gruppe "Domänenadministratoren"**.  
  
3.  Mit der rechten Maustaste die **Domänen-Admins** gruppieren, und klicken Sie auf **Eigenschaften**.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_152.gif)  
  
4.  In der **Eigenschaften von Domänen-Admins**, klicken Sie auf die **Mitglieder** Registerkarte und **klicken Sie auf** hinzufügen. Geben Sie den Namen eines Kontos, das temporäre Domänen-Admins-Berechtigungen erhalten, und klicken Sie auf **Namen überprüfen**. Wenn der Name des Kontos unterstrichen ist, klicken Sie auf **OK** zum Zurückgeben der **Mitglieder** Registerkarte.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_153.gif)  
  
5.  Auf der **Mitglieder** auf der Registerkarte die **Eigenschaften von Domänen-Admins** Dialogfeld klicken Sie auf **übernehmen**. Nach dem Klicken auf **übernehmen**, das Konto sollte ein Mitglied der Gruppe "Daten" bleiben, und Sie sollten keine Fehlermeldungen erhalten.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_154.gif)  
  
6.  Klicken Sie auf die **verwaltet von** Registerkarte die **Eigenschaften von Domänen-Admins** Dialogfeld ein, und stellen Sie sicher, dass Sie können nicht in allen Feldern Text eingeben, und alle Schaltflächen sind abgeblendet.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_155.gif)  
  
7.  Klicken Sie auf die **allgemeine** Registerkarte die **Eigenschaften von Domänen-Admins** Dialogfeld ein, und stellen Sie sicher, dass Sie die Informationen über die Registerkarte nicht ändern können.  
  
    ![Erstellen von Management-Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_156.gif)  
  
8.  Wiederholen Sie diese Schritte für die geschützten Gruppen, die zusätzliche, je nach Bedarf. Wenn Sie fertig sind, melden Sie sich an einem sicheren administrative Host mit einem Konto an, die ein Mitglied der Gruppe ist, die Sie zum Aktivieren und deaktivieren die Management-Konten erstellt. Klicken Sie dann setzen Sie das Kennwort für das Managementkonto Sie gerade getestet, und deaktivieren Sie das Konto an. Sie haben die Einrichtung von den Management-Konten und die Gruppe, die zum Aktivieren und deaktivieren die Konten zuständig ist abgeschlossen.  
