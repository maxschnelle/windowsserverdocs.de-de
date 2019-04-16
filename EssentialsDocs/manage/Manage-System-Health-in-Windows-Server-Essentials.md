---
title: "Verwalten der Systemintegrität in Windows Server Essentials"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3043f83b-389c-4f37-a1ff-85afe99314fa
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 91635a58c64fbf74d3b0139be7c9c36365487319
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="manage-system-health-in-windows-server-essentials"></a>Verwalten der Systemintegrität in Windows Server Essentials

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials
 
 In diesem Thema wird erläutert, wie anzeigen und reagieren auf alle Warnungen in Ihrem Netzwerk über das Dashboard wird.  
  
> [!NOTE]
>  In Windows Server Essentials und Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle, die Warnungen für den Server und Clientcomputer im Netzwerk werden nicht mehr in der Meldungsanzeige angezeigt, sondern können stattdessen angezeigt werden, auf die **Integritätsberichte** auf der Registerkarte der **Home** Seite.  
  
 Windows Server Essentials überwacht aktiv jeden Computer, die mit dem Server verbunden ist, und warnt den Administrator auf Probleme im Zusammenhang mit dem Systemstatus s, wichtige Updates, einschließlich der fehlende Schutz vor Schadsoftware, veralteter Virusdefinitionen auf Clientcomputern und andere wichtige Probleme, die eine Aktion erfordern. Diese Probleme werden angezeigt, in der Meldungsanzeige, das vom Server s Dashboard oder dem Clientcomputer s Launchpad in Windows Server Essentials oder gestartet werden kann als Warnungen der **Integritätsberichte** Registerkarte in Windows Server Essentials. Standardmäßig werden die Warnungen alle 30 Minuten aktualisiert, doch Sie können Warnungen für Ihr Netzwerk jederzeit durch Klicken auf **aktualisieren** in der Meldungsanzeige oder auf die **Integritätsberichte** Registerkarte.  
  
 Die folgenden Themen helfen zu verstehen, anzeigen und reagieren auf Warnungen in der Meldungsanzeige und bieten auch Anweisungen zum Konfigurieren eines Servers zum Empfangen von Benachrichtigungen in einer e-Mail:  
  
-   [Über die Integrität melden-Add-In](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_AddIn)  
  
-   [Anzeigen von Warnungen mithilfe der Meldungsanzeige](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_View)  
  
-   [Organisation von Warnungen in der Meldungsanzeige](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Organize)  
  
-   [Reagieren auf Warnungen](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Respond)  
  
-   [Richten Sie e-Mail-Benachrichtigungen für Warnungen](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Email)  
  
-   [Potenzielle computerwarnungen](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Potential)  
  
##  <a name="BKMK_AddIn"></a>Über die Integrität melden-Add-In  
 Der Statusbericht-add-in für Windows Server Essentials bietet Ihnen konsolidierte Informationen über das Windows Server Essentials-Netzwerk, und ermöglicht es Ihnen, diese Informationen an andere Personen zu verteilen. Diese Informationen können angezeigt werden, auf die **Berichte** Dashboard-Registerkarte. Mit der **Berichte** Registerkarte können Sie Folgendes tun:  
  
-   [Generieren eines Berichts auf Anforderung oder nach Zeitplan](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Generate)  
  
-   [Passen Sie den Inhalt des Berichts](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Customize)  
  
-   [E-Mail-Bericht](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_emailreport)  
  
> [!NOTE]
>  **Windows Server Essentials:** Sie können das Statusbericht-add-in für Windows Server Essentials aus der [Microsoft Download Center](https://go.microsoft.com/fwlink/p/?LinkId=266342).  
>   
>  **Windows Server Essentials:** wird standardmäßig das Statusbericht-add-in integriert ist Windows Server Essentials oder Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle, und die Statusberichte werden auf die **Integritätsberichte** Registerkarte im Dashboard s **Home** Seite.  
  
###  <a name="BKMK_Generate"></a>Generieren eines Berichts auf Anforderung oder nach Zeitplan  
 Nachdem das Statusbericht-add-in installieren und starten das Dashboard, einer neuen Registerkarte **Berichte** wird dem Dashboard hinzugefügt. Sie können einen Statusbericht bei Bedarf zu einem beliebigen Zeitpunkt generieren, indem Sie auf die **Statusbericht erstellen** Aufgabe auf den **Berichte** Registerkarte.  
  
 Nachdem eines Statusberichts wird ein neues Element erstellt, in den Listenbereich identifizierten Datum und Uhrzeit, die der Bericht generiert wurde. Um ein Element zu öffnen, können Sie es in den Listenbereich doppelklicken, oder können Sie es auswählen und klicken Sie dann auf **Statusbericht öffnen** im Aufgabenbereich. Der Bericht wird in einem neuen Fenster im HTML-Format angezeigt.  
  
 Zusätzlich zur Erstellung eines Berichts manuell sollten Sie auch den Bericht nach einem Zeitplan täglich oder stündlich automatisch generiert werden sollen. Klicken Sie dazu im Aufgabenbereich auf **Einstellungen für den Integritätsbericht anpassen**, und klicken Sie dann auf die **planen und senden** Registerkarte. Die **Zeitplan** Feature ist standardmäßig deaktiviert, und Sie können Schalten Sie ihn durch die Auswahl der **ein Integritätsbericht zum geplanten Zeitpunkt generieren** Kontrollkästchen.  
  
###  <a name="BKMK_Customize"></a>Passen Sie den Inhalt des Berichts  
 Der Integritätsbericht enthält Folgendes:  
  
-   **Kritische Warnungen** Dies gilt auch für die kritische Warnungen und Warnungen, die Sie in der Meldungsanzeige auf dem Dashboard angezeigt. Informationswarnungen sind im Integritätsbericht nicht enthalten.  
  
-   **Kritische Fehler in den Ereignisprotokollen** Anwendungs- und Dienstprotokollen gescannt, und Fehler, die in den letzten 24 Stunden protokolliert werden angezeigt, der **Details** Bereich des Berichts.  
  
-   **Server-Sicherung** die Informationen über die letzte serversicherung wird angezeigt, dem **Details** Bereich des Berichts.  
  
-   **AutoStart-Dienste nicht ausgeführt.** zum Zeitpunkt der Bericht generiert wird, wenn ein automatisch gestarteter Dienst nicht ausgeführt wird, werden die Informationen zu diesem Dienst aufgelistet werden die **Details** Bereich des Berichts.  
  
-   **Updates** sehen Sie den Status des Servers und den Clientcomputern in der **Details** Abschnitt.  
  
-   **Speicher** die Liste der Laufwerke und ihre Kapazität wird angezeigt, dem **Details** Abschnitt.  
  
 Im Integritätsbericht zunächst Anzeigen der **Zusammenfassung**, und für diese Elemente mit einem roten Fehlersymbol oder ein gelbes Warnsymbol, klicken Sie dann auf die **Details** Link in der gleichen Zeile, um die Details zu diesem Element anzuzeigen.  
  
 Wenn Sie nicht einige Datenpunkte interessiert, die standardmäßig im Bericht enthalten sind sind, können Sie den Inhalt des Berichts anpassen, indem Sie auf **Einstellungen für den Integritätsbericht anpassen** im Aufgabenbereich, und klicken Sie dann auf die **Inhalt**Registerkarte deaktivieren Sie die Kontrollkästchen für den Inhalt, der vergessen im Bericht angezeigt werden soll. Z. B. Wenn Sie Ihre eigenen serversicherungsplan verfügen und Don ' t die Warnungen zu serversicherungen sehen möchten, Sie ausschließen, serversicherungen aus dem Bericht durch Deaktivieren der **Server-Sicherung** Kontrollkästchen.  
  
###  <a name="BKMK_emailreport"></a>E-Mail-Bericht  
 Melden Sie sich auf das Dashboard, um Berichte zu lesen, ist für einige Administratoren immer noch unpraktisch, insbesondere dann, wenn sie mehrere Server zum Verwalten verfügen. Mit der e-Mail-Funktion aktiviert, nachdem ein Bericht erstellt wird, eine e-Mail gesendet, eine Liste der angegebenen e-Mail-Adressen mit dem Inhalt des Berichts. Der Administrator kann einfach diesen Bericht von jedem Gerät oder jeder Clientanwendung, und stellen Sie sicher, dass der Server im bestmöglichen Zustand ausgeführt wird.  
  
 In der **Einstellungen für Integritätsbericht anpassen** Dialogfeld nach dem Aktivieren von e-Mail, ändern Sie die SMTP-Einstellungen und geben Sie eine Liste der e-Mail-Empfänger, Sie werden feststellen, dass im im Aufgabenbereich eine neue Aufgabe wird angezeigt: **Integritätsbericht**. Weitere Informationen zu SMTP-Einstellungen finden Sie unter [e-Mail-Benachrichtigungen für Warnungen einrichten](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Email).  
  
 Sie können einen vorhandenen Bericht auswählen, und klicken Sie dann auf **Integritätsbericht**. Sie können auch einen neuen Bericht erstellen, und es automatisch an Ihr Postfach gesendet. Wenn Sie einen Zeitplan für den Bericht automatisch generiert werden konfiguriert haben, wird der Bericht automatisch in Ihren Posteingang bereitgestellt, nachdem täglich (oder stündlich) wie geplant werden generiert.  
  
##  <a name="BKMK_View"></a>Anzeigen von Warnungen mithilfe der Meldungsanzeige  
 In diesem Abschnitt wird erläutert, wie Sie das Dashboard oder das Launchpad zum Öffnen der Meldungsanzeige, um den Status aller Computer auf dem Servernetzwerk anzuzeigen.  
  
#### <a name="to-open-the-alert-viewer-by-using-the-dashboard"></a>Um die Meldungsanzeige zu öffnen, mithilfe des Dashboards  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie im Navigationsbereich auf eines der angezeigten Warnsymbole (kritisch, Warnung oder Information). Dadurch wird die Meldungsanzeige geöffnet.  
  
#### <a name="to-open-the-alert-viewer-from-the-launchpad"></a>So öffnen die Meldungsanzeige über das Launchpad  
  
1.  Öffnen Sie das Launchpad auf einem Computer, der mit dem Server verbunden ist. Wenn Sie aufgefordert werden, melden Sie sich an den Startbildschirm mit Ihrem Benutzernamen und Kennwort an.  
  
2.  Klicken Sie auf eines der angezeigten Warnsymbole (kritisch, Warnung und Information) unten im Launchpad, um die Meldungsanzeige zu öffnen, und folgen Sie dann die Anweisungen im Detailbereich der Meldungsanzeige, um die Auflösung der Warnung.  
  
##  <a name="BKMK_Organize"></a>Organisation von Warnungen in der Meldungsanzeige  
 Sie können Warnungen in der Meldungsanzeige organisieren und angezeigt abhängig vom Schweregrad (kritisch, Warnung oder Information) oder basierend auf den Namen des Computers.  
  
#### <a name="to-organize-alerts-in-the-alert-viewer"></a>Warnungen in der Meldungsanzeige organisieren  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie im Navigationsbereich auf eines der angezeigten Warnsymbole (kritisch, Warnung oder Information). Dadurch wird die Meldungsanzeige geöffnet.  
  
3.  Erweitern Sie die **organisieren** Dropdown-Liste, und führen Sie eine der folgenden:  
  
    1.  Wählen Sie **Filter by Computer**, und klicken Sie auf den Namen des Computers, für die Sie die Warnungen anzeigen möchten. Dadurch werden Warnungen in der Meldungsanzeige nur für den ausgewählten Computer angezeigt.  
  
    2.  Wählen Sie **nach Warnungstyp filtern**, und klicken Sie auf den Warnungstyp (kritisch, Warnung oder Information), die für die Sie die Warnungen anzeigen möchten. Dadurch werden nur die ausgewählte Warnungstypen in der Meldungsanzeige angezeigt.  
  
##  <a name="BKMK_Respond"></a>Reagieren auf Warnungen  
 Wenn Sie eine Warnung auftritt, können Sie optional einen der folgenden Schritte aus:  
  
-   [Auflösen einer Warnung](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Resolve)  
  
-   [Warnung ignorieren](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Aktivieren einer Warnung](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Eine Warnung löschen](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_4)  
  
###  <a name="BKMK_Resolve"></a>Auflösen einer Warnung  
 Führen Sie die Anweisungen in der Meldungsanzeige aufgelöst. Wenn eine Warnung behoben wurde, wird sie weiterhin in der Meldungsanzeige angezeigt, bis sie aktualisiert wird.  
  
###  <a name="BKMK_3"></a>Warnung ignorieren  
 Sie können auch eine Warnung ignorieren, wenn Sie später darauf reagieren möchten. Wenn Sie eine Warnung ignorieren, wird Sie weiterhin in der Meldungsanzeige angezeigt, und es ist jedoch deaktiviert und abgeblendet. Eine ignorierte Warnung ist nicht in die gesamtbewertung der Computerintegrität des Computers enthalten. Um eine ignorierte Warnung zu beheben, müssen Sie zuerst aktivieren.  
  
##### <a name="to-ignore-an-alert"></a>Um eine Warnung zu ignorieren.  
  
1.  Öffnen Sie das Launchpad auf dem Computer, der mit dem Windows Server Essentials-Server verbunden ist.  
  
2.  Klicken Sie auf dem Launchpad auf eines der angezeigten Warnsymbole (kritisch, Warnung und Information). Dadurch wird die Meldungsanzeige geöffnet.  
  
3.  Wählen Sie in der Meldungsanzeige die Warnung, die Sie ignorieren möchten, und klicken Sie dann in der **Aufgaben** auf **Warnung ignorieren**.  
  
 Um eine deaktivierte Warnung zu reagieren, müssen Sie zuerst aktivieren.  
  
###  <a name="BKMK_5"></a>Aktivieren einer Warnung  
 Sie können eine Warnung, die Sie zuvor ignoriert haben. Nachdem die Warnung aktiviert ist, können Sie lösen Sie ihn oder ggf. löschen. Eine Warnung angezeigt wird, wie deaktiviert, wenn ignoriert werden. Wenn Sie eine Warnung, die Sie zuvor deaktiviert haben aktivieren, aktiv, und erneut in die gesamtbewertung der Computerintegrität Computer enthalten ist.  
  
##### <a name="to-enable-an-alert"></a>So aktivieren Sie eine Warnung  
  
1.  Öffnen Sie das Launchpad auf dem Computer, der mit dem Server verbunden ist.  
  
2.  Klicken Sie auf dem Launchpad auf eines der angezeigten Warnsymbole (kritisch, Warnung und Information) um die Meldungsanzeige zu öffnen.  
  
3.  In der Meldungsanzeige mit der Maustaste der Warnung, die Sie aktivieren möchten, und klicken Sie dann auf **Warnung aktivieren**.  
  
###  <a name="BKMK_4"></a>Eine Warnung löschen  
 Sie können eine Warnung löschen, wenn nicht behoben oder ignoriert werden möchten. Die Meldungsanzeige können auf dem Launchpad Sie um für Ihren Computer generierte Warnungen zu löschen. Wenn Sie eine Warnung löschen, und der Server das Problem in der nächsten Auswertungszyklus für Netzwerk Integrität erneut erkennt, wird eine neue Warnung generiert.  
  
##### <a name="to-delete-an-alert"></a>So löschen Sie eine Warnung  
  
1.  Öffnen Sie das Launchpad auf dem Computer, der mit dem Server verbunden ist.  
  
2.  Klicken Sie auf dem Launchpad auf eines der angezeigten Warnsymbole (kritisch, Warnung und Information) um die Meldungsanzeige zu öffnen.  
  
3.  In der Meldungsanzeige mit der Maustaste der Warnung, die Sie löschen möchten, und klicken Sie dann auf **Warnung löschen**.  
  
##  <a name="BKMK_Email"></a>Richten Sie e-Mail-Benachrichtigungen für Warnungen  
 Sie können den Server, um Sie per e-Mail über das Auftreten von Warnungen benachrichtigt werden, konfigurieren. Die e-Mail-Benachrichtigungen für diese Warnungen enthalten Informationen zu Netzwerkproblemen und die Lösungsschritte identisch mit den Informationen, die in der Meldungsanzeige angezeigt wird. Einige der Netzwerkintegrität erfolgen programmgesteuert.  
  
 Wenn Sie auf Ihrem Server zum Senden von Benachrichtigungen in einer e-Mail konfigurieren, wird eine e-Mail-Benachrichtigung für Warnungen gesendet, die während der Bewertung der Netzwerkintegrität gefunden werden. Allerdings sind nicht alle Warnungen, die in der Meldungsanzeige gemeldet werden in e-Mails protokolliert.  
  
 Alle 30 Minuten wird die Aufgabe zur Bewertung von Warnungen E-Mail ausgeführt, auf dem Server, der das Netzwerk auf Warnungen ausgewertet wird. Eine e-Mail-Benachrichtigung wird ausgeführt, wenn jede Warnung gesendet, die für e-Mail-Benachrichtigung erfolgt, festgelegt ist. Eine zweite e-Mail wird nicht gesendet werden, wenn die Warnung im nächsten Auswertungszyklus, Überflutung Ihres Postfach noch aktiv ist. Wenn jedoch eine neue Warnung in einem künftigen bewertungszyklus erkannt wird, eine e-Mail-Benachrichtigung wird gesendet, die die neuen und vorherigen Warnungen enthält.  
  
###  <a name="BKMK_list"></a>Warnungen, die dazu führen, dass e-Mail-Benachrichtigungen  
 Die folgenden Warnungen in der Meldungsanzeige führen e-Mail-Benachrichtigungen, wenn Sie den Server zum Senden von e-Mail-Benachrichtigungen für Warnungen einrichten:  
  
-   Fehler sind in einer clientcomputersicherung vorhanden.  
  
-   Der Server wurde neu gestartet.  
  
-   Ein oder mehrere Dienste nicht ausgeführt werden.  
  
-   Die Windows Server-Speicherdienst wird nicht ausgeführt.  
  
-   Der Evaluierungszeitraum ist abgelaufen.  
  
-   Jetzt aktivieren.  
  
-   Quellserver wird heruntergefahren.  
  
-   BPA-Scanergebnisse enthalten Fehler.  
  
-   BPA-Scanergebnisse enthalten Warnungen.  
  
-   Ein Zertifikat ist nicht für Zugriff überall verfügbar.  
  
-   Das Zertifikat für Zugriff überall ist abgelaufen.  
  
-   Der Router ist nicht ordnungsgemäß konfiguriert.  
  
-   Der Webserver ist nicht ordnungsgemäß konfiguriert.  
  
-   Remote Desktop Services ist nicht ordnungsgemäß konfiguriert.  
  
-   Die Firewall ist nicht ordnungsgemäß konfiguriert.  
  
-   Der Internetdomänenname ist abgelaufen.  
  
-   Der Internetdomänenname kann nicht aktualisiert werden.  
  
-   Lizenzfehler: Überprüfung der Gesamtstruktur-Vertrauensstellung.  
  
-   Lizenzfehler: Domänencontrollerüberprüfung.  
  
-   Lizenzfehler: FSMO-Rollenüberprüfung.  
  
-   Lizenzfehler: FSMO-Erzwingungsrichtlinien.  
  
-   Lizenzfehler: Erzwingungslast-Richtlinien.  
  
-   Lizenzfehler: Active Directory-Domänendienste.  
  
-   Office 365-Abonnement ist abgelaufen.  
  
-   Office 365-Authentifizierung war nicht erfolgreich.  
  
-   Die Kennwortrichtlinie ist falsch.  
  
-   Der Dienst für die Kennwortsynchronisierung kann ein Benutzerkennwort mit Office 365 nicht synchronisieren.  
  
-   Das Windows-Kennwort zu ändern.  
  
-   Ihr Office 365-Kennwort ist nicht identisch mit dem Windows-Kennwort.  
  
-   Exchange-Server kann keine Verbindung hergestellt werden.  
  
-   Microsoft Exchange Server wurde ein Problem aufgetreten.  
  
-   Eine oder mehrere Festplatten in Server-Sicherung ist nicht verbunden.  
  
-   Die Sicherungsfestplatte verfügt nicht genügend freien Speicherplatz für den Server-Sicherung.  
  
-   Server-Sicherung war nicht erfolgreich, da eine Momentaufnahme des Laufwerks erstellt werden konnte.  
  
-   Eine geplante Sicherung wurde nicht erfolgreich abgeschlossen.  
  
-   Mindestens ein vordefinierter Serverordner fehlen.  
  
-   Freier Speicherplatz ist auf mindestens einer Serverfestplatte gering.  
  
-   VSS Writer für den Speicherdienst wird nicht ausgeführt.  
  
-   Weisen eine geringe Speicherkapazität auf Festplatten.  
  
-   Ein oder mehrere Laufwerke funktionieren nicht, und es ist offline.  
  
###  <a name="BKMK_SMTP"></a>Konfigurieren von SMTP auf Ihrem Server zum Senden von warnbenachrichtigungen per e-Mail in Windows Server Essentials  
 In diesem Abschnitt wird erläutert, wie so konfigurieren Sie den Server, um e-Mail-Benachrichtigungen für Warnungen gesendet wird.  
  
> [!NOTE]
>  Sie können das Statusbericht-add-in für Windows Server Essentials aus der [Microsoft Download Center](https://go.microsoft.com/fwlink/p/?LinkId=266342).  
  
##### <a name="to-set-up-email-notification-for-alerts"></a>E-Mail-Benachrichtigungen für Warnungen einrichten  
  
1.  Von der **Dashboard**Öffnen der **Alert Viewer**.  
  
2.  In der **Alert Viewer**, klicken Sie auf **warnungsbenachrichtigung per e-Mail einrichten**.  
  
3.  In der **e-Mail-Benachrichtigungen für Warnungen einrichten** Fenster, klicken Sie auf **aktivieren**.  
  
4.  In der **SMTP-Einstellungen** Fenster, gehen Sie folgendermaßen vor:  
  
    1.  Für **von e-Mail-Adresse**, geben Sie die e-Mail-Adresse für das Senden der e-Mails gewünschten Warnungen aus. Diese e-Mail-Adresse wird als die Adresse des Absenders s in der Benachrichtigung angezeigt.  
  
    2.  Für **SMTP-Servername**in der **von e-Mail-Adresse** Text Geben Sie den Namen des SMTP-Servers, die Sie in Schritt 4a angegeben haben. (Siehe Tabelle 1 für eine Liste mit einigen SMTP-Servernamen).  
  
    3.  Für **SMTP-Port**, geben Sie die Portnummer, die vom SMTP-Server zum Senden und Empfangen von e-Mails verwendet wird. (Siehe Tabelle 1 finden Sie die Portnummern, die von einigen SMTP-Servern verwendet werden).  
  
    4.  Wählen Sie **dieser Server erfordert eine sichere Verbindung (SSL)** Falls der SMTP-Server SSL verwendet (siehe Tabelle 1).  
  
    5.  Wählen Sie **Server erfordert Authentifizierung** , wenn der SMTP-Server einen Benutzernamen und Kennwort erfordert (siehe Tabelle 1). Wenn Sie dieses Kontrollkästchen aktivieren, geben Sie den Benutzernamen und das Kennwort für die e-Mail-Adresse, die Sie in eingegeben haben die **von e-Mail-Adresse** Feld in Schritt 4a angegeben haben, und klicken Sie dann auf **OK**.  
  
    > [!NOTE]
    >  Sie können die Informationen über den SMTP-Servernamen Portnummer und SSL-Verwendung von Ihrem Internetdienstanbieter abrufen.  
  
     **Tabelle 1** Beispiele für SMTP-Servernamen, Authentifizierung und SSL-verschlüsselungsanforderungen und Portnummern  
  
    |SMTP-Server|SSL erforderlich|Authentifizierung erforderlich|Portnummer|Konto/Anmeldename|  
    |-----------------|------------------|-----------------------------|-----------------|------------------------------|  
    |SMTP.gmail.com|Ja|Ja|587|Geben Sie vollständige e-Mail-Adresse mit Domänennamen und Kennwort für die Authentifizierung.|  
    |SMTP.Live.com|Ja|Ja|587|Geben Sie vollständige e-Mail-Adresse mit Domänennamen und Kennwort für die Authentifizierung.|  
    |SMTP.Comcast.NET|Ja|Nein|587|Geben Sie vollständige e-Mail-Adresse mit Domänennamen und Kennwort für die Authentifizierung.|  
    |SMTP.Mail.Yahoo.de|Nein|Ja|25|Geben Sie nur die e-Mail-Adresse ohne einen Domänennamen für den Benutzernamen ein.|  
  
5.  In **Benachrichtigungen für Warnungen einrichten**, für **E-Mail-Empfänger**, geben Sie die e-Mail-Adressen der Personen, die Sie per e-Mail-Benachrichtigung erhalten möchten. Stellen Sie sicher, dass Sie die e-Mail-Adressen durch ein Semikolon (;) getrennt.  
  
6.  Um sicherzustellen, dass Sie den SMTP-Server konfiguriert haben, die Einstellungen korrekt zum Senden von e-Mail-Benachrichtigungen für Warnungen, klicken Sie auf **anwenden und e-Mail senden**.  
  
    > [!NOTE]
    >  Beim Klicken auf **anwenden und e-Mail senden**, in der Regel eine Beispiel für die e-Mail-Benachrichtigung mit ohne aufgelisteten Status-Warnungen erhalten. Wenn eine zustandswarnung, die konfiguriert ist, um eine e-Mail-Benachrichtigung senden während dieses Test-Prozesses identifiziert wird, wird diese Warnung jedoch in der-e-Testmail enthalten.  
  
### <a name="configuring-smtp-on-your-server-to-send-health-reports-in-windows-server-essentials"></a>Konfigurieren von SMTP auf Ihrem Server zum Senden von integritätsberichten in Windows Server Essentials  
 In diesem Abschnitt wird erläutert, wie die SMTP-Einstellungen für den Server so konfigurieren, dass Sie Integritätsberichte über e-Mail erhalten wird.  
  
> [!NOTE]
>  Standardmäßig das Statusbericht-add-in integriert ist Windows Server Essentials oder Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle, und die Statusberichte werden auf die **Integritätsberichte** Registerkarte im Dashboard s **Home** Seite.  
  
##### <a name="to-set-up-email-notification-for-health-reports"></a>So richten Sie e-Mail-Benachrichtigungen für Integritätsberichte ein  
  
1.  Von der **Dashboard**, klicken Sie auf die **Berichte** Registerkarte.  
  
2.  In der **Integritätsberichtsaufgaben** Aufgabenbereich, klicken Sie auf **Einstellungen für den Integritätsbericht anpassen**.  
  
3.  In der **Einstellungen für Integritätsbericht anpassen** Fenster, klicken Sie auf die **planen und senden** Registerkarte.  
  
4.  In der **planen und senden** Registerkarte die **E-Mail** Abschnitt, gehen Sie folgendermaßen vor:  
  
    1.  Klicken Sie auf **aktivieren**, und geben Sie die e-Mail-Adresse für das Senden von der Integrität der gewünschten von Berichten aus. Diese e-Mail-Adresse wird als Absenderadresse in die Integritätsberichte s angezeigt, die per e-Mail gesendet werden.  
  
        1.  Für **SMTP-Servername**, geben Sie den Namen des SMTP-Servers. (Siehe Tabelle 1 für eine Liste mit einigen SMTP-Servernamen).  
  
        2.  Für **SMTP-Port**, geben Sie die Portnummer, die vom SMTP-Server zum Senden und Empfangen von e-Mails verwendet wird. (Siehe Tabelle 1 finden Sie die Portnummern, die von einigen SMTP-Servern verwendet werden).  
  
        3.  Wählen Sie **dieser Server erfordert eine sichere Verbindung (SSL)** Falls der SMTP-Server SSL verwendet (siehe Tabelle 1).  
  
        4.  Wählen Sie **Server erfordert Authentifizierung** , wenn der SMTP-Server einen Benutzernamen und Kennwort erfordert (siehe Tabelle 1). Wenn Sie dieses Kontrollkästchen aktivieren, geben Sie den Benutzernamen und das Kennwort für die e-Mail-Adresse, die Sie in eingegeben haben die **von e-Mail-Adresse** Feld in Schritt 4a angegeben haben, und klicken Sie dann auf **OK**.  
  
            > [!NOTE]
            >  Sie können die Informationen über den SMTP-Servernamen Portnummer und SSL-Verwendung von Ihrem Internetdienstanbieter abrufen.  
  
            > [!NOTE]
            >  Microsoft empfiehlt dringend, die Sie SSL verwenden, da der Bericht mehrere Serverstatus enthalten kann, die von böswilligen Parteien zum Aufdecken von Sicherheitsrisiken verwendet werden können (z. B.: fehlen von Windows Update). Aktivieren von SSL werden die Daten während der Übertragung verschlüsselt und das Risiko des Verfügbarmachens von Server-Schwachstelle.  
  
5.  Nach dem Aktivieren von e-Mail, die **SMTP-Einstellungen ändern** Link wird angezeigt. Auch eine neue Aufgabe **Integritätsbericht**, ruft im angezeigten **Integritätsberichtsaufgaben**.  
  
     **Tabelle 1** Beispiele für SMTP-Servernamen, Authentifizierung und SSL-verschlüsselungsanforderungen und Portnummern  
  
    |SMTP-Server|SSL erforderlich|Authentifizierung erforderlich|Portnummer|Konto/Anmeldename|  
    |-----------------|------------------|-----------------------------|-----------------|------------------------------|  
    |SMTP.gmail.com|Ja|Ja|587|Geben Sie vollständige e-Mail-Adresse mit Domänennamen und Kennwort für die Authentifizierung.|  
    |SMTP.Live.com|Ja|Ja|587|Geben Sie vollständige e-Mail-Adresse mit Domänennamen und Kennwort für die Authentifizierung.|  
    |SMTP.Comcast.NET|Ja|Nein|587|Geben Sie vollständige e-Mail-Adresse mit Domänennamen und Kennwort für die Authentifizierung.|  
    |SMTP.Mail.Yahoo.de|Nein|Ja|25|Geben Sie nur die e-Mail-Adresse ohne einen Domänennamen für den Benutzernamen ein.|  
  
6.  In **Einstellungen für Integritätsbericht anpassen**, für **automatisch den Integritätsbericht an die folgenden e-Mail-Empfänger senden:**, geben Sie die e-Mail-Adressen der Personen, die Sie Integritätsberichte per e-Mail erhalten möchten. Stellen Sie sicher, dass Sie die e-Mail-Adressen durch ein Semikolon (;) getrennt.  
  
7.  Um sicherzustellen, dass Sie den SMTP-Server konfiguriert haben Einstellungen ordnungsgemäß zum Senden von integritätsberichten per e-Mail, über die Registerkarte Aufgabenfenster auf dem Dashboard einen Bericht auswählen, und klicken Sie auf **Integritätsbericht** im Aufgabenbereich.  
  
##  <a name="BKMK_Potential"></a>Potenzielle computerwarnungen  
 In diesem Abschnitt wird erläutert, sowie die Verwaltung von Warnungen, die speziell auf den Computer, mit dem Server verbunden ist und die im Launchpad des Computers angezeigt werden.  
  
 Die folgende Tabelle enthält einige der computerwarnungen, die generiert und in der Meldungsanzeige angezeigt werden, wenn sie auf Ihren Computer sind werden können.  
  
|Titel der Warnung|Auswirkung der Warnung und Lösung|  
|-----------------|---------------------------------|  
|Der aktuelle Status der Netzwerkfirewall bietet nur einen geringen Schutz für diesen Computer.|Unbefugte Personen oder Softwareprogramme kann möglicherweise auf diesen Computer zugreifen, wenn Windows-Firewall nicht aktiviert ist.|  
|Virenschutz ist ausgeschaltet, nicht installiert oder nicht auf dem neuesten Stand.|Die Daten auf Ihrem Computer sind gefährdet Wenn die **Virenschutz** sicherheitseinstellung deaktiviert oder nicht aktualisiert. [Zum Schutz Ihres Computers](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Protect), führen Sie die angegebenen Schritte aus.|  
|Spyware und unerwünschte Software Protection deaktiviert ist, nicht installiert oder nicht auf dem neuesten Stand.|Die Daten auf Ihrem Computer sind gefährdet Wenn die **Spyware und unerwünschter Softwareschutz** deaktiviert oder nicht aktualisiert. [Zum Schutz Ihres Computers](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Protect), führen Sie die angegebenen Schritte aus.|  
|Windows Update ist deaktiviert.|Sie werden möglicherweise profitieren Sie von der neuen und berichtigten Funktionen von Updates, wenn Windows Update aktiviert ist. Klicken Sie zum Aktivieren von Windows Update in der Meldungsanzeige auf **Windows Update öffnen**.<br /><br /> Wenn die **Windows Update öffnen** Aufgabe nicht angezeigt wird, Sie sind nicht auf dem Computer, auf dem die Warnung ausgelöst wurde, angemeldet. Sie müssen auf dem Computer angemeldet werden auf denen die Warnung, zum Ausführen dieser Aufgabe im Alert Viewer ausgelöst wurde.|  
|Wichtige Updates sollten installiert werden.|Sie werden möglicherweise profitieren Sie von der neuen und berichtigten Funktionen von Updates, wenn Windows Update aktiviert ist. Klicken Sie zum Aktivieren von Windows Update in der Meldungsanzeige auf **Windows Update öffnen**.<br /><br /> Wenn die **Windows Update öffnen** Aufgabe nicht angezeigt wird, Sie sind nicht auf dem Computer, auf dem die Warnung ausgelöst wurde, angemeldet. Sie müssen auf dem Computer angemeldet werden auf denen die Warnung, zum Ausführen dieser Aufgabe im Alert Viewer ausgelöst wurde.|  
|Starten Sie den Computer aus, um Updates zu installieren.|Sie werden nicht die neuen und berichtigten Funktionen der Updates nutzen, bis sie angewendet werden können. Speichern Sie alle Daten, und starten Sie den Computer aus, um die Updates zu installieren.|  
|Freier Speicherplatz ist niedrig auf Festplatten.|Wenn kein Speicherplatz verfügbar gemacht wird, wird eine zusätzliche Informationen speichern nicht möglich. Um den freien Speicherplatz auf dem Computer zu erhöhen, sollten Sie die folgenden Optionen aus:<br /><br /> – Fügen Sie eine neue Festplatte hinzu.<br /><br /> -Führen Sie **Datenträgerbereinigung** um alte und temporäre Dateien zu entfernen.<br /><br /> – Verschiebt die Dateien in einen freigegebenen Ordner auf einem anderen Computer.<br /><br /> -Archiv Dateien auf Wechselmedien, z. B. einer CD, DVD oder einer externen Festplatte.|  
|Die **Dateiversionsverlauf** -Agent auf dem Server zur Ausführung auf diesem Computer nicht ordnungsgemäß konfiguriert ist.|Sicherungen von Dateiversionsverläufen können nicht erstellt werden.|  
|Ein oder mehrere Dienste nicht ausgeführt werden.||  
|Das Windows-Kennwort zu ändern.||  
|Ihre Microsoft Office 365-Kennwort ist nicht identisch mit dem Windows-Kennwort.||  
  
###  <a name="BKMK_Protect"></a>Zum Schutz Ihres Computers  
  
1.  Öffnen Sie das Sicherheitscenter.  
  
2.  Bestimmen Sie den Status des installierten Virenschutzes.  
  
3.  Führen Sie eine der folgenden Aufgaben je nach Schutzstatus:  
  
    -   Wenn sie nicht aktiviert ist, aktivieren Sie ihn.  
  
    -   Wenn es nicht auf dem neuesten Stand ist, führen Sie das Verfahren zum Aktualisieren der Signaturen.  
  
    -   Wenn kein Virenschutz installiert ist, sollten Sie ihn installieren.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
