---
title: Verwalten mehrerer Remoteserver mit Server-Manager
description: Server-Manager
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a17e686-e7f2-47e2-b7af-733777c38b5f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e4db3e486cec5cb065bfd202b7da2547be41a01a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847611"
---
# <a name="manage-multiple-remote-servers-with-server-manager"></a>Verwalten mehrerer Remoteserver mit Server-Manager

>Gilt für: Windows Server 2016

Server-Manager ist eine Verwaltungskonsole in Windows Server 2012 R2 und Windows Server 2012, die dabei hilft IT-Experten sowohl lokale als auch Windows-basierten Server von ihren Desktops aus, ohne dass Sie entweder physischen Zugriff auf Servern aus bereitstellen und verwalten oder die Sie müssen zum Aktivieren von Remote Desktop Protocol (RdP) Verbindungen zu den einzelnen Servern. Obwohl der Server-Manager in Windows Server 2008 R2 und Windows Server 2008 verfügbar ist, wurde Server Manager aktualisiert, in Windows Server 2012, Remoteunterstützung Management unterstützen, und die Anzahl von Servern zu erhöhen, die ein Administrator verwalten kann.

Bei unseren Tests kann Server-Manager in Windows Server 2012 R2 und Windows Server 2012 verwendet werden, um bis zu 100 Server verwalten, die mit einer typischen Arbeitslast konfiguriert sind. Die Anzahl der Server, die Sie mit einer einzelnen Server-Manager-Konsole verwalten können, kann von der Datenmenge abhängig sein, die Sie von den verwalteten Servern anfordern, sowie von den Hardware- und Netzwerkressourcen, die für den Computer mit dem Server-Manager zur Verfügung stehen. Wenn die anzuzeigende Datenmenge die Ressourcenkapazität des Computers erreicht, kann es zu langsamen Reaktionszeiten des Server-Managers und Verzögerungen bei der Durchführung von Aktualisierungen kommen. Um die Anzahl der Server zu erhöhen, die Sie mit dem Server-Manager verwalten können, sollten Sie die Ereignisdaten, die der Server-Manager von den verwalteten Servern empfängt, über das Dialogfeld **Ereignisdaten konfigurieren** beschränken. Sie können das Dialogfeld über das Menü **Aufgaben** in der Kachel **Ereignisse** öffnen. Wenn Sie in Ihrer Organisation eine organisationsübergreifende Anzahl von Servern verwalten müssen, wird empfohlen, die Produkte in der [Microsoft System Center-Suite](https://go.microsoft.com/fwlink/p/?LinkId=239437) auszuwerten.

In diesem Thema und seine Unterthemen enthalten Informationen zur Verwendung von Features in Server-Manager-Konsole verwenden. Dieses Thema enthält die folgenden Abschnitte:

-   [Vorüberlegungen und Systemanforderungen](#BKMK_1.1)

-   [Aufgaben, die Sie im Server-Manager ausführen können](#BKMK_tasks)

-   [Starten Sie den Server-Manager](#BKMK_start)

-   [Neustarten von Remoteservern](#BKMK_restart)

-   [Server-Manager-Einstellungen auf andere Computer exportieren](#BKMK_export)

## <a name="BKMK_1.1"></a>Vorüberlegungen und Systemanforderungen
Den folgenden Abschnitten werden einige anfänglichen Überlegungen, die Sie benötigen, sowie die Hardware- und softwareanforderungen für Server-Manager zu überprüfen.

### <a name="hardware-requirements"></a>Hardwareanforderungen
Server-Manager wird standardmäßig in allen Editionen von Windows Server 2012 R2 und Windows Server 2012 installiert. Es bestehen keine zusätzlichen hardwareanforderungen sind für Server-Manager vorhanden.

### <a name="BKMK_softconfig"></a>Software- und konfigurationsanforderungen
Server-Manager wird standardmäßig in allen Editionen von Windows Server 2012 installiert. Obwohl Sie Server-Manager verwenden können, zum Verwalten von [Server Core-Installationsoptionen](https://go.microsoft.com/fwlink/p/?LinkID=241573) von Windows Server 2012 und Windows Server 2008 R2, die auf Remotecomputern ausgeführt werden, Server-Manager führt nicht direkt auf Server Core-Installation Optionen.

Für die vollständige Verwaltung von Remoteservern, auf denen Windows Server 2008 oder Windows Server 2008 R2 installieren Sie die folgenden Updates auf den Servern, die Sie in der angezeigten Reihenfolge verwalten möchten.

Für die Verwaltung der Server, auf denen Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 mit Server-Manager in Windows Server 2012 R2 ausgeführt werden, werden wenden Sie die folgenden Updates auf die älteren Betriebssysteme an.

-   [.NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)

-   [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkId=293881). Das Downloadpaket Windows Management Framework 4.0 aktualisiert Anbieter der Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) unter Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008. Die aktualisierten WMI-Anbieter können Server-Manager Sammeln von Informationen zu Rollen und Features, die auf den verwalteten Servern installiert sind. Bis das Update installiert wird, haben Server, auf denen Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ausgeführt werden verwaltbarkeitsstatus **kann nicht zugegriffen werden**.

-   Leistungsupdate mit [Knowledge Base-Artikel 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) ermöglicht Server-Manager zum Erfassen von Leistungsdaten von Windows Server 2008 und Windows Server 2008 R2. Diese Leistungsupdate ist nicht erforderlich, auf Servern, auf denen Windows Server 2012 ausgeführt werden.

Um Servern unter Windows Server 2008 R2 oder Windows Server 2008 verwalten, müssen wenden Sie die folgenden Updates auf die älteren Betriebssysteme an.

-   [.NET Framework 4](https://www.microsoft.com/download/en/details.aspx?id=17718)

-   [Windows Management Framework 3.0](https://go.microsoft.com/fwlink/p/?LinkID=229019) das Windows Management Framework 3.0-Downloadpaket aktualisiert (Windows Management Instrumentation, WMI)-Anbieter für Windows Server 2008 und Windows Server 2008 R2. Die aktualisierten WMI-Anbieter können Server-Manager Sammeln von Informationen zu Rollen und Features, die auf den verwalteten Servern installiert sind. Bis das Update installiert wird, haben Server, auf denen Windows Server 2008 oder Windows Server 2008 R2 verwaltbarkeitsstatus **kann nicht zugegriffen werden - überprüfen Sie die frühere Versionen unter Windows Management Framework 3.0**.

-   Leistungsupdate mit [Knowledge Base-Artikel 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) ermöglicht Server-Manager zum Erfassen von Leistungsdaten von Windows Server 2008 und Windows Server 2008 R2.

Server-Manager wird in die minimale Grafische Serverschnittstelle. d. h., wenn das Feature für die Grafische Shell für Server deinstalliert wurde. Die Grafische Shell für Server-Funktion ist standardmäßig unter Windows Server 2012 R2 und Windows Server 2012 installiert. Wenn Sie die Grafische Shell für Server, die Server-Manager-Konsole ausgeführt wird, deinstallieren, aber einige Anwendungen oder Tools, die von der Konsole nicht verfügbar sind. Internetbrowser können nicht ohne Grafische Shell für Server, Webseiten und Anwendungen ausgeführt werden, wie z. B. HTML-Hilfe (z. B. das Mmc-F1-Hilfe) nicht geöffnet werden kann. Sie können nicht geöffnet werden Dialogfelder zum Konfigurieren von Windows automatische Aktualisierung und Feedback, wenn die Servergrafikshell nicht installiert ist; Befehle zum Öffnen dieser Dialogfelder in Server-Manager-Konsole werden umgeleitet, sodass die Ausführung **sconfig.cmd**.

#### <a name="manage-remote-computers-from-a-client-computer"></a>Verwalten von Remotecomputern über einen Clientcomputer
Die Server-Manager-Konsole ist im Lieferumfang [Remoteserver-Verwaltungstools](https://go.microsoft.com/fwlink/?LinkID=304145) für Windows 8.1 und [Remoteserver-Verwaltungstools](https://go.microsoft.com/fwlink/p/?LinkID=238560) für Windows 8. Beachten Sie, dass wenn Remoteserver-Verwaltungstools auf einem Clientcomputer installiert ist, können nicht Sie den lokalen Computer verwalten, indem Sie mit Server-Manager; Server-Manager kann nicht verwendet werden, zum Verwalten von Computern oder Geräten, die ein Windows-Clientbetriebssystem ausgeführt werden. Sie können die Server-Manager verwenden, nur Windows-basierten Server zu verwalten.

|Server-Manager-Source-Betriebssystem|Ziel unter Windows Server 2012 R2 |Auf WindowsServer 2012 ausgerichtet sind |Auf Windows Server 2008 R2 oder WindowsServer 2008 ausgerichtet sind |Für Windows Server 2003|
|-------------------------------|---------------------------------------|------------------------------------|-----------------------------------------------------------------------|------------------|
|Windows 8 oder WindowsServer 2012 |Nicht unterstützt.|Vollständige Unterstützung|Sobald die [Software- und Konfigurationsanforderungen](#BKMK_softconfig) erfüllt sind, können die meisten Verwaltungsaufgaben, jedoch keine Installation oder Deinstallation von Rollen oder Features ausgeführt werden.|Eingeschränkte Unterstützung, nur Online- und Offlinestatus|
|Windows 8.1 oder Windows Server 2012 R2 |Vollständige Unterstützung|Vollständige Unterstützung|Sobald die [Software- und Konfigurationsanforderungen](#BKMK_softconfig) erfüllt sind, können die meisten Verwaltungsaufgaben, jedoch keine Installation oder Deinstallation von Rollen oder Features ausgeführt werden.|Eingeschränkte Unterstützung, nur Online- und Offlinestatus|

###### <a name="to-start-server-manager-on-a-client-computer"></a>So starten Sie den Server-Manager auf einem Clientcomputer

1.  Führen Sie die Anweisungen im [Bereitstellen von Remoteserver-Verwaltungstools](https://go.microsoft.com/fwlink/?LinkID=238562) , Remote Server Administration Tools für Windows 8.1 oder Remoteserver-Verwaltungstools für Windows 8 zu installieren.

2.  Auf der **starten** auf **Server-Manager**. Die **Server-Manager**-Kachel ist verfügbar, nachdem Sie die Remoteserver-Verwaltungstools installiert haben.

3.  Wenn weder die **Verwaltung** noch die **Server-Manager** Kacheln werden angezeigt, auf die **starten** Bildschirm nach der Installation der Remoteserver-Verwaltungstools, und für Server-Manager nach der **starten** Bildschirm Ergebnisse nicht angezeigt, überprüfen Sie, ob die **Verwaltungstools anzeigen** Einstellung aktiviert ist. Um diese Einstellung anzuzeigen, zeigen Sie auf den Cursor über der oberen rechten Ecke des der **starten** Bildschirm, und klicken Sie dann auf **Einstellungen**. Ist die Einstellung **Verwaltungstools anzeigen** deaktiviert, aktivieren Sie die Einstellung, um Tools anzuzeigen, die Sie als Teil der Remoteserver-Verwaltungstools installiert haben.

Weitere Informationen zum Ausführen der Remoteserver-Verwaltungstools für Windows 8 zum Verwalten von Remoteservern finden Sie unter [Remoteserver-Verwaltungstools](https://go.microsoft.com/fwlink/?LinkID=221055) im TechNet Wiki.

#### <a name="configure-remote-management-on-servers-that-you-want-to-manage"></a>Konfigurieren der Remoteverwaltung auf zu verwaltenden Servern

> [!IMPORTANT]
> Standardmäßig ist die Remoteverwaltung von Server-Manager und Windows PowerShell in Windows Server 2012 R2 und Windows Server 2012 aktiviert.

Um Verwaltungsaufgaben auf Remoteservern mithilfe des Server-Manager ausführen möchten, müssen Remoteserver, die Sie verwalten möchten für die um Remoteverwaltung zu ermöglichen, mithilfe von Server-Manager und Windows PowerShell konfiguriert werden. Wenn remote-Verwaltung auf Windows Server 2012 R2 oder Windows Server 2012 deaktiviert wurde, und Sie ihn wieder aktivieren möchten, führen Sie die folgenden Schritte aus.

##### <a name="BKMK_windows"></a>So konfigurieren Server-Manager-Remoteverwaltung unter Windows Server 2012 R2 oder Windows Server 2012 mithilfe der Windows-Benutzeroberfläche

1.  > [!NOTE]
    > Die Einstellungen, die von gesteuert werden die **Konfigurieren der Remoteverwaltung** Dialogfeld wirken sich nicht auf die Teile des Server-Managers, die DCOM für die Remotekommunikation verwenden.

    Führen Sie einen der folgenden Server-Manager zu öffnen, sofern es nicht bereits geöffnet werden soll.

    -   Klicken Sie auf der Windows-Taskleiste auf die Schaltfläche "Server-Manager".

    -   Auf der **starten** auf **Server-Manager**.

2.  In der **Eigenschaften** Teil der **lokale Server** auf den als Hyperlink dargestellten Wert für die **Remoteverwaltung** Eigenschaft.

3.  Führen Sie einen der folgenden Schritte aus, und klicken Sie anschließend auf **OK**:

    -   Um zu verhindern, dass dieser Computer wird mithilfe von Server-Manager (oder Windows PowerShell, sofern es installiert ist) remote verwaltet werden, deaktivieren Sie die **Remoteverwaltung dieses Servers von anderen Computern aktivieren** Kontrollkästchen.

    -   Damit dieser Computer Remote mithilfe von Server-Manager oder Windows PowerShell verwaltet werden können, wählen Sie **Remoteverwaltung dieses Servers von anderen Computern aktivieren**.

##### <a name="BKMK_ps"></a>So aktivieren Server-Manager-Remoteverwaltung unter Windows Server 2012 R2 oder Windows Server 2012 mithilfe von Windows PowerShell

1.  Führen Sie eine der folgenden Aktionen aus.

    -   Zum Ausführen von Windows PowerShell als Administrator über die **starten** der rechten Maustaste auf die **Windows PowerShell** Kachel, und klicken Sie dann auf **als Administrator ausführen**.

    -   Führen Sie Windows PowerShell als Administrator über den Desktop Maustaste der **Windows PowerShell** der Taskleiste, und klicken Sie dann auf die Verknüpfung **als Administrator ausführen**.

2.  Geben Sie Folgendes ein, und drücken Sie dann die **EINGABETASTE** So aktivieren Sie alle erforderlichen firewallregelausnahmen.

    **Konfigurieren von-SMremoting.exe-aktivieren**

    > [!NOTE]
    > Dieser Befehl kann auch in einer Eingabeaufforderung verwendet werden, die mit erhöhten Benutzerrechten ("Als Administrator ausführen") geöffnet wurde.

    Falls die Remoteverwaltung fehlschlägt, finden Sie unter [About_remote_Troubleshooting](https://go.microsoft.com/fwlink/p/?LinkID=135188) auf Microsoft TechNet Tipps und bewährte Methoden zur Problembehandlung.

###### <a name="to-enable-server-manager-and-windows-powershell-remote-management-on-older-operating-systems"></a>So aktivieren Sie die Remoteverwaltung durch den Server-Manager und Windows PowerShell für ältere Betriebssysteme

-   Führen Sie eine der folgenden Aktionen aus.

    -   Um die Remoteverwaltung auf Servern zu aktivieren, auf denen Windows Server 2008 R2 ausgeführt werden, finden Sie unter [Remoteverwaltung mit Server-Manager](https://go.microsoft.com/fwlink/?LinkID=137378) in der Windows Server 2008 R2-Hilfe.

    -   Um die Remoteverwaltung auf Servern zu aktivieren, auf denen Windows Server 2008 ausgeführt werden, finden Sie unter [aktivieren und Verwenden von Remotebefehlen in Windows PowerShell](https://go.microsoft.com/fwlink/p/?LinkId=242565).

    -   Zum Aktivieren der Remoteverwaltung auf Servern unter Windows Server 2003 aktivieren Sie WMI-DCOM-Ausnahmen in der Windows-Firewall. Weitere Informationen dazu, wie Sie dies auf Servern unter Windows Server 2003 ausführen, finden Sie unter [Herstellen einer Verbindung über die Windows-Firewall](https://msdn.microsoft.com/library/aa389286.aspx) auf der MSDN-Website.

## <a name="BKMK_tasks"></a>Aufgaben, die Sie im Server-Manager ausführen können
Server-Manager-serververwaltung effizienter, da Administratoren Aufgaben in der folgenden Tabelle mithilfe eines einzigen Tools. In Windows Server 2012 R2 und Windows Server 2012 können sowohl Standardbenutzer eines Servers auch Mitglieder der Gruppe "Administratoren" Verwaltungsaufgaben im Server-Manager, in der Standardeinstellung Standardbenutzer werden jedoch gehindert Durchführung bestimmter Aufgaben, wie gezeigt in der in der folgenden Tabelle.

Administratoren können zwei Windows PowerShell-Cmdlets verwenden, im Server-Manager-Cmdlet-Modul, [Enable-ServerManagerStandardUserremoting](https://technet.microsoft.com/library/jj205470.aspx) und [Disable-ServerManagerStandardUserremoting](https://technet.microsoft.com/library/jj205468.aspx)zu Weitere standardbenutzerzugriff auf einige zusätzlichen Daten zu steuern. Die **Enable-ServerManagerStandardUserremoting** Cmdlet kann einem oder mehreren standardmäßigen, nicht-Administrator-Benutzerzugriff für Ereignis "," Dienst "," Leistungsindikator "und" Rollen- und featuredateien Inventurdaten bieten.

> [!IMPORTANT]
> Server-Manager kann nicht verwendet werden, um eine neuere Version des Betriebssystems Windows Server zu verwalten. Server-Manager unter Windows Server 2012 oder Windows 8 kann nicht verwendet werden, zum Verwalten von Servern, auf denen Windows Server 2012 R2 ausgeführt werden.

|Aufgabenbeschreibung|Administratoren (einschließlich des des integrierten Administratorkontos)|Standardserverbenutzer|
|----------|----------------------------------|-------------|
|Hinzufügen von Remoteservern zu einem Pool mit Servern, die Server-Manager kann zum Verwalten.|Ja|Nein|
|Erstellen Sie und bearbeiten Sie benutzerdefinierte Gruppen von Servern, z. B. Server, die in einem bestimmten geografischen Standort oder einen bestimmten Zweck erfüllen.|Ja|Ja|
|Installieren oder Deinstallieren von Rollen, Rollendienste und Features auf lokalen oder Remoteservern, auf denen Windows Server 2012 R2 oder Windows Server 2012. Definitionen von Rollen, Rollendienste und Features, finden Sie unter [Rollen, Rollendienste und Features](https://go.microsoft.com/fwlink/p/?LinkId=239558).|Ja|Nein|
|Anzeigen und Ändern der auf Servern (lokal oder remote) installierten Serverrollen und Features. **Hinweis**: Im Server-Manager wird die Rollen-und Featuredaten in der Basissprache des Systems, auch als GUI-Standardsprache des Systems oder der während der Installation des Betriebssystems ausgewählten Sprache angezeigt.|Ja|Standardbenutzer können Rollen und Features anzeigen und verwalten und Aufgaben wie das Anzeigen von Rollenereignissen durchführen, jedoch keine Rollendienste hinzufügen oder entfernen.|
|Starten von Verwaltungstools wie z. B. Windows PowerShell oder die Mmc-Snap-ins. Sie können eine Windows PowerShell-Sitzung, die mit der rechten Maustaste in des Servers im Ziel auf einem Remoteserver starten die **Server** Kachel, und klicken Sie dann auf **Windows PowerShell**. Sie können Mmc-Snap-ins aus starten die **Tools** im Menü der Server-Manager-Konsole, und zeigen Sie dann die Mmc auf einen Remotecomputer nach der das Snap-in geöffnet ist.|Ja|Ja|
|Verwalten von Remoteservern mit unterschiedlichen Anmeldeinformationen, indem Sie auf der Kachel **Server** mit der rechten Maustaste auf einen Server klicken und dann auf **Verwalten als**klicken. Sie können **Verwalten als** für allgemeine Verwaltungsaufgaben für Server, Dateien und Speicherdienste verwenden.|Ja|Nein|
|Ausführen von Verwaltungsaufgaben in Verbindung mit dem operativen Lebenszyklus von Servern, z. B. starten oder Beenden von Diensten an; und andere Tools, die Sie Netzwerkeinstellungen, Benutzer und Gruppen und Remotedesktopverbindungen eines Servers konfigurieren können.|Ja|Standardbenutzer können keine Dienste starten oder beenden. Sie können Namen, Arbeitsgruppe oder Domänenmitgliedschaft und Remotedesktop-Einstellungen des lokalen Servers ändern, jedoch werden von der Benutzerkontensteuerung aufgefordert, Administratoranmeldeinformationen einzugeben, bevor sie diese Aufgaben abgeschlossen werden können. Sie können keine Remoteverwaltungseinstellungen ändern.|
|Ausführen von Verwaltungsaufgaben in Verbindung mit dem operativen Lebenszyklus der auf dem Server installierten Rollen. Dazu gehört das Überprüfen der Rollen auf die Übereinstimmung mit bewährten Methoden.|Ja|Standardbenutzer können nicht Best Practices Analyzer-Scans ausgeführt werden.|
|Bestimmen des Serverstatus, Ermitteln kritischer Ereignisse sowie Analysieren und Behandeln von Konfigurationsproblemen oder -fehlern.|Ja|Ja|
|Anpassen der Ereignisse, Leistungsdaten, Dienste und Best Practices Analyzer-Ergebnisse, die über die Sie auf dem Server-Manager-Dashboard benachrichtigt werden möchten.|Ja|Ja|
|Neustarten von Servern.|Ja|Nein|
|Aktualisieren von Daten, die in der Server-Manager-Konsole zu verwalteten Servern angezeigt wird.|Ja|Nein|

> [!NOTE]
> Server-Manager kann von Servern unter Windows Server 2003 nur den Online- oder Offlinestatus empfangen. Server-Manager kann nicht verwendet werden, Hinzufügen von Rollen und Features auf Servern, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt werden.

## <a name="BKMK_start"></a>Starten Sie den Server-Manager
Server-Manager wird standardmäßig auf Servern unter Windows Server 2012, wenn ein Mitglied der Administratorengruppe anmeldet eines Servers automatisch gestartet. Wenn Sie Server-Manager schließen, starten Sie ihn in einem der folgenden Methoden neu. Dieser Abschnitt enthält auch Schritte zum Ändern des Standardverhaltens und zu verhindern, dass die Server-Manager automatisch gestartet wird.

#### <a name="to-start-server-manager-from-the-start-screen"></a>So starten Sie Server-Manager über den Startbildschirm

-   Klicken Sie auf der Windows **starten** Bildschirm, klicken Sie auf die **Server-Manager** Kachel.

#### <a name="to-start-server-manager-from-the-windows-desktop"></a>So starten Sie den Server-Manager über den Windows-Desktop

-   Klicken Sie auf der Windows-Taskleiste auf **Server-Manager**.

#### <a name="to-prevent-server-manager-from-starting-automatically"></a>So verhindern Sie den automatischen Start des Server-Managers

1.  In der Server-Manager-Konsole auf die **verwalten** Menü klicken Sie auf **Server-Manager-Eigenschaften**.

2.  Aktivieren Sie im Dialogfeld **Server-Manager-Eigenschaften** das Kontrollkästchen für **Server-Manager beim Anmelden nicht automatisch starten**. Klicken Sie auf **OK**.

3.  Alternativ Sie können verhindern, dass Server-Manager automatisch gestartet, durch Aktivieren der gruppenrichtlinieneinstellung **Server-Manager beim Anmelden nicht automatisch starten**. Der Pfad zu dieser richtlinieneinstellung in der lokalen Gruppenrichtlinien-Editor-Konsole ist Computer Configuration\Administrative Templates\System\Server-Manager.

## <a name="BKMK_restart"></a>Neustarten von Remoteservern
Sie können neu starten, einen Remoteserver über die **Server** Kachel eine Rollen- oder Gruppenseite im Server-Manager.

> [!IMPORTANT]
> Beim eines Remoteservers wird der Server auch dann zum Neustarten gezwungen, wenn noch Benutzer am Remoteserver angemeldet und Programme mit ungespeicherten Daten geöffnet sind. Dieses Verhalten unterscheidet sich um Herunterfahren oder Neustarten des lokalen Computers, auf dem Sie aufgefordert würden, ungespeicherte Programmdaten zu speichern und zu bestätigen, dass angemeldete Benutzer zur Abmeldung gezwungen werden sollen. Stellen Sie sicher, dass Sie Benutzer zur Abmeldung von Remoteservern zwingen und ungespeicherte Daten in Programmen, die auf Remoteservern ausgeführt werden, verwerfen können.
> 
> Wenn eine automatische Aktualisierung im Server-Manager auftritt, während ein verwalteter Server wird heruntergefahren und neu starten, Aktualisierungs- und verwaltbarkeitsstatus statusmeldungen, die für den verwalteten Server, Fehler auftreten können, da der Server-Manager mit dem Remoteserver keine Verbindung herstellen kann, bis er abgeschlossen ist neu starten.

#### <a name="to-restart-remote-servers-in-server-manager"></a>So starten Sie Remoteserver im Server-Manager

1.  Öffnen Sie eine Rollen- oder Servergruppen-Startseite im Server-Manager.

2.  Wählen Sie eine oder mehrere Remoteserver vorhanden, die Sie zum Server-Manager hinzugefügt haben. Halten Sie beim Klicken die **STRG**-Taste gedrückt, um mehrere Warnungen gleichzeitig auszuwählen. Weitere Informationen zum Hinzufügen von Servern zum Serverpool Server-Managers finden Sie unter [Hinzufügen von Servern zu Server Manager](add-servers-to-server-manager.md).

3.  Klicken Sie mit der rechten Maustaste auf die ausgewählten Server, und klicken Sie anschließend auf **Server neu starten**.

## <a name="BKMK_export"></a>Server-Manager-Einstellungen auf andere Computer exportieren
Im Server-Manager die Liste mit den verwalteten Servern zu Server-Manager-Konsole-Einstellungen geändert, und benutzerdefinierte Gruppen, die Sie erstellt haben, werden in den folgenden zwei Dateien gespeichert. Sie können diese Einstellungen auf anderen Computern wiederverwenden, die die gleiche Version von Server-Manager (keine Computer auf denen die Server Core-Installationsoption) oder Windows 8 ausführen. Remoteserver-Verwaltungstools müssen auf Windows-Clientcomputer so exportieren Sie Server-Manager-Einstellungen auf den entsprechenden Computern ausgeführt werden.

-   %*appdata*%\Microsoft\Windows\ServerManager\Serverlist.xml

-   %*appdata*%\Local\Microsoft_Corporation\ServerManager.exe_StrongName_*GUID*\6.2.0.0\user.config

> [!NOTE]
> -   Alternative Anmeldeinformationen (bzw. %%amp;quot;Verwalten als%%amp;quot;) für Server im Serverpool werden nicht im Roamingprofil gespeichert. Server-Manager-Benutzer müssen diese auf dem jeweiligen Computer hinzufügen, den sie verwalten wollen.
> -   Das Netzwerkfreigaben-Roamingprofil wird erst erstellt, wenn sich ein Benutzer erstmalig am Netzwerk anmeldet und dann wieder abmeldet. Die Datei **Serverlist.xml** wird zu diesem Zeitpunkt erstellt.

Sie können Server-Manager-Einstellungen exportieren, Server-Manager-Einstellungen portierbar machen oder auf anderen Computern in einer der beiden folgenden Methoden verwenden.

-   Konfigurieren Sie den Server-Manager-Benutzer ein Roamingprofil in active Directory-Benutzer und Computer, zum Exportieren von Einstellungen auf einem anderen Computer einer Domäne. Sie müssen Domänenadministrator sein, um das Ändern von Eigenschaften in active Directory-Benutzer und Computer sein.

-   Kopieren Sie zum Exportieren von Einstellungen auf einen anderen Computer in einer Arbeitsgruppe die vorhergehenden beiden Dateien an den gleichen Speicherort auf dem Computer, die aus dem Sie mithilfe des Server-Manager verwalten möchten.

#### <a name="to-export-server-manager-settings-to-other-domain-joined-computers"></a>So exportieren Sie Server-Manager-Einstellungen auf andere Computer in einer Domäne

1.  Öffnen Sie in active Directory-Benutzer und Computer die **Eigenschaften** im Dialogfeld für einen Server-Manager-Benutzer.

2.  Auf der **Profil** Registerkarte, fügen Sie einen Pfad zu einer Netzwerkfreigabe zum Speichern des Benutzerprofils.

3.  Führen Sie eine der folgenden Aktionen aus.

    -   In den USA Englisch (En-us) erstellt, ändert sich in der **Serverlist.xml** Datei automatisch im Profil gespeichert werden. Fahren Sie mit dem nächsten Schritt fort.

    -   Kopieren Sie bei anderen Builds die folgenden beiden Dateien auf dem Computer, der auf die Netzwerkfreigabe verfügen, die Teil des servergespeicherten Profil des Benutzers ist, Server-Manager ausgeführt wird.

        -   %*appdata*%\Microsoft\Windows\ServerManager\Serverlist.xml

        -   %*localappdata*%\Microsoft_Corporation\ServerManager.exe_StrongName_*GUID*\6.2.0.0\user.config

4.  Klicken Sie auf **OK** , um die Änderungen zu speichern und das Dialogfeld **Eigenschaften** zu schließen.

#### <a name="to-export-server-manager-settings-to-computers-in-workgroups"></a>So exportieren Sie Server-Manager-Einstellungen auf andere Computer in Arbeitsgruppen

-   Überschreiben Sie auf einem Computer, von dem Sie Remoteserver verwalten möchten die folgenden beiden Dateien mit den gleichen Dateien von einem anderen Computer, die auf dem Server-Manager ausgeführt wird, und die gewünschten Einstellungen aufweist.

    -   %*appdata*%\Microsoft\Windows\ServerManager\Serverlist.xml

    -   %*localappdata*%\Microsoft_Corporation\ServerManager.exe_StrongName_*GUID*\6.2.0.0\user.config


