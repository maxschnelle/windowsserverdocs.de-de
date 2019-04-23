---
title: Verwalten von Server Core
description: Informationen Sie zum Verwalten einer Server Core-Installations von Windows Server
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: 6836e5db36727294d215f7f98e0faeede55a612a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869301"
---
# <a name="manage-a-server-core-server"></a>Verwalten eines Server Core-Servers
 
> Gilt für: WindowsServer (Halbjährlicher Kanal) und WindowsServer 2016

Sie können einen Server Core-Server auf folgende Weise verwalten:
- Mithilfe von [Windows Admin Center](../../manage/windows-admin-center/overview.md)
- Mithilfe von [Remoteserver-Verwaltungstools](../../remote/remote-server-administration-tools.md) auf Windows 10 ausgeführt wird
- Lokal und remote mit Windows PowerShell
- Remote mit [Server-Manager](../server-manager/server-manager.md)
- Remote mit einem [MMC-Snap-in](#managing-with-microsoft-management-console)
- Remote mit [Remote Desktop Services](#managing-with-remote-desktop-services)

Sie können auch Hinzufügen von Hardware und Treiber lokal verwalten, solange Sie über die Befehlszeile dies.

Es gibt einige wichtige Einschränkungen und Tipps zu bedenken, bei der Arbeit mit Server Core:

- Wenn Sie alle Fenster der Eingabeaufforderung zu schließen und ein neues Eingabeaufforderungsfenster geöffnet werden soll, können Sie dies aus dem Task-Manager tun. Drücken Sie **STRG\+ALT\+löschen**, klicken Sie auf **Task-Manager starten**, klicken Sie auf **Weitere Details > Datei > Führen Sie**, und geben Sie dann  **cmd.exe**. (Typ **Powershell.exe** um ein PowerShell-Befehlsfenster zu öffnen.) Alternativ können Sie abmelden und dann wieder anmelden.
- Befehle oder Tools, die versuchen, Windows Explorer zu öffnen, funktionieren nicht. Z. B. Ausführung **starten.** von einer Befehlszeile aus funktioniert nicht.
- Es gibt keine Unterstützung für HTML-Rendering oder HTML-Hilfe im Server Core.
- Server Core unterstützt Windows Installer im stillen Modus, sodass Sie Tools und Dienstprogramme von Windows Installer-Dateien installieren können. Wenn Sie Windows Installer-Pakete auf Server Core installieren möchten, verwenden die **/qb** Option, um die Standardbenutzeroberfläche anzuzeigen.
- Führen Sie zum Ändern der Zeitzone **Set-Date**.
- Um die gebietsschemaeinstellungen zu ändern, führen **steuern "Intl.cpl"**.
- **Control.exe** wird nicht eigenständig ausgeführt. Sie müssen diese ausführen, entweder mit **"timedate.cpl"** oder **Intl.cpl**.
- **Winver.exe** ist in Server Core nicht verfügbar. Zum Abrufen von Informationen verwenden von Version **Systeminfo.exe**.

## <a name="managing-server-core-with-windows-admin-center"></a>Verwalten von Server-Core mit Windows Admin Center
[Windows Admin Center](../../manage/windows-admin-center/overview.md) ist eine browserbasierte Management-App, die die lokale Verwaltung von Windows-Servern ohne Abhängigkeit von Azure oder der Cloud ermöglicht. Windows Admin Center ermöglicht die vollständige Kontrolle über alle Aspekte der Server-Infrastruktur und ist besonders nützlich für die Verwaltung auf privaten Netzwerken, die nicht mit dem Internet verbunden sind. Sie können Windows Admin Center zu installieren, auf Windows 10, auf einem Gatewayserver oder in einer Installation von Windows Server mit Desktopdarstellung und verbinden Sie dann mit dem Server Core-System, das Sie verwalten möchten.

## <a name="managing-server-core-remotely-with-server-manager"></a>Verwalten von Server Core Remote mit Server-Manager

Server-Manager ist eine Verwaltungskonsole in Windows Server, mit dem Sie das Bereitstellen und Verwalten von sowohl lokale als auch Windows-basierten Servern über Ihre Desktops, ohne dass Sie physischen Zugriff auf den Server, oder die Notwendigkeit, Remote Desktop Protocol (RDP) aktivieren Verbindungen zu den einzelnen Servern. Server-Manager unterstützt die Verwaltung von Remoteunterstützung.

Um Ihr lokaler Server mit Server-Manager auf einem Remoteserver verwaltet werden zu aktivieren, führen Sie das Windows PowerShell-Cmdlet **Configure-SMRemoting.exe-aktivieren**.

## <a name="managing-with-microsoft-management-console"></a>Verwalten von mit Microsoft Management Console

Sie können viele-Snap-ins für Microsoft Management Console (MMC) Remote verwenden, um Ihren Server Core-Server verwalten.

So verwenden einen Server Core-Server zu verwalten, der Mitglied einer Domäne ist ein MMC-Snap-in: 

1. Starten Sie ein MMC-Snap-in, z. B. Computerverwaltung.
2. Mit der rechten Maustaste das Snap-in, und klicken Sie dann auf **Herstellen einer Verbindung mit einem anderen Computer**.
2. Geben Sie den Namen des Server Core-Server, und klicken Sie dann auf **OK**. Sie können jetzt das MMC-Snap-in verwenden, um die Server Core-Server zu verwalten, wie alle anderen PC oder Server.

Ein MMC-Snap-in verwenden, um eine Server Core-Server zu verwalten, ist *nicht* Mitglied einer Domäne: 

1. Richten Sie alternative Anmeldeinformationen zur verbindungsherstellung mit dem Server Core-Computer den folgenden Befehl an einer Eingabeaufforderung auf dem Remotecomputer eingeben:
   ```
   cmdkey /add:<ServerName> /user:<UserName> /pass:<password>
   ```
   Wenn Sie nach einem Kennwort gefragt werden möchten, lassen Sie die **/pass** Option.

2. Geben Sie bei entsprechender Aufforderung das Kennwort für den Benutzernamen ein, die, den Sie angegeben haben.
   Wenn die Firewall auf dem Server Core-Server zum MMC-Snap-ins eine Verbindung herstellen dürfen nicht bereits konfiguriert ist, führen Sie die folgenden Schritte zum Konfigurieren der Windows-Firewall, damit MMC-Snap-in. Fahren Sie mit Schritt 3.
3. Auf einem anderen Computer, starten Sie ein MMC-Snap-in, z. B. **Computerverwaltung**.
4. Klicken Sie im linken Bereich mit der rechten Maustaste das Snap-in, und klicken Sie dann auf **Herstellen einer Verbindung mit einem anderen Computer**. (Z. B. in der Computerverwaltung beispielsweise Sie würde mit der rechten Maustaste **Computerverwaltung (lokal)**.)
5. In **einem anderen Computer**, geben Sie den Namen des Server Core-Server, und klicken Sie dann auf **OK**. Sie können nun mit dem MMC-Snap-In den Server im Server-Core-Server wie jeden anderen Computer mit einem Windows-Betriebssystem verwalten.

### <a name="to-configure-windows-firewall-to-allow-mmc-snap-ins-to-connect"></a>So konfigurieren Sie die Windows-Firewall so, dass MMC-Snap-Ins eine Verbindung herstellen dürfen
Damit um alle MMC-Snap-ins eine Verbindung herstellen zu können, führen Sie den folgenden Befehl aus:

```
Enable-NetFirewallRule -DisplayGroup "Remote Administration"
```

Damit um nur bestimmte MMC-Snap-ins eine Verbindung herstellen zu können, führen Sie die folgenden Schritte aus:
```
Enable-NetFirewallRule -DisplayGroup "<rulegroup>"
```

Wo *Rulegroup* ist eine der folgenden Einträge, je nachdem, welche-Snap-in Sie eine Verbindung herstellen möchten:

| MMC-Snap-In                            | Regelgruppe                                            |
|----------------------------------------|-------------------------------------------------------|
| Ereignisanzeige                           | Remote-Ereignisprotokollverwaltung                           |
| Dienste                               | Remotedienstverwaltung                             |
| Freigegebene Ordner                         | Datei- und Druckerfreigabe                              |
| Aufgabenplanung                         | Leistungsprotokolle und Warnungen, die Datei- und Druckerfreigabe |
| Datenträgerverwaltung                        | Remotevolumeverwaltung                              |
| Windows-Firewall- und erweiterte Sicherheit | Windows-Firewallremoteverwaltung                    |


> [!NOTE] 
> Einige MMC-Snap-ins haben keine entsprechende Regelgruppe, die sie über die Firewall eine Verbindung herstellen können. Doch das Aktivieren der Regelgruppen für "Ereignisanzeige", "Dienste" oder "Freigegebene Ordner" können die meisten anderen Snap-Ins eine Verbindung herstellen. 
>
> Darüber hinaus benötigen bestimmte Snap-Ins eine weitere Konfiguration, ehe Sie durch die Windows-Firewall eine Verbindung herstellen können:
>
> - Datenträgerverwaltung. Sie müssen auf dem Server-Core-Computer zunächst den Dienst für virtuelle Datenträger (Virtual Disk Service, VDS) starten. Außerdem müssen Sie Regeln zur Datenträgerverwaltung auf dem Computer, auf dem das MMC-Snap-In ausgeführt wird, entsprechend konfigurieren.
> - IP-Sicherheitsmonitor. Sie müssen zunächst die Remoteverwaltung dieses Snap-Ins aktivieren. Geben Sie dazu an einer Eingabeaufforderung **Cscript \windows\system32\scregedit.wsf /im 1**
> - Zuverlässigkeits- und Leistungsüberwachung. Dieses Snap-In erfordert keine weitere Konfiguration, doch wenn Sie mit ihm einen Server-Core-Computer überwachen, können nur Leistungsdaten überwacht werden. Zuverlässigkeitsdaten sind nicht verfügbar.

## <a name="managing-with-remote-desktop-services"></a>Verwalten mit Remotedesktopdienste

Sie können [Remotedesktop](../../remote/remote-desktop-services/welcome-to-rds.md) zum Verwalten eines Server Core-Servers von Remotecomputern.

Bevor Sie die Server Core zugreifen können, müssen Sie den folgenden Befehl ausführen: 
```
cscript C:\Windows\System32\Scregedit.wsf /ar 0
```
Dadurch wird der Remotedesktop für den Verwaltungsmodus zum Akzeptieren von Verbindungen aktiviert.

## <a name="add-hardware-and-manage-drivers-locally"></a>Hinzufügen von Hardware und Treiber lokal verwalten

Um die Hardware mit einem Server Core-Server hinzuzufügen, befolgen Sie die Anweisungen, die vom Hardwarehersteller zur Installation neuer Hardware aus. 

Wenn die Hardware nicht Plug & Play ist, müssen Sie die Treiber manuell installieren. Hierzu kopieren Sie die Treiberdateien in einen temporären Speicherort auf dem Server, und führen Sie dann den folgenden Befehl aus:
```
pnputil –i –a <driverinf>
```
Wo *Driverinf* ist der Dateiname der INF-Datei für den Treiber.

Starten Sie den Computer bei entsprechender Aufforderung neu.

Um anzuzeigen, welche Treiber installiert sind, führen Sie den folgenden Befehl aus: 
```
sc query type= driver
```

> [!NOTE] 
> Sie müssen hinter dem Gleichheitszeichen ein Leerzeichen einfügen, damit der Befehl erfolgreich ausgeführt werden kann.

Um einen Gerätetreiber zu deaktivieren, führen Sie die folgenden Schritte aus: 
```
sc delete <service_name>
```

In denen *Service_name* ist der Name des Diensts, den Sie abgerufen haben, bei der Ausführung **Abfragetyp sc = Treiber**.