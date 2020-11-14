---
title: Server-Manager
description: Erfahren Sie mehr über die Verwaltungskonsole in Windows Server, mit der IT-Experten lokale Windows-basierte Server und Remote Server von ihren Desktops aus bereitstellen und verwalten können, ohne dass Sie physischen Zugriff auf die Server benötigen oder RDP (Remotedesktop Protocol)-Verbindungen zu den einzelnen Servern benötigen.
ms.topic: conceptual
ms.assetid: d996ef40-8bcc-42b0-b6ae-806b828223f6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7c645698614f78520ed3540e154669a72e659bc1
ms.sourcegitcommit: de207e887575757f3389ccf940c2e0ad2dc70bd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2020
ms.locfileid: "94617210"
---
# <a name="server-manager"></a>Server-Manager

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Server-Manager ist eine Verwaltungskonsole in Windows Server, mit der IT-Experten lokale Windows-basierte Server und Remote Server von ihren Desktops aus bereitstellen und verwalten können, ohne dass Sie physischen Zugriff auf die Server benötigen oder RDP-Verbindungen (Remotedesktop Protocol) zu jedem Server aktivieren müssen. Obwohl Server-Manager in Windows Server 2008 R2 und Windows Server 2008 verfügbar ist, wurde Server-Manager in Windows Server 2012 aktualisiert, um die Remote Verwaltung mehrerer Server zu unterstützen und die Anzahl der Server zu erhöhen, die ein Administrator verwalten kann.

In unseren Tests können Server-Manager in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 verwendet werden, um bis zu 100 Server zu verwalten, abhängig von den Workloads, die auf den Servern ausgeführt werden. Die Anzahl der Server, die Sie mithilfe einer einzigen Server-Manager Konsole verwalten können, kann je nach der von den verwalteten Servern angeforderten Datenmenge und den Hardware-und Netzwerkressourcen, die für den Computer mit Server-Manager verfügbar sind, variieren. Wenn die anzuzeigende Datenmenge die Ressourcenkapazität des Computers erreicht, kann es zu langsamen Antworten von Server-Manager und Verzögerungen bei der Beendigung von Aktualisierungen kommen. Um die Anzahl der Server zu erhöhen, die Sie mithilfe von Server-Manager verwalten können, empfiehlt es sich, die Ereignisdaten, die von den verwalteten Servern abgerufen Server-Manager, mithilfe von Einstellungen im Dialogfeld **Ereignisdaten konfigurieren** einzuschränken. Sie können das Dialogfeld über das Menü **Aufgaben** in der Kachel **Ereignisse** öffnen. Wenn Sie eine unternehmensweite Anzahl von Servern in Ihrer Organisation verwalten müssen, empfiehlt es sich, die Produkte in der [Microsoft System Center-Suite](https://go.microsoft.com/fwlink/p/?LinkId=239437)zu evaluieren.

Dieses Thema und seine Unterthemen enthalten Informationen zur Verwendung von Funktionen in der Server-Manager-Konsole. Dieses Thema enthält folgende Abschnitte:

- [Vorüberlegungen und Systemanforderungen](#review-initial-considerations-and-system-requirements)

- [Im Server-Manager ausführbare Aufgaben](#tasks-that-you-can-perform-in-server-manager)

- [Start Server-Manager](#start-server-manager)

- [Neustarten von Remoteservern](#restart-remote-servers)

- [Exportieren von Server-Manager-Einstellungen auf andere Computer](#export-server-manager-settings-to-other-computers)

## <a name="review-initial-considerations-and-system-requirements"></a>Vorüberlegungen und Systemanforderungen

In den folgenden Abschnitten finden Sie einige Überlegungen, die Sie überprüfen müssen, sowie Hardware-und Softwareanforderungen für Server-Manager.

### <a name="hardware-requirements"></a>Hardwareanforderungen

Server-Manager wird standardmäßig mit allen Editionen von Windows Server 2016 installiert. Für Server-Manager sind keine zusätzlichen Hardwareanforderungen vorhanden.

### <a name="software-and-configuration-requirements"></a>Software- und Konfigurationsanforderungen

Server-Manager wird standardmäßig mit allen Editionen von Windows Server 2016 installiert. Sie können Server-Manager in Windows Server 2016 verwenden, um die [Server Core-Installationsoptionen](https://go.microsoft.com/fwlink/p/?LinkID=241573) von Windows Server 2016, Windows Server 2012 und Windows Server 2008 R2, die auf Remote Computern ausgeführt werden, zu verwalten. Server-Manager wird unter der Server Core-Installationsoption von Windows Server 2016 ausgeführt.

Server-Manager in der grafischen Benutzeroberfläche mit minimalem Server ausgeführt werden. Das heißt, wenn das Feature für die servergrafikshell nicht installiert ist. Das Feature "grafische Shell für Server" wird auf Windows Server 2016 standardmäßig nicht installiert. Wenn Sie die servergrafikshell nicht ausführen, wird die Server-Manager Konsole ausgeführt, aber einige Anwendungen oder Tools, die über die-Konsole verfügbar sind, sind nicht verfügbar. Internet Browser können nicht ohne servergrafikshell ausgeführt werden, sodass Webseiten und Anwendungen wie die HTML-Hilfe (z. b. die MMC-F1-Hilfe) nicht geöffnet werden können. Sie können keine Dialogfelder zum Konfigurieren von automatischen Windows-Updates und Feedback öffnen, wenn die servergrafikshell nicht installiert ist. Befehle, die diese Dialogfelder in der Server-Manager Konsole öffnen, werden umgeleitet, um " **SCONFIG. cmd** " auszuführen.

Zum Verwalten von Servern, auf denen Windows Server-Versionen älter als Windows Server 2016 ausgeführt werden, installieren Sie die folgende Software und Updates, um die älteren Versionen von Windows Server mithilfe von Server-Manager in Windows Server 2016 verwaltbar zu machen.

|Betriebssystem|Erforderliche Software|
|----------|-----------|
| Windows Server 2012 R2 oder Windows Server 2012 |-   [.NET Framework 4,6](https://www.microsoft.com/download/details.aspx?id=45497)<br />-   [Windows Management Framework 5,0](https://go.microsoft.com/fwlink/?LinkID=395058). Das Windows Management Framework 5,0-Downloadpaket aktualisiert Windows-Verwaltungsinstrumentation (WMI)-Anbieter unter Windows Server 2012 R2 und Windows Server 2012. Mit den aktualisierten WMI-Anbietern können Server-Manager Informationen zu den auf den verwalteten Servern installierten Rollen und Features sammeln. Bis zum Anwenden des Updates haben Server, auf denen Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird, den verwaltbarkeitsstatus **nicht zugänglich**.<br />-Das mit dem [Knowledge Base-Artikel 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) verknüpfte Leistungs Update ist auf Servern mit Windows Server 2012 R2 oder Windows Server 2012 nicht mehr erforderlich.|
| Windows Server 2008 R2 |-   [.NET Framework 4,5](https://www.microsoft.com/download/details.aspx?id=30653)<br />-   [Windows Management Framework 4,0](https://go.microsoft.com/fwlink/?LinkId=293881). Das Windows Management Framework 4,0-Downloadpaket aktualisiert Windows-Verwaltungsinstrumentation (WMI)-Anbieter unter Windows Server 2008 R2. Mit den aktualisierten WMI-Anbietern können Server-Manager Informationen zu den auf den verwalteten Servern installierten Rollen und Features sammeln. Bis zum Anwenden des Updates haben Server, auf denen Windows Server 2008 R2 ausgeführt wird, den verwaltbarkeitsstatus **nicht zugänglich**.<br />-Das mit dem [Knowledge Base-Artikel 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) verknüpfte Leistungs Update ermöglicht Server-Manager die Erfassung von Leistungsdaten von Windows Server 2008 R2.|
| Windows Server 2008 |-   [.NET Framework 4](https://www.microsoft.com/download/en/details.aspx?id=17718)<br />-   [Windows Management Framework 3,0](https://go.microsoft.com/fwlink/p/?LinkID=229019) Das Windows Management Framework 3,0-Downloadpaket aktualisiert Windows-Verwaltungsinstrumentation (WMI)-Anbieter unter Windows Server 2008. Mit den aktualisierten WMI-Anbietern können Server-Manager Informationen zu den auf den verwalteten Servern installierten Rollen und Features sammeln. Bis zum Anwenden des Updates haben Server, auf denen Windows Server 2008 ausgeführt wird, den verwaltbarkeitsstatus **nicht verfügbar: Überprüfen Sie, ob frühere Versionen Windows Management Framework 3,0 ausführen**.<br />-Das mit dem [Knowledge Base-Artikel 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) verknüpfte Leistungs Update ermöglicht Server-Manager die Erfassung von Leistungsdaten von Windows Server 2008.|

#### <a name="manage-remote-computers-from-a-client-computer"></a>Verwalten von Remotecomputern über einen Clientcomputer

Die Server-Manager Konsole ist in [Remoteserver-Verwaltungstools](https://go.microsoft.com/fwlink/?LinkID=404281) für Windows 10 enthalten. Beachten Sie Folgendes: Wenn Remoteserver-Verwaltungstools auf einem Client Computer installiert ist, können Sie den lokalen Computer nicht mithilfe von Server-Manager verwalten. Server-Manager können nicht zum Verwalten von Computern oder Geräten verwendet werden, auf denen ein Windows-Client Betriebssystem ausgeführt wird. Sie können Server-Manager nur zum Verwalten von Windows-basierten Servern verwenden.

| Server-Manager Quell Betriebssystem | Ziel auf Windows Server 2016 | Ziel Windows Server 2012 R2 | Ziel auf Windows Server 2012 | Ziel Windows Server 2008 R2 oder Windows Server 2008 | Für Windows Server 2003 | Ziel für Windows 10 Enterprise-Multisitzung auf Windows Virtual Desktop (WVD) |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| Windows 10 oder Windows Server 2016 | Vollständige Unterstützung | Vollständige Unterstützung | Vollständige Unterstützung | Sobald die [Software- und Konfigurationsoptionen](#software-and-configuration-requirements) erfüllt sind, können die meisten Verwaltungsaufgaben, jedoch keine Installation oder Deinstallation von Rollen oder Features durchgeführt werden | Nicht unterstützt | Nicht unterstützt |
| Windows 8.1 oder Windows Server 2012 R2 | Nicht unterstützt | Vollständige Unterstützung| Vollständige Unterstützung | Sobald die [Software- und Konfigurationsoptionen](#software-and-configuration-requirements) erfüllt sind, können die meisten Verwaltungsaufgaben, jedoch keine Installation oder Deinstallation von Rollen oder Features durchgeführt werden | Eingeschränkte Unterstützung, nur Online- und Offlinestatus | Nicht unterstützt |
| Windows 8 oder Windows Server 2012 | Nicht unterstützt | Nicht unterstützt | Vollständige Unterstützung | Sobald die [Software- und Konfigurationsoptionen](#software-and-configuration-requirements) erfüllt sind, können die meisten Verwaltungsaufgaben, jedoch keine Installation oder Deinstallation von Rollen oder Features durchgeführt werden | Eingeschränkte Unterstützung, nur Online- und Offlinestatus | Nicht unterstützt |

##### <a name="to-start-server-manager-on-a-client-computer"></a>So starten Sie den Server-Manager auf einem Clientcomputer

1.  Befolgen Sie die Anweisungen in [Remoteserver-Verwaltungstools](../../remote/remote-server-administration-tools.md) , um Remoteserver-Verwaltungstools für Windows 10 zu installieren.

2.  Klicken Sie auf dem **Start** Bildschirm auf **Server-Manager**. Die **Server-Manager** -Kachel ist verfügbar, nachdem Sie die Remoteserver-Verwaltungstools installiert haben.

3.  Wenn **nach der Installation** von Remoteserver-Verwaltungstools weder die-noch die **Server-Manager** Kacheln auf dem **Start** Bildschirm angezeigt werden und nach Server-Manager auf dem **Start** Bildschirm suchen, überprüfen Sie, ob die Einstellung **Verwaltungs Tools anzeigen** aktiviert ist. Um diese Einstellung anzuzeigen, zeigen Sie mit dem Mauszeiger auf die obere rechte Ecke der **Start** Seite, und klicken Sie dann auf **Einstellungen**. Ist die Einstellung **Verwaltungstools anzeigen** deaktiviert, aktivieren Sie die Einstellung, um Tools anzuzeigen, die Sie als Teil der Remoteserver-Verwaltungstools installiert haben.

Weitere Informationen zum Ausführen von Remoteserver-Verwaltungstools für Windows 10 zur Verwaltung von Remote Servern finden Sie im TechNet wiki unter [Remoteserver-Verwaltungstools](https://go.microsoft.com/fwlink/?LinkID=221055) .

#### <a name="configure-remote-management-on-servers-that-you-want-to-manage"></a>Konfigurieren der Remoteverwaltung auf zu verwaltenden Servern

> [!IMPORTANT]
> Standardmäßig ist Server-Manager und Windows PowerShell-Remote Verwaltung in Windows Server 2016 aktiviert.

Zum Ausführen von Verwaltungsaufgaben auf Remote Servern mithilfe von Server-Manager müssen Remote Server, die Sie verwalten möchten, so konfiguriert werden, dass Sie die Remote Verwaltung mithilfe von Server-Manager und Windows PowerShell zulassen. Wenn die Remote Verwaltung unter Windows Server 2012 R2 oder Windows Server 2012 deaktiviert wurde und Sie Sie erneut aktivieren möchten, führen Sie die folgenden Schritte aus.

##### <a name="to-configure-server-manager-remote-management-on--windows-server-2012-r2--or--windows-server-2012--by-using-the-windows-interface"></a>So konfigurieren Sie Server-Manager-Remote Verwaltung unter Windows Server 2012 R2 oder Windows Server 2012 mithilfe der Windows-Benutzeroberfläche

1.  > [!NOTE]
    > Die Einstellungen, die im Dialogfeld **Remote Verwaltung konfigurieren** gesteuert werden, wirken sich nicht auf Teile von Server-Manager aus, die DCOM für die Remote Kommunikation verwenden.

    Führen Sie eine der folgenden Aktionen aus, um Server-Manager zu öffnen, wenn es nicht bereits geöffnet ist.

    -   Klicken Sie in der Windows-Taskleiste auf die Schaltfläche Server-Manager.

    -   Klicken Sie auf dem **Start** Bildschirm auf **Server-Manager**.

2.  Klicken Sie im Bereich **Eigenschaften** der Seite **lokale Server** auf den hyperverknüpften Wert für die Eigenschaft **Remote Verwaltung** .

3.  Führen Sie einen der folgenden Schritte aus, und klicken Sie anschließend auf **OK** :

    -   Deaktivieren Sie das Kontrollkästchen **Remote Verwaltung dieses Servers von anderen Computern aktivieren** , um zu verhindern, dass dieser Computer mithilfe Server-Manager (oder mithilfe von Windows PowerShell bei der Installation) Remote verwaltet wird.

    -   Um die Remote Verwaltung dieses Computers mithilfe von Server-Manager oder Windows PowerShell zuzulassen, wählen Sie **Remote Verwaltung dieses Servers von anderen Computern aktivieren aus**.

##### <a name="to-enable-server-manager-remote-management-on--windows-server-2012-r2--or--windows-server-2012--by-using-windows-powershell"></a>So aktivieren Sie Server-Manager-Remote Verwaltung unter Windows Server 2012 R2 oder Windows Server 2012 mithilfe von Windows PowerShell

1.  Führen Sie einen der folgenden Schritte aus:

    -   Wenn Sie Windows PowerShell als Administrator über den **Start** Bildschirm ausführen möchten, klicken Sie mit der rechten Maustaste auf die Kachel **Windows PowerShell** , und klicken Sie dann auf **als Administrator ausführen**.

    -   Wenn Sie Windows PowerShell als Administrator über den Desktop ausführen möchten, klicken Sie in der Taskleiste mit der rechten Maustaste auf die Verknüpfung **Windows PowerShell** , und klicken Sie dann auf **als Administrator ausführen**.

2.  Geben Sie Folgendes ein, und drücken **Sie** dann die EINGABETASTE, um alle erforderlichen Firewallregelausnahmen zu aktivieren.

    **Configure-SMremoting.exe aktivieren**

    > [!NOTE]
    > Dieser Befehl kann auch in einer Eingabeaufforderung verwendet werden, die mit erhöhten Benutzerrechten ("Als Administrator ausführen") geöffnet wurde.

    Wenn das Aktivieren der Remote Verwaltung fehlschlägt, finden Sie unter [about_remote_Troubleshooting](https://go.microsoft.com/fwlink/p/?LinkID=135188) auf Microsoft TechNet Tipps und bewährte Methoden zur Problembehandlung.

##### <a name="to-enable-server-manager-and-windows-powershell-remote-management-on-older-operating-systems"></a>So aktivieren Sie die Remoteverwaltung durch den Server-Manager und Windows PowerShell für ältere Betriebssysteme

-   Führen Sie einen der folgenden Schritte aus:

    -   Informationen zum Aktivieren der Remote Verwaltung auf Servern, auf denen Windows Server 2008 R2 ausgeführt wird, finden Sie unter [Remote Verwaltung mit Server-Manager](https://go.microsoft.com/fwlink/?LinkID=137378) in der Hilfe zu Windows Server 2008 R2.

    -   Informationen zum Aktivieren der Remote Verwaltung auf Servern, auf denen Windows Server 2008 ausgeführt wird, finden Sie unter [aktivieren und Verwenden von Remote Befehlen in Windows PowerShell](https://go.microsoft.com/fwlink/p/?LinkId=242565).

## <a name="tasks-that-you-can-perform-in-server-manager"></a>Im Server-Manager ausführbare Aufgaben

Server-Manager wird die Serververwaltung effizienter, da Administratoren mithilfe eines einzigen Tools Aufgaben in der folgenden Tabelle ausführen können. In Windows Server 2012 R2 und Windows Server 2012 können sowohl Standardbenutzer eines Servers als auch Mitglieder der Gruppe "Administratoren" Verwaltungsaufgaben in Server-Manager ausführen. Standardbenutzer werden jedoch standardmäßig daran gehindert, einige Aufgaben auszuführen, wie in der folgenden Tabelle gezeigt.

Administratoren können im Server-Manager Cmdlet-Modul, [enable-servermanagerstandarduserremoting](https://technet.microsoft.com/library/jj205470.aspx) und [Deaktivieren-servermanagerstandarduserremoting](https://technet.microsoft.com/library/jj205468.aspx), zwei Windows PowerShell-Cmdlets verwenden, um den Standardbenutzer Zugriff auf einige zusätzliche Daten weiter zu steuern. Das **enable-servermanagerstandarduserremoting-** Cmdlet kann einen oder mehrere Standardbenutzer ohne Administrator Rechte für den Zugriff auf Ereignis-, Dienst-, Leistungs-und Rollen-und featureinventur Daten bereitstellen.

> [!IMPORTANT]
> Server-Manager können nicht verwendet werden, um eine neuere Version des Windows Server-Betriebssystems zu verwalten. Server-Manager, die unter Windows Server 2012 oder Windows 8 ausgeführt werden, können nicht zum Verwalten von Servern verwendet werden, auf denen Windows Server 2012 R2 ausgeführt wird.

|Taskbeschreibung|Administratoren (einschließlich des des integrierten Administratorkontos)|Standardserverbenutzer|
|----------|----------------------------------|-------------|
|Hinzufügen von Remote Servern zu einem Pool von Servern, die Server-Manager zur Verwaltung von verwendet werden können.|Ja|Nein|
|Erstellen und bearbeiten Sie benutzerdefinierte Server Gruppen, z. b. Server, die sich an einem bestimmten geografischen Standort befinden oder einen bestimmten Zweck erfüllen.|Ja|Ja|
|Installieren oder Deinstallieren von Rollen, Rollen Diensten und Features auf dem lokalen Server oder auf Remote Servern, auf denen Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird. Definitionen von Rollen, Rollen Diensten und Features finden Sie unter [Rollen, Rollen Dienste und Features](https://go.microsoft.com/fwlink/p/?LinkId=239558).|Ja|Nein|
|Anzeigen und Ändern der auf Servern (lokal oder remote) installierten Serverrollen und Features. **Hinweis:** In Server-Manager werden Rollen-und Featuredaten in der Basis Sprache des Systems, auch als "System Default GUI Language" bezeichnet, oder der während der Installation des Betriebssystems ausgewählten Sprache angezeigt.|Ja|Standardbenutzer können Rollen und Features anzeigen und verwalten und Aufgaben wie das Anzeigen von Rollenereignissen durchführen, jedoch keine Rollendienste hinzufügen oder entfernen.|
|Starten Sie Verwaltungs Tools wie Windows PowerShell oder MMC-Snap-Ins. Sie können eine Windows PowerShell-Sitzung für einen Remote Server starten, indem Sie in der Kachel **Server** mit der rechten Maustaste auf den Server klicken und dann auf **Windows PowerShell** klicken. Sie können MMC-Snap-Ins über das **Menü Extras der Server-Manager** -Konsole starten und die MMC nach dem Öffnen des Snap-Ins auf einen Remote Computer verweisen.|Ja|Ja|
|Verwalten von Remoteservern mit unterschiedlichen Anmeldeinformationen, indem Sie auf der Kachel **Server** mit der rechten Maustaste auf einen Server klicken und dann auf **Verwalten als** klicken. Sie können **Verwalten als** für allgemeine Verwaltungsaufgaben für Server, Dateien und Speicherdienste verwenden.|Ja|Nein|
|Ausführen von Verwaltungsaufgaben im Zusammenhang mit dem operativen Lebenszyklus von Servern (z. b. starten oder Beenden von Diensten) und starten Sie weitere Tools, mit denen Sie die Netzwerkeinstellungen, Benutzer und Gruppen eines Servers und Remotedesktop Verbindungen konfigurieren können.|Ja|Standardbenutzer können keine Dienste starten oder beenden. Sie können den Namen, die Arbeitsgruppe oder die Domänen Mitgliedschaft des lokalen Servers und Remotedesktop Einstellungen ändern, werden jedoch von der Benutzerkontensteuerung aufgefordert, Administrator Anmelde Informationen bereitzustellen, bevor Sie diese Aufgaben ausführen können. Sie können keine Remoteverwaltungseinstellungen ändern.|
|Ausführen von Verwaltungsaufgaben in Verbindung mit dem operativen Lebenszyklus der auf dem Server installierten Rollen. Dazu gehört das Überprüfen der Rollen auf die Übereinstimmung mit bewährten Methoden.|Ja|Standard Benutzer können keine Best Practices Analyzer Scans ausführen.|
|Bestimmen des Serverstatus, Ermitteln kritischer Ereignisse sowie Analysieren und Behandeln von Konfigurationsproblemen oder -fehlern.|Ja|Ja|
|Passen Sie die Ereignisse, Leistungsdaten, Dienste und Best Practices Analyzer Ergebnisse an, über die Sie im Server-Manager-Dashboard benachrichtigt werden möchten.|Ja|Ja|
|Neustarten von Servern.|Ja|Nein|
|Aktualisieren Sie die Daten, die in der Server-Manager Konsole zu verwalteten Servern angezeigt werden.|Ja|Nein|

> [!NOTE]
> Server-Manager können nicht zum Hinzufügen von Rollen und Features zu Servern verwendet werden, auf denen Windows Server 2008 R2 oder Windows Server 2008 ausgeführt wird.

## <a name="start-server-manager"></a>Starten des Server-Managers

Server-Manager wird standardmäßig auf Servern, auf denen Windows Server 2016 ausgeführt wird, automatisch gestartet, wenn sich ein Mitglied der Gruppe "Administratoren" bei einem Server anmeldet. Wenn Sie Server-Manager schließen, starten Sie ihn mit einer der folgenden Methoden neu. Dieser Abschnitt enthält auch Schritte zum Ändern des Standard Verhaltens und verhindern, dass Server-Manager automatisch gestartet werden.

### <a name="to-start-server-manager-from-the-start-screen"></a>So starten Sie Server-Manager über den Startbildschirm

-   Klicken Sie auf dem Windows- **Start** Bildschirm auf die Kachel **Server-Manager** .

### <a name="to-start-server-manager-from-the-windows-desktop"></a>So starten Sie den Server-Manager über den Windows-Desktop

-   Klicken Sie auf der Windows-Taskleiste auf **Server-Manager**.

### <a name="to-prevent-server-manager-from-starting-automatically"></a>So verhindern Sie den automatischen Start des Server-Managers

1.  Klicken Sie in der Server-Manager-Konsole im Menü **Verwalten** auf **Server-Manager Eigenschaften**.

2.  Aktivieren Sie im Dialogfeld **Server-Manager-Eigenschaften** das Kontrollkästchen für **Server-Manager beim Anmelden nicht automatisch starten**. Klicken Sie auf **OK**.

3.  Alternativ können Sie verhindern, dass Server-Manager automatisch gestartet wird, indem Sie die Einstellung Gruppenrichtlinie aktivieren, **Server-Manager bei der Anmeldung nicht automatisch starten**. Der Pfad zu dieser Richtlinien Einstellung ist in der Konsole des lokalen Gruppenrichtlinie-Editors Computerkonfiguration\Administrative vorlagen\system\servermanager.

## <a name="restart-remote-servers"></a>Neustarten von Remoteservern
Sie können einen Remote Server über die Kachel **Server** einer Rollen-oder Gruppenseite in Server-Manager neu starten.

> [!IMPORTANT]
> Beim eines Remoteservers wird der Server auch dann zum Neustarten gezwungen, wenn noch Benutzer am Remoteserver angemeldet und Programme mit ungespeicherten Daten geöffnet sind. Dieses Verhalten unterscheidet sich um Herunterfahren oder Neustarten des lokalen Computers, auf dem Sie aufgefordert würden, ungespeicherte Programmdaten zu speichern und zu bestätigen, dass angemeldete Benutzer zur Abmeldung gezwungen werden sollen. Stellen Sie sicher, dass Sie Benutzer zur Abmeldung von Remoteservern zwingen und ungespeicherte Daten in Programmen, die auf Remoteservern ausgeführt werden, verwerfen können.
>
> Wenn eine automatische Aktualisierung in Server-Manager erfolgt, während ein verwalteter Server heruntergefahren und neu gestartet wird, können Aktualisierungs-und verwaltbarkeitsstatusfehler für den verwalteten Server auftreten, da Server-Manager keine Verbindung mit dem Remote Server herstellen kann, bis der Neustart abgeschlossen ist.

### <a name="to-restart-remote-servers-in-server-manager"></a>So starten Sie Remoteserver im Server-Manager

1.  Öffnen Sie eine Rollen-oder Server Gruppen-Startseite in Server-Manager.

2.  Wählen Sie einen oder mehrere Remote Server aus, die Sie Server-Manager hinzugefügt haben. Halten Sie beim Klicken die **STRG** -Taste gedrückt, um mehrere Warnungen gleichzeitig auszuwählen. Weitere Informationen zum Hinzufügen von Servern zum Server-Manager-Server Pool finden Sie unter [Hinzufügen von Servern zu Server-Manager](add-servers-to-server-manager.md).

3.  Klicken Sie mit der rechten Maustaste auf die ausgewählten Server, und klicken Sie anschließend auf **Server neu starten**.

## <a name="export-server-manager-settings-to-other-computers"></a>Exportieren von Server-Manager-Einstellungen auf andere Computer

In Server-Manager werden die Liste der verwalteten Server, Änderungen an Server-Manager Konsolen Einstellungen und von Ihnen erstellte benutzerdefinierte Gruppen in den folgenden beiden Dateien gespeichert. Sie können diese Einstellungen auf anderen Computern, auf denen dieselbe Version von Server-Manager ausgeführt wird (oder Windows 10 mit installierter Remoteserver-Verwaltungstools), wieder verwenden. Remoteserver-Verwaltungstools müssen auf Windows-Client basierten Computern ausgeführt werden, um Server-Manager Einstellungen auf diese Computer zu exportieren.

-   %*AppData* % \Microsoft\Windows\ServerManager\Serverlist.xml

-   %*AppData* % \Local\Microsoft_Corporation\ServerManager.exe_StrongName_ *GUID* \6.2.0.0\user.config

> [!NOTE]
> -   Alternative Anmeldeinformationen (bzw. %%amp;quot;Verwalten als%%amp;quot;) für Server im Serverpool werden nicht im Roamingprofil gespeichert. Server-Manager Benutzer müssen Sie auf allen Computern hinzufügen, von denen Sie verwaltet werden möchten.
> -   Das Netzwerkfreigaben-Roamingprofil wird erst erstellt, wenn sich ein Benutzer erstmalig am Netzwerk anmeldet und dann wieder abmeldet. Die Datei **Serverlist.xml** wird zu diesem Zeitpunkt erstellt.

Sie können Server-Manager Einstellungen exportieren, Server-Manager Einstellungen portierbar machen oder Sie auf anderen Computern mithilfe einer der beiden folgenden Methoden verwenden.

-   Zum Exportieren von Einstellungen auf einen anderen in die Domäne eingebundenen Computer konfigurieren Sie den Server-Manager Benutzer so, dass er ein Roamingprofil in Active Directory-Benutzer und-Computer Sie müssen Domänen Administrator sein, um Benutzereigenschaften in Active Directory-Benutzer und-Computer zu ändern.

-   Wenn Sie Einstellungen auf einen anderen Computer in einer Arbeitsgruppe exportieren möchten, kopieren Sie die vorangehenden beiden Dateien an den gleichen Speicherort auf dem Computer, von dem aus Sie mithilfe Server-Manager verwalten möchten.

### <a name="to-export-server-manager-settings-to-other-domain-joined-computers"></a>So exportieren Sie Server-Manager-Einstellungen auf andere Computer in einer Domäne

1.  Öffnen Sie unter "Active Directory-Benutzer und-Computer" das Dialogfeld " **Eigenschaften** " für einen Server-Manager Benutzer.

2.  Fügen Sie auf der Registerkarte **Profil** einen Pfad zu einer Netzwerkfreigabe hinzu, um das Benutzerprofil zu speichern.

3.  Führen Sie einen der folgenden Schritte aus:

    -   Bei US-amerikanischen Builds (en-US) werden Änderungen an der **Serverlist.xml** Datei automatisch im Profil gespeichert. Fahren Sie mit dem nächsten Schritt fort.

    -   Kopieren Sie bei anderen Builds die beiden folgenden Dateien von dem Computer, auf dem Server-Manager ausgeführt wird, auf die Netzwerkfreigabe, die zum Roamingprofil des Benutzers gehört.

        -   %*AppData* % \Microsoft\Windows\ServerManager\Serverlist.xml

        -   %*LocalAppData* % \Microsoft_Corporation\ServerManager.exe_StrongName_ *GUID* \6.2.0.0\user.config

4.  Klicken Sie auf **OK** , um die Änderungen zu speichern und das Dialogfeld **Eigenschaften** zu schließen.

### <a name="to-export-server-manager-settings-to-computers-in-workgroups"></a>So exportieren Sie Server-Manager-Einstellungen auf andere Computer in Arbeitsgruppen

-   Überschreiben Sie auf einem Computer, über den Sie Remote Server verwalten möchten, die beiden folgenden Dateien mit den gleichen Dateien von einem anderen Computer, auf dem Server-Manager ausgeführt wird und der über die gewünschten Einstellungen verfügt.

    -   %*AppData* % \Microsoft\Windows\ServerManager\Serverlist.xml

    -   %*LocalAppData* % \Microsoft_Corporation\ServerManager.exe_StrongName_ *GUID* \6.2.0.0\user.config