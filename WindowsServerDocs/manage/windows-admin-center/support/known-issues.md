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
ms.openlocfilehash: a579d0274ff4b53a72c17760a6d53ef796625d3a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356912"
---
# <a name="windows-admin-center-known-issues"></a>Windows Admin Center – bekannte Probleme

> Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Wenn Sie ein Problem haben, das auf dieser Seite nicht beschrieben ist, bitte [Teilen Sie uns dies mit](http://aka.ms/WACfeedback).

## <a name="lenovo-xclarity-integrator"></a>Lenovo xclarity Integrator

Das zuvor offengelegte Inkompatibilitäts Problem der Lenovo xclarity Integrator-Erweiterung und der Windows Admin Center-Version 1904 wurde nun mit Windows Admin Center, Version 1904,1, aufgelöst. Es wird dringend empfohlen, dass Sie ein Update auf die neueste unterstützte Version von Windows Admin Center durch haben.

- Die Lenovo xclarity Integrator-Erweiterungs Version 1,1 ist vollständig kompatibel mit Windows Admin Center 1904,1. Es wird dringend empfohlen, dass Sie ein Update auf die neueste Version von Windows Admin Center und die Lenovo-Erweiterung durch haben.
- Wenn Sie Windows Admin Center 1809,5 weiterhin verwenden müssen, können Sie aus irgendeinem Grund xclarity Integrator 1.0.4 verwenden, das auch im Windows Admin Center-Erweiterungs Feed verfügbar ist, bis Windows Admin Center 1809,5 nicht mehr unterstützt wird. unsere [Unterstützungs Richtlinie](../support/index.md).

## <a name="installer"></a>Installer

- Beim Installieren von Windows Admin Center mit einem eigenen Zertifikat, wenn Sie den Fingerabdruck aus dem Zertifikat-Manager-MMC-Tool kopieren, [enthält dieser ein ungültiges Zeichen am Anfang.](https://support.microsoft.com/help/2023835/certificate-thumbprint-displayed-in-mmc-certificate-snap-in-has-extra) Um dieses Problem zu umgehen, geben Sie das erste Zeichen des Fingerabdrucks ein und kopieren Sie den Rest.

- Die Verwendung von Port unter 1024 wird nicht unterstützt. Im Dienst Modus können Sie optional Port 80 für die Umleitung an den angegebenen Port konfigurieren.

- Wenn der Windows Update-Dienst (wuauserv) beendet und deaktiviert wird, kann das Installationsprogramm nicht ausgeführt werden. [19100629]

### <a name="upgrade"></a>Upgrade/Aktualisieren

- Wenn Sie das Windows Admin Center im Dienst Modus von einer früheren Version aktualisieren und msiexec im stillen Modus verwenden, tritt möglicherweise ein Problem auf, bei dem die eingehende Firewallregel für den Port des Windows Admin Centers gelöscht wird.
  - Zum erneuten Erstellen der Regel führen Sie den folgenden Befehl in einer PowerShell-Konsole mit \<erhöhten Rechten aus und ersetzen dabei Port > durch den Port, der für das Windows Admin Center konfiguriert ist (standardmäßig 443).

    ```powershell
    New-NetFirewallRule -DisplayName "SmeInboundOpenException" -Description "Windows Admin Center inbound port exception" -LocalPort <port> -RemoteAddress Any -Protocol TCP
    ```

## <a name="general"></a>Allgemein

- Wenn Sie Windows Admin Center als Gateway unter **Windows Server 2016** unter starker Verwendung installiert haben, stürzt der Dienst möglicherweise mit einem Fehler im Ereignisprotokoll ab, der ```Faulting application name: sme.exe``` und ```Faulting module name: WsmSvc.dll```enthält. Der Grund hierfür ist ein Fehler, der in Windows Server 2019 behoben wurde. Der Patch für Windows Server 2016 enthielt das kumulative Update vom Februar 2019, [KB4480977](https://www.catalog.update.microsoft.com/Search.aspx?q=4480977).

- Wenn Sie Windows Admin Center als Gateway installiert haben und die Verbindungsliste beschädigt erscheint, führen Sie die folgenden Schritte aus:

   > [!WARNING]
   >Hierdurch werden die Verbindungsliste und Einstellungen für alle Benutzer des Windows Admin Centers auf dem Gateway gelöscht.

  1. Deinstallieren Sie Windows Admin Center
  2. Löschen Sie den Ordner **Server Management Experience** unter **C:\Windows\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft**
  3. Installieren Sie Windows Admin Center erneut

- Wenn Sie das Tool für einen längeren Zeitraum geöffnet lassen und sich im Leerlauf befinden, werden möglicherweise **mehrere Fehler angezeigt: Der Runspace-Status ist für diese Vorgangs** Fehler ungültig. Aktualisieren Sie dann den Browser. Wenn dies der Meinung ist, [Senden Sie uns Feedback](http://aka.ms/WACfeedback).

- Ein **500 Fehler** kann auftreten, wenn Sie Seiten mit sehr langen URLs aktualisieren. [12443710]

- In einigen Tools kann die Rechtschreibprüfung Ihres Browsers bestimmte Feldwerte als falsch geschriebenen kennzeichnen. [12425477]

- In einigen Tools spiegeln Befehlsschaltflächen möglicherweise die Änderungen nicht unmittelbar nach einem Klick wieder, und die Tool-UI spiegelt möglicherweise nicht automatisch Änderungen an bestimmte Eigenschaften wider. Klicken Sie auf **Aktualisieren**, um den aktuellen Stand vom Zielserver abzurufen. [11445790]

- Tagfilterung in der Verbindungsliste: Wenn Sie mithilfe der Kontrollkästchen für Mehrfachauswahl Verbindungen auswählen und dann die Verbindungsliste nach Tags filtern, wird die ursprüngliche Auswahl beibehalten, sodass alle ausgewählten Aktionen auf alle zuvor ausgewählten Computer angewendet werden. [18099259]

- Möglicherweise gibt es eine geringfügige Abweichung zwischen den Versionsnummern von Betriebssystemen, die in den Modulen des Windows Admin Centers ausgeführt werden, und den im Software Hinweis eines Drittanbieters aufgeführten Betriebssystemen.

### <a name="extension-manager"></a>Erweiterungs-Manager

- Wenn Sie das Windows Admin Center aktualisieren, müssen Sie die Erweiterungen neu installieren.
- Wenn Sie einen Erweiterungs Feed hinzufügen, auf den nicht zugegriffen werden kann, wird keine Warnung angezeigt. [14412861]

## <a name="browser-specific-issues"></a>Bestimmte Browserprobleme

### <a name="microsoft-edge"></a>Microsoft Edge

- In einigen Fällen gibt es möglicherweise lange Ladezeiten, wenn Sie Microsoft Edge verwenden, wenn Sie auf ein Windows Admin Center-Gateway über das Internet zugreifen. Dies kann auf virtuellen Azure-Computern auftreten, auf dem das Windows Admin Center Gateway ein selbstsigniertes Zertifikat verwendet wird. [13819912]

- Wenn Sie AAD als Identitätsanbieter verwenden und Windows Admin Center mit einem selbstsignierten oder nicht vertrauenswürdigen Zertifikat konfiguriert ist, kann die Authentifizierung AAD in Microsoft Edge nicht abschließen.  [15968377]

- Wenn Sie das Windows Admin Center als Dienst bereitgestellt haben und Microsoft Edge als Browser verwenden, kann das Verbinden Ihres Gateways mit Azure nach dem Auslösen eines neuen Browserfensters fehlschlagen. Versuchen Sie, dieses Problem zu umgehen, https://login.microsoftonline.com indem https://login.live.com Sie, und die URL Ihres Gateways als vertrauenswürdige Sites und zulässige Websites für die Popup Blocker Einstellungen in Ihrem Client seitigen Browser hinzufügen. Weitere Anleitungen zur Behebung dieses Problem finden Sie im [Handbuch zur Problem](troubleshooting.md#azure-features-dont-work-properly-in-edge)Behandlung. [17990376]

- Wenn Sie das Windows Admin Center im Desktop Modus installiert haben, wird die Favicon auf der Registerkarte Browser in Microsoft Edge nicht angezeigt. [17665801]

### <a name="google-chrome"></a>Google Chrome

- Vor Version 70 (veröffentlicht am Ende Oktober, 2018) gab es einen [Fehler](https://bugs.chromium.org/p/chromium/issues/detail?id=423609) im Zusammenhang mit dem websockets-Protokoll und der NTLM-Authentifizierung. Dies hat Auswirkungen auf die folgenden Tools: Ereignisse, PowerShell, Remotedesktop.

- Chrome zeigt eventuell mehrere Anmeldeinformationen an, vor allem in Zeiten der Verbindungsprozesse in einer **Arbeitsgruppen**-Umgebung (nicht der Domäne).

- Wenn Sie das Windows Admin Center als Dienst bereitgestellt haben, müssen Popups von der Gateway-URL aktiviert werden, damit alle Azure-Integrationsfunktionen funktionieren. Zu diesen Diensten gehören der Azure-Netzwerk Adapter, Azure Updateverwaltung und Azure Site Recovery.

### <a name="mozilla-firefox"></a>Mozilla Firefox

Windows Admin Center wurde nicht mit Mozilla Firefox getestet, aber die meisten Funktionen sollten funktionieren.

- Windows 10-Installation: Mozilla Firefox verfügt über einen eigenen Zertifikat Speicher, deshalb müssen Sie das ```Windows Admin Center Client``` Zertifikat in Firefox importieren, um Windows Admin Center unter Windows 10 zu verwenden.

## <a name="websocket-compatibility-when-using-a-proxy-service"></a>WebSocket-Kompatibilität bei Verwendung eines Proxy Dienstanbieter

Remotedesktop, PowerShell und Ereignismodule im Windows Admin Center nutzen das WebSocket-Protokoll, das häufig nicht unterstützt wird, wenn ein Proxydienst verwendet wird. WebSocket unterstützt Azure AD-Anwendungsproxy-Kompatibilität in der [Vorschau](https://blogs.technet.microsoft.com/applicationproxyblog/2018/03/28/limited-websocket-support-now-in-public-preview/) und sucht nach Feedback zur Kompatibilität.

## <a name="support-for-windows-server-versions-before-2016-2012-r2-2012-2008-r2"></a>Unterstützung für Windows Server-Versionen vor 2016 (2012 R2, 2012, 2008 R2)

> [!NOTE]
> Windows Admin Center erfordert PowerShell-Features, die nicht in Windows Server 2012 R2, 2012 oder 2008 R2 enthalten sind. Wenn Sie Windows Server mit dem Windows Admin Center verwalten, müssen Sie WMF Version 5,1 oder höher auf diesen Servern installieren.

Geben Sie `$PSVersiontable` in PowerShell ein, um zu prüfen, ob WMF 5.1 oder einen neuere Version installiert ist.

Wenn dies nicht der Fall ist, können Sie [herunterladen und WMF 5.1 installieren](https://www.microsoft.com/en-us/download/details.aspx?id=54616).

## <a name="role-based-access-control-rbac"></a>Rollenbasierte Access Control (RBAC)

- RBAC-Bereitstellung ist auf Computern, die für die Windows Defender-Anwendungssteuerung (WDAC, früher als Integrität des Codes bezeichnet) konfiguriert werden, nicht erfolgreich [16568455]

- Um RBAC in einem Cluster verwenden, müssen Sie die Konfiguration für jeden Memberknoten einzeln bereitstellen.

- Wenn RBAC bereitgestellt wird, können Sie unauthorized-Fehler erhalten, die nicht ordnungsgemäß an der RBAC-Konfiguration Ergebnisarray als Attribut zugewiesen werden. [16369238]

## <a name="server-manager-solution"></a>Server-Manager-Lösung

### <a name="server-settings"></a>Server Einstellungen

- Wenn Sie eine Einstellung ändern und dann versuchen, ohne speichern zu navigieren, werden Sie von der Seite vor den nicht gespeicherten Änderungen gewarnt, aber fahren Sie fort. Möglicherweise wird ein Status angezeigt, in dem die ausgewählte Registerkarte "Einstellungen" nicht mit dem Inhalt der Seite identisch ist. [19905798] [19905787]

### <a name="certificates"></a>Zertifikate

- Kann nicht importiert werden. PFX verschlüsselt Zertifikat im Speicher des aktuellen Benutzers. [11818622]

### <a name="devices"></a>Geräte

- Wenn Sie durch die Tabelle mit der Tastatur navigieren, springt die Auswahl möglicherweise zum Anfang der Tabellen Gruppe. [16646059]

### <a name="events"></a>Ereignisse

- Ereignisse erfolgen durch [Websocket-Kompatibilität bei Verwendung eines Proxydiensts.](#websocket-compatibility-when-using-a-proxy-service)

- Möglicherweise erhalten Sie die Fehlermeldung "Packet Size" beim Exportieren von großen Protokolldateien. [16630279]

  - Um dieses Problem zu beheben, verwenden Sie den folgenden Befehl an einer Eingabeaufforderung mit erhöhten Rechten auf dem Gatewaycomputer:```winrm set winrm/config @{MaxEnvelopeSizekb="8192"}```

### <a name="files"></a>Dateien

- Hoch- oder heruntergeladen großer Dateien wird noch nicht unterstützt. (\~100mb Limit) [12524234]

### <a name="powershell"></a>PowerShell

- PowerShell erfolgt durch [Websocket-Kompatibilität bei Verwendung eines Proxydiensts](#websocket-compatibility-when-using-a-proxy-service)

- Das Einfügen mit einem einzelnen Klick mit der rechten Maustaste wie in der Desktop PowerShell-Konsole ist nicht funktionsfähig. Stattdessen erhalten Sie Kontextmenüs des Browsers, in dem Sie „einfügen” auswählen können. STRG + V funktioniert auch.

- STRG + C kann nicht zum Kopieren verwendet werden, es sendet immer den Befehl STRG + C an die Konsole. Das Kopieren über das mit der rechten Maustaste aufgerufenen Kontextmenü funktioniert.

- Wenn Sie das Windows Admin Center-Fenster kleiner machen, wird der Terminalinhalt umgeleitet, aber wenn Sie es erneut vergrößern, kann der Inhalt nicht in den vorherigen Zustand zurückkehren. Wenn Dinge durcheinander geraten, können Sie Clear-Host verwenden, oder die Verbindung trennen und erneut eine Verbindung mit der Schaltfläche oberhalb des Terminaldienstes herstellen.

### <a name="registry-editor"></a>Registrierungs-Editor

- Die Suchfunktion ist nicht implementiert. [13820009]

### <a name="remote-desktop"></a>Remotedesktop

- Das Remotedesktop Tool kann bei der Verwaltung von Windows Server 2012 möglicherweise keine Verbindung herstellen. [20258278]

- Wenn Sie die Remotedesktop zum Herstellen einer Verbindung mit einem Computer verwenden, der keiner Domäne beigetreten ist, müssen Sie ```MACHINENAME\USERNAME``` Ihr Konto im Format eingeben.

- Einige Konfigurationen können den Remote Desktop Client des Windows Admin Centers mit der Gruppenrichtlinie blockieren. Wenn dies der gibt, aktivieren ```Allow users to connect remotely by using Remote Desktop Services``` Sie unter```Computer Configuration/Policies/Administrative Templates/Windows Components/Remote Desktop Services/Remote Desktop Session Host/Connections```

- Remotedesktop wird von der [WebSocket-Kompatibilität beeinflusst.](#websocket-compatibility-when-using-a-proxy-service)

- Das Tool Remotedesktop unterstützt derzeit weder Text, Bild oder Datei Kopieren/Einfügen zwischen dem lokalen Desktop und der Remotesitzung.

- Zum Kopieren/Einfügen innerhalb der Remotesitzung können Sie normal kopieren (Klicken + Kopieren oder STRG + C), das Einfügen erfordert Klick + Einfügen (STRG + V funktioniert nicht)

- Sie können die folgenden Befehle nicht an die Remotesitzung senden.
  - ALT+TAB
  - Funktionstasten
  - Windows-Taste
  - DRUCK

- Remote-app – nachdem Sie das Remote-app-Tool aus Remotedesktop Einstellungen aktiviert haben, wird das Tool möglicherweise nicht in der Toolliste angezeigt, wenn ein Server mit Desktop Darstellung verwaltet wird. [18906904]

### <a name="roles-and-features"></a>Rollen und Features

- Bei der Auswahl von Rollen oder Funktionen mit nicht verfügbaren Quellen zur Installation, werden diese übersprungen. [12946914]

- Wenn Sie nach der Installation der Serverrollen nicht automatisch neu starten, wird nicht erneut gefragt. [13098852]

- Wenn Sie automatisch neu starten auswählen, wird der Neustart erfolgen, bevor der Status auf 100 % aktualisiert wird. [13098852]

### <a name="storage"></a>Speicher

- Das Abrufen von Kontingent Informationen schlägt möglicherweise fehl, ohne dass eine Fehler Benachrichtigung vorliegt (in der Browser Konsole wird weiterhin ein Fehler angezeigt) [18962274]

- Herabstufen: DVD/CD/Diskettenlaufwerke werden nicht als Volumes auf untergeordneten Ebenen angezeigt.

- Herabstufen: Einige Eigenschaften in Volumes und Datenträgern sind nicht im Detailbereich als "unbekannt" oder "leer" verfügbar.

- Herabstufen: Wenn Sie ein neues Volume erstellen, unterstützt Refs nur die Größe der Zuordnungs Einheiten von 64 KB auf Computern mit Windows 2012 und 2012 R2. Wenn ein Volume ReFS mit einer kleineren Zuordnungseinheit für ältere Ziele erstellt wird, schlägt die File System-Formatierung fehl. Das neue Volume kann nicht verwendet werden. Die Lösung besteht darin, das Volume zu löschen und Zuordnungseinheiten mit 64 KB zu verwenden.

### <a name="updates"></a>Updates

- Nach der Installation von Updates kann der Installationsstatus zwischengespeichert werden und eine Browser Aktualisierung erfordern.

- Möglicherweise wird der folgende Fehler angezeigt: "Keyset ist nicht vorhanden" beim Versuch, die Azure-Update Verwaltung einzurichten. Versuchen Sie in diesem Fall die folgenden Schritte zur Behebung auf dem verwalteten Knoten:
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

- Switch Embedded Teaming (Set): Beim Hinzufügen von NICs zu einem Team müssen Sie sich im selben Subnetz befinden.

## <a name="computer-management-solution"></a>Computer-Management-Lösung

Die Computer-Management-Lösung enthält eine Teilmenge der Tools der Server-Manager-Lösung, daher sind die gleichen bekannten Probleme vorhanden, sowie die folgenden Computer Management-Lösungen für bestimmte Probleme:

- Wenn Sie ein Microsoft-Konto ([MSA](https://account.microsoft.com/account/)) verwenden oder Azure Active Directory (AAD) verwenden, um sich bei Ihrem Windows 10-Computer anzumelden, müssen Sie die Anmelde Informationen für die Verwaltung des lokalen Computers angeben. [16568455]

- Wenn Sie versuchen, den "localhost" zu verwalten, werden Sie aufgefordert, den Gateway-Prozess zu erhöhen. Wenn Sie **Nein** im folgenden Benutzerkontensteuerungsfenster anklicken, kann Windows Admin Center dies nicht erneut anzeigen. Beenden Sie in diesem Fall den Gateway-Prozess, indem Sie das Windows Admin Center-Symbol in der Taskleiste mit der rechten Maustaste anklicken, und beenden wählen. Starten Sie Windows Admin Center im Startmenü dann erneut.

- Auf Windows 10 ist WinRM/PowerShell-Remoting standardmäßig nicht vorhanden
  
  - Um die Verwaltung des Windows 10-Clients zu ermöglichen, müssen Sie den Befehl ```Enable-PSRemoting``` aus einer PowerShell-Eingabeaufforderung mit erhöhten Rechten eingeben.

  - Sie müssen auch Ihre Firewall für Verbindungen von außerhalb des lokalen Subnetzes mit ```Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any``` aktualisieren. Restriktiver Netzwerke Szenarien finden Sie in [dieser Dokumentation](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enable-psremoting?view=powershell-5.1).

## <a name="failover-cluster-manager-solution"></a>Failovercluster-Manager-Lösung

- Wenn Sie einen Cluster verwalten (entweder hyperkonvergent oder herkömmlich) tritt möglicherweise der Fehler **shell was not found** auf. Laden Sie in diesem Fall entweder Ihren Browser erneut oder navigieren Sie zu einem anderen Tool und zurück. [13882442]

- Ein Problem kann auftreten, wenn Sie einen älteren Cluster verwalten (Windows Server 2012 oder 2012 R2), der nicht vollständig konfiguriert wurde. Die Fehlerbehebung für dieses Problem besteht darin, sicherzustellen, dass das Windows-Feature **RSAT-Clustering-PowerShell** installiert und auf **jedem Mitgliedsknoten** des Clusters aktiviert wurde. Um dies mit PowerShell auszuführen, geben Sie den Befehl `Install-WindowsFeature -Name RSAT-Windows-PowerShell` auf den Clusterknoten an. [12524664]

- Cluster müssen möglicherweise über den gesamten FQDN hinzugefügt werden, um richtig erkannt zu werden.

- Bei der Verbindung mit einem Cluster mit Windows Admin Center als Gateway und beim Bereitstellen des expliziten Benutzernamens und Kennwort,um sich zu authentifizieren, müssen Sie **diese Anmeldeinformationen für alle Verbindungen verwenden** auswählen, damit die Anmeldeinformationen zum Abfragen des Mitgliedknotens verfügbar sind.

## <a name="hyper-converged-cluster-manager-solution"></a>Hyperkonvergente Cluster-Manager-Lösung

- Einige Befehle wie **Drives - Update firmware**, **Servers - Remove** und **Volumes - Open** sind nicht aktiviert und zur Zeit nicht verfügbar.