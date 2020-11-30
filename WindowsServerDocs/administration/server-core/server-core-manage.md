---
title: Verwalten von Server Core
description: Erfahren Sie, wie Sie eine Server Core-Installation von Windows Server verwalten.
ms.mktglfcycl: manage
ms.sitesec: library
author: pronichkin
ms.author: artemp
ms.localizationpriority: medium
ms.date: 07/23/2019
ms.openlocfilehash: 754211824208e582382cb9c6ad196483c6506708
ms.sourcegitcommit: 3181fcb69a368f38e0d66002e8bc6fd9628b1acc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/30/2020
ms.locfileid: "96330376"
---
# <a name="manage-a-server-core-server"></a>Verwalten eines Server Core-Servers
 
> Gilt für: Windows Server 2019, Windows Server 2016 und Windows Server (halbjährlicher Kanal)

Sie können einen Server Core-Server wie folgt verwalten:
- Verwenden des [Windows Admin Centers](../../manage/windows-admin-center/overview.md)
- Verwenden von [Remoteserver-Verwaltungstools](../../remote/remote-server-administration-tools.md) , die unter Windows 10 ausgeführt werden
- Lokal und remote mit Windows PowerShell
- Remote Verwendung [Server-Manager](../server-manager/server-manager.md)
- Remote mit einem [MMC-Snap-in](#managing-with-microsoft-management-console)
- Remote mit [Remotedesktopdienste](#managing-with-remote-desktop-services)

Sie können auch Hardware hinzufügen und Treiber lokal verwalten, solange Sie dies über die Befehlszeile ausführen.

Beim Arbeiten mit Server Core sind einige wichtige Einschränkungen und Tipps zu beachten:

- Wenn Sie alle Eingabe Aufforderungs Fenster schließen und ein neues Eingabe Aufforderungs Fenster öffnen möchten, können Sie dies über den Task-Manager tun. Drücken Sie **STRG \+ alt \+** ENTF, klicken Sie auf **Task-Manager starten**, klicken Sie auf **Weitere Details > Datei > ausführen**, und geben Sie dann **cmd.exe** ein. (Geben Sie **Powershell.exe** ein, um ein PowerShell-Befehlsfenster zu öffnen.) Alternativ können Sie sich abmelden und dann wieder anmelden.
- Befehle oder Tools, die versuchen, Windows Explorer zu öffnen, funktionieren nicht. Beispiel: Ausführung von **starten.** an einer Eingabeaufforderung funktioniert nicht.
- Das HTML-Rendering oder die HTML-Hilfe in Server Core wird nicht unterstützt.
- Server Core unterstützt Windows Installer im stillen Modus, sodass Sie Tools und Hilfsprogramme aus Windows Installer Dateien installieren können. Verwenden Sie bei der Installation von Windows Installer-Paketen auf Server Core die **/qb** -Option, um die grundlegende Benutzeroberfläche anzuzeigen.
- Um die Zeitzone zu ändern, führen Sie **Set-Date** aus.
- Um internationale Einstellungen zu ändern, führen Sie die **Steuerelement intl.cpl** aus.
- **Control.exe** werden nicht selbst ausgeführt. Sie müssen ihn entweder mit **Timedate.cpl** oder **Intl.cpl** ausführen.
- **Winver.exe** ist in Server Core nicht verfügbar. Verwenden Sie zum Abrufen von Versionsinformationen **Systeminfo.exe**.

## <a name="managing-server-core-with-windows-admin-center"></a>Verwalten von Server Core mit Windows Admin Center
[Windows Admin Center](../../manage/windows-admin-center/overview.md) ist eine browserbasierte Verwaltungs-APP, die die lokale Verwaltung von Windows-Servern ohne Azure-oder cloudabhängigkeit ermöglicht. Das Windows Admin Center bietet Ihnen vollständige Kontrolle über alle Aspekte Ihrer Serverinfrastruktur und ist besonders nützlich für die Verwaltung von privaten Netzwerken, die nicht mit dem Internet verbunden sind. Sie können Windows Admin Center unter Windows 10, auf einem Gatewayserver oder auf einer Installation von Windows Server mit Desktop Darstellung installieren und dann eine Verbindung mit dem Server Core-System herstellen, das Sie verwalten möchten.

## <a name="managing-server-core-remotely-with-server-manager"></a>Remote Verwaltung von Server Core mit Server-Manager

Server-Manager ist eine Verwaltungskonsole in Windows Server, mit der Sie sowohl lokale als auch Remote-Windows-basierte Server von ihren Desktops aus bereitstellen und verwalten können, ohne dass Sie physischen Zugriff auf die Server benötigen oder RDP-Verbindungen (Remotedesktop Protocol) zu jedem Server aktivieren müssen. Server-Manager unterstützt die Remote Verwaltung von mehreren Servern.

Damit Ihr lokaler Server durch Server-Manager auf einem Remote Server verwaltet werden kann, führen Sie das Windows PowerShell-Cmdlet **Configure-SMRemoting.exe – enable** aus.

## <a name="managing-with-microsoft-management-console"></a>Verwalten mit Microsoft Management Console

Sie können viele Snap-Ins für Microsoft Management Console (MMC) Remote verwenden, um Ihren Server Core-Server zu verwalten.

So verwenden Sie ein MMC-Snap-in zum Verwalten eines Server Core-Servers, der ein Domänen Mitglied ist:

1. Starten Sie ein MMC-Snap-In, z. B. Computerverwaltung.
2. Klicken Sie mit der rechten Maustaste auf das Snap-in, und klicken Sie dann **auf Verbindung mit anderem Computer herstellen**.
2. Geben Sie den Computernamen des Server Core-Servers ein, und klicken Sie dann auf **OK**. Nun können Sie das MMC-Snap-in verwenden, um den Server Core-Server wie jeden anderen PC oder Server zu verwalten.

So verwenden Sie ein MMC-Snap-in zum Verwalten eines Server Core-Servers, der *kein* Domänen Mitglied ist:

1. Richten Sie alternative Anmelde Informationen für die Verbindung mit dem Server Core-Computer ein, indem Sie den folgenden Befehl an einer Eingabeaufforderung auf dem Remote Computer eingeben:

   ```
   cmdkey /add:<ServerName> /user:<UserName> /pass:<password>
   ```

   Wenn Sie zur Eingabe eines Kennworts aufgefordert werden möchten, lassen Sie die Option **/Pass** aus.

2. Wenn Sie dazu aufgefordert werden, geben Sie das Kennwort für den angegebenen Benutzernamen ein.
   Wenn die Firewall auf dem Server-Core-Server nicht bereits so konfiguriert ist, dass MMC-Snap-Ins eine Verbindung herstellen können, führen Sie die folgenden Schritte aus, um die Windows-Firewall so zu konfigurieren, dass das MMC- Fahren Sie anschließend mit Schritt 3 fort.
3. Starten Sie auf einem anderen Computer ein MMC-Snap-in, z. b. **Computer Verwaltung**.
4. Klicken Sie im linken Bereich mit der rechten Maustaste auf das Snap-in, und klicken Sie dann auf **Verbindung mit anderem Computer herstellen**. (Beispiel: im Beispiel Computer Verwaltung klicken Sie mit der rechten Maustaste auf **Computer Verwaltung (lokal)**.)
5. Geben Sie auf **einem anderen Computer** den Computernamen des Server Core-Servers ein, und klicken Sie dann auf **OK**. Sie können nun mit dem MMC-Snap-In den Server im Server-Core-Server wie jeden anderen Computer mit einem Windows-Betriebssystem verwalten.

### <a name="to-configure-windows-firewall-to-allow-mmc-snap-ins-to-connect"></a>So konfigurieren Sie die Windows-Firewall so, dass MMC-Snap-Ins eine Verbindung herstellen dürfen
Damit alle MMC-Snap-Ins eine Verbindung herstellen können, führen Sie den folgenden Befehl aus:

```PowerShell
Enable-NetFirewallRule -DisplayGroup "Windows Remote Management"
```

Damit nur bestimmte MMC-Snap-Ins eine Verbindung herstellen können, führen Sie Folgendes aus:

```PowerShell
Enable-NetFirewallRule -DisplayGroup "<rulegroup>"
```

Dabei ist *rulegroup* abhängig von dem Snap-in, das Sie verbinden möchten, eine der folgenden:

| MMC-Snap-In                            | Regelgruppe                                            |
| ---------------------------------------- | ------------------------------------------------------- |
| Ereignisanzeige                           | Remote-Ereignisprotokollverwaltung                           |
| Dienste                               | Remotedienstverwaltung                             |
| Freigegebene Ordner                         | Datei- und Druckerfreigabe                              |
| Aufgabenplanung                         | Leistungsprotokolle und-Warnungen, Datei-und Druckerfreigabe |
| Datenträgerverwaltung                        | Remotevolumeverwaltung                              |
| Windows-Firewall und erweiterte Sicherheit | Windows-Firewallremoteverwaltung                    |


> [!NOTE]
> Für einige MMC-Snap-Ins gibt es keine entsprechende Regelgruppe, die Ihnen das Herstellen einer Verbindung über die Firewall ermöglicht. Doch das Aktivieren der Regelgruppen für "Ereignisanzeige", "Dienste" oder "Freigegebene Ordner" können die meisten anderen Snap-Ins eine Verbindung herstellen.
>
> Darüber hinaus benötigen bestimmte Snap-Ins eine weitere Konfiguration, ehe Sie durch die Windows-Firewall eine Verbindung herstellen können:
>
> - Datenträgerverwaltung. Sie müssen auf dem Server-Core-Computer zunächst den Dienst für virtuelle Datenträger (Virtual Disk Service, VDS) starten. Außerdem müssen Sie Regeln zur Datenträgerverwaltung auf dem Computer, auf dem das MMC-Snap-In ausgeführt wird, entsprechend konfigurieren.
> - IP-Sicherheitsmonitor. Sie müssen zunächst die Remoteverwaltung dieses Snap-Ins aktivieren. Geben Sie dazu an einer Eingabeaufforderung **cscript c:\windows\system32\scregedit.wsf/im-Befehl 1** ein.
> - Zuverlässigkeits- und Leistungsüberwachung. Dieses Snap-In erfordert keine weitere Konfiguration, doch wenn Sie mit ihm einen Server-Core-Computer überwachen, können nur Leistungsdaten überwacht werden. Zuverlässigkeitsdaten sind nicht verfügbar.

## <a name="managing-with-remote-desktop-services"></a>Verwalten mit Remotedesktopdienste

Sie können [Remotedesktop](../../remote/remote-desktop-services/welcome-to-rds.md) verwenden, um einen Server Core-Server von Remote Computern aus zu verwalten.

Bevor Sie auf Server Core zugreifen können, müssen Sie den folgenden Befehl ausführen:

```
cscript C:\Windows\System32\Scregedit.wsf /ar 0
```

Dadurch wird der Remotedesktop für den Verwaltungsmodus zum Akzeptieren von Verbindungen aktiviert.

## <a name="add-hardware-and-manage-drivers-locally"></a>Hinzufügen von Hardware und lokales Verwalten von Treibern

Befolgen Sie zum Hinzufügen von Hardware zu einem Server Core-Server die Anweisungen des Hardwareherstellers zur Installation neuer Hardware.

Wenn die Hardware nicht Plug & amp; Play ist, müssen Sie den Treiber manuell installieren. Kopieren Sie hierzu die Treiberdateien an einen temporären Speicherort auf dem Server, und führen Sie dann den folgenden Befehl aus:

```
pnputil –i –a <driverinf>
```

Dabei ist " *driverinf* " der Dateiname der INF-Datei für den Treiber.

Starten Sie den Computer neu, wenn Sie dazu aufgefordert werden.

Führen Sie den folgenden Befehl aus, um zu sehen, welche Treiber installiert sind:

```
sc query type= driver
```

> [!NOTE]
> Sie müssen hinter dem Gleichheitszeichen ein Leerzeichen einfügen, damit der Befehl erfolgreich ausgeführt werden kann.

Um einen Gerätetreiber zu deaktivieren, führen Sie Folgendes aus:

```
sc delete <service_name>
```

Dabei ist *SERVICE_NAME* der Name des Dienstanbieter, den Sie beim Durchlaufen der **SC-Abfragetyp = Treiber** erhalten haben.
