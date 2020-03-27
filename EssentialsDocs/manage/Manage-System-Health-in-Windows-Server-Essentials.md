---
title: Verwalten der Systemintegrität in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3043f83b-389c-4f37-a1ff-85afe99314fa
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: bbe05c0564e706ef0227e723a52bd10b2f774756
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311077"
---
# <a name="manage-system-health-in-windows-server-essentials"></a>Verwalten der Systemintegrität in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
 
 In diesem Thema wird erläutert, wie Sie alle Warnungen in Ihrem Netzwerk anzeigen und sie im Dashboard behandeln können.  
  
> [!NOTE]
>  In Windows Server Essentials und Windows Server 2012 R2 mit installierter Windows Server Essentials-Rolle werden die Integritäts Warnungen für den Server und die Client Computer im Netzwerk nicht mehr in der Meldungs Anzeige angezeigt, sondern können stattdessen auf der Registerkarte Integritäts **Berichte** der **Start** Seite angezeigt werden.  
  
 Windows Server Essentials überwacht aktiv jeden Computer, der mit dem Server verbunden ist, und benachrichtigt den Administrator um Probleme im Zusammenhang mit der Systemintegrität, einschließlich kritischer Updates, fehlender Malware Schutz, veraltete Virendefinitionen auf dem Client. Computer und andere wichtige Probleme, die eine Aktion erfordern. Diese Probleme werden in der Meldungs Anzeige als Warnungen angezeigt, die über das Dashboard des Servers oder das Launchpad des Client Computers in Windows Server Essentials oder auf der Registerkarte Integritäts **Berichte** in Windows Server Essentials gestartet werden können. Standardmäßig werden die Warnungen alle 30 Minuten aktualisiert, doch Sie können die Warnungen für Ihr Netzwerk jederzeit abrufen, indem Sie in der Meldungsanzeige oder auf der Registerkarte **Integritätsberichte** auf **Aktualisieren** klicken.  
  
 In den folgenden Themen wird erläutert, was die Warnungen in der Meldungsanzeige bedeuten und wie Sie sie anzeigen und behandeln können. Außerdem finden Sie in diesen Themen Anweisungen zum Konfigurieren Ihres Servers, sodass Warnbenachrichtigungen über E-Mail eingehen:  
  
-   [Informationen zum Integritäts Bericht-Add-in](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_AddIn)  
  
-   [Anzeigen von Warnungen mithilfe der Meldungs Anzeige](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_View)  
  
-   [Organisieren von Warnungen in der Meldungs Anzeige](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Organize)  
  
-   [Reagieren auf Warnungen](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Respond)  
  
-   [Einrichten von e-Mail-Benachrichtigungen für Warnungen](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Email)  
  
-   [Potenzielle Computer Warnungen](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Potential)  
  
##  <a name="about-the-health-report-add-in"></a><a name="BKMK_AddIn"></a>Informationen zum Integritäts Bericht-Add-in  
 Das Add-In für den Integritätsbericht für Windows Server Essentials stellt Ihnen konsolidierte Informationen über das Windows Server Essentials-Netzwerk bereit und ermöglicht die Verteilung dieser Informationen an andere Personen. Diese Informationen können auf der Registerkarte **Berichte** auf dem Dashboard angezeigt werden. Auf der Registerkarte **Berichte** können Sie Folgendes durchführen:  
  
-   [Bericht bei Bedarf oder nach Zeitplan generieren](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Generate)  
  
-   [Anpassen des Inhalts des Berichts](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Customize)  
  
-   [Bericht per e-Mail senden](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_emailreport)  
  
> [!NOTE]
>  **Windows Server Essentials:** Sie können das Add-in für den Integritäts Bericht für Windows Server Essentials aus dem [Microsoft Download Center](https://go.microsoft.com/fwlink/p/?LinkId=266342)herunterladen.  
>   
>  **Windows Server Essentials:** Standardmäßig ist das Add-in für den Integritäts Bericht in Windows Server Essentials oder Windows Server 2012 R2 mit installierter Windows Server Essentials-Rolle integriert, und die Integritäts Berichte werden auf der Registerkarte Integritäts **Berichte** auf der **Start** Seite des Dashboards angezeigt.  
  
###  <a name="generate-a-report-on-demand-or-on-schedule"></a><a name="BKMK_Generate"></a>Bericht bei Bedarf oder nach Zeitplan generieren  
 Nach dem Installieren des Add-ins für den Statusbericht und dem erneuten Start des Dashboards wird eine neue Registerkarte, **Berichte**, zum Dashboard hinzugefügt. Sie können einen Statusbericht jederzeit auf Anforderung erstellen, indem Sie auf die Aufgabe **Statusbericht erstellen** auf der Registerkarte **Berichte** klicken.  
  
 Nach der Erstellung eines Statusberichts wird im Listenbereich ein neues Element erstellt, das durch das Datum und die Uhrzeit der Berichterstellung gekennzeichnet ist. Sie öffnen ein Element, indem Sie im Listenbereich darauf doppelklicken, oder Sie können es auswählen und dann im Listenbereich auf **Statusbericht öffnen** klicken. Der Bericht wird in einem neuen Fenster im HTML-Format angezeigt.  
  
 Zusätzlich zur manuellen Erstellung eines Berichts können Sie den Bericht auch nach einem Zeitplan täglich oder stündlich automatisch generieren. Klicken Sie hierzu im Aufgabenbereich auf Einstellungen für den Integritäts **Bericht anpassen**, und klicken Sie dann auf die Registerkarte **Zeitplan und e-Mail-Adresse** . Die Zeit **Plan** Funktion ist standardmäßig deaktiviert, und Sie können Sie aktivieren, indem Sie das Kontrollkästchen Integritäts **Bericht zum geplanten Zeitpunkt generieren** aktivieren.  
  
###  <a name="customize-the-content-of-the-report"></a><a name="BKMK_Customize"></a>Anpassen des Inhalts des Berichts  
 Der Integritätsbericht enthält Folgendes:  
  
- **Kritische Warnungen** Diese entsprechen den kritischen Warnungen, die in der Meldungsanzeige auf dem Dashboard angezeigt werden. Informationsmeldungen sind im Integritätsbericht nicht enthalten.  
  
- **Kritische Fehler in den Ereignisprotokollen** Anwendungen und Dienstprotokolle werde gescannt, und die in den letzten 24 Stunden protokollierten Fehler werden im Abschnitt **Details** des Berichts aufgeführt.  
  
- **Serversicherung** Die Informationen über die letzte Serversicherung werden im Abschnitt **Details** des Berichts aufgeführt.  
  
- **Nicht ausgeführte Autostartdienste** Wenn zum Zeitpunkt der Berichterstellung kein Autostartdienst ausgeführt wird, werden die Informationen zu diesem Dienst im Detailabschnitt des Berichts aufgeführt.  
  
- **Updates** Im Detailabschnitt wird der Updatestatus des Servers und aller Clientcomputer angezeigt.  
  
- **Speicher** Im Detailabschnitt wird die Liste der Treiber und ihre Kapazität aufgeführt.  
  
  Zeigen Sie im Integritätsbericht zunächst die **Zusammenfassung** an, und klicken Sie dann bei den Elementen mit einem roten Fehlersymbol oder einem gelben Warnsymbol auf den Link **Details** auf derselben Zeile, um die Details zum Element anzuzeigen.  
  
  Wenn Sie für einige der Datenpunkte, die standardmäßig im Bericht enthalten sind, nicht interessiert sind, können Sie den Inhalt des Berichts anpassen, indem Sie im Aufgabenbereich auf Einstellungen für den Integritäts **Bericht anpassen** und dann auf die Registerkarte **Inhalt** klicken. deaktivieren Sie die Kontrollkästchen für den Inhalt, der im Bericht nicht angezeigt werden soll. Wenn Sie z. b. über einen eigenen Server Sicherungs Plan verfügen und keine Warnungen zu Server Sicherungen sehen möchten, können Sie Server Sicherungen aus dem Bericht ausschließen, indem Sie das Kontrollkästchen **Server Sicherung** deaktivieren.  
  
###  <a name="email-the-report"></a><a name="BKMK_emailreport"></a>Bericht per e-Mail senden  
 Sich beim Dashboard anmelden zu müssen, um Berichte zu lesen, ist für einige Administratoren immer noch unpraktisch, vor allem wenn sie mehr als nur einen Server verwalten. Wenn die E-Mail-Funktion aktiviert ist, wird nach der Berichterstellung eine E-Mail an eine Liste von definierten E-Mail-Adressen mit dem Inhalt des Berichts gesendet. Der Administrator kann diesen Bericht von jedem Gerät oder jeder Clientanwendung aus öffnen und sicherstellen, dass der Server im bestmöglichen Zustand ausgeführt wird.  
  
 Nachdem Sie die E-Mail-Funktion aktiviert haben, ändern Sie im Dialogfeld **Einstellungen für den Integritätsbericht anpassen** die SMTP-Einstellungen, und geben Sie eine Liste der E-Mail-Empfänger an. Sie werden feststellen, dass im Aufgabenbereich eine neue Aufgabe angezeigt wird: **Integritätsbericht senden**. Weitere Informationen zu SMTP-Einstellungen finden Sie unter [Einrichtung von E-Mail-Benachrichtigungen für Warnungen](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Email).  
  
 Sie können einen vorhandenen Bericht auswählen und dann auf **Integritätsbericht senden** klicken. Sie können auch einen neuen Bericht erstellen und einstellen, dass er automatisch an Ihr Postfach gesendet wird. Wenn Sie einen Zeitplan für die automatische Berichterstellung konfiguriert haben, wird der Bericht automatisch an Ihr Postfach gesendet, nachdem er wie konfiguriert täglich (oder stündlich) erstellt wird.  
  
##  <a name="view-alerts-by-using-the-alert-viewer"></a><a name="BKMK_View"></a>Anzeigen von Warnungen mithilfe der Meldungs Anzeige  
 In diesem Abschnitt wird die Verwendung des Dashboards oder des Launchpads zum Öffnen der Meldungsanzeige erläutert, um den Integritätsstatus aller Computer auf dem Servernetzwerk anzuzeigen.  
  
#### <a name="to-open-the-alert-viewer-by-using-the-dashboard"></a>So öffnen Sie die Meldungsanzeige über das Dashboard  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie im Navigationsbereich auf die angezeigten Warnsymbole (Kritisch, Warnung oder Information). Daraufhin wird die Meldungsanzeige geöffnet.  
  
#### <a name="to-open-the-alert-viewer-from-the-launchpad"></a>So öffnen Sie die Meldungsanzeige vom Launchpad aus  
  
1.  Öffnen Sie das Launchpad auf einem mit dem Server verbundenen Computer. Melden Sie sich, wenn Sie dazu aufgefordert werden, mit Ihrem Benutzernamen und Kennwort beim Launchpad an.  
  
2.  Klicken Sie auf eines der angezeigten Warnsymbole (Kritisch, Warnung oder Information) unten im Launchpad, um die Meldungsanzeige zu öffnen, und befolgen Sie dann die Anweisungen im Detailbereich der Meldungsanzeige, um die Warnung zu beheben.  
  
##  <a name="organize-alerts-in-the-alert-viewer"></a><a name="BKMK_Organize"></a>Organisieren von Warnungen in der Meldungs Anzeige  
 Sie können Warnungen in der Meldungsanzeige organisieren, sodass sie nach Schweregrad (Kritisch, Warnung oder Information) oder nach Computernamen angezeigt werden.  
  
#### <a name="to-organize-alerts-in-the-alert-viewer"></a>Organisation von Warnungen in der Meldungsanzeige  
  
1.  Öffnen Sie das Dashboard.  
  
2.  Klicken Sie im Navigationsbereich auf eines der angezeigten Warnsymbole (Kritisch, Warnung oder Information). Daraufhin wird die Meldungsanzeige geöffnet.  
  
3.  Erweitern Sie die Dropdownliste **Organisieren**, und führen Sie eine der folgenden Aktionen durch:  
  
    1.  Wählen Sie **Nach Computer filtern** aus, und klicken Sie auf den Computernamen, für den Sie die Warnungen anzeigen möchten. Dadurch werden in der Meldungsanzeige nur die Warnungen für den ausgewählten Computer angezeigt.  
  
    2.  Wählen Sie **Nach Warnungstyp filtern** aus, und klicken Sie auf den Warnungstyp (Kritisch, Warnung oder Information), für den Sie die Warnungen anzeigen möchten. Dadurch werden in der Meldungsanzeige nur die ausgewählten Warnungstypen angezeigt.  
  
##  <a name="respond-to-alerts"></a><a name="BKMK_Respond"></a>Reagieren auf Warnungen  
 Wenn eine Warnung vorliegt, können Sie wie folgt vorgehen:  
  
-   [Auflösen einer Warnung](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Resolve)  
  
-   [Warnung ignorieren](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [Aktivieren einer Warnung](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [Löschen einer Warnung](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_4)  
  
###  <a name="resolve-an-alert"></a><a name="BKMK_Resolve"></a>Auflösen einer Warnung  
 Befolgen Sie die Anweisungen in der Meldungsanzeige, um die Warnung zu beheben. Nach ihrer Behebung wird eine Warnung so lange in der Meldungsanzeige angezeigt, bis sie aktualisiert wird.  
  
###  <a name="ignore-an-alert"></a><a name="BKMK_3"></a>Warnung ignorieren  
 Sie haben die Möglichkeit, eine Warnung zu ignorieren und später darauf zu reagieren. Wenn Sie eine Warnung ignorieren, wird sie weiterhin in der Meldungsanzeige angezeigt, doch sie wird deaktiviert und abgeblendet. Eine ignorierte Warnung wird in die Gesamtbewertung der Computerintegrität nicht einbezogen. Um eine ignorierte Warnung zu behandeln, müssen Sie sie zuerst aktivieren.  
  
##### <a name="to-ignore-an-alert"></a>So ignorieren Sie eine Warnung  
  
1. Öffnen Sie das Launchpad auf einem mit dem Windows Server Essentials-Server verbundenen Computer.  
  
2. Klicken Sie auf dem Launchpad auf eines der angezeigten Warnsymbole (Kritisch, Warnung oder Information). Daraufhin wird die Meldungsanzeige geöffnet.  
  
3. Wählen Sie in der Meldungsanzeige die zu ignorierende Warnung aus, und klicken Sie im Abschnitt **Aufgaben** auf **Warnung ignorieren**.  
  
   Um eine deaktivierte Warnung zu behandeln, müssen Sie sie zuerst aktivieren.  
  
###  <a name="enable-an-alert"></a><a name="BKMK_5"></a>Aktivieren einer Warnung  
 Sie können eine Warnung, die Sie zuvor ignoriert haben, aktivieren. Nachdem die Warnung aktiviert ist, können Sie sie beheben oder ggf. löschen. Eine Warnung wird als deaktiviert angezeigt, wenn sie ignoriert und entsprechend gekennzeichnet wurde. Wenn Sie eine zuvor deaktivierte Warnung aktivieren, wird sie wieder in die Gesamtbewertung der Computerintegrität einbezogen.  
  
##### <a name="to-enable-an-alert"></a>So aktivieren Sie eine Benachrichtigung  
  
1.  Öffnen Sie das Launchpad auf einem mit dem Server verbundenen Computer.  
  
2.  Klicken Sie auf dem Launchpad auf eines der angezeigten Warnsymbole (Kritisch, Warnung oder Information), um die Meldungsanzeige zu öffnen.  
  
3.  Klicken Sie in der Meldungsanzeige mit der rechten Maustaste auf die Warnung, die Sie aktivieren möchten, und klicken Sie dann auf **Warnung aktivieren**.  
  
###  <a name="delete-an-alert"></a><a name="BKMK_4"></a>Löschen einer Warnung  
 Sie können eine Warnung löschen, wenn sie nicht behoben oder ignoriert werden soll. Verwenden Sie die Meldungsanzeige auf dem Launchpad, um Warnungen zu löschen, die für Ihren Computer erstellt wurden. Wenn Sie eine Warnung löschen und der Server das Problem im nächsten Evaluierungszyklus für die Netzwerkintegrität erneut erkennt, erstellt er eine neue Warnung.  
  
##### <a name="to-delete-an-alert"></a>So löschen Sie eine Warnung  
  
1.  Öffnen Sie das Launchpad auf einem mit dem Server verbundenen Computer.  
  
2.  Klicken Sie auf dem Launchpad auf eines der angezeigten Warnsymbole (Kritisch, Warnung oder Information), um die Meldungsanzeige zu öffnen.  
  
3.  Klicken Sie in der Meldungsanzeige mit der rechten Maustaste auf die Warnung, die Sie löschen möchten, und klicken Sie dann auf **Warnung löschen**.  
  
##  <a name="set-up-email-notifications-for-alerts"></a><a name="BKMK_Email"></a>Einrichten von e-Mail-Benachrichtigungen für Warnungen  
 Sie können Ihren Server so konfigurieren, dass Sie über E-Mail über das Auftreten von Warnungen benachrichtigt werden. Die E-Mail-Benachrichtigungen für diese Warnungen enthalten Informationen zu Netzwerkproblemen und die Schritte zu ihrer Behebung, die mit den in der Meldungsanzeige aufgeführten Informationen identisch sind. Einige der Bewertungen der Netzwerkintegrität erfolgen programmgesteuert.  
  
 Wenn Sie Ihren Server konfigurieren, sodass Benachrichtigungen über E-Mail gesendet werden, wird eine E-Mail-Benachrichtigung für Warnungen gesendet, die bei einer Bewertung der Netzwerkintegrität auftreten. Es werden jedoch nicht alle Warnungen, die in der Meldungsanzeige protokolliert werden, in E-Mails protokolliert.  
  
 Alle 30 Minuten wird auf dem Server eine Aufgabe zur Bewertung von Warnungs-E-Mails ausgeführt, bei der das Netzwerk auf Warnungen überprüft wird. Eine E-Mail-Benachrichtigung wird gesendet, wenn eine Warnung auftritt, die für E-Mail-Benachrichtigungen konfiguriert wurde. Eine zweite E-Mail wird nicht gesendet, wenn die Warnung im nächsten Bewertungszyklus noch aktiv ist. So wird eine Überflutung Ihres Postfach verhindert. Wenn eine Warnung jedoch in einem künftigen Bewertungszyklus erkannt wird, enthält die daraufhin gesendete E-Mail-Benachrichtigung sowohl die neuen als auch die vorherigen Warnungen.  
  
###  <a name="alerts-that-result-in-email-notifications"></a><a name="BKMK_list"></a>Warnungen, die zu e-Mail-Benachrichtigungen führen  
 Die folgenden Warnungen in der Meldungsanzeige führen zu E-Mail-Benachrichtigungen, wenn Sie Ihren Server für das Senden von E-Mail-Benachrichtigungen für Warnungen einrichten:  
  
-   Fehler sind in einer Clientcomputersicherung vorhanden.  
  
-   Der Server wurde neu gestartet.  
  
-   Mindestens ein Dienst wird nicht ausgeführt.  
  
-   Der Windows Server-Speicherdienst wird nicht ausgeführt.  
  
-   Der Evaluierungszeitraum ist abgelaufen.  
  
-   Jetzt aktivieren.  
  
-   Quellserver wird heruntergefahren.  
  
-   BPA-Scanergebnisse enthalten Fehler.  
  
-   BPA-Scanergebnisse enthalten Warnungen.  
  
-   Ein Zertifikat ist für Zugriff überall nicht verfügbar.  
  
-   Das Zertifikat für Zugriff überall ist abgelaufen.  
  
-   Der Router ist nicht ordnungsgemäß konfiguriert.  
  
-   Der Webserver ist nicht ordnungsgemäß konfiguriert.  
  
-   Remotedesktopdienste sind nicht ordnungsgemäß konfiguriert.  
  
-   Die Firewall ist nicht ordnungsgemäß konfiguriert.  
  
-   Der Internetdomänenname ist abgelaufen.  
  
-   Der Internetdomänenname kann nicht aktualisiert werden.  
  
-   Lizenzfehler: Überprüfung der Gesamtstruktur-Vertrauensstellung.  
  
-   Lizenzfehler: Domänencontrollerüberprüfung.  
  
-   Lizenzfehler: FSMO-Rollenüberprüfung.  
  
-   Lizenzfehler: FSMO-Erzwingungsrichtlinien.  
  
-   Lizenzfehler: Erzwingungslast-Richtlinien.  
  
-   Lizenzfehler: Active Directory-Domänendienste.  
  
-   Ihr Office 365-Abonnement ist abgelaufen.  
  
-   Office 365-Authentifizierung fehlgeschlagen.  
  
-   Die Kennwortrichtlinie ist falsch.  
  
-   Der Dienst für die Kennwortsynchronisierung kann ein Benutzerkennwort mit Office 365 nicht synchronisieren.  
  
-   Eigenes Windows-Kennwort ändern.  
  
-   Ihr Office 365-Kennwort ist mit Ihrem Windows-Kennwort nicht identisch.  
  
-   Es kann keine Verbindung mit dem Exchange-Server hergestellt werden.  
  
-   Problem mit dem Microsoft Exchange Server.  
  
-   Mindestens eine Festplatte in der Serversicherung ist nicht verbunden.  
  
-   Die Sicherungsfestplatte weist nicht genügend freien Speicherplatz für die Serversicherung auf.  
  
-   Fehler bei der Serversicherung, weil keine Momentaufnahme des Laufwerks erstellt werden konnte.  
  
-   Eine geplante Sicherung wurde nicht erfolgreich abgeschlossen.  
  
-   Mindestens ein vordefinierter Serverordner fehlt.  
  
-   Wenig freier Speicherplatz auf mindestens einer Serverfestplatte.  
  
-   VSS Writer für den Speicherdienst wird nicht ausgeführt.  
  
-   Festplatten weisen eine geringe Speicherkapazität auf.  
  
-   Mindestens ein Laufwerk funktioniert nicht und ist offline.  
  
###  <a name="configuring-smtp-on-your-server-to-send-alert-notifications-by-email-in-windows-server-essentials"></a><a name="BKMK_SMTP"></a>Konfigurieren von SMTP auf Ihrem Server zum Senden von Warn Benachrichtigungen per e-Mail in Windows Server Essentials  
 In diesem Abschnitt wird erläutert, wie Sie Ihren Server konfigurieren, sodass bei Warnungen E-Mail-Benachrichtigungen gesendet werden.  
  
> [!NOTE]
>  Sie können das Add-in für den Integritäts Bericht für Windows Server Essentials aus dem [Microsoft Download Center](https://go.microsoft.com/fwlink/p/?LinkId=266342)herunterladen.  
  
##### <a name="to-set-up-email-notification-for-alerts"></a>Einrichtung von E-Mail-Benachrichtigungen für Warnungen  
  
1.  Öffnen Sie auf dem **Dashboard** die **Meldungsanzeige**.  
  
2.  Klicken Sie in der **Meldungsanzeige** auf **Warnungsbenachrichtigung per E-Mail einrichten**.  
  
3.  Klicken Sie im Fenster **E-Mail-Benachrichtigungen für Warnungen einrichten** auf **Aktivieren**.  
  
4.  Gehen Sie im Fenster **SMTP-Einstellungen** folgendermaßen vor:  
  
    1.  Geben Sie als **Absender-E-Mail-Adresse** die E-Mail-Adresse ein, die Sie für das Senden von E-Mail-Benachrichtigungen verwenden möchten. Diese e-Mail-Adresse wird in der Warn Benachrichtigung als Adresse des Absenders angezeigt.  
  
    2.  Geben Sie im Textfeld für die **Absender-E-Mail-Adresse** unter **SMTP-Servername** den Namen des SMTP-Servers ein, den Sie in Schritt 4a angegeben haben. (In Tabelle 1 finden Sie einige der SMTP-Servernamen.)  
  
    3.  Geben Sie unter **SMTP-Port** die Portnummer ein, die vom SMTP-Server zum Senden und Empfangen von E-Mail verwendet wird. (In Tabelle 1 finden Sie die Portnummern, die von einigen SMTP-Servern verwendet werden.)  
  
    4.  Wählen Sie **Dieser Server erfordert eine sichere Verbindung (SSL)** aus, falls der SMTP-Server SSL verwendet (siehe Tabelle 1).  
  
    5.  Wählen Sie **Server erfordert Authentifizierung** aus, falls der SMTP-Server einen Benutzernamen und Kennwortinformationen erfordert (siehe Tabelle 1). Wenn Sie dieses Kontrollkästchen aktivieren, geben Sie den Benutzernamen und das Kennwort für die E-Mail-Adresse ein, die Sie im Feld **Absender-E-Mail-Adresse** in Schritt 4a angegeben haben, und klicken Sie auf **OK**.  
  
    > [!NOTE]
    >  Sie erhalten die Informationen zum SMTP-Servernamen, zur Portnummer und SSL-Verwendung bei Ihrem Internetanbieter.  
  
     **Tabelle 1** Beispiele für SMTP-Servernamen, Authentifizierungs- und SSL-Verschlüsselungsanforderungen sowie Portnummern  
  
    |SMTP-Server|SSL erforderlich|Authentifizierung erforderlich|Portnummer|Kontoname/Anmeldename|  
    |-----------------|------------------|-----------------------------|-----------------|------------------------------|  
    |smtp.gmail.com|Ja|Ja|587|Geben Sie die vollständige E-Mail-Adresse mit dem Domänennamen und Kennwort für die Authentifizierung an.|  
    |smtp.live.com|Ja|Ja|587|Geben Sie die vollständige E-Mail-Adresse mit dem Domänennamen und Kennwort für die Authentifizierung an.|  
    |smtp.comcast.net|Ja|Nein|587|Geben Sie die vollständige E-Mail-Adresse mit dem Domänennamen und Kennwort für die Authentifizierung an.|  
    |smtp.mail.yahoo.com|Nein|Ja|25|Geben Sie nur die E-Mail-Adresse ohne einen Domänennamen für den Anmeldenamen an.|  
  
5.  Geben Sie unter **E-Mail-Benachrichtigungen für Warnungen einrichten** für die **E-Mail-Empfänger** die E-Mail-Adressen der Personen an, die Warnbenachrichtigungen über E-Mail erhalten sollen. Stellen Sie sicher, dass die E-Mail-Adressen durch ein Semikolon (;) getrennt sind.  
  
6.  Um sicherzustellen, dass Sie den SMTP-Server für das Senden von E-Mail-Benachrichtigungen für Warnungen richtig konfiguriert haben, klicken Sie auf **Anwenden und E-Mail senden**.  
  
    > [!NOTE]
    >  Beim Klicken auf **Anwenden und E-Mails enden**, erhalten Sie in der Regel eine Beispiel-E-Mail-Benachrichtigung ohne aufgelistete Status-Warnungen. Wenn bei diesem Testvorgang jedoch eine Integritätswarnung auftritt, für die eine E-Mail-Benachrichtigung konfiguriert wurde, wird diese Warnung in der Test-E-Mail aufgeführt.  
  
### <a name="configuring-smtp-on-your-server-to-send-health-reports-in-windows-server-essentials"></a>Konfigurieren von SMTP auf Ihrem Server zum Senden von Integritäts Berichten in Windows Server Essentials  
 In diesem Abschnitt wird erläutert, wie Sie die SMTP-Einstellungen für Ihren Server konfigurieren, sodass Sie Integritätsberichte über E-Mail erhalten.  
  
> [!NOTE]
>  Standardmäßig ist das Add-in für den Integritäts Bericht in Windows Server Essentials oder Windows Server 2012 R2 mit installierter Windows Server Essentials-Rolle integriert, und die Integritäts Berichte werden auf der Registerkarte Integritäts **Berichte** auf der **Start** Seite des Dashboards angezeigt.  
  
##### <a name="to-set-up-email-notification-for-health-reports"></a>So richten Sie E-Mail-Benachrichtigungen für Integritätsberichte ein  
  
1.  Klicken Sie im **Dashboard** auf die Registerkarte **Berichte**.  
  
2.  Klicken Sie im Aufgabenbereich für **Integritäsberichtaufgaben** auf **Einstellungen für Integritätsbericht anpassen**.  
  
3.  Klicken Sie im Fenster **Einstellungen für Integritätsbericht anpassen** auf die Registerkarte **Planen und senden**.  
  
4.  Gehen Sie auf der Registerkarte **Planen und senden** im Bereich **E-Mail** wie folgt vor:  
  
    1.  Klicken Sie auf **Aktivieren**, und geben Sie die E-Mail-Adresse ein, die Sie zum Versenden von Integritätsberichten verwenden möchten. Diese e-Mail-Adresse wird in den per e-Mail gesendeten Integritäts Berichten als Adresse des Absenders angezeigt.  
  
        1.  Geben Sie unter **Name des SMTP-Servers** den Namen des SMTP-Servers ein. (In Tabelle 1 finden Sie einige der SMTP-Servernamen.)  
  
        2.  Geben Sie unter **SMTP-Port** die Portnummer ein, die vom SMTP-Server zum Senden und Empfangen von E-Mail verwendet wird. (In Tabelle 1 finden Sie die Portnummern, die von einigen SMTP-Servern verwendet werden.)  
  
        3.  Wählen Sie **Dieser Server erfordert eine sichere Verbindung (SSL)** aus, falls der SMTP-Server SSL verwendet (siehe Tabelle 1).  
  
        4.  Wählen Sie **Server erfordert Authentifizierung** aus, falls der SMTP-Server einen Benutzernamen und Kennwortinformationen erfordert (siehe Tabelle 1). Wenn Sie dieses Kontrollkästchen aktivieren, geben Sie den Benutzernamen und das Kennwort für die E-Mail-Adresse ein, die Sie im Feld **Absender-E-Mail-Adresse** in Schritt 4a angegeben haben, und klicken Sie auf **OK**.  
  
            > [!NOTE]
            >  Sie erhalten die Informationen zum SMTP-Servernamen, zur Portnummer und SSL-Verwendung bei Ihrem Internetanbieter.  
  
            > [!NOTE]
            >  Microsoft empfiehlt ausdrücklich die Verwendung von SSL, da der Bericht mehrere Serverstatus enthalten kann, die von böswilligen Parteien zum Aufdecken von Sicherheitsrisiken verwendet werden können (zum Beispiel fehlende Windows-Udpates). Beim Aktivieren von SSL werden die Daten während der Übertragung verschlüsselt, und das Risiko, dass Sicherheitslücken beim Server erkannt werden, wird verringert.  
  
5.  Nachdem Sie das Senden per E-Mail aktiviert haben, wird der Link **SMTP-Einstellungen ändern** angezeigt. Außerdem wird die neue Aufgabe **Integritätsbericht senden** unter den **Integritätsberichtsaufgaben** angezeigt.  
  
     **Tabelle 1** Beispiele für SMTP-Servernamen, Authentifizierungs- und SSL-Verschlüsselungsanforderungen sowie Portnummern  
  
    |SMTP-Server|SSL erforderlich|Authentifizierung erforderlich|Portnummer|Kontoname/Anmeldename|  
    |-----------------|------------------|-----------------------------|-----------------|------------------------------|  
    |smtp.gmail.com|Ja|Ja|587|Geben Sie die vollständige E-Mail-Adresse mit dem Domänennamen und Kennwort für die Authentifizierung an.|  
    |smtp.live.com|Ja|Ja|587|Geben Sie die vollständige E-Mail-Adresse mit dem Domänennamen und Kennwort für die Authentifizierung an.|  
    |smtp.comcast.net|Ja|Nein|587|Geben Sie die vollständige E-Mail-Adresse mit dem Domänennamen und Kennwort für die Authentifizierung an.|  
    |smtp.mail.yahoo.com|Nein|Ja|25|Geben Sie nur die E-Mail-Adresse ohne einen Domänennamen für den Anmeldenamen an.|  
  
6.  Geben Sie unter **Einstellungen für Integritätsbericht anpassen** für **Den Integritätsbericht an die folgenden E-Mail-Empfänger senden** die E-Mail-Adressen der Personen ein, die die Integritätsberichte per E-Mail erhalten sollen. Stellen Sie sicher, dass die E-Mail-Adressen durch ein Semikolon (;) getrennt sind.  
  
7.  Um zu überprüfen, dass Sie die SMTP-Servereinstellungen zum Senden von Integritätsberichten per E-Mail richtig konfiguriert haben, wählen Sie auf der Registerkarte für Integritätsberichte im Dashboard einen Bericht aus, und klicken Sie im Aufgabenfenster auf **Integritätsbericht senden**.  
  
##  <a name="potential-computer-alerts"></a><a name="BKMK_Potential"></a>Potenzielle Computer Warnungen  
 In diesem Abschnitt werden Warnungen sowie die Verwaltung von Warnungen erläutert, die sich speziell auf den mit dem Server verbundenen Computer beziehen, und die im Launchpad des Computers angezeigt werden.  
  
 Die folgende Tabelle enthält einige der Computerwarnungen, die generiert und in der Meldungsanzeige angezeigt werden können, wenn sie sich auf Ihren Computer beziehen.  
  
|Titel der Warnung|Auswirkung der Warnung und Lösung|  
|-----------------|---------------------------------|  
|Der aktuelle Status der Netzwerkfirewall bietet nur einen geringen Schutz für diesen Computer.|Unbefugte Personen oder Softwareprogramme können möglicherweise auf diesen Computer zugreifen, wenn die Windows-Firewall nicht aktiviert ist.|  
|Virenschutz ist deaktiviert, nicht installiert oder nicht auf dem neuesten Stand.|Die Daten auf Ihrem Computer sind gefährdet, wenn die **Virenschutz**-Sicherheitseinstellung deaktiviert oder nicht aktualisiert ist. [To protect your computer](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Protect): Führen Sie die angegebenen Schritte aus.|  
|Der Schutz gegen Spyware und unerwünschte Software ist deaktiviert, nicht installiert oder nicht auf dem neuesten Stand.|Die Daten auf Ihrem Computer sind gefährdet, wenn der **Schutz vor Spyware und unerwünschter Software** deaktiviert oder nicht aktualisiert ist. [To protect your computer](Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Protect): Führen Sie die angegebenen Schritte aus.|  
|Windows Update ist deaktiviert.|Sie können die in den Updates enthaltenen neuen und berichtigten Funktionen nur dann nutzen, wenn Windows Update aktiviert ist. Um Windows Update zu aktivieren, klicken Sie in der Meldungsanzeige auf **Windows Update öffnen**.<br /><br /> Wenn die Aufgabe **Windows Update öffnen** nicht angezeigt wird, sind Sie nicht bei dem Computer angemeldet, auf dem die Warnung ausgegeben wurde. Sie müssen auf dem Computer angemeldet sein, auf dem die Warnung ausgegeben wurde, um diese Aufgabe in der Meldungsanzeige ausführen zu können.|  
|Wichtige Updates sollten installiert werden.|Sie können die in den Updates enthaltenen neuen und berichtigten Funktionen nur dann nutzen, wenn Windows Update aktiviert ist. Um Windows Update zu aktivieren, klicken Sie in der Meldungsanzeige auf **Windows Update öffnen**.<br /><br /> Wenn die Aufgabe **Windows Update öffnen** nicht angezeigt wird, sind Sie nicht bei dem Computer angemeldet, auf dem die Warnung ausgegeben wurde. Sie müssen auf dem Computer angemeldet sein, auf dem die Warnung ausgegeben wurde, um diese Aufgabe in der Meldungsanzeige ausführen zu können.|  
|Führen Sie einen Neustart des Computers durch, um Updates zu installieren.|Sie können erst dann die in den Updates enthaltenen neuen und berichtigten Funktionen nutzen, nachdem die Updates installiert wurden. Speichern Sie alle Daten, und starten Sie den Computer, um die Updates zu installieren.|  
|Der freie Speicherplatz auf den Festplatten ist gering.|Wenn kein Speicherplatz verfügbar gemacht wird, können Sie keine zusätzlichen Informationen speichern. Um den freien Speicherplatz auf dem Computer zu erhöhen, ziehen Sie die folgenden Möglichkeiten in Betracht:<br /><br /> -Hinzufügen einer neuen Festplatte.<br /><br /> -Führen Sie die Datenträger **Bereinigung** aus, um alte und temporäre Dateien zu entfernen.<br /><br /> -Verschieben Sie die Dateien in einen freigegebenen Ordner auf einem anderen Computer.<br /><br /> -Archivdateien auf Wechselmedien, z. b. eine CD, DVD oder eine externe Festplatte.|  
|Der **Dateiversionsverlauf**-Agent auf dem Server ist für die Ausführung auf diesem Computer nicht ordnungsgemäß konfiguriert.|Dateiversionsverlauf-Sicherungen können nicht erstellt werden.|  
|Mindestens ein Dienst wird nicht ausgeführt.||  
|Eigenes Windows-Kennwort ändern.||  
|Ihr Office 365-Kennwort ist mit Ihrem Windows-Kennwort nicht identisch.||  
  
###  <a name="to-protect-your-computer"></a><a name="BKMK_Protect"></a>So schützen Sie Ihren Computer  
  
1.  Öffnen Sie das Sicherheitscenter.  
  
2.  Bestimmen Sie den Status des installierten Virenschutzes.  
  
3.  Führen Sie eine der folgenden Aufgaben durch, je nach Schutzstatus:  
  
    -   Wenn der Virenschutz nicht aktiviert ist, aktivieren Sie ihn.  
  
    -   Wenn der Virenschutz nicht auf dem neuesten Stand ist, führen Sie den Aktualisierungsprozess für die Signaturen durch.  
  
    -   Wenn kein Virenschutz installiert ist, sollten Sie ihn installieren.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Verwenden von Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)  
  
-   [Verwalten von Windows Server Essentials](Manage-Windows-Server-Essentials.md)
