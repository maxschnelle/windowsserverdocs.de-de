---
ms.assetid: 13fe87d9-75cf-45bc-a954-ef75d4423839
title: "Anlage I - Erstellen von Konten für geschützte Konten und Gruppen in Active Directory"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 666180adca691d6c9783a43063df76877115fc40
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="appendix-i-creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>Anhang I: Erstellen von Verwaltungskonten für geschützte Konten und Gruppen in Active Directory

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

  
## <a name="appendix-i-creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>Anhang I: Erstellen von Verwaltungskonten für geschützte Konten und Gruppen in Active Directory  

Eine der Herausforderungen bei der Implementierung einer Active Directory-Modell, das nicht auf permanente Mitgliedschaft in sehr privilegierten Gruppen basiert ist, dass es dafür ein Mechanismus für diese Gruppen auffüllen, wenn ein temporärer Mitgliedschaften in den Gruppen erforderlich ist. Einige privileged Identity Management-Lösungen erforderlich, dass die Software-Dienstkonten permanente Mitgliedschaft in Gruppen wie z. B. DA oder Administratoren in jeder Domäne in der Gesamtstruktur erteilt werden. Allerdings ist es technisch nicht erforderlich für Privileged Identity Management (PIM)-Lösungen für ihre Dienste in solchen privilegierten Kontexten ausgeführt.  
  
Dieser Anhang enthält Informationen, mit denen Sie für systemeigene implementiert oder Drittanbieter-PIM-Lösungen können Konten erstellen, die Berechtigungen eingeschränkt und repräsentative Motoröltemperatur gesteuert werden können, aber kann zum Auffüllen von privilegierter Gruppen in Active Directory, wenn temporäre erhöhte Rechte erforderlich sind. Wenn Sie PIM als einheitlichen Lösung implementieren, können diese Konten von administrative Mitarbeiter verwendet werden, die temporäre gruppenauffüllung ausführen, und wenn Sie PIM über Drittanbieter-Software implementieren, können Sie möglicherweise passen Sie diese Konten als Dienstkonten verwendet werden.  
  
> [!NOTE]  
> Die Verfahren in diesem Anhang beschrieben bieten eine Möglichkeit für die Verwaltung von sehr privilegierten Gruppen in Active Directory. Sie können passen Sie diese Verfahren entsprechend Ihren Anforderungen, fügen zusätzliche Einschränkungen oder einige der Einschränkungen, die hier beschriebenen weglassen.  
  
### <a name="creating-management-accounts-for-protected-accounts-and-groups-in-active-directory"></a>Erstellen von Verwaltungskonten für geschützte Konten und Gruppen in Active Directory  
Konten erstellen, kann verwendet werden, um die Mitgliedschaft der privilegierten Gruppen zu verwalten, ohne dass die Management-Konten an, eine übermäßige Rechte erteilt werden, und Berechtigungen besteht aus vier allgemeinen Aktivitäten, die in der schrittweisen Anleitung beschrieben werden:  
  
1.  Zunächst sollten Sie eine Gruppe, die die Konten verwalten erstellen, da diese Konten durch eine begrenzte Anzahl von vertrauenswürdigen Benutzern verwaltet werden soll. Wenn Sie nicht bereits eine OE-Struktur, die durch GALs privilegierten und geschützte Konten und Systemen über die allgemeinen Benutzer in der Domäne ausgelegt ist verfügen, sollten Sie eine erstellen. Screenshots können zwar spezifische Anweisungen in diesem Anhang nicht bereitgestellt werden, ein Beispiel für eine solche eine OE-Hierarchie angezeigt.  
  
2.  Erstellen Sie die Management-Konten. Diese Konten sollten als "normalen" Benutzerkonten erstellt und keine Benutzerrechte, die bereits in der Standardeinstellung Benutzern erteilt werden neben den gewährt werden.  
  
3.  Implementieren Sie Einschränkungen bei der Management-Konten, die sie nur für den speziellen Zweck verwendet für die sie erstellt wurden zusätzlich zu steuern werden, wer aktivieren und die Konten (die Gruppe, die Sie im ersten Schritt erstellt haben) verwenden können.  
  
4.  Konfigurieren Sie Berechtigungen für das AdminSDHolder-Objekt in jeder Domäne, um die Konten so ändern Sie die Mitgliedschaft der privilegierten Gruppen in der Domäne zu ermöglichen.  
  
Sie sollten sorgfältig alle der folgenden Verfahren und je nach Bedarf für Ihre Umgebung vor der Implementierung in einer produktionsumgebung zu ändern. Außerdem sollten Sie überprüfen, dass alle Einstellungen erwartungsgemäß (einige Prüfverfahren sind in diesem Anhang bereitgestellt), und Testen Sie ein Notfallwiederherstellungsszenario in der die Management-Konten sind nicht verfügbar für das Auffüllen geschützter Gruppen für die Wiederherstellung verwendet werden. Weitere Informationen zum Sichern und Wiederherstellen von Active Directory finden Sie unter der [AD DS-Sicherung und Wiederherstellung schrittweisen Anleitung für](https://technet.microsoft.com/library/cc771290(v=ws.10).aspx).  
  
> [!NOTE]  
> Durch die Implementierung der Schritte in diesem Anhang beschrieben, erstellen Sie Konten, die die Mitgliedschaft in allen geschützten Gruppen in jeder Domäne, nicht nur die höchste Berechtigung Active Directory-Gruppen wie EAs, DAs und BAs verwaltet werden. Weitere Informationen zu geschützten Gruppen in Active Directory finden Sie unter [Anhang C: geschützte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md).  
  
#### <a name="step-by-step-instructions-for-creating-management-accounts-for-protected-groups"></a>Eine schrittweise Anleitung zum Erstellen von Konten für geschützter Gruppen  
  
##### <a name="creating-a-group-to-enable-and-disable-management-accounts"></a>Erstellen einer Gruppe zum Aktivieren und Deaktivieren von Konten  
Konten sollte ihre Kennwörter zurücksetzen bei jeder Verwendung und sollte deaktiviert werden, wenn Ihre Aktivitäten abgeschlossen sind. Obwohl sich unter Umständen Smartcard-Anmeldung Anforderungen für diese Konten implementieren empfiehlt, es ist eine optionale Konfiguration, und diesen Anweisungen wird davon ausgegangen, dass die Management-Konten als minimale Steuerelemente mit einer Kombination aus Benutzername und lange und komplexe Kennwörter konfiguriert werden soll. In diesem Schritt erstellen Sie eine Gruppe, die über Berechtigungen für die Verwaltung Konten Kennwort zurücksetzen und zum Aktivieren und deaktivieren die Konten verfügt.  
  
Um eine Gruppe zum Aktivieren und Deaktivieren von Konten zu erstellen, führen Sie die folgenden Schritte aus:  
  
1.  In der OE-Struktur, in dem Sie werden der Verwaltung Gruppenkonten werden, mit der Maustaste der Organisationseinheit, in dem Sie die Gruppe erstellen möchten, klicken Sie auf **neu** , und klicken Sie auf **Gruppe**.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_115.png)  
  
2.  In der **neues Objekt - Gruppe** Dialogfeld Geben Sie einen Namen für die Gruppe. Wenn Sie dieser Gruppe "alle Konten in Ihrer Gesamtstruktur aktivieren" verwenden möchten, stellen sie eine universelle Sicherheitsgruppe. Wenn Sie die Gesamtstruktur mit eine einzelnen Domäne verfügen, oder wenn Sie eine Gruppe in jeder Domäne erstellen möchten, können Sie eine globale Sicherheitsgruppe erstellen. Klicken Sie auf **OK** zum Erstellen der Gruppe.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_116.png)  
  
3.  Mit der rechten Maustaste in der Gruppe, die Sie gerade erstellt haben, klicken Sie auf **Eigenschaften**, und klicken Sie auf die **Objekt** Registerkarte. In der Gruppennamens **Objekteigenschaft** wählen Sie im Dialogfeld **schützen Objekt vor zufälligem Löschen**, die nur verhindert nicht anderweitig autorisierte Benutzer die Gruppe löschen, sondern auch in eine andere Organisationseinheit verschieben, es sei denn, die Attribut ist zunächst deaktiviert.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_117.png)  
  
    > [!NOTE]  

    > Wenn Sie Berechtigungen für die Gruppe übergeordneten Organisationseinheiten Verwaltung, um eine begrenzte Anzahl von Benutzern einschränken bereits konfiguriert haben, müssen Sie möglicherweise nicht die folgenden Schritte ausführen. Sie werden hier bereitgestellt, sodass auch, wenn Sie noch nicht eingeschränkte administrative Kontrolle über die OU-Struktur implementiert wurde in denen Sie dieser Gruppe erstellt haben, können Sie die Gruppe vor Änderung sichern durch nicht autorisierte Benutzer.  
  
4.  Klicken Sie auf die **Mitglieder** Registerkarte, und fügen Sie die Konten für Mitglieder des Teams, die zum Aktivieren von Konten oder Auffüllen verantwortlich sind Gruppen bei Bedarf geschützt.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_118.png)  
  
5.  Wenn Sie nicht bereits im geschehen ist die **Active Directory-Benutzer und-Computer** -Konsole, klicken Sie auf **Ansicht** , und wählen Sie **erweiterte Funktionen**. Mit der rechten Maustaste in der Gruppe, die Sie gerade erstellt haben, klicken Sie auf **Eigenschaften**, und klicken Sie auf die **Security** Registerkarte. Auf der **Security** auf **erweitert**.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_119.png)  
  
6.  In der **Advanced Security Settings for [Gruppe]** Dialogfeld, klicken Sie auf **Vererbung deaktivieren**. Wenn Sie dazu aufgefordert werden, klicken Sie auf **Convert vererbte Berechtigungen in explizite Berechtigungen für dieses Objekt**, und klicken Sie auf **OK** zurückkehren zu der Gruppennamens **Security** Dialogfeld.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_120.png)  
  
7.  Auf der **Security** Registerkarte, Entfernen von Gruppen, die dieser Gruppe den Zugriff auf nicht zulässig ist. Wenn Sie nicht authentifizierte Benutzer in der Lage, Namen und die allgemeinen Eigenschaften der Gruppennamens zu lesen sein möchten, können Sie z. B. ACE entfernen. Sie können auch ACEs, z. B. für Operatoren und Prä-Windows 2000 Server kompatibel Kontozugriff entfernen. Sie sollten jedoch einen minimalen Satz von Berechtigungen für Objekte behalten. Behalten Sie die folgenden ACEs bei:  
  
    -   SELBST  
  
    -   SYSTEM  
  
    -   Domänen-Admins  
  
    -   Organisations-Admins  
  
    -   Administratoren  
  
    -   Windows-Autorisierungszugriffsgruppe (sofern zutreffend)  
  
    -   DOMÄNENCONTROLLER DER ORGANISATION  
  
    Es mag nicht besonders intuitiv, um die höchsten privilegierten Gruppen in Active Directory zum Verwalten dieser Gruppe zu ermöglichen, ist Ihr Ziel bei der Implementierung dieser Einstellungen nicht verhindern, dass Mitglieder dieser Gruppen autorisierte Änderungen vornehmen. Vielmehr ist das Ziel, stellen Sie sicher, dass bei Gelegenheit sehr hohe Rechte erforderlich sind, die autorisierte Änderungen erfolgreich ist. Es ist daher, dass das Ändern der standardmäßigen privilegierten Gruppe verschachteln, Rechte und Berechtigungen werden in diesem Dokument nicht empfohlen. Standard-Strukturen erhalten bleibt, und leeren die Mitgliedschaft der höchsten Rechte Gruppen in das Verzeichnis, können Sie eine sicherere Umgebung erstellen, die weiterhin erwartungsgemäß funktioniert.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_121.png)  
  
    > [!NOTE]  
    > Wenn Sie nicht bereits Überwachungsrichtlinien für die Objekte in der OE-Struktur konfiguriert haben, in dem Sie dieser Gruppe erstellt haben, konfigurieren Sie zum Melden von Änderungen Überwachung dieser Gruppe.  
  
8.  Konfiguration der Gruppe, die mit "sehen Sie sich" abgeschlossen haben Management Konten, wenn sie benötigt werden, und "Check-in" die Konten, wenn ihre Aktivitäten abgeschlossen wurden.  
  
##### <a name="creating-the-management-accounts"></a>Erstellen der Management-Konten  
Erstellen Sie mindestens ein Konto, das verwendet wird, um die Mitgliedschaft der privilegierten Gruppen in Ihrer Active Directory-Installation zu verwalten und vorzugsweise ein sekundäres Konto, das als Sicherung dienen soll. Gibt an, ob Sie die Management-Konten in einer einzigen Domäne in der Gesamtstruktur erstellen und diesen Verwaltungsfunktionen für alle Domänen erteilen möchten Gruppen geschützt, oder, ob Sie Konten in jeder Domäne in der Gesamtstruktur implementieren möchten, die Verfahren sind effektiv identisch.  
  
> [!NOTE]  
> Die Schritte in diesem Dokument wird davon ausgegangen, dass Sie rollenbasierten Zugriffskontrolle und privileged Identitätsmanagement für Active Directory noch nicht implementiert wurde. Aus diesem Grund müssen einige Verfahren von einem Benutzer ausgeführt werden, dessen Konto Mitglied der Gruppe "Domänen-Admins" für die betreffende Domäne ist.  
>   
> Wenn Sie ein Konto mit Berechtigungen DA verwenden, können Sie auf einen Domänencontroller, der Konfigurationsaktivitäten ausführen anmelden. Schritte, die nicht DA Berechtigungen benötigen, können von Konten mit weniger Berechtigungen ausgeführt werden, die auf administrativen Arbeitsstationen angemeldet sind. Die Screenshots, die zeigen, Dialogfelder, die in der helleren blaue Farbe Tabellenzelle Aktivitäten darstellen, die auf einem Domänencontroller ausgeführt werden können. Die Screenshots, die zeigen, dass Dialogfelder in der dunkleres Blau Aktivitäten darstellen, die auf administrativen Arbeitsstationen mit Konten ausgeführt werden können, die eingeschränkte Berechtigungen haben.  
  
Um die Management-Konten zu erstellen, führen Sie die folgenden Schritte aus:  
  
1.  Melden Sie sich auf einem Domänencontroller mit einem Konto, das Mitglied der Domänengruppe DA ist.  
  
2.  Starten Sie **Active Directory-Benutzer und-Computer** und navigieren Sie zu der Organisationseinheit, in dem Sie erstellen das Verwaltungsserver ein.  
  
3.  Maustaste auf die Organisationseinheit, und klicken Sie auf **neu** , und klicken Sie auf **Benutzer**.  
  
4.  In der **neues Objekt – Benutzer** Dialogfeld ein, geben Sie die gewünschten naming Informationen für das Konto aus, und klicken Sie auf **Weiter**.  
  
5.  Melden Sie sich auf einem Domänencontroller mit einem Konto, das Mitglied der Domänengruppe DA ist.  
  
6.  Starten Sie **Active Directory-Benutzer und-Computer** und navigieren Sie zu der Organisationseinheit, in dem Sie erstellen das Verwaltungsserver ein.  
  
7.  Maustaste auf die Organisationseinheit, und klicken Sie auf **neu** , und klicken Sie auf **Benutzer**.  
  
8.  In der **neues Objekt – Benutzer** Dialogfeld ein, geben Sie die gewünschten naming Informationen für das Konto aus, und klicken Sie auf **Weiter**.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_122.png)  
  
9. Geben Sie ein Kennwort für das Benutzerkonto, eine klare **Benutzer muss Kennwort bei der nächsten Anmeldung ändern**Option **Benutzer kann Kennwort nicht ändern** und **Konto ist deaktiviert**, und klicken Sie auf **Weiter**.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_123.png)  
  
10. Stellen Sie sicher, dass die Kontodetails richtig sind, und klicken Sie auf **Fertig stellen**.  
  
11. Mit der rechten Maustaste die User-Objekt, das Sie gerade erstellt haben, und klicken Sie auf **Eigenschaften**.  
  
12. Klicken Sie auf die **Konto** Registerkarte.  
  
13. In der **Kontooptionen** aus, die **Konto ist vertraulich und kann nicht delegiert werden** kennzeichnen, wählen die **dieses Konto unterstützt Kerberos-AES-128-Bit-Verschlüsselung** bzw. die **dieses Konto unterstützt Kerberos-AES-256-Verschlüsselung** kennzeichnen, und klicken Sie auf **OK**.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_124.png)  
  
    > [!NOTE]  
    > Da dieses Konto andere Konten eine beschränkt, aber leistungsstarke Funktion verwendet werden, sollte das Konto nur auf sichere administrative Hosts verwendet werden. Für alle sichere administrative Hosts in Ihrer Umgebung, sollten Sie die Einstellung der Gruppenrichtlinie implementieren **Netzwerksicherheit: Konfigurieren von Verschlüsselungstypen für Kerberos zulässige** können nur die sichersten Verschlüsselungstypen, die Sie für die sichere Hosts implementieren können.  
    >   
    > Obwohl sicherere Verschlüsselungsarten implementieren, für die Hosts nicht Methoden des anmeldeinformationsdiebstahls verringern, wird die richtige Verwendung und Konfiguration des sicheren Hosts. Einstellung sichereren Verschlüsselungsarten für Hosts, die nur von privilegierten Konten verwendet werden wird einfach die gesamte Angriffsfläche der Computer reduziert.  
    >   
    > Weitere Informationen zum Konfigurieren von Verschlüsselungstypen auf Systeme und Konten finden Sie unter [Windows-Konfigurationen für Kerberos unterstützt Verschlüsselungstyp](http://blogs.msdn.com/b/openspecification/archive/2011/05/31/windows-configurations-for-kerberos-supported-encryption-type.aspx).  
    >   
    > **Hinweis:** diese Einstellungen werden nur auf Computern unter Windows Server 2012, Windows Server 2008 R2, Windows 8 oder Windows 7 unterstützt.  
  
14. Auf der **Objekt** Registerkarte **schützen Objekt vor zufälligem Löschen**. Dies wird nicht nur verhindert, dass das Objekt (auch von autorisierten Benutzern) gelöscht wird, aber Sie können verhindern, dass er in einer anderen Organisationseinheit in der AD DS-Hierarchie verschoben wird, wenn von einem Benutzer mit der Berechtigung zum Ändern des Attributs zuerst das Kontrollkästchen deaktiviert ist.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_125.png)  
  
15. Klicken Sie auf die **Remotesteuerung** Registerkarte.  
  
16. Deaktivieren der **Aktivieren der Remotesteuerung** Kennzeichen. Es sollte nie Supportmitarbeitern für die Verbindung mit diesem Konto Sitzungen Patches implementieren erforderlich sein.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_126.png)  
  
    > [!NOTE]  
    > Jedes Objekt in Active Directory sollten einen bestimmten IT-Besitzer und einen Besitzer festgelegten Unternehmen haben, wie unter [für Sicherheitsgefährdungen](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md). Wenn Sie den Besitz des AD DS-Objekte in Active Directory (im Gegensatz zu einer externen Datenbank) verfolgen, sollten Sie geeignete Besitzerinformationen in Eigenschaften des Objekts eingeben.  
    >   
    > In diesem Fall den geschäftlichen Besitzer ist in der Regel eine IT-Abteilung, Andthere ist keine Verbot Geschäftsinhaber auch die IT-Besitzer. Der Punkt für die Ermittlung der Besitz von Objekten ist, können Sie Kontakte zu identifizieren, wenn Änderungen auf die Objekte, z. B. Jahre aus ihrer Erstellung vorgenommen werden müssen.  
  
17. Klicken Sie auf die **Organisation** Registerkarte.  
  
18. Geben Sie alle erforderlichen Informationen in Ihrer AD DS-Objekt-Standards.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_127.png)  
  
19. Klicken Sie auf die **-Einwahl** Registerkarte.  
  
20. In der **Netzwerkzugriffsberechtigungen** Feld **Verweigern des Zugriffs**. Dieses Konto sollte nie über eine Remoteverbindung herstellen müssen.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_128.png)  
  
    > [!NOTE]  
    > Es ist unwahrscheinlich, dass dieses Konto auf schreibgeschützten Domänencontrollern (RODCs) in Ihrer Umgebung anmelden verwendet werden. Allerdings sollten Umstände jemals muss das Konto, melden Sie sich bei einem RODC addieren Sie dieses Konto zu verweigert RODC-Kennwortreplikationsgruppe, damit das Kennwort nicht auf dem RODC zwischengespeichert werden.  
    >   
    > Obwohl das Kennwort des Kontos nach jeder Verwendung zurückgesetzt werden soll, und das Konto deaktiviert werden sollte, implementieren diese Einstellung hat keinen zeitliche für das Konto, und ist es vielleicht hilfreich in Situationen, in denen ein Administrator vergisst, setzen Sie das Kennwort des Kontos zurück, und deaktivieren es.  
  
21. Klicken Sie auf die **Mitglied von** Registerkarte.  
  
22. Klicken Sie auf **hinzufügen**.  
  
23. Typ **verweigert RODC-Kennwortreplikationsgruppe** in der **Auswahl von Benutzern, Kontakten, Computern** im Dialogfeld, und klicken Sie dann auf **Namen überprüfen**. Wenn Sie der Namen der Gruppe in der Objektauswahl unterstrichen ist, klicken Sie auf **OK** und stellen Sie sicher, dass das Konto nun zwei Gruppen angezeigt, die im folgenden Screenshot angehört. Fügen Sie das Konto nicht geschützten Gruppen.  
  
24. Klicken Sie auf **OK**.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_129.png)  
  
25. Klicken Sie auf die **Security** Registerkarte, und klicken Sie auf **erweitert**.  
  
26. In der **Advanced Security Settings** Dialogfeld, klicken Sie auf **Deaktivieren der Vererbung** und kopieren Sie die geerbten Berechtigungen als expliziten Berechtigungen, und klicken Sie auf **hinzufügen**.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_130.png)  
  
27. In der **Berechtigungseintrag für [Konto]** Dialogfeld, klicken Sie auf **Prinzipal auswählen** und fügen Sie die Gruppe, die Sie im vorherigen Verfahren erstellt haben. Führen Sie einen Bildlauf nach unten im Dialogfeld, und klicken Sie auf **deaktivieren Sie alle** So entfernen Sie alle standardmäßigen Berechtigungen.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_131.png)  
  
28. Führen Sie einen Bildlauf zum oberen Rand der **Berechtigungseintrag** Dialogfeld. Stellen Sie sicher, dass die **Typ** Dropdown-Liste auf festgelegt ist **zulassen**, und in der **gilt für** Dropdown-Liste, wählen **nur dieses Objekt**.  
  
29. In der **Berechtigungen** Feld **alle Eigenschaften lesen**, **Leseberechtigungen**, und **Zurücksetzen des Kennworts**.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_132.png)  
  
30. In der **Eigenschaften** Feld **lesen UserAccountControl** und **schreiben UserAccountControl**.  
  
31. Klicken Sie auf **OK**, **OK** erneut in die **Advanced Security Settings** Dialogfeld.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_133.png)  
  
    > [!NOTE]  
    > Die **UserAccountControl** Attribut steuert mehrere Konto Konfigurationsoptionen. Sie können nicht über die Berechtigung zum Ändern nur einige Konfigurationsoptionen beim Erteilen von Schreibberechtigungen für das Attribut erteilen.  
  
32. In der **Gruppen-oder Benutzernamen** im Feld der **Security** Registerkarte, entfernen Sie alle Gruppen, die nicht zum Abrufen oder verwalten das Konto zwischengespeichert werden dürfen. Alle Gruppen, die mit ACEs verweigern konfiguriert wurden nicht entfernt, z. B. der Gruppe "Jeder" und der eigenen Konto berechnet (ACE wurde festgelegt, wenn die **Benutzer kann Kennwort nicht ändern** Flag während der Erstellung des Kontos aktiviert wurde. Entfernen Sie auch nicht die Gruppe, die Sie gerade hinzugefügt haben, das Systemkonto oder Gruppen wie z. B. EA, DA, BA oder der Windows-Autorisierungszugriffsgruppe.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_134.png)  
  
33. Klicken Sie auf **erweitert** und stellen Sie sicher, dass das Dialogfeld "Erweiterte Sicherheitseinstellungen" ähnlich wie im folgenden Screenshot.  
  
34. Klicken Sie auf **OK**, und **OK** erneut aus, um das Konto-Eigenschaft-Dialogfeld zu schließen.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_135.png)  
  
35. Installation des ersten Management-Kontos ist nun abgeschlossen. Testen Sie das Konto in einem späteren Verfahren.  
  
###### <a name="creating-additional-management-accounts"></a>Erstellen zusätzlicher Management-Konten  
Sie können zusätzliche Konten erstellen, indem Sie die vorherigen Schritte wiederholen, kopieren Sie das Konto, das Sie gerade erstellt haben oder durch Erstellen eines Skripts zum Erstellen von Konten mit Einstellungen für die gewünschte Konfiguration. Beachten Sie jedoch, dass wenn Sie das Konto, das Sie gerade erstellt haben kopieren, viele der benutzerdefinierten Einstellungen und ACLs nicht in das neue Konto kopiert werden und die meisten der Konfigurationsschritte, wiederholen müssen.  
  
Sie können stattdessen erstellen Sie eine Gruppe, die Sie Rechte zum Füllen und unpopulate geschützte Gruppen delegieren, aber Sie müssen zum Schutz der Gruppe und die Konten, die Sie darin zu platzieren. Da es sollte nur sehr wenige Konten im Verzeichnis, die die Fähigkeit zum Verwalten der Mitgliedschaft geschützten Gruppen gewährt werden, möglicherweise die individuelle Konten erstellen, dass der einfachste Ansatz.  
  
Unabhängig davon, wie Sie eine Gruppe erstellen, in der Sie die Konten platzieren, möchten, sollten Sie sicherstellen, dass jedes Konto gesichert ist, wie zuvor beschrieben. Erwägen Sie auch die Implementierung der GPO-Einschränkungen ähnlich wie in [Anhang D: schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  
  
###### <a name="auditing-management-accounts"></a>Überwachung von Konten  
Konfigurieren Sie die Überwachung für das Konto mindestens alle Schreibvorgänge an das Konto anzumelden. Dies ermöglicht, dass Sie nicht nur zu identifizieren, erfolgreiche Aktivierung des Kontos und der sein Kennwort zurücksetzen, während der genehmigten Verwendungen, aber auch das Konto ändern Streams durch nicht autorisierte Benutzer zu identifizieren. Fehler bei Schreibvorgängen auf das Konto in Ihrem Sicherheitsinformations- und Ereignis Überwachung SIEM-System (sofern zutreffend) aufgezeichnet werden sollte, und Warnungen, die der Mitarbeiter zum Untersuchen von potenziellen Kompromisse mitgeteilt auslösen soll.  
  
SIEM-Lösungen Ereignisinformationen aus betreffenden Quellen (z. B. Ereignisprotokolle, Anwendungsdaten, Netzwerk-Datenströme, Antischadsoftware-Produkte und Erkennen von Eindringlingen Erkennungsquellen) aufnehmen, die Daten zu sortieren und intelligent und proaktive Aktionen vornehmen. Es gibt viele kommerzielle SIEM-Lösungen, und viele Unternehmen erstellen private Implementierungen. Eine gut durchdachte und entsprechend implementierten SIEM kann sicherheitsüberwachung und Reaktion auf Sicherheitsvorfälle Funktionen erheblich verbessern. Jedoch unterschiedlich Funktionen und Genauigkeit überaus Lösungen. SIEM werden würde den Rahmen dieses Dokuments sprengen, aber bestimmten Ereignis Empfehlungen enthalten sollte durch eine beliebige SIEM-Implementierung berücksichtigt werden.  
  
Weitere Informationen zu empfohlenen Konfiguration überwachungseinstellungen für Domänencontroller, finden Sie unter [Überwachung von Active Directory für Zeichen der Gefährdung](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md). Domain Controller-spezifische Einstellungen finden Sie unter [Überwachung von Active Directory für Zeichen der Gefährdung](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md).  
  
##### <a name="enabling-management-accounts-to-modify-the-membership-of-protected-groups"></a>Aktivieren der Verwaltung von Konten zum Ändern der Mitgliedschaft geschützter Gruppen  
In diesem Verfahren konfigurieren Sie Berechtigungen auf die Domäne AdminSDHolder-Objekt, um die neu erstellten Konten zum Ändern der Mitgliedschaft geschützter Gruppen in der Domäne zu ermöglichen. Dieses Verfahren kann über eine grafische Benutzeroberfläche (GUI) ausgeführt werden.  
  
Wie beschrieben [Anhang C: geschützte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md), die ACL für eine Domäne AdminSDHolder-Objekt wird effektiv "kopiert" auf Objekte geschützt, wenn Sie von SDProp Aufgabe ausgeführt wird. Geschützter Gruppen und Konten erben nicht die Berechtigungen aus dem AdminSDHolder-Objekt; Ihre Berechtigungen werden explizit festgelegt, mit denen auf das AdminSDHolder-Objekt übereinstimmen. Daher beim Ändern von Berechtigungen für das AdminSDHolder-Objekt, müssen Sie diese Attribute ändern, die in den Typ des geschützten Objekts geeignet sind, die Sie verwenden möchten.  
  
In diesem Fall werden Sie gewährt der neu erstellten Konten zum Lesen und Schreiben der Mitglieder Attribut für Gruppenobjekte zulassen. Allerdings das AdminSDHolder-Objekt ist kein Gruppenobjekt und Attribute werden nicht in die grafische ACL-Editor verfügbar gemacht. Es ist daher, dass Sie die Berechtigungen Änderungen über das Befehlszeilenprogramm "Dsacls" implementiert werden. Um die Verwaltung (deaktiviert) Konten Berechtigungen zum Ändern der Mitgliedschaft geschützter Gruppen gewähren, führen Sie die folgenden Schritte aus:  
  
1.  Melden Sie sich auf einem Domänencontroller, vorzugsweise für den Domänencontroller, die mit der Rolle PDC-Emulator (PDCE) mit den Anmeldeinformationen des Benutzerkontos, das Mitglied der Gruppe "DA" in der Domäne hergestellt wurde.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_136.png)  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, indem Sie mit der rechten Maustaste **Eingabeaufforderung** , und klicken Sie auf **als Administrator ausführen**.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_137.gif)  
  
3.  Wenn Sie aufgefordert werden, die für erhöhte Rechte zu genehmigen, klicken Sie auf **Ja**.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_138.gif)  
  
    > [!NOTE]  
    > Weitere Informationen über erhöhte Rechte und Benutzer Benutzerkontensteuerung (UAC) in Windows finden Sie unter [UAC-Prozesse und Interaktionen](https://technet.microsoft.com/library/dd835561(v=WS.10).aspx) auf der TechNet-Website.  
  
4.  An der Befehlszeile (ersetzen Sie dabei Ihre domänenspezifische Informationen) geben **Dsacls [distinguished Name des AdminSDHolder-Objekts in der Domäne] / g [Managementkonto UPN]: RPWP; Member**.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_139.gif)  
  
    Der vorherige Befehl (Groß-/Kleinschreibung nicht beachtet) funktioniert wie folgt:  
  
    -   DSACLS festgelegt oder ACEs für Verzeichnisobjekte zeigt  
  
    -   CN = AdminSDHolder, CN = System, DC = TailSpinToys, DC = Msft gibt das Objekt geändert werden  
  
    -   / G weist darauf hin, dass Grant ACE konfiguriert wird  
  
    -   PIM001@tailspintoys.msftist der Benutzerprinzipalname (UPN) des Sicherheitsprinzipals für die die ACEs erteilt werden soll  
  
    -   RPWP gewährt Eigenschaft lesen und Schreiben von Berechtigungen  
  
    -   Member ist der Name der Eigenschaft (Attribute) auf dem die Berechtigungen festgelegt werden  
  
    Weitere Informationen zur Verwendung von **Dsacls**, Dsacls ohne Parameter an einer Eingabeaufforderung eingeben.  
  
    Wenn Sie mehrere Konten für die Domäne erstellt haben, sollten Sie den Befehl "Dsacls" für jedes Konto ausführen. Wenn Sie die ACL-Konfiguration für das AdminSDHolder-Objekt abgeschlossen haben, sollten Sie erzwingen, SDProp ausführen, oder warten, bis der geplanten Ausführung abgeschlossen ist. Weitere Informationen zum Erzwingen von SDProp ausführen, finden Sie unter "Manually SDProp ausführen" im [Anhang C: geschützte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md).  
  
    Wenn SDProp ausgeführt wurde, können Sie überprüfen, ob die Änderungen an das AdminSDHolder-Objekt auf geschützten Gruppen in der Domäne angewendet wurden. Können nicht Sie dies überprüfen, indem Sie die ACL für das AdminSDHolder-Objekt zuvor beschriebenen Gründen anzeigen, aber Sie können überprüfen, ob die Berechtigungen angewendet wurden, indem Sie die ACLs auf geschützten Gruppen anzeigen.  
  
5.  In **Active Directory-Benutzer und-Computer**, stellen Sie sicher, dass Sie aktiviert haben **erweiterte Funktionen**. Klicken Sie hierzu auf **Ansicht**, suchen Sie nach der **Domänen-Admins** gruppieren, mit der rechten Maustaste in der Gruppe aus, und klicken Sie auf **Eigenschaften**.  
  
6.  Klicken Sie auf die **Sicherheit** Registerkarte, und klicken Sie auf **erweitert** zum Öffnen der **Advanced Security Settings for Domänen-Admins** Dialogfeld.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_140.gif)  
  
7.  Wählen Sie **zulassen ACE für das Managementkonto** , und klicken Sie auf **bearbeiten**. Stellen Sie sicher, dass das Konto nur gewährt wurde **Mitglieder lesen** und **Mitglieder schreiben** Berechtigungen auf dem Directaccess-Gruppe, und klicken Sie auf **OK**.  
  
8.  Klicken Sie auf **OK** in der **Advanced Security Settings** Dialogfeld, und klicken Sie dann auf **OK** erneut aus, um das Eigenschaftendialogfeld für die DA-Gruppe zu schließen.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_141.gif)  
  
9. Sie können die vorherigen Schritte für andere geschützten Gruppen in der Domäne wiederholen; die Berechtigungen sollten für alle geschützten Gruppen übereinstimmen. Sie haben jetzt die Erstellung und Konfiguration von der Konten für die geschützten Gruppen in dieser Domäne abgeschlossen.  
  
    > [!NOTE]  
    > Jedes Konto mit der Berechtigung zum Schreiben von Mitgliedschaft einer Gruppe in Active Directory kann auch selbst die Gruppe hinzufügen. Dieses Verhalten ist beabsichtigt und kann nicht deaktiviert werden. Aus diesem Grund sollten stets die Konten nicht deaktiviert, und die Konten sollten genau überwacht werden, wenn die Benachrichtigungen deaktiviert sind und wann sie verwendet werden.  
  
##### <a name="verifying-group-and-account-configuration-settings"></a>Überprüfen der Gruppe und Kontoeinstellungen-Konfiguration  
Nun, dass Sie erstellt und Konten, die die Mitgliedschaft der geschützten Gruppen in der Domäne ändern können (einschließlich der meisten sehr privilegierten Gruppen von EA, DA und BA) konfiguriert haben, sollten Sie sicherstellen, dass die Konten und ihre Verwaltungsgruppe ordnungsgemäß erstellt wurde. Überprüfung umfasst diese allgemeine Aufgaben:  
  
1.  Testen Sie die Gruppe, die kann aktivieren und deaktivieren die Management-Konten, um sicherzustellen, dass Mitglieder der Gruppe kann aktivieren und deaktivieren Sie die Konten und Kennwörter zurücksetzen, aber andere administrativen Aktionen, auf die Management-Konten ausführen können.  
  
2.  Testen Sie die Management-Konten, um sicherzustellen, dass hinzufügen und Entfernen von Mitgliedern zu Gruppen in der Domäne geschützt, aber keine anderen Eigenschaften geschützte Konten und Gruppen ändern.  
  
###### <a name="test-the-group-that-will-enable-and-disable-management-accounts"></a>Testen Sie die Gruppe, die zu aktivieren und Deaktivieren von Konten  
  
1.  Um ein Managementkonto aktivieren und das zugehörige Kennwort zurücksetzen zu testen, melden Sie sich bei einer sicheren administrativen Arbeitsstation mit einem Konto, das Mitglied der Gruppe ist, der im erstellten [Anhang I: Erstellen von Konten für geschützte Konten und Gruppen in Active Directory](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md).  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_142.gif)  
  
2.  Öffnen **Active Directory-Benutzer und-Computer**mit der rechten Maustaste auf den Verwaltungsserver ein, und klicken Sie auf **Konto aktivieren**.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_143.gif)  
  
3.  Ein Dialogfeld sollte anzeigen, bestätigt, dass das Konto aktiviert wurde.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_144.gif)  
  
4.  Als Nächstes Zurücksetzen des Kennworts für das Konto für die Verwaltung. Klicken Sie hierzu mit der rechten Maustaste erneut auf des Kontos, und klicken Sie auf **Kennwort zurücksetzen**.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_145.gif)  
  
5.  Geben Sie ein neues Kennwort für das Konto in der **neues Kennwort** und **Kennwort bestätigen** Felder ein, und klicken Sie dann auf **OK**.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_146.gif)  
  
6.  Ein Dialogfeld sollte angezeigt werden, bestätigt, dass das Kennwort für das Konto zurückgesetzt wurde.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_147.gif)  
  
7.  Versuchen Sie nun, zusätzliche Eigenschaften des Kontos Management zu ändern. Maustaste auf das Konto, und klicken Sie auf **Eigenschaften**, und klicken Sie auf die **Remotesteuerung** Registerkarte.  
  
8.  Wählen Sie **Aktivieren der Remotesteuerung** , und klicken Sie auf **übernehmen**. Der Vorgang sollte fehlerhaft sein und ein **Zugriff verweigert** Fehlermeldung sollte angezeigt werden.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_148.gif)  
  
9. Klicken Sie auf die **Konto** Registerkarte für das Konto, und versuchen, den Namen des Kontos, den Anmeldezeiten oder Anmeldearbeitsstationen ändern. Alle fehlschlagen soll, und berücksichtigen Optionen, die nicht durch gesteuert werden die **UserAccountControl** Attribut sollte deaktiviert werden, nicht mehr und nicht geändert.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_149.gif)  
  
10. Der Versuch, die Verwaltungsgruppe einer geschützten Gruppe wie die DA-Gruppe hinzuzufügen. Beim Klicken auf **OK**, sollte eine Meldung angezeigt, Sie darüber informiert, dass Sie nicht über Berechtigungen zum Ändern der Gruppe verfügen.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_150.gif)  
  
11. Zusätzliche Tests durchführen, wie erforderlich, um sicherzustellen, dass Sie etwas auf dem Managementkonto, mit Ausnahme von konfigurieren können **UserAccountControl** Einstellungen und das Zurücksetzen von Kennwörtern.  
  
    > [!NOTE]  
    > Die **UserAccountControl** Attribut steuert mehrere Konto Konfigurationsoptionen. Sie können nicht über die Berechtigung zum Ändern nur einige Konfigurationsoptionen beim Erteilen von Schreibberechtigungen für das Attribut erteilen.  
  
###### <a name="test-the-management-accounts"></a>Testen Sie die Management-Konten  
Nun, dass Sie ein oder mehrere Konten aktiviert haben, die die Mitgliedschaft der geschützten Gruppen ändern können, können Sie die Konten, um sicherzustellen, dass sie geschützte Gruppenmitgliedschaft ändern können, jedoch nicht anderer auf geschützte Konten und Gruppen möglich testen.  
  
1.  Melden Sie sich an einen sicheren administrative Hosts als das erste Managementkonto an.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_151.gif)  
  
2.  Starten Sie **Active Directory-Benutzer und-Computer** , und suchen Sie die **Domänen-Admins**.  
  
3.  Mit der rechten Maustaste die **Domänen-Admins** Gruppe, und klicken Sie auf **Eigenschaften**.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_152.gif)  
  
4.  In der **Eigenschaften von Domänen-Admins**, klicken Sie auf die **Mitglieder** Registerkarte und **klicken Sie auf** hinzufügen. Geben Sie den Namen eines Kontos, das temporäre Domänen-Admins-Berechtigungen erhalten, und klicken Sie auf **Namen überprüfen**. Wenn der Name des Kontos unterstrichen ist, klicken Sie auf **OK** wieder die **Mitglieder** Registerkarte.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_153.gif)  
  
5.  Auf der **Mitglieder** Registerkarte für die **Eigenschaften von Domänen-Admins** Dialogfeld klicken Sie auf **übernehmen**. Nach dem Klicken auf **übernehmen**, das Konto muss ein Mitglied der Gruppe DA bleiben und Sie erhalten keine Fehlermeldungen angezeigt.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_154.gif)  
  
6.  Klicken Sie auf die **verwaltet von** Registerkarte die **Eigenschaften von Domänen-Admins** Dialogfeld Feld, und stellen Sie sicher, dass Sie alle Felder Text eingeben können und alle Schaltflächen deaktiviert werden.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_155.gif)  
  
7.  Klicken Sie auf die **allgemeine** Registerkarte die **Eigenschaften von Domänen-Admins** Dialogfeld ein, und stellen Sie sicher, dass Sie die Informationen zu dieser Registerkarte ändern können.  
  
    ![Erstellen von Konten](media/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory/SAD_156.gif)  
  
8.  Wiederholen Sie diese Schritte für weitere geschützter Gruppen nach Bedarf. Wenn Sie fertig sind, melden Sie sich an einem sicheren administrative Host mit einem Konto, das Mitglied der Gruppe ist, die Sie zum Aktivieren und deaktivieren die Konten erstellt. Klicken Sie dann zurücksetzen Sie das Kennwort für das Managementkonto Sie gerade getestet, und deaktivieren Sie das Konto. Sie haben Setup die Management-Konten und die Gruppe, die zum Aktivieren und deaktivieren die Konten zuständig ist abgeschlossen.  
  


