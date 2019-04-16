---
title: Server Core verwalten
description: Erfahren Sie, wie die Server Core-Installationsoption von Windows Server verwalten.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: 6836e5db36727294d215f7f98e0faeede55a612a
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2018
ms.locfileid: "1718710"
---
# <a name="manage-a-server-core-server"></a>Verwalten eines Server Core-Servers
 
> Betrifft: WindowsServer (Semikolons jährlichen Channel) und WindowsServer 2016

Sie können einen Server Core-Server auf folgende Weise verwalten:
- Verwenden von [Windows Admin Center](../../manage/windows-admin-center/overview.md)
- Mithilfe der [Remoteserver-Verwaltungstools](../../remote/remote-server-administration-tools.md) auf Windows 10 ausgeführt
- Lokal und Remote mithilfe von Windows PowerShell
- Remote mit dem [Server-Manager](../server-manager/server-manager.md)
- Mit den Remote ein [MMC-Snap-in](#managing-with-microsoft-management-console)
- Remote mit [Remote Desktop Services](#managing-with-remote-desktop-services)

Sie können auch Treiber lokal, solange Sie dies, über die Befehlszeile tun zu verwalten und Hinzufügen von Hardware.

Es gibt einige wichtige Einschränkungen und Tipps im Hinterkopf behalten Sie beim Arbeiten mit Server Core:

- Wenn Sie alle Eingabeaufforderungsfenster schließen und ein Eingabeaufforderungsfenster öffnen möchten, können Sie, die den Task-Manager tun. Drücken Sie **CTRL\ + ALT\ + ENTF**, klicken Sie auf **Task-Manager starten**, klicken Sie auf **Weitere Details > Datei > Ausführen**, und geben Sie **cmd.exe**. (Geben Sie **Powershell.exe** zum Öffnen von Windows PowerShell-Befehl). Alternativ können Sie abmelden und dann wieder anmelden.
- Alle Befehle oder Tool, das versucht, Windows Explorer zu starten, funktionieren nicht. Beispielsweise ausgeführt **starten.** über eine Befehlszeile funktioniert nicht.
- Es ist keine Unterstützung für HTML-Rendering oder HTML-Hilfe in Server Core.
- Server Core unterstützt Windows Installer im stillen Modus, sodass Sie Tools und Dienstprogramme von Windows Installer-Dateien installieren können. Beim Installieren von Windows Installer-Pakete auf Server Core, verwenden Sie die **Option/qb** , um die grundlegende Benutzeroberfläche anzuzeigen.
- Um die Zeitzone zu ändern, führen Sie **Set-Datum**.
- Führen Sie zum Ändern von internationaler Einstellungen **Steuerelement intl.cpl**.
- Einem eigenen **Control.exe** werden nicht ausgeführt auf. Sie müssen sie mit **Timedate.cpl** oder **Intl.cpl**ausgeführt.
- **Winver.exe** ist nicht verfügbar in Server Core. Verwenden Sie zum Abrufen von Informationen zur Version **Systeminfo.exe**.

## <a name="managing-server-core-with-windows-admin-center"></a>Verwalten von Server Core mit Windows-Verwaltungskonsole
[Windows-Verwaltungskonsole](../../manage/windows-admin-center/overview.md) ist eine browserbasierte Management-app, mit die der lokale Verwaltung von Windows-Servern mit keine Abhängigkeit Azure oder in der Cloud zu können. Windows-Verwaltungskonsole erhalten Sie vollständige Kontrolle über alle Aspekte der Server-Infrastruktur und ist besonders nützlich für die Verwaltung auf private Netzwerke, die nicht mit dem Internet verbunden sind. Sie können Windows Admin Center für Windows 10, auf einem Gatewayserver oder auf einer Installation von Windows Server mit Desktop Experience zu installieren und dann verbinden mit dem Server Core-System, das Sie verwalten möchten.

## <a name="managing-server-core-remotely-with-server-manager"></a>Verwalten von Server Core Remote mit dem Server-Manager

Server-Manager ist eine Verwaltungskonsole in Windows Server, die Unterstützung bei der Bereitstellung und Verwaltung von lokalen und remote-Windows-basierten Servern aus Ihre Desktops ohne entweder physisch auf Servern oder Remote Desktop-Protokoll (RDP) aktiviert werden müssen Verbindungen zu den einzelnen Servern. Server-Manager unterstützt remote Management mit mehreren Servern.

Um Ihre lokalen Server zu verwaltenden vom Server-Manager auf einem Remoteserver ausgeführt zu aktivieren, führen Sie das Windows PowerShell-Cmdlet **Konfigurieren SMRemoting.exe – aktivieren**.

## <a name="managing-with-microsoft-management-console"></a>Verwalten von mit Microsoft Management Console

Sie können viele-Snap-ins für Microsoft Management Console (MMC) zum Verwalten von Ihrem Server Core-Servers Remote verwenden.

Ein MMC-Snap-in mit um einen Server Core-Server zu verwalten, der Mitglied einer Domäne ist: 

1. Starten Sie MMC-Snap-in, wie etwa Computerverwaltung.
2. Mit der rechten Maustaste das Snap-in, und klicken Sie dann auf **Verbindung mit einem anderen Computer herstellen**.
2. Geben Sie den Computernamen des Server Core-Servers ein, und klicken Sie dann auf **OK**. Sie jetzt können das MMC-Snap-in Sie den Server Core-Server verwalten wie andere PC oder Server.

Ein MMC-Snap-in verwenden zum Verwalten von eines Server Core-Servers also *nicht* Mitglied einer Domäne: 

1. Richten Sie alternative Anmeldeinformationen an, an den Server Core-Computer anschließen, indem Sie den folgenden Befehl an einer Eingabeaufforderung auf dem Remotecomputer eingeben:
   ```
   cmdkey /add:<ServerName> /user:<UserName> /pass:<password>
   ```
   Wenn Sie zur Eingabe eines Kennworts aufgefordert werden möchten, lassen Sie die **Option/übergeben** .

2. Wenn Sie aufgefordert werden, geben Sie das Kennwort für den Benutzernamen ein, den Sie angegeben haben.
   Wenn die Firewall auf dem Server Core-Server zum Zulassen des MMC-Snap-ins für die Verbindung nicht bereits konfiguriert ist, gehen Sie zum Konfigurieren der Windows-Firewall zum MMC-Snap-in zu ermöglichen. Fahren Sie mit Schritt 3.
3. Starten Sie auf einem anderen Computer eine MMC-Snap-in, wie etwa **Computerverwaltung**.
4. Im linken Bereich mit der rechten Maustaste das Snap-in, und klicken Sie dann auf **Verbindung mit einem anderen Computer herstellen**. (Beispielsweise würde im Beispiel Computerverwaltung Sie **Computerverwaltung (lokal)** mit der rechten Maustaste.)
5. Geben Sie in **einem anderen Computer**den Computernamen des Server Core-Servers ein, und klicken Sie dann auf **OK**. Sie jetzt können das MMC-Snap-in Sie den Server Core-Server verwalten wie bei jedem anderen Computer unter einem Windows Server-Betriebssystem.

### <a name="to-configure-windows-firewall-to-allow-mmc-snap-ins-to-connect"></a>So konfigurieren Sie Windows-Firewall zum MMC-Snap-in (s) für die Verbindung zulassen
Wenn alle MMC-Snap-ins für die Verbindung zulassen möchten, führen Sie den folgenden Befehl ein:

```
Enable-NetFirewallRule -DisplayGroup "Remote Administration"
```

Wenn nur bestimmte MMC-Snap-ins für die Verbindung zulassen möchten, führen Sie folgenden Befehl:
```
Enable-NetFirewallRule -DisplayGroup "<rulegroup>"
```

Wobei *Regelgruppe* eine der folgenden ist je nachdem, welche-Snap-in eine Verbindung herstellen möchten:

| MMC-Snap-in                            | Regelgruppe                                            |
|----------------------------------------|-------------------------------------------------------|
| Ereignisanzeige                           | Remote Event Log-Management                           |
| Dienste                               | Remote-Service-Management                             |
| Freigegebene Ordner                         | Datei- und Druckerfreigabe                              |
| Aufgabenplanung                         | Performance-Protokolle und Warnungen, Datei- und Druckerfreigabe |
| Datenträgerverwaltung                        | Volume Remote Management                              |
| Windows-Firewall und erweiterte Sicherheit | Windows-Firewall-Remoteverwaltung                    |


> [!NOTE] 
> Einige MMC-Snap-ins müssen keine entsprechende Regelgruppe, die durch die Firewall eine Verbindung herstellen können. Aktivieren der Regelgruppen für Ereignisanzeige, Dienste und freigegebene Ordner können jedoch die meisten anderen-Snap-ins zu verbinden. 
>
> Darüber hinaus müssen bestimmte-Snap-ins weiter konfiguriert werden, bevor sie über die Windows-Firewall eine Verbindung herstellen können:
>
> - Datenträgerverwaltung. Sie müssen zunächst die Virtual Disk Service (VDS) auf dem Server Core-Computer starten. Sie müssen auch die Datenträgerverwaltung Regeln entsprechend auf dem Computer konfigurieren, die das MMC-Snap-in ausgeführt wird.
> - IP-Sicherheitsmonitor. Sie müssen zuerst Remoteverwaltung von diesem-Snap-in aktivieren. Geben Sie dazu an der Befehlszeile **Cscript \windows\system32\scregedit.wsf /im 1**
> - Zuverlässigkeit und Leistung. Das Snap-In erfordert keine weitere Konfiguration, aber bei Verwendung einen Server Core-Computer überwachen, können Sie nur Leistungsdaten überwachen. Zuverlässigkeit Daten ist nicht verfügbar.

## <a name="managing-with-remote-desktop-services"></a>Mit Remote Desktop Services verwalten

[Remotedesktop](../../remote/remote-desktop-services/welcome-to-rds.md) können Sie um einen Server Core-Server von einem Remotecomputer zu verwalten.

Bevor Sie die Server Core zugreifen können, müssen Sie den folgenden Befehl ausführen: 
```
cscript C:\Windows\System32\Scregedit.wsf /ar 0
```
Auf diese Weise können die Remotedesktop für die Verwaltungsmodus um Verbindungen zu übernehmen.

## <a name="add-hardware-and-manage-drivers-locally"></a>Lokal Treiber verwalten und Hinzufügen von hardware

Führen Sie die Anweisungen, die vom Hersteller Hardware für die Installation neuen Hardware Hardware auf einen Server Core-Server hinzuzufügen. 

Wenn die Hardware nicht Plug & Play ist, müssen Sie die Treiber manuell installieren. Klicken Sie dazu kopieren Sie die Dateien an einen temporären Speicherort auf dem Server, und führen Sie dann den folgenden Befehl aus:
```
pnputil –i –a <driverinf>
```
Dabei ist *Driverinf* der Dateiname der INF-Datei für den Treiber.

Wenn Sie aufgefordert werden, starten Sie den Computer neu.

Um herauszufinden, welche Treiber installiert sind, führen Sie den folgenden Befehl aus: 
```
sc query type= driver
```

> [!NOTE] 
> Sie müssen nach dem Gleichheitszeichen für den Befehl erfolgreich abgeschlossen das Leerzeichen enthalten.

Führen Sie die folgenden Schritte aus, um Gerätetreiber zu deaktivieren: 
```
sc delete <service_name>
```

Wobei *Dienstname* ist der Name des Diensts, die Sie erhalten haben, als Sie ausgeführt haben **sc Abfragetyp = Treiber**.