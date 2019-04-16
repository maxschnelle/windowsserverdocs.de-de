---
title: Windows Admin Center – bekannte Probleme
description: Windows Admin Center – bekannte Probleme (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 04/12/2019
ms.openlocfilehash: b0159d88251c7f4f6422dffd8f1e1414e1f30f33
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297045"
---
# Windows Admin Center – bekannte Probleme

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

Wenn Sie ein Problem haben, das auf dieser Seite nicht beschrieben ist, bitte [Teilen Sie uns dies mit](http://aka.ms/WACfeedback).

## Lenovo XClarity Integrator
Eine Inkompatibilität besteht zwischen eine bestimmte Version Kombination Lenovo XClarity Integrator und Windows Admin Center. Wenn Sie derzeit verwenden oder die Lenovo XClarity Integrator-Erweiterung in Windows Admin Center verwenden möchten, ist was Sie wissen müssen:

- Lenovo XClarity Integrator Erweiterungsversion 1.0.4 ist vollständig kompatibel mit Windows Admin Center 1809.5.
- Lenovo XClarity Integrator Erweiterungsversion 1.0.4 verfügt über eine Kompatibilitätsprobleme auf Windows Admin Center 1904 verfügbar gemacht. Microsoft und Lenovo-Mitarbeitern sind aktiv zusammen untersuchen, und wir hoffen, um eine Lösung so bald wie möglich bereitzustellen. Alle Updates werden hier auf der Website des Windows Admin Center-Dokumentation bereitgestellt werden, und können auch finden Sie [Support-Seite Lenovo](https://support.lenovo.com/solutions/ht507549) Referenz.
- Wenn Sie eine Liste häufig verwendeter Benutzer Lenovos XClarity Funktionen sind, können Sie entweder bleiben auf Windows Admin Center 1809.5 weiterhin XClarity Integrator 1.0.4 verwenden, oder Sie können upgrade auf Windows Admin Center 1904 und separat verwenden den eigenständigen XClarity Administrator Software-as-dieses Problem vorerst zu umgehen.


## Installer

- Beim Installieren von Windows Admin Center mit einem eigenen Zertifikat, wenn Sie den Fingerabdruck aus dem Zertifikat-Manager-MMC-Tool kopieren, [enthält dieser ein ungültiges Zeichen am Anfang.](https://support.microsoft.com/help/2023835/certificate-thumbprint-displayed-in-mmc-certificate-snap-in-has-extra) Um dieses Problem zu umgehen, geben Sie das erste Zeichen des Fingerabdrucks ein und kopieren Sie den Rest.

- Verwendung von Port unter 1024 wird nicht unterstützt. Im Dienstmodus können Sie optional Port 80 an die angegebene Port umleiten konfigurieren.

- Wenn Windows Update-Dienst (Wuauserv) beendet und deaktiviert ist, schlägt das Installationsprogramm fehl. [19100629]

### Upgrade/Aktualisieren

- Beim Windows Admin Center im Dienstmodus von einer früheren Version, aktualisieren, wenn Sie Msiexec im stillen Modus verwenden, können ein Problem auftreten, in denen die eingehenden Firewall-Regel für Windows Admin Center gelöscht wird.
  - Um die Regel neu zu erstellen, führen Sie den folgenden Befehl aus einer mit erhöhten Rechten PowerShell-Konsole, ersetzen \<port> mit dem Port konfiguriert für Windows Admin Center (Standard 443).

    ```powershell
    New-NetFirewallRule -DisplayName "SmeInboundOpenException" -Description "Windows Admin Center inbound port exception" -LocalPort <port> -RemoteAddress Any -Protocol TCP
    ```

## Allgemein

- Wenn Sie Windows Admin Center als Gateway unter **Windows Server 2016** unter rechenintensiven verwenden installiert haben, stürzt der Dienst ein Fehler im Ereignisprotokoll, die enthält ```Faulting application name: sme.exe``` und ```Faulting module name: WsmSvc.dll```. Dies ist aufgrund eines Fehlers, das in Windows Server 2019 behoben wurde. Der Patch für Windows Server 2016 wurde enthalten die Februar 2019 kumulative update, [KB4480977](https://www.catalog.update.microsoft.com/Search.aspx?q=4480977).

- Wenn Sie Windows Admin Center als Gateway installiert haben, und die Verbindungsliste angezeigt wird, beschädigt, führen Sie die folgenden Schritte aus:

>[!WARNING]
>Dadurch wird die Verbindungsliste und Einstellungen für alle Windows Admin Center-Benutzer auf dem Gateway gelöscht.

  1. Deinstallieren Sie Windows Admin Center
  2. Löschen Sie den Ordner **Server Management Experience** unter **C:\Windows\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft**
  3. Installieren Sie Windows Admin Center erneut

- Wenn Sie das Tool geöffnet und für einen längeren Zeitraum im Leerlauf lassen, erhalten Sie möglicherweise mehrere **Error: The runspace state is not valid for this operation**. Aktualisieren Sie dann den Browser. Wenn Sie dies, [Senden Sie uns Feedback](http://aka.ms/WACfeedback)auftreten.

- Ein **500 Fehler** kann auftreten, wenn Sie Seiten mit sehr langen URLs aktualisieren. [12443710]

- In einigen Tools kann die Rechtschreibprüfung Ihres Browsers bestimmte Feldwerte als falsch geschriebenen kennzeichnen. [12425477]

- In einigen Tools spiegeln Befehlsschaltflächen möglicherweise die Änderungen nicht unmittelbar nach einem Klick wieder, und die Tool-UI spiegelt möglicherweise nicht automatisch Änderungen an bestimmte Eigenschaften wider. Klicken Sie auf **Aktualisieren**, um den aktuellen Stand vom Zielserver abzurufen. [11445790]

- Tag auf der Liste der Verbindung - Filterung, wenn Sie Verbindungen mit der Mehrfachauswahl Kontrollkästchen aktivieren, Filtern die Verbindungsliste von tags, die ursprüngliche Auswahl beibehalten, damit alle von Ihnen ausgewählte Aktion aller zuvor ausgewählten Computer angewendet wird. [18099259]

- Möglicherweise gibt es geringfügige abweichungen zwischen Versionsnummern der Betriebssysteme ausführen in Windows Admin Center-Modulen und was innerhalb der 3. Softwarebekanntmachung aufgeführt ist.

### Erweiterungs-Managers

- Wenn Sie Windows Admin Center aktualisieren, müssen Sie Ihre Erweiterungen neu installieren.
- Wenn Sie eine Erweiterung feed, auf die zugegriffen werden kann hinzufügen, wird keine Warnung. [14412861]

## Bestimmte Browserprobleme

### Microsoft Edge

- In einigen Fällen gibt es möglicherweise lange Ladezeiten, wenn Sie Microsoft Edge verwenden, wenn Sie auf ein Windows Admin Center-Gateway über das Internet zugreifen. Dies kann auf virtuellen Azure-Computern auftreten, auf dem das Windows Admin Center Gateway ein selbstsigniertes Zertifikat verwendet wird. [13819912]

- Wenn Sie AAD als Identitätsanbieter verwenden und Windows Admin Center mit einem selbstsignierten oder nicht vertrauenswürdigen Zertifikat konfiguriert ist, kann die Authentifizierung AAD in Microsoft Edge nicht abschließen.  [15968377]

- Wenn Sie Windows Admin Center als Dienst bereitgestellt haben, und Sie Microsoft Edge als Standardbrowser verwenden, verbinden das Gateway mit Azure wird möglicherweise nach ein neues Browserfenster eintreten. Versuchen Sie, dieses Problem umgehen, indem Sie hinzufügen https://login.microsoftonline.com, https://login.live.com, und die URL der das Gateway als vertrauenswürdige Sites Websites für den Popupblockereinstellungen auf Ihrer Seite Clientbrowser zulässig sind. Weitere Informationen zum Beheben von dies in der [Handbuch zur Problembehandlung](troubleshooting.md#azlogin). [17990376]

- Wenn Sie Windows Admin Center im Desktopmodus installiert haben, wird nicht die Browserregisterkarte in Microsoft Edge die Favicon anzuzeigen. [17665801]

### Google Chrome

- Vor Version 70 (spät Oktober 2018 veröffentlicht) Chrome hat einen [Fehler](https://bugs.chromium.org/p/chromium/issues/detail?id=423609) bezüglich des Websockets-Protokolls und der NTLM-Authentifizierung. Dies wirkt sich auf die folgenden Tools aus: Ereignisse, PowerShell, Remotedesktop.

- Chrome zeigt eventuell mehrere Anmeldeinformationen an, vor allem in Zeiten der Verbindungsprozesse in einer **Arbeitsgruppen**-Umgebung (nicht der Domäne).

- Wenn Sie Windows Admin Center als Dienst bereitgestellt haben, müssen Popups aus der Gateway-URL für alle Azure-Integration Funktionen für die aktiviert werden. Diese Dienste umfassen Azure-Netzwerkadapter, Azure-Updateverwaltung und Azure Site Recovery.

### Mozilla Firefox

Windows Admin Center wurde nicht mit Mozilla Firefox getestet, aber die meisten Funktionen sollten funktionieren.

- Windows 10-Installation: Mozilla Firefox hat eigene Zertifikatspeicher, daher müssen Sie das ```Windows Admin Center Client```-Zertifikat für Firefox zur Verwendung von Windows Admin Center auf Windows 10 importieren.

<a id="websockets"></a>

## WebSocket-Kompatibilität bei Verwendung eines Proxydiensts

Remotedesktop, PowerShell und Ereignismodule im Windows Admin Center nutzen das WebSocket-Protokoll, das häufig nicht unterstützt wird, wenn ein Proxydienst verwendet wird. WebSocket unterstützt Azure AD-Anwendungsproxy-Kompatibilität in der [Vorschau](https://blogs.technet.microsoft.com/applicationproxyblog/2018/03/28/limited-websocket-support-now-in-public-preview/) und sucht nach Feedback zur Kompatibilität.

## Unterstützung für Windows Server-Versionen vor 2016 (2012 R2, 2012, 2008 R2)

> [!NOTE]
> Windows Admin Center erfordert PowerShell-Features, die nicht in Windows Server 2012 R2, 2012 oder 2008 R2 enthalten sind. Wenn Sie diese mit Windows Admin Center Verwalten von Windows Server werden, müssen Sie WMF Version 5.1 oder höher auf diesen Servern installieren.

Geben Sie `$PSVersiontable` in PowerShell ein, um zu prüfen, ob WMF 5.1 oder einen neuere Version installiert ist.

Wenn dies nicht der Fall ist, können Sie [herunterladen und WMF 5.1 installieren](https://www.microsoft.com/en-us/download/details.aspx?id=54616).

<a id="rbacknownissues"></a>

## Rollenbasierte Zugriffssteuerung (RBAC)

- RBAC-Bereitstellung ist auf Computern, die für die Windows Defender-Anwendungssteuerung (WDAC, früher als Integrität des Codes bezeichnet) konfiguriert werden, nicht erfolgreich [16568455]

- Um RBAC in einem Cluster verwenden, müssen Sie die Konfiguration für jeden Memberknoten einzeln bereitstellen.

- Wenn RBAC bereitgestellt wird, können Sie unauthorized-Fehler erhalten, die nicht ordnungsgemäß an der RBAC-Konfiguration Ergebnisarray als Attribut zugewiesen werden. [16369238]

## Server-Manager-Lösung

### Servereinstellungen

- Wenn Sie eine Einstellung ändern, und dann versuchen verlassen, ohne es zu speichern, wird die Seite Warnen Sie den einer Warnung vor ungespeicherten Änderungen, aber weiterhin verlassen. Sie landen in einem Zustand, in denen die Registerkarte "Einstellungen", die ausgewählt ist nicht mit den Inhalt der Seite übereinstimmt. [19905798] [19905787]

### Zertifikate

- Kann nicht importiert werden. PFX verschlüsselt Zertifikat im Speicher des aktuellen Benutzers. [11818622]

### Geräte

- Beim Navigieren durch die Tabelle mit Ihrer Tastatur möglicherweise die Markierung an den Anfang der Tabellengruppe Tabellengruppe. [16646059]

### Ereignisse

- Ereignisse erfolgen durch [Websocket-Kompatibilität bei Verwendung eines Proxydiensts.](#websockets)

- Möglicherweise erhalten Sie die Fehlermeldung "Packet Size" beim Exportieren von großen Protokolldateien. [16630279]

  - Verwenden Sie den folgenden Befehl mit einer Eingabeaufforderung mit erhöhten Rechten, um dieses Problem auf dem Gateway-Computer zu beheben: ```winrm set winrm/config @{MaxEnvelopeSizekb="8192"}```

### Dateien

- Hoch- oder heruntergeladen großer Dateien wird noch nicht unterstützt. (\~100mb Begrenzung) [12524234]

### PowerShell

- PowerShell erfolgt durch [Websocket-Kompatibilität bei Verwendung eines Proxydiensts](#websockets)

- Das Einfügen mit einem einzelnen Klick mit der rechten Maustaste wie in der Desktop PowerShell-Konsole ist nicht funktionsfähig. Stattdessen erhalten Sie Kontextmenüs des Browsers, in dem Sie „einfügen” auswählen können. STRG + V funktioniert auch.

- STRG + C kann nicht zum Kopieren verwendet werden, es sendet immer den Befehl STRG + C an die Konsole. Das Kopieren über das mit der rechten Maustaste aufgerufenen Kontextmenü funktioniert.

- Wenn Sie das Windows Admin Center-Fenster kleiner machen, wird der Terminalinhalt umgeleitet, aber wenn Sie es erneut vergrößern, kann der Inhalt nicht in den vorherigen Zustand zurückkehren. Wenn Dinge durcheinander geraten, können Sie Clear-Host verwenden, oder die Verbindung trennen und erneut eine Verbindung mit der Schaltfläche oberhalb des Terminaldienstes herstellen.

### Registrierungs-Editor

- Die Suchfunktion ist nicht implementiert. [13820009]

### Remotedesktop

- Das Tool Remotedesktop Fehlschlagen beim Verwalten von Windows Server 2012 eine Verbindung herstellen. [20258278]

- Verwendung der Remotedesktop Verbindung zu einem Computer, die nicht der Domäne verbunden ist, geben Sie Ihr Konto in der ```MACHINENAME\USERNAME``` Format.

- Einige Konfigurationen können Windows Admin Center Remotedesktopclient mit "Gruppenrichtlinie" blockieren. Wenn Sie in diesem Fall aktivieren ```Allow users to connect remotely by using Remote Desktop Services``` unter ```Computer Configuration/Policies/Administrative Templates/Windows Components/Remote Desktop Services/Remote Desktop Session Host/Connections```

- Remotedesktop erfolgt durch [Websocket-Kompatibilität.](#websockets)

- Das Tool Remotedesktop unterstützt derzeit weder Text, Bild oder Datei Kopieren/Einfügen zwischen dem lokalen Desktop und der Remotesitzung.

- Zum Kopieren/Einfügen innerhalb der Remotesitzung können Sie normal kopieren (Klicken + Kopieren oder STRG + C), das Einfügen erfordert Klick + Einfügen (STRG + V funktioniert nicht)

- Sie können die folgenden Befehle nicht an die Remotesitzung senden.
  - ALT+TAB
  - Funktionstasten
  - Windows-Taste
  - DRUCK

- Remote-App kann nach dem Aktivieren der Remote-App-Tool von Remotedesktop-Einstellungen, das Tool nicht in der Tool-Liste angezeigt, wenn einen Server mit Desktop Experience verwalten. [18906904]

### Rollen und Features

- Bei der Auswahl von Rollen oder Funktionen mit nicht verfügbaren Quellen zur Installation, werden diese übersprungen. [12946914]

- Wenn Sie nach der Installation der Serverrollen nicht automatisch neu starten, wird nicht erneut gefragt. [13098852]

- Wenn Sie automatisch neu starten auswählen, wird der Neustart erfolgen, bevor der Status auf 100 % aktualisiert wird. [13098852]

### Speicher

- Abrufen von Informationen Kontingent fehlschlagen ohne eine Benachrichtigung Fehler (es werden diese weiterhin ein Fehler in den Browser-Konsole) [18962274]

- Älter: DVD/CD/Diskettenlaufwerke werden nicht als Volumes angezeigt.

- Älter: Einige Eigenschaften in Volumes und Datenträgern sind nicht kompatible, und werden als unbekannt oder ein Leerzeichen im Detailbereich angezeigt.

- Älter: Beim Erstellen eines neuen Volumes unterstützt ReFS nur Zuordnungseinheiten mit 64K auf Windows 2012 und 2012 R2-Computern. Wenn ein Volume ReFS mit einer kleineren Zuordnungseinheit für ältere Ziele erstellt wird, schlägt die File System-Formatierung fehl. Das neue Volume kann nicht verwendet werden. Die Lösung besteht darin, das Volume zu löschen und Zuordnungseinheiten mit 64 KB zu verwenden.

### Updates

- Nach der Installation von Updates, wird der Installationsstatus zwischengespeichert und erfordern eine Aktualisierung des Browsers.

- Sie können den Fehler auftreten: "Schlüsselsatz ist nicht vorhanden" beim Versuch, Azure-updateverwaltung einrichten. In diesem Fall versuchen Sie die folgenden Schritte Wartung aus, auf dem verwalteten Knoten-
    1. Beenden Sie Dienst "Kryptografischen Dienste".
    2. Änderung Ordneroptionen zur Anzeige ausgeblendet Dateien (falls erforderlich).
    3. Haben Sie zum Ordner "% allusersprofile%\Microsoft\Crypto\RSA\S-1-5-18", und löschen Sie die gesamten.
    4. Starten Sie neu Dienst "Kryptografischen Dienste".
    5. Wiederholen Sie die Einrichtung von Update-Verwaltung mit Windows Admin Center

### Virtuelle Computer

- Wenn Sie die virtuellen Computer auf einem Windows Server 2012-Host zu verwalten, die im Browser-VM verbinden Tool zum Herstellen des virtuellen Computers nicht. Herunterladen der RDP-Datei zum Herstellen des virtuellen Computers sollten weiterhin funktionieren. [20258278]

- Azure Site Recovery – wenn ASR Setup auf dem Host außerhalb WAC, werden Sie nicht schützen, einen virtuellen Computer aus innerhalb WAC [18972276] sein

- Erweiterte Funktionen in Hyper-V-Manager wie Virtual SAN-Manager, Move VM, Export VM und VM-Replikation werden derzeit nicht unterstützt.

### Virtuelle Switches

- Switch Embedded Teaming (SET): Beim Hinzufügen von Netzwerkschnittstellenkarten (NICs) zu einem Team müssen sie im gleichen Subnetz sein.

## Computer-Management-Lösung

Die Computer-Management-Lösung enthält eine Teilmenge der Tools der Server-Manager-Lösung, daher sind die gleichen bekannten Probleme vorhanden, sowie die folgenden Computer Management-Lösungen für bestimmte Probleme:

- Wenn Sie ein Microsoft Account ([MSA](https://account.microsoft.com/account/)) oder wenn Sie Azure Active Directory (AAD) verwenden, um Sie Windows 10-Computer anmelden, müssen Sie angeben "verwalten – als" Anmeldeinformationen zum Verwalten Ihres lokalen Computers [16568455]

- Wenn Sie versuchen, den "localhost" zu verwalten, werden Sie aufgefordert, den Gateway-Prozess zu erhöhen. Wenn Sie **Nein** im folgenden Benutzerkontensteuerungsfenster anklicken, kann Windows Admin Center dies nicht erneut anzeigen. Beenden Sie in diesem Fall den Gateway-Prozess, indem Sie das Windows Admin Center-Symbol in der Taskleiste mit der rechten Maustaste anklicken, und beenden wählen. Starten Sie Windows Admin Center im Startmenü dann erneut.

- Auf Windows 10 ist WinRM/PowerShell-Remoting standardmäßig nicht vorhanden
  
  - Um die Verwaltung des Windows 10-Clients zu ermöglichen, müssen Sie den Befehl ```Enable-PSRemoting``` aus einer PowerShell-Eingabeaufforderung mit erhöhten Rechten eingeben.

  - Sie müssen auch Ihre Firewall für Verbindungen von außerhalb des lokalen Subnetzes mit ```Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any``` aktualisieren. Restriktiver Netzwerke Szenarien finden Sie in [dieser Dokumentation](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enable-psremoting?view=powershell-5.1).

## Failovercluster-Manager-Lösung

- Wenn Sie einen Cluster verwalten (entweder hyperkonvergent oder herkömmlich) tritt möglicherweise der Fehler **shell was not found** auf. Laden Sie in diesem Fall entweder Ihren Browser erneut oder navigieren Sie zu einem anderen Tool und zurück. [13882442]

- Ein Problem kann auftreten, wenn Sie einen älteren Cluster verwalten (Windows Server 2012 oder 2012 R2), der nicht vollständig konfiguriert wurde. Die Fehlerbehebung für dieses Problem besteht darin, sicherzustellen, dass das Windows-Feature **RSAT-Clustering-PowerShell** installiert und auf **jedem Mitgliedsknoten** des Clusters aktiviert wurde. Um dies mit PowerShell auszuführen, geben Sie den Befehl `Install-WindowsFeature -Name RSAT-Windows-PowerShell` auf den Clusterknoten an. [12524664]

- Cluster müssen möglicherweise über den gesamten FQDN hinzugefügt werden, um richtig erkannt zu werden.

- Bei der Verbindung mit einem Cluster mit Windows Admin Center als Gateway und beim Bereitstellen des expliziten Benutzernamens und Kennwort,um sich zu authentifizieren, müssen Sie **diese Anmeldeinformationen für alle Verbindungen verwenden** auswählen, damit die Anmeldeinformationen zum Abfragen des Mitgliedknotens verfügbar sind.

## Hyperkonvergente Cluster-Manager-Lösung

- Einige Befehle wie **Drives - Update firmware**, **Servers - Remove** und **Volumes - Open** sind nicht aktiviert und zur Zeit nicht verfügbar.