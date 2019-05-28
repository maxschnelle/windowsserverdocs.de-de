---
title: Konfigurieren der Remoteverwaltung im Server-Manager
description: Server-Manager
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 63d90d52b55357b5de823f2ca5e0a9fa2a3468e6
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222992"
---
# <a name="configure-remote-management-in-server-manager"></a>Konfigurieren der Remoteverwaltung im Server-Manager

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

In Windows Server können Sie Server-Manager verwenden, um Verwaltungsaufgaben auf Remoteservern ausführen. Remoteverwaltung ist auf Servern standardmäßig aktiviert, die Windows Server 2016 ausgeführt werden. Um einen Server mithilfe von Server-Manager Remote zu verwalten, fügen Sie dem Serverpool des Server-Manager den Server hinzu.

Sie können Server-Manager verwenden, um die Verwaltung von Remoteservern, auf denen ältere Versionen von Windows Server ausgeführt werden, aber die folgenden Updates sind erforderlich, um diese älteren Betriebssysteme vollständig verwalten.

Für die Verwaltung der Server, auf denen Windows Server-Versionen älter als Windows Server 2016 ausgeführt werden, installieren Sie die folgende Software und Updates für die älteren Versionen von Windows Server mit Server-Manager in Windows Server 2016 verwaltbar zu machen.

|Betriebssystem|Erforderliche Software|Verwaltbarkeit|
|----------|-----------|---------|
| Windows Server 2012 R2 oder WindowsServer 2012 |-   [.NET Framework 4.6](https://www.microsoft.com/download/details.aspx?id=45497)<br />-   [Windows Management Framework 5.0](https://go.microsoft.com/fwlink/?LinkID=395058). Das Downloadpaket Windows Management Framework 5.0 aktualisiert Anbieter der Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) unter Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2. Die aktualisierten WMI-Anbieter können Server-Manager Sammeln von Informationen zu Rollen und Features, die auf den verwalteten Servern installiert sind. Bis das Update installiert wird, haben Server, auf denen Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 ausgeführt werden verwaltbarkeitsstatus **kann nicht zugegriffen werden**.<br />– Die Leistungsupdate mit [Knowledge Base-Artikel 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) ist nicht mehr auf Servern unter Windows Server 2012 R2 oder Windows Server 2012 erforderlich.||
| Windows Server 2008 R2 |-   [.NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)<br />-   [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkId=293881). Das Downloadpaket Windows Management Framework 4.0 aktualisiert Anbieter der Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) unter Windows Server 2008 R2. Die aktualisierten WMI-Anbieter können Server-Manager Sammeln von Informationen zu Rollen und Features, die auf den verwalteten Servern installiert sind. Bis das Update installiert wird, haben Server, auf denen Windows Server 2008 R2 einen verwaltbarkeitsstatus von **kann nicht zugegriffen werden**.<br />– Die Leistungsupdate mit [Knowledge Base-Artikel 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) können Sie Server-Manager für das Sammeln von Leistungsdaten von Windows Server 2008 R2.||
| WindowsServer 2008 |-   [.NET Framework 4](https://www.microsoft.com/download/en/details.aspx?id=17718)<br />-   [Windows Management Framework 3.0](https://go.microsoft.com/fwlink/p/?LinkID=229019) das Windows Management Framework 3.0-Downloadpaket aktualisiert (Windows Management Instrumentation, WMI) Anbieter unter Windows Server 2008. Die aktualisierten WMI-Anbieter können Server-Manager Sammeln von Informationen zu Rollen und Features, die auf den verwalteten Servern installiert sind. Bis das Update installiert wird, haben Server, auf denen Windows Server 2008 verwaltbarkeitsstatus **kann nicht zugegriffen werden - überprüfen Sie die frühere Versionen unter Windows Management Framework 3.0**.<br />– Die Leistungsupdate mit [Knowledge Base-Artikel 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) können Sie Server-Manager für das Sammeln von Leistungsdaten von Windows Server 2008.||

Ausführliche Informationen zum Hinzufügen von Servern, die sich in Arbeitsgruppen befinden, verwalten oder Verwaltung von Remoteservern über einen Arbeitsgruppencomputer, auf dem Server-Manager ausgeführt wird, finden Sie unter [Hinzufügen von Servern zu Server Manager](add-servers-to-server-manager.md).

## <a name="enabling-or-disabling-remote-management"></a>Aktivieren oder Deaktivieren der Remoteverwaltung
In Windows Server 2016 ist die Remoteverwaltung standardmäßig aktiviert. Bevor Sie auf einem Computer, die Windows Server 2016 verbinden können mithilfe des Server-Manager Remote ausgeführt wird, muss Server-Manager-Remoteverwaltung auf dem Zielcomputer aktiviert werden, wenn er deaktiviert wurde. In den Prozeduren dieses Abschnitts werden die Vorgehensweise zum Deaktivieren der Remoteverwaltung sowie die Vorgehensweise zum Reaktivieren der deaktivierten Remoteverwaltung beschrieben. Der remoteverwaltungsstatus für den lokalen Server wird in der Server-Manager-Konsole der **Eigenschaften** Teil der **lokalen Server** Seite.

Von den lokalen Administratorkonten verfügt unter Umständen nur das integrierte Administratorkonto über Rechte für die Remoteverwaltung eines Servers. Dies gilt auch bei aktivierter Remoteverwaltung. Die remote Benutzerkontensteuerung (UAC) **"LocalAccountTokenFilterPolicy"** registrierungseinstellung muss konfiguriert werden, um die lokalen Konten der Gruppe "Administratoren" als das integrierte Administratorkonto Remoteverwaltung ermöglicht die Server.

In Windows Server 2016 verwendet Server-Manager Windows-Remoteverwaltung (WinRM) und Distributed Component Object Model (DCOM) für die Remotekommunikation genutzt. Die Einstellungen, die von gesteuert werden die **Konfigurieren der Remoteverwaltung** Dialogfeld wirken sich nur auf die Teile des Server-Manager und Windows PowerShell, die WinRM für die Remotekommunikation verwenden. Sie haben keine Teile des Server-Managers Auswirkungen, die DCOM für die Remotekommunikation verwenden. Beispielsweise Server-Manager verwendet WinRM, um die Kommunikation mit Remoteservern, auf denen Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt werden, allerdings verwendet DCOM für die Kommunikation mit Servern unter Windows Server 2008 und Windows Server 2008 R2 aber keine der [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkId=293881) oder [Windows Management Framework 3.0](https://go.microsoft.com/fwlink/p/?LinkID=229019) angewendeten Updates. Microsoft Management Console (Mmc) und anderen älteren Verwaltungstools verwendet DCOM. Weitere Informationen zum Ändern dieser Einstellungen finden Sie unter [so konfigurieren Sie Mmc oder andere Remoteverwaltung Tool über DCOM](#to-configure-mmc-or-other-tool-remote-management-over-dcom) in diesem Thema.

> [!NOTE]
> Die Prozeduren in diesem Abschnitt können nur auf Computern unter Windows Server ausgeführt werden. Sie können nicht aktivieren oder deaktivieren die Remoteverwaltung auf einem Computer, der mithilfe der folgenden Vorgehensweisen, Windows 10 ausgeführt wird, da das Clientbetriebssystem mithilfe von Server-Manager verwaltet werden können.

-   Wählen Sie zum Aktivieren der WinRM-Remoteverwaltung eines der folgenden Verfahren:

    -   [Um die Remoteverwaltung des Server-Manager zu aktivieren, indem Sie mithilfe der Windows-Benutzeroberfläche](#to-enable-server-manager-remote-management-by-using-the-windows-interface)

    -   [So aktivieren Server-Manager-Remoteverwaltung mithilfe von Windows PowerShell](#to-enable-server-manager-remote-management-by-using-windows-powershell)

    -   [So aktivieren Sie die Remoteverwaltung des Server-Managers über die Befehlszeile](#to-enable-server-manager-remote-management-by-using-the-command-line)

    -   [So aktivieren Sie die Server-Manager und Windows PowerShell-Remoteverwaltung unter früheren Versionen von Windows Server](#to-enable-server-manager-and-windows-powershell-remote-management-on-earlier-releases-of-windows-server)

-   Wählen Sie zum Deaktivieren der WinRM und Server-Manager-Remoteverwaltung eine der folgenden Verfahren aus.

    -   [Zum Deaktivieren der Remoteverwaltung mithilfe von Gruppenrichtlinien](#to-disable-remote-management-by-using-group-policy)

    -   [Zum Deaktivieren der Remoteverwaltung mithilfe einer Antwortdatei während der unbeaufsichtigten installation](#to-disable-remote-management-by-using-an-answer-file-during-unattended-installation)

-   Informationen zum Konfigurieren der DCOM-Remoteverwaltung finden Sie in [To configure DCOM remote management](#to-configure-mmc-or-other-tool-remote-management-over-dcom).

### <a name="to-enable-server-manager-remote-management-by-using-the-windows-interface"></a>So aktivieren Sie die Remoteverwaltung des Server-Managers auf der Windows-Benutzeroberfläche

1.  > [!NOTE]
    > Die Einstellungen, die von gesteuert werden die **Konfigurieren der Remoteverwaltung** Dialogfeld wirken sich nicht auf die Teile des Server-Managers, die DCOM für die Remotekommunikation verwenden.

    Öffnen Sie Server-Manager auf dem Computer, den Sie per Remotezugriff verwalten möchten, ist dies nicht bereits geöffnet. Klicken Sie auf der Windows-Taskleiste auf **Server-Manager**. Auf der **starten** Bildschirm, klicken Sie auf die **Server-Manager** Kachel.

2.  In der **Eigenschaften** Teil der **lokale Server** auf den als Hyperlink dargestellten Wert für die **Remoteverwaltung** Eigenschaft.

3.  Führen Sie einen der folgenden Schritte aus, und klicken Sie anschließend auf **OK**:

    -   Um zu verhindern, dass dieser Computer wird mithilfe von Server-Manager (oder Windows PowerShell, sofern es installiert ist) remote verwaltet werden, deaktivieren Sie die **Remoteverwaltung dieses Servers von anderen Computern aktivieren** Kontrollkästchen.

    -   Damit dieser Computer Remote mithilfe von Server-Manager oder Windows PowerShell verwaltet werden können, wählen Sie **Remoteverwaltung dieses Servers von anderen Computern aktivieren**.

### <a name="to-enable-server-manager-remote-management-by-using-windows-powershell"></a>So aktivieren Sie die Remoteverwaltung des Server-Managers mithilfe von Windows PowerShell

1.  Gehen Sie auf dem Computer, den Sie per Remotezugriff verwalten möchten zu eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten zu öffnen.

    -   Klicken Sie auf dem Windows-Desktop auf der Taskleiste mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.

    -   Klicken Sie auf der Windows **starten** der rechten Maustaste auf **Windows PowerShell**, und klicken Sie auf der app-Leiste auf **als Administrator ausführen**.

2.  Geben Sie Folgendes ein, und drücken Sie dann die **EINGABETASTE** So aktivieren Sie alle erforderlichen firewallregelausnahmen.

    **Konfigurieren von-SMremoting.exe-aktivieren**

### <a name="to-enable-server-manager-remote-management-by-using-the-command-line"></a>So aktivieren Sie die Remoteverwaltung des Server-Managers über die Befehlszeile

1.  Öffnen Sie auf dem Computer, den Sie per Remotezugriff verwalten möchten, eine Eingabeaufforderungssitzung mit erhöhten Benutzerrechten. Zu diesem Zweck die **starten** geben **Cmd**, mit der rechten Maustaste die **Eingabeaufforderung** Kachel angezeigt wird der **Apps** Ergebnisse zu erzielen, und Klicken Sie auf der app-Leiste auf **als Administrator ausführen**.

2.  Führen Sie die folgende ausführbare Datei aus:

    **%windir%\system32\Configure-SMremoting.exe**

3.  Führen Sie eines der folgenden Verfahren aus:

    -   Geben Sie zum Deaktivieren der Remoteverwaltung **Configure-SMremoting.exe-deaktivieren**, und drücken Sie dann die **EINGABETASTE**.

    -   Geben Sie zum Aktivieren der Remoteverwaltung **Configure-SMremoting.exe-aktivieren**, und drücken Sie dann die **EINGABETASTE**.

    -   Geben Sie zum Anzeigen der aktuellen remoteverwaltungseinstellung **Configure-SMremoting.exe-get**, und drücken Sie dann die EINGABETASTE.

### <a name="to-enable-server-manager-and-windows-powershell-remote-management-on-earlier-releases-of-windows-server"></a>So aktivieren Sie die Remoteverwaltung von Server-Manager und Windows PowerShell für ältere Versionen von Windows Server

-   Führen Sie eines der folgenden Verfahren aus:

    -   Um die Remoteverwaltung auf Servern zu aktivieren, auf denen Windows Server 2012 ausgeführt werden, finden Sie unter [um die Remoteverwaltung des Server-Manager zu aktivieren, indem Sie mithilfe der Windows-Benutzeroberfläche](#to-enable-server-manager-remote-management-by-using-the-windows-interface) in diesem Thema.

    -   Um die Remoteverwaltung auf Servern zu aktivieren, auf denen Windows Server 2008 R2 ausgeführt werden, finden Sie unter [Remoteverwaltung mit Server-Manager](https://go.microsoft.com/fwlink/?LinkID=137378) in der Windows Server 2008 R2-Hilfe.

    -   Um die Remoteverwaltung auf Servern zu aktivieren, auf denen Windows Server 2008 ausgeführt werden, finden Sie unter [aktivieren und Verwenden von Remotebefehlen in Windows PowerShell](https://go.microsoft.com/fwlink/p/?LinkId=242565).

### <a name="to-configure-mmc-or-other-tool-remote-management-over-dcom"></a>So konfigurieren Sie Mmc oder andere Remoteverwaltung Tool über DCOM

1.  Führen Sie eine der folgenden Aktionen aus, um die Windows-Firewall mit dem Snap-In für erweiterte Sicherheit zu öffnen:

    -   In der **Eigenschaften** Teil der **lokalen Server** Seite im Server-Manager, klicken Sie auf den als Hypertext dargestellten Wert für die **Windows-Firewall** -Eigenschaft, und klicken Sie dann auf  **Erweiterte Einstellungen**.

    -   Auf der **starten** geben **WF.msc**, und klicken Sie auf der Snap-in-Kachel angezeigt wird der **Apps** Ergebnisse.

2.  Wählen Sie im Bereich mit der Struktur die Option **Eingehende Regeln** aus.

3.  Stellen Sie sicher, dass Ausnahmen für die folgenden Firewallregeln aktiviert sind und nicht durch gruppenrichtlinieneinstellungen deaktiviert wurde. Ist eine der Optionen nicht aktiviert, fahren Sie mit dem nächsten Schritt fort.

    -   COM+-Netzwerkzugriff (DCOM-In)

    -   Remote-Ereignisprotokollverwaltung (NP eingehend)

    -   Remote Event Log-Management (RPC)

    -   Remote-Ereignisprotokollverwaltung (RPC-EPMAP)

4.  Klicken Sie mit der rechten Maustaste auf die nicht aktivierten Regeln, und klicken Sie anschließend im Kontextmenü auf **Regel aktivieren** .

5.  Schließen Sie das Snap-In %%amp;quot;Windows-Firewall mit erweiterter Sicherheit%%amp;quot;.

### <a name="to-disable-remote-management-by-using-group-policy"></a>So deaktivieren Sie die Remoteverwaltung mithilfe von Gruppenrichtlinien

1.  Führen Sie eine der folgenden lokalen Gruppenrichtlinien-Editor wird geöffnet.

    -   Auf einem Server, die auf Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird die **starten** geben **"Gpedit.msc"** , und klicken Sie dann auf die **Gpedit** Kachel Wenn er angezeigt wird.

    -   Auf einem Server, die Windows Server 2008 R2 oder Windows Server 2008 ausgeführt wird die **ausführen** (Dialogfeld), Typ **"Gpedit.msc"** , und drücken Sie dann **EINGABETASTE**.

2.  Open **Computer Computerkonfiguration\Administrative Vorlagen\Windows-Komponenten\Windows remote Management (WinRM) \WinRM Service**.

3.  Doppelklicken Sie im Inhaltsbereich auf **Remoteserververwaltung über WinRM zulassen**.

4.  Wählen Sie im Dialogfeld für die Richtlinieneinstellung **Remoteserververwaltung über WinRM zulassen** die Option **Deaktiviert** aus, um die Remoteverwaltung zu deaktivieren. Klicken Sie auf **OK**, um die Änderungen zu speichern und das Dialogfeld für die Richtlinieneinstellung zu schließen.

### <a name="to-disable-remote-management-by-using-an-answer-file-during-unattended-installation"></a>So deaktivieren Sie die Remoteverwaltung mithilfe einer Antwortdatei während einer unbeaufsichtigten Installation

1.  Erstellen Sie mithilfe von Windows System Image Manager (Windows SIM) eine Antwortdatei für die unbeaufsichtigte Installation für Windows Server 2016-Installationen. Weitere Informationen zum Erstellen einer Antwortdatei, und Verwenden von Windows SIM finden Sie unter [neuerungen Windows System Image Manager?](https://technet.microsoft.com/library/cc766347.aspx) und [Schritt für Schritt: Grundlegende Windows-Bereitstellung für IT-Experten](https://technet.microsoft.com/library/dd349348.aspx).

2.  Suchen Sie in der Antwortdatei die Einstellung **Microsoft-Windows-Web-Services-for-Management-Core\EnableServerremoteManagement**.

3.  Legen Sie zum Deaktivieren der Remoteverwaltung von Server-Manager wird standardmäßig auf allen Servern, um die Antwortdatei angewendet werden soll, **Microsoft \EnableServerremoteManagement** zu **"false"** .

    > [!NOTE]
    > Durch diese Einstellung wird die Remoteverwaltung bei der Installation des Betriebssystems deaktiviert. Für diese Einstellung verhindert nicht, dass einen Administrator über das Aktivieren der Remoteverwaltung von Server-Manager auf einem Server nach Abschluss der Installation des Betriebssystems. Administratoren können Server-Manager erneut mithilfe von in remoteverwaltungsschritte [so konfigurieren Server-Manager-Remoteverwaltung mithilfe der Windows-Benutzeroberfläche](#to-enable-server-manager-remote-management-by-using-the-windows-interface) oder [zum Aktivieren der Remoteverwaltung von Server-Manager mithilfe von Windows PowerShell](#to-enable-server-manager-remote-management-by-using-windows-powershell) in diesem Thema.
    > 
    > Wenn Sie die Remoteverwaltung standardmäßig im Rahmen einer unbeaufsichtigten Installation deaktivieren und Sie die Remoteverwaltung auf dem Server nicht erneut nach der Installation aktivieren, können nicht Server, auf die diese Antwortdatei angewendet wird, vollständig mithilfe von Server-Manager verwaltet werden. Server, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt werden (und deren Remoteverwaltung standardmäßig deaktiviert) generiert verwaltbarkeitsstatusfehler in Server-Manager-Konsole, nachdem sie sich an den Server-Manager-Server hinzugefügt wurden Dieser Pool.

## <a name="windows-remote-management-winrm-listener-settings"></a>Windows remote Management (WinRM)-Listener-Einstellungen
Server-Manager stützt sich auf standardmäßige WinRM-Listenereinstellungen auf den Remoteservern, die Sie verwalten möchten. Wenn der standardmäßige Authentifizierungsmechanismus oder die Portnummer des WinRM-Listener auf einem Remoteserver Standardeinstellungen geändert wurde, können keine Server-Manager mit dem Remoteserver kommunizieren.

Die folgende Liste zeigt standardmäßige WinRM-Listenereinstellungen auf, für die Verwaltung mit Server-Manager.

-   Der WinRM-Dienst wird ausgeführt.

-   Ein WinRM-Listener wird erstellt, um HTTP-Anforderungen über die Portnummer 5985 zu akzeptieren.

-   Die Portnummer 5985 ist in den Einstellungen der Windows-Firewall aktiviert, um Anforderungen über WinRM zuzulassen.

-   Die Authentifizierungstypen **Kerberos** und **Negotiate** sind beide aktiviert.

Die Standardportnummer für die WinRM-Kommunikation mit einem Remotecomputer lautet 5985.

Weitere Informationen zum Konfigurieren der WinRM-Listenereinstellungen an einer Eingabeaufforderung geben **Winrm Help Config**, und drücken Sie dann die EINGABETASTE.

## <a name="see-also"></a>Siehe auch
[Hinzufügen von Servern zu Server Manager](add-servers-to-server-manager.md)
[Windows PowerShell: About_remote_Troubleshooting im Windows Server TechCenter](https://technet.microsoft.com/library/dd347642.aspx)
[Beschreibung der Benutzerkontensteuerung](https://support.microsoft.com/kb/951016)



