---
title: Konfigurieren der Remote Verwaltung in Server-Manager
description: Server-Manager
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 509182ed-c37d-4b81-84bc-aee43d006873
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8e1058a5679f73fcd2ceb8586da687158762d10f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383209"
---
# <a name="configure-remote-management-in-server-manager"></a>Konfigurieren der Remote Verwaltung in Server-Manager

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In Windows Server können Sie Server-Manager verwenden, um Verwaltungsaufgaben auf Remote Servern auszuführen. die Remote Verwaltung ist auf Servern, auf denen Windows Server 2016 ausgeführt wird, standardmäßig aktiviert. Wenn Sie einen Server mithilfe von Server-Manager Remote verwalten möchten, fügen Sie den Server zum Server-Manager Server Pool hinzu.

Sie können Server-Manager zum Verwalten von Remote Servern verwenden, auf denen ältere Versionen von Windows Server ausgeführt werden, aber die folgenden Updates sind erforderlich, um diese älteren Betriebssysteme vollständig verwalten zu können.

Zum Verwalten von Servern, auf denen Windows Server-Versionen älter als Windows Server 2016 ausgeführt werden, installieren Sie die folgende Software und Updates, um die älteren Versionen von Windows Server mithilfe von Server-Manager in Windows Server 2016 verwaltbar zu machen.

|Betriebssystem|Erforderliche Software|Verwaltbarkeit|
|----------|-----------|---------|
| Windows Server 2012 R2 oder Windows Server 2012 |-   [.NET Framework 4,6](https://www.microsoft.com/download/details.aspx?id=45497)<br />-   [Windows Management Framework 5,0](https://go.microsoft.com/fwlink/?LinkID=395058). Das Windows Management Framework 5,0 Download Package Updates Windows-Verwaltungsinstrumentation (WMI)-Anbieter unter Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2. Mit den aktualisierten WMI-Anbietern können Server-Manager Informationen zu den auf den verwalteten Servern installierten Rollen und Features sammeln. Bis zum Anwenden des Updates haben Server, auf denen Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 ausgeführt wird, den verwaltbarkeitsstatus **nicht zugänglich**.<br />-Das mit dem [Knowledge Base-Artikel 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) verknüpfte Leistungs Update ist auf Servern mit Windows Server 2012 R2 oder Windows Server 2012 nicht mehr erforderlich.||
| Windows Server 2008 R2 |-   [.NET Framework 4,5](https://www.microsoft.com/download/details.aspx?id=30653)<br />-   [Windows Management Framework 4,0](https://go.microsoft.com/fwlink/?LinkId=293881). Das Windows Management Framework 4,0-Downloadpaket aktualisiert Windows-Verwaltungsinstrumentation (WMI)-Anbieter unter Windows Server 2008 R2. Mit den aktualisierten WMI-Anbietern können Server-Manager Informationen zu den auf den verwalteten Servern installierten Rollen und Features sammeln. Bis zum Anwenden des Updates haben Server, auf denen Windows Server 2008 R2 ausgeführt wird, den verwaltbarkeitsstatus **nicht zugänglich**.<br />-Das mit dem [Knowledge Base-Artikel 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) verknüpfte Leistungs Update ermöglicht Server-Manager die Erfassung von Leistungsdaten von Windows Server 2008 R2.||
| WindowsServer 2008 |-   [.NET Framework 4](https://www.microsoft.com/download/en/details.aspx?id=17718)<br />-   [Windows Management Framework 3,0](https://go.microsoft.com/fwlink/p/?LinkID=229019) Windows Management Framework 3,0 Download Package Updates Windows-Verwaltungsinstrumentation (WMI)-Anbieter unter Windows Server 2008. Mit den aktualisierten WMI-Anbietern können Server-Manager Informationen zu den auf den verwalteten Servern installierten Rollen und Features sammeln. Bis zum Anwenden des Updates haben Server, auf denen Windows Server 2008 ausgeführt wird, den verwaltbarkeitsstatus **nicht verfügbar: Überprüfen Sie, ob frühere Versionen Windows Management Framework 3,0 ausführen**.<br />-Das mit dem [Knowledge Base-Artikel 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) verknüpfte Leistungs Update ermöglicht Server-Manager die Erfassung von Leistungsdaten von Windows Server 2008.||

Ausführliche Informationen zum Hinzufügen von Servern in zu verwaltenden Arbeitsgruppen oder zum Verwalten von Remote Servern über einen Arbeitsgruppen Computer, auf dem Server-Manager ausgeführt wird, finden [Sie unter Hinzufügen von Servern zu Server-Manager](add-servers-to-server-manager.md).

## <a name="enabling-or-disabling-remote-management"></a>Aktivieren oder Deaktivieren der Remoteverwaltung
In Windows Server 2016 ist die Remote Verwaltung standardmäßig aktiviert. Bevor Sie mit Server-Manager eine Remote Verbindung mit einem Computer herstellen können, auf dem Windows Server 2016 ausgeführt wird, muss Server-Manager Remote Verwaltung auf dem Zielcomputer aktiviert sein, wenn er deaktiviert wurde. In den Prozeduren dieses Abschnitts werden die Vorgehensweise zum Deaktivieren der Remoteverwaltung sowie die Vorgehensweise zum Reaktivieren der deaktivierten Remoteverwaltung beschrieben. In der Server-Manager Konsole wird der Remote Verwaltungsstatus für den lokalen Server im Bereich **Eigenschaften** der Seite **lokaler Server** angezeigt.

Von den lokalen Administratorkonten verfügt unter Umständen nur das integrierte Administratorkonto über Rechte für die Remoteverwaltung eines Servers. Dies gilt auch bei aktivierter Remoteverwaltung. Die Registrierungs Einstellung **LocalAccountTokenFilterPolicy** der Remote-Benutzerkontensteuerung (User Account Control, UAC) muss so konfiguriert werden, dass lokale Konten der Gruppe "Administratoren" außer dem integrierten Administrator Konto für die Remote Verwaltung des Servers zugelassen werden.

In Windows Server 2016 stützt Server-Manager die Windows-Remote Verwaltung (WinRM) und das verteilte Component Object Model (DCOM) für die Remote Kommunikation. Die Einstellungen, die im Dialogfeld **Remote Verwaltung konfigurieren** gesteuert werden, wirken sich nur auf Teile von Server-Manager und Windows PowerShell aus, von denen WinRM für die Remote Kommunikation verwendet wird. Sie wirken sich nicht auf Teile von Server-Manager aus, die DCOM für die Remote Kommunikation verwenden. Beispielsweise verwendet Server-Manager WinRM für die Kommunikation mit Remote Servern, auf denen Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird, verwendet aber DCOM für die Kommunikation mit Servern, auf denen Windows Server 2008 und Windows Server 2008 R2 ausgeführt wird, auf denen jedoch nicht [Windows Management Framework 4,0](https://go.microsoft.com/fwlink/?LinkId=293881) oder [Windows Management Framework 3,0](https://go.microsoft.com/fwlink/p/?LinkID=229019) installiert ist. Die Microsoft Management Console (MMC) und andere Legacy Verwaltungs Tools verwenden DCOM. Weitere Informationen zum Ändern dieser Einstellungen finden Sie unter so [Konfigurieren Sie MMC oder andere Tools Remote Verwaltung über DCOM](#to-configure-mmc-or-other-tool-remote-management-over-dcom) in diesem Thema.

> [!NOTE]
> Die Prozeduren in diesem Abschnitt können nur auf Computern unter Windows Server ausgeführt werden. Mithilfe der folgenden Verfahren können Sie die Remote Verwaltung auf einem Computer unter Windows 10 nicht aktivieren oder deaktivieren, da das Client Betriebssystem nicht mithilfe von Server-Manager verwaltet werden kann.

-   Wählen Sie zum Aktivieren der WinRM-Remoteverwaltung eines der folgenden Verfahren:

    -   [So aktivieren Sie Server-Manager-Remote Verwaltung mithilfe der Windows-Benutzeroberfläche](#to-enable-server-manager-remote-management-by-using-the-windows-interface)

    -   [So aktivieren Sie Server-Manager-Remote Verwaltung mithilfe von Windows PowerShell](#to-enable-server-manager-remote-management-by-using-windows-powershell)

    -   [So aktivieren Sie Server-Manager-Remote Verwaltung über die Befehlszeile](#to-enable-server-manager-remote-management-by-using-the-command-line)

    -   [So aktivieren Sie die Remote Verwaltung von Server-Manager und Windows PowerShell unter früheren Versionen von Windows Server](#to-enable-server-manager-and-windows-powershell-remote-management-on-earlier-releases-of-windows-server)

-   Wählen Sie eines der folgenden Verfahren aus, um WinRM und Server-Manager Remote Verwaltung zu deaktivieren.

    -   [So deaktivieren Sie die Remote Verwaltung mithilfe von Gruppenrichtlinie](#to-disable-remote-management-by-using-group-policy)

    -   [So deaktivieren Sie die Remote Verwaltung mithilfe einer Antwortdatei während der unbeaufsichtigten Installation](#to-disable-remote-management-by-using-an-answer-file-during-unattended-installation)

-   Informationen zum Konfigurieren der DCOM-Remoteverwaltung finden Sie in [To configure DCOM remote management](#to-configure-mmc-or-other-tool-remote-management-over-dcom).

### <a name="to-enable-server-manager-remote-management-by-using-the-windows-interface"></a>So aktivieren Sie die Remoteverwaltung des Server-Managers auf der Windows-Benutzeroberfläche

1.  > [!NOTE]
    > Die Einstellungen, die im Dialogfeld **Remote Verwaltung konfigurieren** gesteuert werden, wirken sich nicht auf Teile von Server-Manager aus, die DCOM für die Remote Kommunikation verwenden.

    Öffnen Sie auf dem Computer, den Sie remote verwalten möchten, Server-Manager, falls dieser nicht bereits geöffnet ist. Klicken Sie auf der Windows-Taskleiste auf **Server-Manager**. Klicken Sie auf dem **Start** Bildschirm auf die Kachel **Server-Manager** .

2.  Klicken Sie im Bereich **Eigenschaften** der Seite **lokale Server** auf den hyperverknüpften Wert für die Eigenschaft **Remote Verwaltung** .

3.  Führen Sie einen der folgenden Schritte aus, und klicken Sie anschließend auf **OK**:

    -   Deaktivieren Sie das Kontrollkästchen **Remote Verwaltung dieses Servers von anderen Computern aktivieren** , um zu verhindern, dass dieser Computer mithilfe Server-Manager (oder mithilfe von Windows PowerShell bei der Installation) Remote verwaltet wird.

    -   Um die Remote Verwaltung dieses Computers mithilfe von Server-Manager oder Windows PowerShell zuzulassen, wählen Sie **Remote Verwaltung dieses Servers von anderen Computern aktivieren aus**.

### <a name="to-enable-server-manager-remote-management-by-using-windows-powershell"></a>So aktivieren Sie die Remoteverwaltung des Server-Managers mithilfe von Windows PowerShell

1.  Führen Sie auf dem Computer, den Sie per Remote Zugriff verwalten möchten, eine der folgenden Aktionen aus, um eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten zu öffnen.

    -   Klicken Sie auf dem Windows-Desktop auf der Taskleiste mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.

    -   Klicken Sie auf dem Windows- **Start** Bildschirm mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf der APP-Leiste auf **als Administrator ausführen**.

2.  Geben Sie Folgendes ein, und drücken **Sie** dann die EINGABETASTE, um alle erforderlichen Firewallregelausnahmen zu aktivieren.

    **Configure-SMRemoting. exe-enable**

### <a name="to-enable-server-manager-remote-management-by-using-the-command-line"></a>So aktivieren Sie die Remoteverwaltung des Server-Managers über die Befehlszeile

1.  Öffnen Sie auf dem Computer, den Sie per Remotezugriff verwalten möchten, eine Eingabeaufforderungssitzung mit erhöhten Benutzerrechten. Geben Sie hierzu im **Start** Bildschirm **cmd**ein, klicken Sie mit der rechten Maustaste auf die Kachel **Eingabeaufforderung** , wenn diese in den **apps** -Ergebnissen angezeigt wird, und klicken Sie dann auf der APP-Leiste auf **als Administrator ausführen**.

2.  Führen Sie die folgende ausführbare Datei aus:

    **%windir%\system32\konfiguriert-SMRemoting.exe**

3.  Führen Sie eines der folgenden Verfahren aus:

    -   Um die Remote Verwaltung zu deaktivieren, geben Sie **configure-SMRemoting. exe-deaktivieren**ein, und drücken Sie dann die **Eingabe**Taste.

    -   Um die Remote Verwaltung zu aktivieren, geben Sie **configure-SMRemoting. exe-enable**ein, und drücken Sie dann die **Eingabe**Taste.

    -   Wenn Sie die aktuelle Remote Verwaltungs Einstellung anzeigen möchten, geben Sie **configure-SMRemoting. exe-get**ein, und drücken Sie dann die EINGABETASTE.

### <a name="to-enable-server-manager-and-windows-powershell-remote-management-on-earlier-releases-of-windows-server"></a>So aktivieren Sie die Remoteverwaltung von Server-Manager und Windows PowerShell für ältere Versionen von Windows Server

-   Führen Sie eines der folgenden Verfahren aus:

    -   Informationen zum Aktivieren der Remote Verwaltung auf Servern, auf denen Windows Server 2012 ausgeführt wird, finden Sie unter so [Aktivieren Sie Server-Manager-Remote Verwaltung mithilfe der Windows-Benutzeroberfläche](#to-enable-server-manager-remote-management-by-using-the-windows-interface) in diesem Thema.

    -   Informationen zum Aktivieren der Remote Verwaltung auf Servern, auf denen Windows Server 2008 R2 ausgeführt wird, finden Sie unter [Remote Verwaltung mit Server-Manager](https://go.microsoft.com/fwlink/?LinkID=137378) in der Hilfe zu Windows Server 2008 R2.

    -   Informationen zum Aktivieren der Remote Verwaltung auf Servern, auf denen Windows Server 2008 ausgeführt wird, finden Sie unter [aktivieren und Verwenden von Remote Befehlen in Windows PowerShell](https://go.microsoft.com/fwlink/p/?LinkId=242565).

### <a name="to-configure-mmc-or-other-tool-remote-management-over-dcom"></a>So konfigurieren Sie die Remote Verwaltung von MMC oder einem anderen Tool über DCOM

1.  Führen Sie eine der folgenden Aktionen aus, um die Windows-Firewall mit dem Snap-In für erweiterte Sicherheit zu öffnen:

    -   Klicken Sie im Bereich **Eigenschaften** der Seite **lokaler Server** in Server-Manager auf den Hypertext-Wert für die Eigenschaft **Windows-Firewall** , und klicken Sie dann auf **Erweiterte Einstellungen**.

    -   Geben Sie auf dem **Start** Bildschirm **WF. msc**ein, und klicken Sie dann auf die Snap-in-Kachel, wenn Sie in den **apps** -Ergebnissen angezeigt wird.

2.  Wählen Sie im Bereich mit der Struktur die Option **Eingehende Regeln** aus.

3.  Vergewissern Sie sich, dass Ausnahmen für die folgenden Firewallregeln aktiviert sind und nicht durch Gruppenrichtlinie Einstellungen deaktiviert wurden. Ist eine der Optionen nicht aktiviert, fahren Sie mit dem nächsten Schritt fort.

    -   COM+-Netzwerkzugriff (DCOM-In)

    -   Remote-Ereignisprotokoll Verwaltung (NP eingehend)

    -   Remote-Ereignisprotokoll Verwaltung (RPC)

    -   Remote-Ereignisprotokoll Verwaltung (RPC-EPMAP)

4.  Klicken Sie mit der rechten Maustaste auf die nicht aktivierten Regeln, und klicken Sie anschließend im Kontextmenü auf **Regel aktivieren** .

5.  Schließen Sie das Snap-In %%amp;quot;Windows-Firewall mit erweiterter Sicherheit%%amp;quot;.

### <a name="to-disable-remote-management-by-using-group-policy"></a>So deaktivieren Sie die Remoteverwaltung mithilfe von Gruppenrichtlinien

1.  Führen Sie eine der folgenden Aktionen aus, um den Editor für lokale Gruppenrichtlinie zu öffnen

    -   Geben Sie auf einem Server unter Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 auf dem **Start** Bildschirm **gpeer dit. msc**ein, und klicken Sie dann auf die Kachel **gpeer dit** , wenn diese angezeigt wird.

    -   Geben Sie auf einem Server unter Windows Server 2008 R2 oder Windows Server 2008 im Dialogfeld **Ausführen** den Befehl **gpeer dit. msc**ein, und drücken Sie dann die **Eingabe**Taste.

2.  Öffnen Sie **Computerkonfiguration\Administrative Vorlagen\Windows-komponents\windows-Remoteverwaltung (WinRM) \winrm-Dienst**.

3.  Doppelklicken Sie im Inhaltsbereich auf **Remoteserververwaltung über WinRM zulassen**.

4.  Wählen Sie im Dialogfeld für die Richtlinieneinstellung **Remoteserververwaltung über WinRM zulassen** die Option **Deaktiviert** aus, um die Remoteverwaltung zu deaktivieren. Klicken Sie auf **OK**, um die Änderungen zu speichern und das Dialogfeld für die Richtlinieneinstellung zu schließen.

### <a name="to-disable-remote-management-by-using-an-answer-file-during-unattended-installation"></a>So deaktivieren Sie die Remoteverwaltung mithilfe einer Antwortdatei während einer unbeaufsichtigten Installation

1.  Erstellen Sie mithilfe von Windows System Image Manager (Windows SIM) eine Antwortdatei für die unbeaufsichtigte Installation für Windows Server 2016-Installationen. Weitere Informationen zum Erstellen einer Antwortdatei und zum Verwenden von Windows SIM finden Sie unter [Was ist der Windows System Image Manager?](https://technet.microsoft.com/library/cc766347.aspx) und [Schrittweise Anleitung: Grundlegende Windows-Bereitstellung für IT-Spezialisten](https://technet.microsoft.com/library/dd349348.aspx).

2.  Suchen Sie in der Antwortdatei die Einstellung **Microsoft-Windows-Web-Services-for-Management-Core\EnableServerremoteManagement**.

3.  Wenn Sie Server-Manager Remote Verwaltung standardmäßig auf allen Servern deaktivieren möchten, auf die die Antwortdatei angewendet werden soll, legen Sie **Microsoft-Windows-Web-Services-for-Management-Core \enableserverremotemanagement** auf **false**fest.

    > [!NOTE]
    > Durch diese Einstellung wird die Remoteverwaltung bei der Installation des Betriebssystems deaktiviert. Durch das Konfigurieren dieser Einstellung wird verhindert, dass ein Administrator Server-Manager Remote Verwaltung auf einem Server aktiviert, nachdem das Betriebssystem Setup beendet wurde. Administratoren können Server-Manager Remote Verwaltung erneut aktivieren, indem Sie die Schritte in [zum Konfigurieren Server-Manager der Remote Verwaltung mithilfe der Windows-Benutzeroberfläche](#to-enable-server-manager-remote-management-by-using-the-windows-interface) oder [zum Aktivieren der Server-Manager-Remote Verwaltung mithilfe von Windows PowerShell](#to-enable-server-manager-remote-management-by-using-windows-powershell) in diesem Thema ausführen.
    > 
    > Wenn Sie die Remote Verwaltung standardmäßig im Rahmen einer unbeaufsichtigten Installation deaktivieren und die Remote Verwaltung auf dem Server nach der Installation nicht wieder aktivieren, können Server, auf die diese Antwortdatei angewendet wird, nicht vollständig mithilfe Server-Manager verwaltet werden. Server, auf denen Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird (und die Remote Verwaltung standardmäßig deaktiviert haben), generieren verwaltbarkeitsstatusfehler in der Server-Manager-Konsole, nachdem Sie dem Server-Manager Server hinzugefügt wurden. Spool.

## <a name="windows-remote-management-winrm-listener-settings"></a>WinRM-Listenereinstellungen (Windows Remote Management)
Server-Manager stützt sich auf den Remote Servern, die Sie verwalten möchten, auf den Standardeinstellungen des WinRM-Listener. Wenn der Standard Authentifizierungsmechanismus oder die WinRM-listenerportnummer auf einem Remote Server von den Standardeinstellungen geändert wurde, kann Server-Manager nicht mit dem Remote Server kommunizieren.

In der folgenden Liste werden die WinRM-Standard Listenereinstellungen für die Verwaltung von mit Server-Manager angezeigt.

-   Der WinRM-Dienst wird ausgeführt.

-   Ein WinRM-Listener wird erstellt, um HTTP-Anforderungen über die Portnummer 5985 zu akzeptieren.

-   Die Portnummer 5985 ist in den Einstellungen der Windows-Firewall aktiviert, um Anforderungen über WinRM zuzulassen.

-   Die Authentifizierungstypen **Kerberos** und **Negotiate** sind beide aktiviert.

Die Standardportnummer für die WinRM-Kommunikation mit einem Remotecomputer lautet 5985.

Weitere Informationen zum Konfigurieren von WinRM-Listenereinstellungen erhalten Sie, wenn Sie an einer Eingabeaufforderung **WinRM Help config**eingeben und dann die EINGABETASTE drücken.

## <a name="see-also"></a>Weitere Informationen
[Hinzufügen von Servern zu Server-Manager](add-servers-to-server-manager.md)
[Windows PowerShell: about_remote_Troubleshooting im Windows Server TechCenter](https://technet.microsoft.com/library/dd347642.aspx)
[Beschreibung der Benutzerkontensteuerung](https://support.microsoft.com/kb/951016)



