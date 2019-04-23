---
title: Verwalten von Server Core
description: Informationen Sie zum Verwalten einer Server Core-Installations von Windows Server
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.date: 12/18/2018
ms.openlocfilehash: 39fbb92645d39a46613f2142d0258c78a6ba425b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842661"
---
# <a name="administer-a-server-core-server"></a>Verwaltung einer Server Core-server

>Gilt für: WindowsServer (Halbjährlicher Kanal) und WindowsServer 2016

Da Server Core nicht über eine Benutzeroberfläche verfügt, müssen Sie Windows PowerShell-Cmdlets, Befehlszeilentools oder remote Tools zu verwenden, um grundlegende Verwaltungsaufgaben ausführen. Den folgenden Abschnitten werden die PowerShell-Cmdlets und Befehle, die für grundlegende Aufgaben verwendet. Sie können auch [Windows Admin Center](../../manage/windows-admin-center/overview.md), ein einheitliches Verwaltungsportal derzeit in der öffentlichen Vorschau, um Ihre Installation zu verwalten. 

## <a name="administrative-tasks-using-powershell-cmdlets"></a>Mithilfe von PowerShell-Cmdlets für administrative Aufgaben
Verwenden Sie die folgende Informationen, um einfache administrative Aufgaben mit Windows PowerShell-Cmdlets ausführen.

### <a name="set-a-static-ip-address"></a>Festlegen einer statischen IP-Adresse
Wenn Sie einen Server Core-Server installieren, ist es standardmäßig ein DHCP-Adresse. Wenn Sie eine statische IP-Adresse benötigen, können Sie es mit den folgenden Schritten festlegen.

Verwenden Sie zum Anzeigen Ihrer aktuellen Netzwerkkonfiguration **Get-NetIPConfiguration**.

Verwenden Sie zum Anzeigen der IP-Adressen Sie bereits verwenden **Get-NetIPAddress**.

Um eine statische IP-Adresse festzulegen, führen Sie folgende Schritte aus: 

1. Führen Sie **Get-NetIPInterface**. 
2. Die Treuenummer ist in der **IfIndex** Spalte für Ihre IP-Schnittstelle oder die **InterfaceDescription** Zeichenfolge. Wenn Sie mehrere Netzwerkadapter verfügen, beachten Sie die Anzahl oder eine Zeichenfolge, die für die Schnittstelle, der Sie die statische IP-Adresse festlegen möchten.
3. Führen Sie das folgende Cmdlet zum Festlegen der statischen IP-Adresse:

   ```powershell
   New-NetIPaddress -InterfaceIndex 12 -IPAddress 192.0.2.2 -PrefixLength 24 -DefaultGateway 192.0.2.1
   ```

   Dabei gilt Folgendes:
   - **InterfaceIndex** ist der Wert des **IfIndex** aus Schritt 2. (In unserem Beispiel 12)
   - **IP-Adresse** ist die statische IP-Adresse, die Sie festlegen möchten. (In unserem Beispiel 191.0.2.2)
   - **PrefixLength** ist die Präfixlänge (eine andere Form der Subnetzmaske) für die IP-Adresse, die Sie festlegen. (Für unser Beispiel 24).
   - **DefaultGateway** ist die IP-Adresse des Standardgateways. (Für unser Beispiel 192.0.2.1).
4. Führen Sie das folgende Cmdlet, um den DNS-Client-Serveradresse festzulegen: 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4
   ```
   
   Dabei gilt Folgendes:
   - **InterfaceIndex** ist der Wert der IfIndex aus Schritt 2.
   - **ServerAddresses** ist die IP-Adresse Ihres DNS-Servers.
5. Um mehrere DNS-Server hinzuzufügen, führen Sie das folgende Cmdlet aus: 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4,192.0.2.5
   ```

   der Ort, in diesem Beispiel **192.0.2.4** und **192.0.2.5** sind beide IP-Adressen der DNS-Server.

Wenn Sie benötigen, wechseln zur Verwendung von DHCP, führen Sie **Set-DnsClientServerAddress – InterfaceIndex 12 – ResetServerAddresses**.

### <a name="join-a-domain"></a>Beitreten zu einer Domäne
Verwenden Sie die folgenden Cmdlets zum Hinzufügen eines Computers zu einer Domäne an.

1. Führen Sie **Computer hinzufügen**. Sie werden beide Anmeldeinformationen für die Domäne und den Domänennamen beitreten aufgefordert werden.
2. Wenn Sie der lokalen Gruppe "Administratoren" ein Domänenbenutzerkonto hinzufügen müssen, führen Sie den folgenden Befehl an einer Eingabeaufforderung (nicht in das PowerShell-Fenster):

   ```
   net localgroup administrators /add <DomainName>\<UserName>
   ```
3. Starten Sie den Computer neu. Hierzu können Sie ausführen **Restart-Computer**.

### <a name="rename-the-server"></a>Umbenennen des Servers
Verwenden Sie die folgenden Schritte aus, um den Server umbenennen.

1. Ermitteln Sie mit dem Befehl **hostname** oder **ipconfig** den aktuellen Namen des Servers.
2. Führen Sie **Rename-Computer: ComputerName \<New_name\>**.
3. Starten Sie den Computer neu.

### <a name="activate-the-server"></a>Aktivieren des Servers

Führen Sie **slmgr.vbs – Ipk\<Productkey\>**. Führen Sie dann **slmgr.vbs – Ato**. Wenn die Aktivierung erfolgreich ist, erhalten Sie keine Nachricht.

> [!NOTE]
> Sie können auch den Server durch Aktivieren Telefon, mithilfe einer [Schlüsselverwaltungsdienst (KMS) Server](../../get-started/server-2016-activation.md), oder Remote. Um per Remotezugriff zu aktivieren, führen Sie das folgende Cmdlet auf einem Remotecomputer aus: 

>```powershell
>**cscript windows\system32\slmgr.vbs <ServerName> <UserName> <password>:-ato**
>```
 
### <a name="configure-windows-firewall"></a>Konfigurieren der Windows-Firewall

Die Windows-Firewall können Sie lokal auf dem Server Core-Computer mithilfe von Windows PowerShell-Cmdlets und -Skripts konfigurieren. Finden Sie unter [NetSecurity](/powershell/module/netsecurity/?view=win10-ps) für die Cmdlets Sie die Windows-Firewall zu konfigurieren können.

### <a name="enable-windows-powershell-remoting"></a>Aktivieren von Windows PowerShell-Remoting

Wenn Sie Windows PowerShell-Remoting aktivieren, werden in Windows PowerShell auf einem Computer eingegebene Befehle auf einem anderen Computer ausgeführt. Aktivieren Sie Windows PowerShell-Remoting mit **Enable-PSRemoting**.

Weitere Informationen finden Sie unter [About_remote_faq](/powershell/module/microsoft.powershell.core/about/about_remote_faq?view=powershell-5.1)
</br>

## <a name="administrative-tasks-from-the-command-line"></a>Verwaltungsaufgaben über die Befehlszeile
Verwenden Sie die folgenden Referenzinformationen für Verwaltungsaufgaben über die Befehlszeile an.

### <a name="configuration-and-installation"></a>Konfiguration und Installation
|Aufgabe | Befehl |
|-----|-------|
|Festlegen des lokalen Administratorkennworts| **NET Benutzeradministrator** \* |
|Hinzufügen eines Computers zu einer Domäne| **Netdom Join %Computername%** **/Domain:\<Domäne\> /userd:\<Domäne\\Benutzername \> /passwordd:**\* <br> Starten Sie den Computer neu.|
|Bestätigen, dass die Domäne geändert wurde| **set** |
|Entfernen eines Computer aus einer Domäne|**Netdom Remove \<Computername\>**| 
|Hinzufügen eines Benutzers zu der lokalen Gruppe "Administratoren"|**net Localgroup Administratoren / add \<Domäne\\Benutzername\>** |
|Entfernen eines Benutzers aus der lokalen Gruppe "Administratoren"|**net Localgroup Administratoren/Delete \<Domäne\\Benutzername\>** |
|Hinzufügen eines Benutzers zum lokalen Computer|**NET Benutzer \<"Domäne\Benutzername"\> * / add** |
|Hinzufügen einer Gruppe zum lokalen Computer|**net Localgroup \<Gruppenname\> / add**|
|Ändern des Namens eines Computers, der einer Domäne angehört|**Netdom Renamecomputer % Computername % / NewName:\<neuen Computernamen\> /userd:\<Domäne\\Benutzername \> /passwordd:** * |
|Bestätigen des neuen Computernamens|**set**| 
|Ändern des Namens eines Computers in einer Arbeitsgruppe|**Netdom Renamecomputer \<AktuellerComputername\> /NewName:\<Newcomputername\>** <br>Starten Sie den Computer neu.|
|Deaktivieren der Verwaltung von Auslagerungsdateien|**WMIC-Computersystem, wobei name = "\<Computername\>" Festlegen von AutomaticManagedPagefile = "false"**| 
|Konfigurieren der Auslagerungsdatei|**WMIC Pagefileset, wobei name = "\<Pfad/Dateiname\>" Festlegen von InitialSize =\<Initialsize\>, MaximumSize =\<MaxSize-Wert\>** <br>In denen *Pfad/Dateiname* ist der Pfad und den Namen der Auslagerungsdatei, *Initialsize* ist die Anfangsgröße der Auslagerungsdatei in Byte und *Maxsize* ist die maximale Größe der der Auslagerungsdatei in Byte.|
|Wechseln zu einer statischen IP-Adresse|**ipconfig /all** <br>Notieren Sie die relevanten Informationen ein, oder leiten Sie ihn in eine Textdatei (**Ipconfig/all > ipconfig.txt**).<br>**"Netsh Interface IPv4-Show Interfaces"**<br>Stellen Sie sicher, dass eine Schnittstellenliste vorhanden ist.<br>**Netsh Interface ipv4-Adresse znamen \<-ID aus Schnittstellenliste\> Quelle = statische Adresse =\<bevorzugte IP-Adresse\> Gateway =\<-Gatewayadresse\>**<br>Führen Sie **Ipconfig/all** zu Vierfy, die DHCP-aktiviert, um festgelegt ist **keine**.|
|Festlegen der statischen DNS-Adresse.|**Netsh Interface ipv4 Hinzufügen von DNS-Server-Name =\<Name oder ID der Netzwerkkarte\> Adresse =\<IP-Adresse des primären DNS-Servers\> Index = 1 <br>** Netsh Interface ipv4 add DNS-Server-Name =\<Name des sekundären DNS-Server\> Adresse =\<IP-Adresse des sekundären DNS-Servers\> Index = 2 ** <br> Wiederholen Sie je nach Bedarf zusätzliche Server hinzufügen.<br>Führen Sie **Ipconfig/all** um sicherzustellen, dass die Adressen richtig sind.|
|Wechseln von einer statischen IP-Adresse zu einer von DHCP bereitgestellten IP-Adresse|**Netsh Interface ipv4-Adresse znamen =\<IP-Adresse des lokalen Systemkontos\> Source = DHCP** <br>Führen Sie **Ipconfig/all** zu überprüfen, ob DHCP aktiviert, um festgelegt ist **Ja**.|
|Eingeben eines Product Keys|**slmgr.vbs – Ipk \<Produktschlüssel\>**| 
|Lokales Aktivieren des Servers|**slmgr.vbs -ato**| 
|Remotes Aktivieren des Servers|**Cscript slmgr.vbs – Ipk \<Produktschlüssel\>\<Servernamen\>\<Benutzername\>\<Kennwort\>** <br>**Cscript slmgr.vbs – Ato \<Servername\> \<Benutzername\> \<Kennwort\>** <br>Rufen Sie die GUID des Computers durch Ausführen **Cscript slmgr.vbs – hat** <br> Führen Sie **Cscript slmgr.vbs – Dli \<GUID\>** <br>Überprüfen, ob Softwarelizenz-Statusangaben zu **(aktiviert) lizenziert**.


### <a name="networking-and-firewall"></a>Netzwerk und Firewall

|Aufgabe|Befehl| 
|----|-------|
|Konfigurieren Sie den Server, um einen Proxyserver verwenden|**Netsh Winhttp-Proxy festlegen \<Servername\>:\<Portnummer\>** <br>**Hinweis**: Server Core-Installationen können nicht im Internet über einen Proxy zugreifen, die ein Kennwort für Verbindungen erforderlich sind.|
|Konfigurieren Sie den Server, um den Proxy für Internetadressen umgangen|**netsh winttp set proxy \<servername\>:\<port number\> bypass-list="\<local\>"**| 
|Anzeigen oder Ändern der IPSEC-Konfiguration|**Netsh-ipsec**| 
|Zeigen Sie an oder ändern Sie die NAP-Konfiguration|**Netsh nap**| 
|Zeigen Sie an oder ändern Sie der IP für physische Adresse übersetzen|**arp**| 
|Anzeigen oder Konfigurieren der lokalen Routingtabelle|**route**| 
|Anzeigen oder Konfigurieren von DNS-servereinstellungen|**nslookup**| 
|Anzeigen von Protokollstatistiken und von aktuellen TCP/IP-Netzwerkverbindungen|**netstat**| 
|Anzeigen von Protokollstatistik und aktuellen TCP/IP-Verbindungen mithilfe von NetBIOS über TCP/IP (NBT)|**nbtstat**| 
|Anzeigen von Hops für Netzwerkverbindungen|**pathping**| 
|Verfolgen von Hops für Netzwerkverbindungen|**tracert**| 
|Anzeigen der Konfiguration des Multicastrouters|**mrinfo**| 
|Aktivieren der Remoteverwaltung der firewall|**Netsh Advfirewall Firewall legen Regelgruppe = "Windows-Firewall-Remoteverwaltung" neue Enable = Yes**| 
 

### <a name="updates-error-reporting-and-feedback"></a>Updates, Fehlerberichterstattung und feedback

|Aufgabe|Befehl| 
|----|-------|
|Installieren eines Updates|**wusa \<update\>.msu /quiet**| 
|Auflisten von installierten Updates|**systeminfo**| 
|Entfernen eines Updates|**expand /f:\* \<update\>.msu c:\test** <br>Navigieren Sie zu c:\test\ und Open \<aktualisieren\>XML in einem Text-Editor.<br>Ersetzen Sie dies **installieren** mit **entfernen** und speichern Sie die Datei.<br>**pkgmgr /n:\<update\>.xml**|
|Konfigurieren von automatischen Updates|Um zu überprüfen, ob die aktuelle Einstellung: ** "cscript" %systemroot%\system32\scregedit.wsf au/v **<br>So aktivieren Sie automatische Updates: **Cscript scregedit.wsf au-4** <br>So deaktivieren Sie automatische Updates: **Cscript %systemroot%\system32\scregedit.wsf au 1**| 
|Aktivieren der Fehlerberichterstattung|Um zu überprüfen, ob die aktuelle Einstellung: **ServerWerOptin/Query** <br>Automatisch ausführliche Berichte senden: **ServerWerOptin / detailed** <br>Damit diese automatisch Zusammenfassungsberichte senden: **ServerWerOptin/Summary** <br>So deaktivieren Sie die Fehlerberichterstattung: **ServerWerOptin/Disable**|
|Teilnehmen am Programm zur Verbesserung der Benutzerfreundlichkeit|Um zu überprüfen, ob die aktuelle Einstellung: **ServerCEIPOptin/Query** <br>Um CEIP zu aktivieren: **ServerCEIPOptin/Enable /** <br>Um CEIP zu deaktivieren: **ServerCEIPOptin/Disable**|

### <a name="services-processes-and-performance"></a>Dienste, Prozesse und Leistung

|Aufgabe|Befehl| 
|----|-------|
|Die ausgeführten Dienste aufgelistet.|**SC-Abfrage** oder **net Start**| 
|Starten eines Diensts|**sc Start \<Dienstnamen\>**  oder **net Start \<Dienstname\>**| 
|Beenden eines Diensts|**sc Stop \<Dienstnamen\>**  oder **net Stop \<Dienstname\>**| 
|Abrufen einer Liste mit ausgeführten Anwendungen und zugehörigen Prozessen|**tasklist**||Erzwingen der Beendigung eines Prozesses|Führen Sie **Tasklist** rufen Sie die Prozess-ID (PID), und führen Sie **Taskkill "/ PID" \<Prozess-ID\>**|
|Starten des Task-Managers|**taskmgr**| 
|Erstellen und Verwalten von Sitzung und die Leistung Protokolle der ereignisablaufverfolgung|Ein Indikator, Ablaufverfolgung, Serverkonfigurations-Datensammlung oder eine API zu erstellen: **Logman erstellen** <br>Beim Abfragen der Data Collector Eigenschaften: **Logman-Abfrage** <br>So starten oder Beenden der Datensammlung: **Logman Start\|beenden** <br>So löschen Sie eine Sammlung: **Logman löschen** <br> Um die Eigenschaften einer Sammlung zu aktualisieren: **Logman Update** <br>Um einen datensammlersatz aus einer XML-Datei importieren oder exportieren es in eine XML-Datei: **Logman Import\|exportieren**|

### <a name="event-logs"></a>Ereignisprotokolle

|Aufgabe|Befehl| 
|----|-------|
|Liste von Ereignisprotokollen|**wevtutil el**| 
|Abfragen von Ereignissen in einem angegebenen Protokoll|**wevtutil qe /f:text \<log name\>**| 
|Exportieren Sie ein Ereignisprotokoll|**Wevtutil Epl \<Protokollname\>**| 
|Ein Ereignisprotokoll löschen|**Wevtutil cl \<Protokollname\>**| 


### <a name="disk-and-file-system"></a>Datenträger- und Dateisystem

|Aufgabe|Befehl|
|----|-------|
|Verwalten von Datenträgerpartitionen|Führen Sie für eine vollständige Liste der Befehle, **Diskpart /?**|  
|Verwalten von Software-RAID|Führen Sie für eine vollständige Liste der Befehle, **Diskraid /?**|  
|Verwalten von Volumebereitstellungspunkten|Führen Sie für eine vollständige Liste der Befehle, **Mountvol /?**| 
|Defragmentieren eines Volumes|Führen Sie für eine vollständige Liste der Befehle, **Defragmentieren /?**|  
|Konvertieren eines Volumes in das NTFS-Dateisystem|**Konvertieren von \<Volumebuchstaben\> FS: NTFS**| 
|Komprimieren einer Datei|Führen Sie für eine vollständige Liste der Befehle, **compact /?**|  
|Verwalten geöffneter Dateien|Führen Sie für eine vollständige Liste der Befehle, **Openfiles /?**|  
|Verwalten von VSS-Ordnern|Führen Sie für eine vollständige Liste der Befehle, **Vssadmin /?**| 
|Verwalten des Dateisystems|Führen Sie für eine vollständige Liste der Befehle, **Fsutil /?**||Überprüfen einer Dateisignatur|**sigverif /?**| 
|Übernehmen des Besitzes für eine Datei oder einen Ordner|Führen Sie für eine vollständige Liste der Befehle, **Icacls /?**| 
 
### <a name="hardware"></a>Hardware

|Aufgabe|Befehl| 
|----|-------|
|Hinzufügen eines Treibers für ein neues Hardwaregerät|Kopieren Sie den Treiber in einen Ordner unter %HOMEDRIVE%\\\<Treiberordner\>. Run **pnputil -i -a %homedrive%\\\<driver folder\>\\\<driver\>.inf**|
|Entfernen eines Treibers für ein Hardwaregerät|Führen Sie eine Liste von geladenen Treibern, **Abfragetyp sc = Treiber**. Führen Sie dann **sc Delete \<Service_name\>**|
