---
title: Windows Admin Center – bekannte Probleme
description: Windows Admin Center – bekannte Probleme (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 06/07/2019
ms.openlocfilehash: 4a91d09d6824795a21a9a7cdc7695c407aa70756
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822703"
---
# <a name="windows-admin-center-known-issues"></a>Windows Admin Center – bekannte Probleme

> Gilt für: Windows Admin Center, Windows Admin Center Preview

Wenn Sie ein Problem haben, das auf dieser Seite nicht beschrieben ist, bitte [Teilen Sie uns dies mit](https://aka.ms/WACfeedback).

## <a name="installer"></a>Installer

- Beim Installieren von Windows Admin Center mit einem eigenen Zertifikat, wenn Sie den Fingerabdruck aus dem Zertifikat-Manager-MMC-Tool kopieren, [enthält dieser ein ungültiges Zeichen am Anfang.](https://support.microsoft.com/help/2023835/certificate-thumbprint-displayed-in-mmc-certificate-snap-in-has-extra) Um dieses Problem zu umgehen, geben Sie das erste Zeichen des Fingerabdrucks ein und kopieren Sie den Rest.

- Die Verwendung von Port unter 1024 wird nicht unterstützt. Im Dienst Modus können Sie optional Port 80 für die Umleitung an den angegebenen Port konfigurieren.

## <a name="general"></a>„Allgemein“

- Wenn Sie Windows Admin Center als Gateway unter **Windows Server 2016** unter hoher Auslastung installiert haben, stürzt der Dienst möglicherweise mit einem Fehler im Ereignisprotokoll ab, der ```Faulting application name: sme.exe``` und ```Faulting module name: WsmSvc.dll```enthält. Der Grund hierfür ist ein Fehler, der in Windows Server 2019 behoben wurde. Der Patch für Windows Server 2016 enthielt das kumulative Update vom Februar 2019, [KB4480977](https://www.catalog.update.microsoft.com/Search.aspx?q=4480977).

- Wenn Sie Windows Admin Center als Gateway installiert haben und die Verbindungsliste beschädigt erscheint, führen Sie die folgenden Schritte aus:

   > [!WARNING]
   >Hierdurch werden die Verbindungsliste und Einstellungen für alle Benutzer des Windows Admin Centers auf dem Gateway gelöscht.

  1. Deinstallieren Sie Windows Admin Center
  2. Löschen Sie den Ordner **Server Management Experience** unter **C:\Windows\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft**
  3. Installieren Sie Windows Admin Center erneut

- Wenn Sie das Tool geöffnet und für einen längeren Zeitraum im Leerlauf lassen, erhalten Sie möglicherweise mehrere **Error: The runspace state is not valid for this operation**. Aktualisieren Sie dann den Browser. Wenn dies der Meinung ist, [Senden Sie uns Feedback](https://aka.ms/WACfeedback).

- Möglicherweise gibt es eine geringfügige Abweichung zwischen den Versionsnummern von Betriebssystemen, die in den Modulen des Windows Admin Centers ausgeführt werden, und den im Software Hinweis eines Drittanbieters aufgeführten Betriebssystemen.

### <a name="extension-manager"></a>Erweiterungs-Manager

- Wenn Sie das Windows Admin Center aktualisieren, müssen Sie die Erweiterungen neu installieren.
- Wenn Sie einen Erweiterungs Feed hinzufügen, auf den nicht zugegriffen werden kann, wird keine Warnung angezeigt. [14412861]

## <a name="browser-specific-issues"></a>Bestimmte Browserprobleme

### <a name="microsoft-edge"></a>Microsoft Edge

- Wenn Sie das Windows Admin Center als Dienst bereitgestellt haben und Microsoft Edge als Browser verwenden, kann das Verbinden Ihres Gateways mit Azure nach dem Auslösen eines neuen Browserfensters fehlschlagen. Versuchen Sie, dieses Problem zu umgehen, indem Sie https://login.microsoftonline.com , https://login.live.com und die URL Ihres Gateways als vertrauenswürdige Sites und zulässige Websites für Popup Blocker-Einstellungen auf dem Client seitigen Browser hinzufügen. Weitere Anleitungen zur Behebung dieses Problem finden Sie im [Handbuch zur Problem](troubleshooting.md#azure-features-dont-work-properly-in-edge)Behandlung. [17990376]

### <a name="google-chrome"></a>Google Chrome

- Vor Version 70 (veröffentlicht am Ende Oktober, 2018) gab es einen [Fehler](https://bugs.chromium.org/p/chromium/issues/detail?id=423609) im Zusammenhang mit dem websockets-Protokoll und der NTLM-Authentifizierung. Dies wirkt sich auf die folgenden Tools aus: Ereignisse, PowerShell, Remotedesktop.

- Chrome zeigt eventuell mehrere Anmeldeinformationen an, vor allem in Zeiten der Verbindungsprozesse in einer **Arbeitsgruppen**-Umgebung (nicht der Domäne).

- Wenn Sie das Windows Admin Center als Dienst bereitgestellt haben, müssen Popups von der Gateway-URL aktiviert werden, damit alle Azure-Integrationsfunktionen funktionieren.

### <a name="mozilla-firefox"></a>Mozilla Firefox

Windows Admin Center wurde nicht mit Mozilla Firefox getestet, aber die meisten Funktionen sollten funktionieren.

- Windows 10-Installation: Mozilla Firefox verfügt über einen eigenen Zertifikat Speicher, sodass Sie das ```Windows Admin Center Client``` Zertifikat in Firefox importieren müssen, damit Windows Admin Center unter Windows 10 verwendet werden kann.

## <a name="websocket-compatibility-when-using-a-proxy-service"></a>WebSocket-Kompatibilität bei Verwendung eines Proxy Dienstanbieter

Remotedesktop, PowerShell und Ereignismodule im Windows Admin Center nutzen das WebSocket-Protokoll, das häufig nicht unterstützt wird, wenn ein Proxydienst verwendet wird. WebSocket unterstützt Azure AD-Anwendungsproxy-Kompatibilität in der [Vorschau](https://blogs.technet.microsoft.com/applicationproxyblog/2018/03/28/limited-websocket-support-now-in-public-preview/) und sucht nach Feedback zur Kompatibilität.

## <a name="support-for-windows-server-versions-before-2016-2012-r2-2012-2008-r2"></a>Unterstützung für Windows Server-Versionen vor 2016 (2012 R2, 2012, 2008 R2)

> [!NOTE]
> Windows Admin Center erfordert PowerShell-Features, die nicht in Windows Server 2012 R2, 2012 oder 2008 R2 enthalten sind. Wenn Sie Windows Server mit dem Windows Admin Center verwalten, müssen Sie WMF Version 5,1 oder höher auf diesen Servern installieren.

Geben Sie `$PSVersiontable` in PowerShell ein, um zu prüfen, ob WMF 5.1 oder einen neuere Version installiert ist.

Wenn dies nicht der Fall ist, können Sie [herunterladen und WMF 5.1 installieren](https://www.microsoft.com/download/details.aspx?id=54616).

## <a name="role-based-access-control-rbac"></a>Rollenbasierte Access Control (RBAC)

- RBAC-Bereitstellung ist auf Computern, die für die Windows Defender-Anwendungssteuerung (WDAC, früher als Integrität des Codes bezeichnet) konfiguriert werden, nicht erfolgreich [16568455]

- Um RBAC in einem Cluster verwenden, müssen Sie die Konfiguration für jeden Memberknoten einzeln bereitstellen.

- Wenn RBAC bereitgestellt wird, können Sie unauthorized-Fehler erhalten, die nicht ordnungsgemäß an der RBAC-Konfiguration Ergebnisarray als Attribut zugewiesen werden. [16369238]

## <a name="server-manager-solution"></a>Server-Manager-Lösung

### <a name="certificates"></a>Zertifikate

- Kann nicht importiert werden. PFX verschlüsselt Zertifikat im Speicher des aktuellen Benutzers. [11818622]

### <a name="events"></a>Veranstaltungen

- Ereignisse erfolgen durch [Websocket-Kompatibilität bei Verwendung eines Proxydiensts.](#websocket-compatibility-when-using-a-proxy-service)

- Möglicherweise erhalten Sie die Fehlermeldung "Packet Size" beim Exportieren von großen Protokolldateien.

  - Um dieses Problem zu beheben, verwenden Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten auf dem Gatewaycomputer: ```winrm set winrm/config @{MaxEnvelopeSizekb="8192"}```

### <a name="files"></a>Dateien

- Hoch- oder heruntergeladen großer Dateien wird noch nicht unterstützt. (\~100 MB Limit) [12524234]

### <a name="powershell"></a>PowerShell

- PowerShell erfolgt durch [Websocket-Kompatibilität bei Verwendung eines Proxydiensts](#websocket-compatibility-when-using-a-proxy-service)

- Das Einfügen mit einem einzelnen Klick mit der rechten Maustaste wie in der Desktop PowerShell-Konsole ist nicht funktionsfähig. Stattdessen erhalten Sie Kontextmenüs des Browsers, in dem Sie „einfügen” auswählen können. STRG + V funktioniert auch.

- STRG + C kann nicht zum Kopieren verwendet werden, es sendet immer den Befehl STRG + C an die Konsole. Das Kopieren über das mit der rechten Maustaste aufgerufenen Kontextmenü funktioniert.

- Wenn Sie das Windows Admin Center-Fenster kleiner machen, wird der Terminalinhalt umgeleitet, aber wenn Sie es erneut vergrößern, kann der Inhalt nicht in den vorherigen Zustand zurückkehren. Wenn Dinge durcheinander geraten, können Sie Clear-Host verwenden, oder die Verbindung trennen und erneut eine Verbindung mit der Schaltfläche oberhalb des Terminaldienstes herstellen.

### <a name="registry-editor"></a>Registrierungs-Editor

- Die Suchfunktion ist nicht implementiert. [13820009]

### <a name="remote-desktop"></a>Remotedesktop

- Wenn das Windows Admin Center als Dienst bereitgestellt wird, kann das Remotedesktop Tool nach dem Aktualisieren des Windows Admin Center-Dienstanbieter auf eine neue Version möglicherweise nicht geladen werden. Um dieses Problem zu umgehen, löschen Sie den Browser Cache.   [23824194]

- Das Remotedesktop Tool kann bei der Verwaltung von Windows Server 2012 möglicherweise keine Verbindung herstellen. [20258278]

- Wenn Sie die Remotedesktop zum Herstellen einer Verbindung mit einem Computer verwenden, der keiner Domäne beigetreten ist, müssen Sie Ihr Konto im ```MACHINENAME\USERNAME``` Format eingeben.

- Einige Konfigurationen können den Remote Desktop Client des Windows Admin Centers mit der Gruppenrichtlinie blockieren. Wenn dies auftritt, aktivieren Sie ```Allow users to connect remotely by using Remote Desktop Services``` unter ```Computer Configuration/Policies/Administrative Templates/Windows Components/Remote Desktop Services/Remote Desktop Session Host/Connections```

- Remotedesktop wird von der [WebSocket-Kompatibilität beeinflusst.](#websocket-compatibility-when-using-a-proxy-service)

- Das Tool Remotedesktop unterstützt derzeit weder Text, Bild oder Datei Kopieren/Einfügen zwischen dem lokalen Desktop und der Remotesitzung.

- Zum Kopieren/Einfügen innerhalb der Remotesitzung können Sie normal kopieren (Klicken + Kopieren oder STRG + C), das Einfügen erfordert Klick + Einfügen (STRG + V funktioniert nicht)

- Sie können die folgenden Befehle nicht an die Remotesitzung senden.
  - ALT+TAB
  - Funktionstasten
  - Windows-Taste
  - DRUCK

### <a name="roles-and-features"></a>Rollen und Features

- Bei der Auswahl von Rollen oder Funktionen mit nicht verfügbaren Quellen zur Installation, werden diese übersprungen. [12946914]

- Wenn Sie nach der Installation der Serverrollen nicht automatisch neu starten, wird nicht erneut gefragt. [13098852]

- Wenn Sie automatisch neu starten auswählen, wird der Neustart erfolgen, bevor der Status auf 100 % aktualisiert wird. [13098852]

### <a name="storage"></a>„Speicher“.

- Älter: DVD/CD/Diskettenlaufwerke werden nicht als Volumes angezeigt.

- Älter: Einige Eigenschaften in Volumes und Datenträgern sind nicht kompatible, und werden als unbekannt oder ein Leerzeichen im Detailbereich angezeigt.

- Älter: Beim Erstellen eines neuen Volumes unterstützt ReFS nur Zuordnungseinheiten mit 64K auf Windows 2012 und 2012 R2-Computern. Wenn ein Volume ReFS mit einer kleineren Zuordnungseinheit für ältere Ziele erstellt wird, schlägt die File System-Formatierung fehl. Das neue Volume kann nicht verwendet werden. Die Lösung besteht darin, das Volume zu löschen und Zuordnungseinheiten mit 64 KB zu verwenden.

### <a name="updates"></a>Updates

- Nach der Installation von Updates kann der Installationsstatus zwischengespeichert werden und eine Browser Aktualisierung erfordern.

- Bei dem Versuch, die Azure-Update Verwaltung einzurichten, wird möglicherweise der folgende Fehler angezeigt: "Keyset ist nicht vorhanden". Versuchen Sie in diesem Fall die folgenden Schritte zur Behebung auf dem verwalteten Knoten:
    1. Beendet den Dienst "Kryptografiedienste".
    2. Ändern Sie die Ordneroptionen, um ausgeblendete Dateien anzuzeigen (falls erforderlich).
    3. Sie haben den Ordner "%ALLUSERSPROFILE%\microsoft\crypto\rsa\s-1-5-18" erhalten, und löschen Sie den gesamten Inhalt.
    4. Starten Sie den Dienst "Kryptografiedienste" neu.
    5. Wiederholen der Einrichtung von Updateverwaltung mit dem Windows Admin Center

### <a name="virtual-machines"></a>Virtuelle Computer

- Beim Verwalten der virtuellen Computer auf einem Windows Server 2012-Host kann das in-Browser-VM-Verbindungs Tool keine Verbindung mit dem virtuellen Computer herstellen. Das Herunterladen der RDP-Datei, um eine Verbindung mit dem virtuellen Computer herzustellen, sollte weiterhin funktionieren. [20258278]

- Azure Site Recovery – Wenn ASR auf dem Host außerhalb von WAC eingerichtet ist, können Sie einen virtuellen Computer nicht innerhalb von WAC schützen [18972276]

- Erweiterte Funktionen in Hyper-V-Manager wie Virtual SAN-Manager, Move VM, Export VM und VM-Replikation werden derzeit nicht unterstützt.

### <a name="virtual-switches"></a>Virtuelle Switches

- Switch Embedded Teaming (SET): Beim Hinzufügen von Netzwerkschnittstellenkarten (NICs) zu einem Team müssen sie im gleichen Subnetz sein.

## <a name="computer-management-solution"></a>Computer-Management-Lösung

Die Computer-Management-Lösung enthält eine Teilmenge der Tools der Server-Manager-Lösung, daher sind die gleichen bekannten Probleme vorhanden, sowie die folgenden Computer Management-Lösungen für bestimmte Probleme:

- Wenn Sie ein Microsoft-Konto ([MSA](https://account.microsoft.com/account/)) verwenden oder Azure Active Directory (AAD) verwenden, um sich bei Ihrem Windows 10-Computer anzumelden, müssen Sie "Manage-as" verwenden, um Anmelde Informationen für ein lokales Administrator Konto anzugeben [16568455]

- Wenn Sie versuchen, den "localhost" zu verwalten, werden Sie aufgefordert, den Gateway-Prozess zu erhöhen. Wenn Sie im folgenden Popup Fenster "Benutzerkontensteuerung" auf **Nein** klicken, müssen Sie den Verbindungsversuch abbrechen und beginnen.

- Für Windows 10 ist standardmäßig kein WinRM-/PowerShell-Remoting aktiviert.
  
  - Um die Verwaltung des Windows 10-Clients zu ermöglichen, müssen Sie den Befehl ```Enable-PSRemoting``` aus einer PowerShell-Eingabeaufforderung mit erhöhten Rechten eingeben.

  - Sie müssen auch Ihre Firewall für Verbindungen von außerhalb des lokalen Subnetzes mit ```Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any``` aktualisieren. Restriktiver Netzwerke Szenarien finden Sie in [dieser Dokumentation](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enable-psremoting?view=powershell-5.1).

## <a name="failover-cluster-manager-solution"></a>Failovercluster-Manager-Lösung

- Wenn Sie einen Cluster verwalten (entweder hyperkonvergent oder herkömmlich) tritt möglicherweise der Fehler **shell was not found** auf. Laden Sie in diesem Fall entweder Ihren Browser erneut oder navigieren Sie zu einem anderen Tool und zurück. [13882442]

- Ein Problem kann auftreten, wenn Sie einen älteren Cluster verwalten (Windows Server 2012 oder 2012 R2), der nicht vollständig konfiguriert wurde. Die Fehlerbehebung für dieses Problem besteht darin, sicherzustellen, dass das Windows-Feature **RSAT-Clustering-PowerShell** installiert und auf **jedem Mitgliedsknoten** des Clusters aktiviert wurde. Um dies mit PowerShell auszuführen, geben Sie den Befehl `Install-WindowsFeature -Name RSAT-Clustering-PowerShell` auf den Clusterknoten an. [12524664]

- Cluster müssen möglicherweise über den gesamten FQDN hinzugefügt werden, um richtig erkannt zu werden.

- Bei der Verbindung mit einem Cluster mit Windows Admin Center als Gateway und beim Bereitstellen des expliziten Benutzernamens und Kennwort,um sich zu authentifizieren, müssen Sie **diese Anmeldeinformationen für alle Verbindungen verwenden** auswählen, damit die Anmeldeinformationen zum Abfragen des Mitgliedknotens verfügbar sind.

## <a name="hyper-converged-cluster-manager-solution"></a>Hyperkonvergente Cluster-Manager-Lösung

- Einige Befehle wie **Drives - Update firmware**, **Servers - Remove** und **Volumes - Open** sind nicht aktiviert und zur Zeit nicht verfügbar.

## <a name="azure-services"></a>Azure-Dienste

### <a name="azure-file-sync-permissions"></a>Azure-Dateisynchronisierung Berechtigungen

Azure-Dateisynchronisierung erfordert Berechtigungen in Azure, die von Windows Admin Center vor Version 1910 nicht bereitgestellt wurden. Wenn Sie Ihr Windows Admin Center-Gateway in Azure mit einer früheren Version als Windows Admin Center, Version 1910, registriert haben, müssen Sie Ihre Azure Active Directory Anwendung aktualisieren, um die richtigen Berechtigungen für die Verwendung Azure-Dateisynchronisierung in der neuesten Version von zu erhalten. Windows Admin Center. Mit der zusätzlichen Berechtigung können Azure-Dateisynchronisierung die automatische Konfiguration des Speicherkonto Zugriffs ausführen, wie in diesem Artikel beschrieben: [sicherstellen, dass Azure-Dateisynchronisierung Zugriff auf das Speicherkonto hat](https://docs.microsoft.com/azure/storage/files/storage-sync-files-troubleshoot?tabs=portal1%2Cazure-portal#tabpanel_CeZOj-G++Q-5_azure-portal).

Zum Aktualisieren Ihrer Azure Active Directory-App können Sie eine der beiden folgenden Aktionen ausführen:
1. Wechseln Sie zu **Einstellungen** > **Azure** > **Registrierung**aufheben, und registrieren Sie dann das Windows Admin Center erneut bei Azure, und stellen Sie sicher, dass Sie eine neue Azure Active Directory Anwendung erstellen. 
2. Wechseln Sie zu ihrer Azure Active Directory Anwendung, und fügen Sie die erforderliche Berechtigung manuell zu Ihrer vorhandenen Azure Active Directory-APP hinzu, die im Windows Admin Center registriert ist. Wechseln Sie hierzu zu **Einstellungen** > **Azure** > **Ansicht in Azure**. Navigieren Sie auf dem Blatt für die **App-Registrierung** in Azure zu **API-Berechtigungen**, und wählen Sie **Berechtigung hinzufügen**aus. Scrollen Sie nach unten, und wählen Sie **Azure Active Directory Graph**aus, wählen Sie **Delegierte Berechtigungen**und dann **Verzeichnis**, und wählen Sie **Directory. accessasuser. all**aus. Klicken Sie auf **Berechtigungen hinzufügen** , um die Updates für die APP zu speichern.

### <a name="options-for-setting-up-azure-management-services"></a>Optionen zum Einrichten von Azure-Verwaltungsdiensten

Azure-Verwaltungsdienste, einschließlich Azure Monitor, Azure Updateverwaltung und Azure Security Center, verwenden denselben Agent für einen lokalen Server: die Microsoft Monitoring Agent. Azure Updateverwaltung verfügt über eine begrenzte Anzahl von unterstützten Regionen und erfordert, dass der Arbeitsbereich Log Analytics mit einem Azure Automation Konto verknüpft ist. Wenn Sie im Windows Admin Center mehrere Dienste einrichten möchten, müssen Sie die Azure-Updateverwaltung zuerst einrichten und dann entweder Azure Security Center oder Azure Monitor. Wenn Sie Azure-Verwaltungsdienste konfiguriert haben, die die Microsoft Monitoring Agent verwenden, und dann versuchen, Azure Updateverwaltung mithilfe des Windows Admin Centers einzurichten, gestattet Ihnen Windows Admin Center nur das Konfigurieren von Azure Updateverwaltung, wenn die vorhandene Ressourcen, die mit dem Microsoft Monitoring Agent verknüpft sind, unterstützen Azure Updateverwaltung. Wenn dies nicht der Fall ist, haben Sie zwei Möglichkeiten:

1. Wechseln Sie zur Systemsteuerung > Microsoft Monitoring Agent, um [den Server von den vorhandenen Azure-Verwaltungslösungen](https://docs.microsoft.com/azure/azure-monitor/platform/log-faq#q-how-do-i-stop-an-agent-from-communicating-with-log-analytics) (wie Azure Monitor oder Azure Security Center) zu trennen. Richten Sie dann das Azure-Updateverwaltung im Windows Admin Center ein. Danach können Sie Ihre anderen Azure-Verwaltungslösungen ohne Probleme über das Windows Admin Center einrichten.
2. Sie können [die erforderlichen Azure-Ressourcen für Azure Updateverwaltung manuell einrichten](https://docs.microsoft.com/azure/automation/automation-update-management) und dann [die Microsoft Monitoring Agent](https://docs.microsoft.com/azure/azure-monitor/platform/agent-manage#adding-or-removing-a-workspace) (außerhalb des Windows Admin Centers) manuell aktualisieren, um den neuen Arbeitsbereich hinzuzufügen, der der Updateverwaltung Lösung entspricht, die Sie verwenden möchten.
