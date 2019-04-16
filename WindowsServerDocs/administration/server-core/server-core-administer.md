---
title: Verwalten von servercore
description: Informationen Sie zum Verwalten von Server Core-Installationsoption von Windows Server
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.date: 12/18/2018
ms.openlocfilehash: 39fbb92645d39a46613f2142d0258c78a6ba425b
ms.sourcegitcommit: 4df1bc940338219316627ad03f0525462a05a606
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2018
ms.locfileid: "8977997"
---
# Verwalten von eines Server Core-Servers

>Gilt für: Windows Server (Semi-Annual Channel) and Windows Server 2016

Da Server Core nicht über eine Benutzeroberfläche verfügt, müssen Sie Windows PowerShell-Cmdlets, Befehlszeilentools oder Remotetools verwenden, um grundlegende Verwaltungsaufgaben ausführen. Den folgenden Abschnitten wird beschrieben, die PowerShell-Cmdlets und Befehle, die für einfache Aufgaben verwendet. [Windows Admin Center](../../manage/windows-admin-center/overview.md), eine einheitliche-Verwaltungsportal derzeit in der öffentlichen Vorschau, können auch die Installation verwalten. 

## Verwaltungsaufgaben mithilfe von PowerShell-cmdlets
Verwenden Sie die folgende Informationen, um grundlegende Verwaltungsaufgaben mit Windows PowerShell-Cmdlets.

### Legen Sie eine statische IP-Adresse
Wenn Sie einen Server Core-Server installieren, hat sie standardmäßig ein DHCP-Adresse. Wenn Sie eine statische IP-Adresse benötigen, können Sie es mit den folgenden Schritten festlegen.

Verwenden Sie zum Anzeigen der aktuellen Netzwerkkonfiguration **Get-NetIPConfiguration**.

Verwenden Sie **Get-NetIPAddress**, um die IP-Adressen anzuzeigen, die Sie bereits verwenden.

Um eine statische IP-Adresse einzurichten, gehen Sie wie folgt: 

1. Führen Sie **Get-NetIPInterface**. 
2. Beachten Sie die Zahl in der Spalte **IfIndex** für die IP-Schnittstelle oder die **InterfaceDescription** -Zeichenfolge. Wenn Sie mehr als ein Netzwerkadapter vorhanden sind, beachten Sie die Zahl oder eine Zeichenfolge, die für die Schnittstelle, der Sie die statische IP-Adresse festlegen möchten.
3. Führen Sie das folgende Cmdlet, um die statische IP-Adresse festzulegen:

   ```powershell
   New-NetIPaddress -InterfaceIndex 12 -IPAddress 192.0.2.2 -PrefixLength 24 -DefaultGateway 192.0.2.1
   ```

   Dabei gilt Folgendes:
   - **InterfaceIndex** ist der Wert der **IfIndex** aus Schritt 2. (In unserem Beispiel 12)
   - **IP-Adresse** ist die statische IP-Adresse, die Sie festlegen möchten. (In unserem Beispiel 191.0.2.2)
   - **PrefixLength** ist die Präfixlänge (eine andere Art Subnetzmaske) für die IP-Adresse, die Sie festlegen. (Für unser Beispiel 24)
   - **DefaultGateway** ist die IP-Adresse des Standardgateways. (Für unser Beispiel 192.0.2.1)
4. Führen Sie das folgende Cmdlet, um die DNS-Client-Serveradresse festzulegen: 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4
   ```
   
   Dabei gilt Folgendes:
   - **InterfaceIndex** ist der Wert der IfIndex aus Schritt 2.
   - **ServerAddresses** ist die IP-Adresse des DNS-Servers.
5. Um mehrere DNS-Server hinzuzufügen, führen Sie das folgende Cmdlet: 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4,192.0.2.5
   ```

   in diesem Beispiel sind **192.0.2.4** und **192.0.2.5** , beide IP-Adressen der DNS-Server.

Wenn Sie von DHCP, führen Sie wechseln müssen **Satz DnsClientServerAddress – InterfaceIndex 12 – ResetServerAddresses**.

### Einer Domäne beitreten
Verwenden Sie die folgenden Cmdlets, um einen Computer mit einer Domäne zu verknüpfen.

1. Führen Sie **Computer hinzufügen**. Sie werden für beide Anmeldeinformationen für die Domäne und den Domänennamen aufgefordert.
2. Wenn Sie ein Domänenbenutzerkonto zur lokalen Administratorengruppe hinzufügen müssen, führen Sie den folgenden Befehl in einer Befehlszeile (nicht in das PowerShell-Fenster):

   ```
   net localgroup administrators /add <DomainName>\<UserName>
   ```
3. Starten Sie den Computer neu. Sie können dies tun, indem **Restart-Computer**ausführen.

### Benennen Sie den server
Verwenden Sie die folgenden Schritte aus, um den Server umbenennen.

1. Bestimmen Sie den aktuellen Namen des Servers mit dem **Hostnamen** oder **Ipconfig** -Befehl.
2. Führen Sie **Umbenennen-Computer - ComputerName \<new_name\ >**.
3. Starten Sie den Computer neu.

### Aktivieren Sie den server

Führen Sie **slmgr.vbs – Ipk\<productkey\ >**. Führen Sie **slmgr.vbs – Ato**. Wenn die Aktivierung erfolgreich ist, erhalten Sie keine Nachricht.

> [!NOTE]
> Sie können auch aktivieren Sie den Server per Telefon, mit einem [Server (Key Management Service, KMS)](../../get-started/server-2016-activation.md), oder Remote. Führen Sie das folgende Cmdlet von einem Remotecomputer, um Remote zu aktivieren: 

>```powershell
>**cscript windows\system32\slmgr.vbs <ServerName> <UserName> <password>:-ato**
>```
 
### Konfigurieren von Windows-Firewall

Sie können Windows-Firewall lokal auf dem Server Core-Computer mit Windows PowerShell-Cmdlets und Skripts konfigurieren. Die Cmdlets, die Sie verwenden können, um Windows-Firewall konfigurieren finden Sie unter [NetSecurity](/powershell/module/netsecurity/?view=win10-ps) .

### Aktivieren von Windows PowerShell-remoting

Sie können Windows PowerShell-Remoting der Befehle in Windows PowerShell auf einem Computer auf einem anderen Computer ausführen Eingabe. Aktivieren Sie Windows PowerShell-Remoting mit **Enable-PSRemoting**.

Weitere Informationen finden Sie [Über Remote – häufig gestellte Fragen](/powershell/module/microsoft.powershell.core/about/about_remote_faq?view=powershell-5.1)
</br>

## Verwaltungsaufgaben über die Befehlszeile
Verwenden Sie die folgenden Referenzinformationen Verwaltungsaufgaben über die Befehlszeile ausführen.

### Konfiguration und installation
|Aufgabe | Befehl |
|-----|-------|
|Legen Sie das Kennwort des lokale administrative| **NET Benutzeradministrator** \* |
|Hinzufügen eines Computers zu einer Domäne| **Netdom Join Computername%** **/domain:\<domain\ > /userd:\<domain\\username\ >/passwordd:**\* <br> Starten Sie den Computer neu.|
|Stellen Sie sicher, dass die Domäne geändert wurde| **set** |
|Entfernen eines Computers aus einer Domäne|**Netdom entfernen \ < Computername\ >**| 
|Hinzufügen eines Benutzers zu der lokalen Gruppe Administratoren|**die lokale Gruppe Administratoren NET / add \ < Domain\\username\ >** |
|Entfernen eines Benutzers aus der lokalen Gruppe Administratoren|**NET lokale Gruppe Administratoren/Delete \ < Domain\\username\ >** |
|Hinzufügen eines Benutzers auf den lokalen computer|**NET Benutzer \ < Domain\username\ > * "/" hinzufügen** |
|Hinzufügen einer Gruppe auf dem lokalen computer|**NET lokale Gruppe \ < Gruppe Name\ > / Hinzufügen**|
|Ändern Sie den Namen eines Computers Domäne|**Netdom Renamecomputer % Computername % /NewName:\<new Computer Name\ > /userd:\<domain\\username\ >/passwordd:** * |
|Bestätigen Sie den neuen Computernamen|**set**| 
|Ändern Sie den Namen eines Computers in einer Arbeitsgruppe|**Netdom Renamecomputer \ < Currentcomputername\ > NewName: \ < Newcomputername\ >** <br>Starten Sie den Computer neu.|
|Paging dateiverwaltung deaktivieren|**WMIC Computersystem, wobei Name = "\ < Computername\ >" festlegen AutomaticManagedPagefile = False**| 
|Konfigurieren Sie die Auslagerungsdatei|**WMIC Pagefileset, wobei Name = "\ < Pfad/Filename\ >" InitialSize festlegen = \ < Initialsize\ >, Max = \ < Maxsize\ >** <br>Dabei *Pfad/Dateiname* den Pfad und den Namen der Auslagerungsdatei, *Initialsize* den Ausgangspunkt Größe der Auslagerungsdatei in Bytes und *Maxsize* ist die maximale Größe der Page-Datei in Byte.|
|Ändern Sie in eine statische IP-Adresse|**Ipconfig/all** <br>Notieren Sie die entsprechende Informationen oder in eine Textdatei umleiten (**Ipconfig/all > ipconfig.txt**).<br>**Netsh Interface IPv4-anzeigen Schnittstellen**<br>Stellen Sie sicher, dass eine Schnittstellenliste vorhanden ist.<br>**Netsh Interface ipv4 legen Adressnamen \ <-ID aus der Schnittstelle List\ > Quelle = statischen Adresse = \ < IP-mailto:\[Email Address\ bevorzugte > Gateway = \ < Gateway mailto:\[Email Address\ >**<br>Führen Sie **Ipconfig/all** , Vierfy, die DHCP aktiviert auf **Nein**festgelegt ist.|
|Legen Sie eine statische DNS-Adresse.|**Netsh Interface ipv4 hinzufügen, Name des \<name oder die ID des Netzwerk-Schnittstelle-Card\ = > Adresse = \<IP Adresse das primäre DNS-Server\ > Index = 1 <br> **Netsh Interface ipv4 hinzufügen, Name des \<name der sekundäre DNS-Server\ = > Adresse = \<IP Adresse die sekundäre DNS-Server\ > Index 2 = ** <br> Wiederholen Sie zum Hinzufügen zusätzlicher Server angemessen.<br>Führen Sie **Ipconfig/all** um sicherzustellen, dass die Adressen richtig sind.|
|Ändern Sie in einer bereitgestellten DHCP-IP-Adresse von einer statischen IP-Adresse|**Netsh Interface ipv4 festlegen Adressname = \ < IP-Adresse des lokalen Betriebssystemebene und > Quelle DHCP =** <br>Führen Sie **Ipconfig/all** um sicherzustellen, dass DHCP aktiviert auf **Ja**festgelegt ist.|
|Geben Sie einen Product key|**slmgr.vbs – Ipk \ < Produkt Key\ >**| 
|Aktivieren Sie den Server lokal|**slmgr.vbs - ato**| 
|Aktivieren Sie den Server Remote|**Cscript slmgr.vbs – Ipk \ < Key\ Produkt > \ < Server Name\ > \ < Username\ > \ < Password\ >** <br>**Cscript slmgr.vbs - Ato \ < Servername\ > \ < Username\ > \ < Password\ >** <br>Rufen Sie die GUID des Computers mit **Cscript slmgr.vbs-haben** <br> Führen Sie **Cscript slmgr.vbs - Dli \<GUID\ >** <br>Stellen Sie sicher, dass Lizenzstatus **lizenziert (aktiviert)** festgelegt ist.


### Netzwerk- und firewall

|Aufgabe|Befehl| 
|----|-------|
|Konfigurieren Sie den Server aus, um einen Proxyserver verwenden|**Legen Sie Netsh Winhttp Proxy \ < Servername\ >: \ < Port Number\ >** <br>**Hinweis:** Server Core-Installationen können nicht über einen Proxy, die Verbindungen Kennwort erforderlich ist, das Internet zugreifen.|
|Konfigurieren Sie den Server aus, um den Proxyserver für Internetadressen umgehen|**Legen Sie Netsh Winttp Proxy \ < Servername\ >: \ < Port Number\ > umgehen-Liste = "\ < Local\ >"**| 
|Anzeigen oder Ändern von IPSec-Konfiguration|**Netsh-IPSec-**| 
|Anzeigen oder Ändern von NAP-Konfiguration|**Netsh nap**| 
|Anzeigen oder Ändern von IP auf physischen Adressübersetzung|**ARP**| 
|Anzeigen oder die lokale Routingtabelle konfigurieren|**Route**| 
|Zeigen Sie an, oder konfigurieren Sie DNS-server|**nslookup**| 
|Anzeigen von Protokollstatistiken und aktuelle TCP/IP-Netzwerkverbindungen|**netstat**| 
|Anzeigen von Protokollstatistiken und aktuelle TCP/IP-Verbindungen mit NetBIOS über TCP/IP (NBT)|**nbtstat**| 
|Anzeigen der Abschnitte für Netzwerkverbindungen|**pathping**| 
|Verfolgen Sie die Abschnitte für Netzwerkverbindungen|**tracert**| 
|Zeigen Sie die Konfiguration der multicast-router|**mrinfo**| 
|Aktivieren der Remoteverwaltung der firewall|**Netsh Advfirewall Firewall Regelgruppe festlegen = "Windows-Firewall-Remoteverwaltung" neue Enable = Yes**| 
 

### Updates, Fehlerberichterstattung und feedback

|Aufgabe|Befehl| 
|----|-------|
|Installieren Sie ein update|**Wusa \ < Update\ > MSU ausgeführte**| 
|Der installierten Listenupdates|**systeminfo**| 
|Entfernen eines Updates|**Erweitern Sie /f:\* \ < Update\ > MSU c:\test** <br>Navigieren Sie zu c:\test\, und öffnen Sie \ < Update\ > XML in einem Text-Editor.<br>Ersetzen Sie **Installieren** durch **Entfernen** , und speichern Sie die Datei.<br>**Pkgmgr /n:\ < Update\ > XML**|
|Automatische Updates konfigurieren|Überprüfen Sie die aktuelle Einstellung: ** Cscript %systemroot%\system32\scregedit.wsf au/v **<br>Automatische Updates aktivieren: **Cscript scregedit.wsf au 4** <br>So deaktivieren Sie automatische Updates: **Cscript %systemroot%\system32\scregedit.wsf au 1**| 
|Aktivieren Sie den Fehler.|Überprüfen Sie die aktuelle Einstellung: **ServerWerOptin/Query** <br>Detaillierte Berichte automatisch zu senden: **ServerWerOptin / detaillierte** <br>Zusammenfassung Berichte automatisch zu senden: **ServerWerOptin/Summary** <br>So deaktivieren Sie die Fehlerberichterstattung: **ServerWerOptin/Disable**|
|Teilnehmen Sie Customer Experience Improvement Program (CEIP)|Überprüfen Sie die aktuelle Einstellung: **ServerCEIPOptin/Query** <br>Um CEIP zu aktivieren: **ServerCEIPOptin/Enable** <br>So deaktivieren Sie CEIP: **ServerCEIPOptin/Disable**|

### Dienste, Prozesse und Leistung

|Aufgabe|Befehl| 
|----|-------|
|Liste der ausgeführten Dienste|**sc Query** "oder" **net start**| 
|Starten Sie einen Dienst|**sc starten \<service name\ >** oder **Net start \<service name\ >**| 
|Beenden Sie einen Dienst|**sc beenden \<service name\ >** oder **Net stop \<service name\ >**| 
|Rufen Sie eine Liste der ausgeführten Apps und die zugehörigen Prozesse ab|**tasklist**||Beenden Sie einen Prozess erzwingen|Führen Sie die Prozess-ID (PID) **Tasklist** abrufen, und führen Sie **Taskkill/pid \<process ID\ >**|
|Starten Sie Task-Manager|**taskmgr**| 
|Erstellen Sie und Verwalten von Ereignis-Sitzung und Leistung Protokolle|Ein Zähler, Trace, Konfiguration der Datensammlung oder eine API erstellen: **Logman ceate** <br>Abfrage Daten Collector Eigenschaften: **Logman Abfrage** <br>So starten oder beenden die Datensammlung: **Logman Start\ | beenden** <br>So löschen Sie eine Sammlung: **Logman löschen** <br> Aktualisieren Sie die Eigenschaften einer Sammlung: **Logman aktualisieren** <br>Eine Sammlung ein aus einer XML-Datei importieren oder exportieren es in einer XML-Datei: **Logman Import\ | export**|

### Ereignisprotokolle

|Aufgabe|Befehl| 
|----|-------|
|Liste der Ereignisprotokolle|**Wevtutil el**| 
|Abfrage-Ereignisse in einem angegebenen Protokoll|**Wevtutil Qe /f:text \ < protokollieren Name\ >**| 
|Ein Ereignisprotokoll exportieren|**Wevtutil Epl \ < protokollieren Name\ >**| 
|Löschen eines Ereignisprotokolls|**Wevtutil cl \ < protokollieren Name\ >**| 


### Datenträger und Dateisystem

|Aufgabe|Befehl|
|----|-------|
|Verwalten von Datenträgerpartitionen|Führen Sie eine vollständige Liste von Befehlen, **Diskpart /?**|  
|Verwalten von Software-RAID|Führen Sie eine vollständige Liste von Befehlen, **Diskraid /?**|  
|Verwalten von Bereitstellungspunkte|Führen Sie eine vollständige Liste von Befehlen, **Mountvol /?**| 
|Ein Volume Defragmentieren|Führen Sie eine vollständige Liste von Befehlen, **Disk Defragmenter ist aktiv /?**|  
|Konvertieren Sie ein Volume in das NTFS-Dateisystem|**Konvertieren Sie \ < Volume Letter\ >/FS: NTFS**| 
|Komprimieren Sie eine Datei|Führen Sie eine vollständige Liste von Befehlen, **compact /?**|  
|Verwalten von geöffneten Dateien|Führen Sie eine vollständige Liste von Befehlen, **Openfiles /?**|  
|Verwalten von VSS-Ordner|Führen Sie eine vollständige Liste von Befehlen, **Vssadmin /?**| 
|Verwalten des Dateisystems|Führen Sie eine vollständige Liste von Befehlen, **Fsutil /?**||Überprüfen Sie die Signatur einer Datei|**Sigverif /?**| 
|Übernehmen des Besitzes an Dateien und Ordner|Führen Sie eine vollständige Liste von Befehlen, **Icacls /?**| 
 
### Hardware

|Aufgabe|Befehl| 
|----|-------|
|Einen Treiber für neue Hardware hinzufügen|Kopieren Sie die Treiber in einen Ordner auf %homedrive%\\\ < Treiber Folder\ >. Führen Sie **Pnputil -i - ein %homedrive%\\\<driver Folder\ > \\\<driver\ > INF**|
|Treiber für ein Gerät zu entfernen|Führen Sie eine Liste von geladenen Treibern, **sc Query Type = Treiber**. Führen Sie **sc löschen \<service_name\ >**|
