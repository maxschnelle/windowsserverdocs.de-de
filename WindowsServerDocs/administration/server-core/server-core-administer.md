---
title: Verwalten von Server Core
description: Erfahren Sie, wie Sie eine Server Core-Installation von Windows Server verwalten.
ms.prod: windows-server
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.date: 12/18/2018
ms.openlocfilehash: bcc4bf7b3fbdbff1aed2c8dd07b90346fe9eebab
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383435"
---
# <a name="administer-a-server-core-server"></a>Verwalten eines Server Core-Servers

>Gilt für: Windows Server 2019, Windows Server 2016 und Windows Server (halbjährlicher Kanal)

Da Server Core nicht über eine Benutzeroberfläche verfügt, müssen Sie Windows PowerShell-Cmdlets, Befehlszeilen Tools oder Remote Tools verwenden, um grundlegende Verwaltungsaufgaben auszuführen. In den folgenden Abschnitten werden die PowerShell-Cmdlets und-Befehle für grundlegende Aufgaben erläutert. Sie können auch das [Windows Admin Center](../../manage/windows-admin-center/overview.md), ein einheitliches Verwaltungs Portal, das sich zurzeit in der öffentlichen Vorschau befindet, zum Verwalten Ihrer-Installation verwenden. 

## <a name="administrative-tasks-using-powershell-cmdlets"></a>Administrative Aufgaben mithilfe von PowerShell-Cmdlets
Verwenden Sie die folgenden Informationen, um grundlegende administrative Aufgaben mit Windows PowerShell-Cmdlets auszuführen.

### <a name="set-a-static-ip-address"></a>Festlegen einer statischen IP-Adresse
Wenn Sie einen Server Core-Server installieren, verfügt er standardmäßig über eine DHCP-Adresse. Wenn Sie eine statische IP-Adresse benötigen, können Sie Sie mithilfe der folgenden Schritte festlegen.

Verwenden Sie **Get-nettipconfiguration**, um die aktuelle Netzwerkkonfiguration anzuzeigen.

Verwenden Sie **Get-nettipaddress**, um die bereits verwendeten IP-Adressen anzuzeigen.

Gehen Sie folgendermaßen vor, um eine statische IP-Adresse festzulegen: 

1. Führen **Sie Get-nettipinterface**aus. 
2. Notieren Sie sich die Zahl in der **ifindex** -Spalte für Ihre IP-Schnittstelle oder die **interfacedescription** -Zeichenfolge. Wenn Sie über mehrere Netzwerkadapter verfügen, notieren Sie sich die Anzahl oder Zeichenfolge, die der Schnittstelle entspricht, für die Sie die statische IP-Adresse festlegen möchten.
3. Führen Sie das folgende Cmdlet aus, um die statische IP-Adresse festzulegen:

   ```powershell
   New-NetIPaddress -InterfaceIndex 12 -IPAddress 192.0.2.2 -PrefixLength 24 -DefaultGateway 192.0.2.1
   ```

   Dabei gilt Folgendes:
   - **Interfakeindex** ist der Wert von **ifindex** aus Schritt 2. (In unserem Beispiel 12)
   - **IPAddress** ist die statische IP-Adresse, die Sie festlegen möchten. (In unserem Beispiel 191.0.2.2)
   - **Prefixlength** ist die Präfix Länge (eine andere Form der Subnetzmaske) für die IP-Adresse, die Sie festlegen. (In unserem Beispiel 24)
   - **DefaultGateway** ist die IP-Adresse des Standard Gateways. (In unserem Beispiel 192.0.2.1)
4. Führen Sie das folgende Cmdlet aus, um die DNS-Client Server Adresse festzulegen: 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4
   ```
   
   Dabei gilt Folgendes:
   - **Interfakeindex** ist der Wert von ifindex aus Schritt 2.
   - **ServerAddress** ist die IP-Adresse Ihres DNS-Servers.
5. Wenn Sie mehrere DNS-Server hinzufügen möchten, führen Sie das folgende Cmdlet aus: 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4,192.0.2.5
   ```

   Dabei sind in diesem Beispiel **sind 192.0.2.4** und **192.0.2.5** beide IP-Adressen von DNS-Servern.

Wenn Sie zur Verwendung von DHCP wechseln müssen, führen Sie **Set-dnsclientserveraddress – interfakeindex 12 – resetserveraddress**aus.

### <a name="join-a-domain"></a>Beitreten zu einer Domäne
Verwenden Sie die folgenden Cmdlets, um einen Computer einer Domäne hinzuzufügen.

1. Führen **Sie Add-Computer**aus. Sie werden aufgefordert, beide Anmelde Informationen für den Beitritt zur Domäne und den Domänen Namen einzugeben.
2. Wenn Sie ein Domänen Benutzerkonto zur lokalen Administrator Gruppe hinzufügen müssen, führen Sie den folgenden Befehl an einer Eingabeaufforderung aus (nicht im PowerShell-Fenster):

   ```
   net localgroup administrators /add <DomainName>\<UserName>
   ```
3. Starten Sie den Computer neu. Führen Sie hierzu **Restart-Computer**aus.

### <a name="rename-the-server"></a>Umbenennen des Servers
Führen Sie die folgenden Schritte aus, um den Server umzubenennen.

1. Ermitteln Sie mit dem Befehl **hostname** oder **ipconfig** den aktuellen Namen des Servers.
2. Führen Sie **Rename-Computer-Computername \<new_name @ no__t-2**aus.
3. Starten Sie den Computer neu.

### <a name="activate-the-server"></a>Aktivieren des Servers

Führen Sie **slmgr. VSB – IPK @ no__t-1productkey @ no__t-2**aus. Führen Sie dann **slmgr. VSB – ATO**aus. Wenn die Aktivierung erfolgreich ist, erhalten Sie keine Nachricht.

> [!NOTE]
> Sie können den Server auch per Telefon aktivieren, indem Sie einen [KMS-Server (Key Management Service)](../../get-started/server-2016-activation.md)oder Remote verwenden. Um Remote zu aktivieren, führen Sie das folgende Cmdlet auf einem Remote Computer aus: 
> 
> ```
> cscript windows\system32\slmgr.vbs <ServerName> <UserName> <password>:-ato
> ```
 
### <a name="configure-windows-firewall"></a>Konfigurieren der Windows-Firewall

Die Windows-Firewall können Sie lokal auf dem Server Core-Computer mithilfe von Windows PowerShell-Cmdlets und -Skripts konfigurieren. Weitere Informationen finden Sie unter [Netsecurity](/powershell/module/netsecurity/?view=win10-ps) für die Cmdlets, mit denen Sie die Windows-Firewall konfigurieren können.

### <a name="enable-windows-powershell-remoting"></a>Aktivieren von Windows PowerShell-Remoting

Wenn Sie Windows PowerShell-Remoting aktivieren, werden in Windows PowerShell auf einem Computer eingegebene Befehle auf einem anderen Computer ausgeführt. Aktivieren Sie Windows PowerShell-Remoting mit **enable-psremoting**.

Weitere Informationen finden Sie unter Informationen [zu Remote-FAQ](/powershell/module/microsoft.powershell.core/about/about_remote_faq?view=powershell-5.1).

## <a name="administrative-tasks-from-the-command-line"></a>Verwaltungsaufgaben über die Befehlszeile
Verwenden Sie die folgenden Referenzinformationen, um Verwaltungsaufgaben über die Befehlszeile auszuführen.

### <a name="configuration-and-installation"></a>Konfiguration und Installation

|                             Aufgabe                              |                                                                                                                                                                                                                 Befehl                                                                                                                                                                                                                 |
|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|             Festlegen des lokalen Administratorkennworts             |                                                                                                                                                                                                      **net-Benutzer Administrator** \*                                                                                                                                                                                                      |
|                  Hinzufügen eines Computers zu einer Domäne                  |                                                                                                                                                       **netdom Join% Computername%** **/Domain: \<domain @ no__t-3/userd: \<domain @ no__t-5Username @ no__t-6/passwordd:** \* <br> Starten Sie den Computer neu.                                                                                                                                                        |
|              Bestätigen, dass die Domäne geändert wurde              |                                                                                                                                                                                                                 **set**                                                                                                                                                                                                                 |
|                Entfernen eines Computer aus einer Domäne                |                                                                                                                                                                                                   **netdom Remove \<computername @ no__t-2**                                                                                                                                                                                                    |
|         Hinzufügen eines Benutzers zur lokalen Gruppe "Administratoren"          |                                                                                                                                                                                       **net localgroup-Administratoren/Add \< Domäne @ no__t-2username @ no__t-3**                                                                                                                                                                                       |
|       Entfernen eines Benutzers aus der lokalen Gruppe "Administratoren"       |                                                                                                                                                                                     **net localgroup-Administratoren/DELETE \< Domäne @ no__t-2username @ no__t-3**                                                                                                                                                                                      |
|               Hinzufügen eines Benutzers zum lokalen Computer                |                                                                                                                                                                                                **NET User \<domäne \ Benutzername @ no__t-2 \*/Add**                                                                                                                                                                                                 |
|               Hinzufügen einer Gruppe zum lokalen Computer               |                                                                                                                                                                                                 **net localgroup \<Group Name @ no__t-2/Add**                                                                                                                                                                                                  |
|          Ändern des Namens eines Computers, der einer Domäne angehört          |                                                                                                                                                           **netdom renamecomputer% Computername%/newname: \<neuer Computername @ no__t-2/userd: \<domain @ no__t-4username @ no__t-5/passwordd:** \*                                                                                                                                                            |
|                 Bestätigen des neuen Computernamens                 |                                                                                                                                                                                                                 **set**                                                                                                                                                                                                                 |
|         Ändern des Namens eines Computers in einer Arbeitsgruppe         |                                                                                                                                                                **netdom renamecomputer \<currentcomputername @ no__t-2/newname: \<newcomputername @ no__t-4** <br>Starten Sie den Computer neu.                                                                                                                                                                 |
|                Deaktivieren der Verwaltung von Auslagerungsdateien                 |                                                                                                                                                                        **WMIC Computersystem WHERE Name = "\<computername @ no__t-2" Set AutomaticManagedPagefile = False**                                                                                                                                                                         |
|                   Konfigurieren der Auslagerungsdatei                   |                                                            **WMIC pagefileset WHERE Name = "\<path/filename @ no__t-2" Set InitialSize = \<initialsize @ no__t-4, MaximumSize = \<maxsize @ no__t-6** <br>Dabei ist *Pfad/Dateiname* der Pfad und Name der Auslagerungs Datei, *InitialSize* ist die Anfangs Größe der Auslagerungs Datei in Bytes, und *MaxSize* ist die maximale Größe der Auslagerungs Datei (in Bytes).                                                             |
|                 Wechseln zu einer statischen IP-Adresse                 | **ipconfig/all** <br>Notieren Sie die relevanten Informationen, oder leiten Sie Sie in eine Textdatei (**ipconfig/all > ipconfig. txt**) um.<br>**Netsh Interface IPv4 Show Interfaces**<br>Überprüfen Sie, ob eine Schnittstellen Liste vorhanden ist.<br>**Netsh Interface IPv4 set address Name \< ID from Interface List @ no__t-2 source = static address = \<preferred IP Address @ no__t-4 Gateway = \<gateway Address @ no__t-6**<br>Führen Sie **ipconfig/all** aus, um sicherzustellen, dass DHCP aktiviert auf **Nein**festgelegt ist. |
|                   Legen Sie eine statische DNS-Adresse fest.                   |   <strong>netsh Interface IPv4 Add DNSServer Name = \<name oder ID der Netzwerkschnittstellenkarte @ no__t-2 Address = \<IP-Adresse des primären DNS-Servers @ no__t-4 Index = 1 <br></strong>netsh Interface IPv4 Add DNSServer Name = \<name des sekundären DNS-Servers @ no__t-2 Address = \<IP-Adresse des sekundären DNS-Servers @ no__t-4 Index = 2 @ no__t-5 @ no__t-6 <br> Wiederholen Sie den Vorgang, um weitere Server hinzuzufügen.<br>Führen Sie **ipconfig/all** aus, um zu überprüfen, ob die Adressen korrekt sind.   |
| Wechseln von einer statischen IP-Adresse zu einer von DHCP bereitgestellten IP-Adresse |                                                                                                                                      **Netsh Interface IPv4 set address Name = \< IP-Adresse des lokalen Systems @ no__t-2 Quelle = DHCP** <br>Führen Sie **ipconfig/all** aus, um zu überprüfen, ob DCHP aktiviert auf **Ja**festgelegt ist.                                                                                                                                      |
|                      Eingeben eines Product Keys                      |                                                                                                                                                                                                   **slmgr. VSB – IPK \<product Key @ no__t-2**                                                                                                                                                                                                    |
|                  Lokales Aktivieren des Servers                  |                                                                                                                                                                                                           **slmgr. VSB-ATO**                                                                                                                                                                                                            |
|                 Remotes Aktivieren des Servers                  |                                            **cscript slmgr. VSB – IPK \<product Key @ no__t-2 @ no__t-3server Name @ no__t-4 @ no__t-5Username @ no__t-6 @ no__t-7password @ no__t-8** <br>**cscript slmgr. vb-ATO \<Server Name @ no__t-2 \<username @ no__t-4 \<password @ no__t-6** <br>Holen Sie sich die GUID des Computers durch Ausführen von **cscript slmgr. VSB-did** <br> Führen Sie **cscript slmgr. VSB-DLI \<guid @ no__t-2 aus.** <br>Vergewissern Sie sich, dass der Lizenzstatus auf **lizenziert (aktiviert)** festgelegt ist.                                             |

### <a name="networking-and-firewall"></a>Netzwerk und Firewall

|Aufgabe|Befehl| 
|----|-------|
|Konfigurieren des Servers für die Verwendung eines Proxy Servers|**Netsh WinHTTP Set Proxy \<Server Name @ no__t-2: \<port Nummer @ no__t-4** <br>**Hinweis**: Server Core-Installationen können nicht über einen Proxy auf das Internet zugreifen, das ein Kennwort erfordert, um Verbindungen zuzulassen.|
|Konfigurieren Sie den Server so, dass der Proxy für Internet Adressen umgangen wird.|**Netsh WinHTTP Set Proxy \<servername @ no__t-2: \<port Nummer @ no__t-4 Bypass-List = "\<local @ no__t-6"**| 
|Anzeigen oder Ändern der IPSec-Konfiguration|**Netsh IPSec**| 
|Anzeigen oder Ändern der NAP-Konfiguration|**netsh nap**| 
|Anzeigen oder Ändern der IP-Adresse für die physische Adressübersetzung|**arp**| 
|Anzeigen oder Konfigurieren der lokalen Routing Tabelle|**Seeweg**| 
|Anzeigen oder Konfigurieren von DNS-Servereinstellungen|**nslookup**| 
|Anzeigen von Protokollstatistiken und von aktuellen TCP/IP-Netzwerkverbindungen|**netstat**| 
|Anzeigen von Protokoll Statistiken und aktuellen TCP/IP-Verbindungen unter Verwendung von NetBIOS über TCP/IP (NBT)|**nbtstat**| 
|Anzeigen von Hops für Netzwerkverbindungen|**pathping**| 
|Ablaufverfolgungs-Hops für Netzwerkverbindungen|**tracert**| 
|Anzeigen der Konfiguration des Multicastrouters|**mrinfo**| 
|Aktivieren der Remote Verwaltung der Firewall|**netsh advfirewall firewall set rule Group = "Windows Defender Firewall Remote Management" New enable = yes**| 
 

### <a name="updates-error-reporting-and-feedback"></a>Updates, Fehlerberichterstattung und Feedback

|                               Aufgabe                                |                                                                                                                               Befehl                                                                                                                                |
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                         Installieren eines Updates                         |                                                                                                                    **Wusa @no__t -1Update\>.msu/quiet**                                                                                                                    |
|                      Auflisten von installierten Updates                       |                                                                                                                            **systeminfo**                                                                                                                            |
|                         Entfernen eines Updates                          |                                 **Expand/f: \* @no__t -2Update\>.msu c:\test** <br>Navigieren Sie zu "" c:\test\ "", und öffnen Sie @no__t -0update\>.XML in einem Text-Editor.<br>Ersetzen Sie **install** with **Remove** , und speichern Sie die Datei.<br>**pkgmgr/n: @no__t -1Update\>.XML**                                 |
|                    Konfigurieren von automatischen Updates                    |          So überprüfen Sie die aktuelle Einstellung: **cscript%systemroot%\system32\scregedit.wsf/au/v \* @ no__t-2 @ no__t-3to enable Automatic Updates: \* @ no__t-5cscript scregedit. wsf/au 4** <br>So deaktivieren Sie automatische Updates: **cscript%systemroot%\system32\scregedit.wsf/au 1**          |
|                      Aktivieren der Fehlerberichterstattung                       | So überprüfen Sie die aktuelle Einstellung: **serverweroptin/Query "aus** <br>So senden Sie automatisch ausführliche Berichte: **serverweroptin/detailed** <br>So senden Sie automatisch Zusammenfassungs Berichte: **serverweroptin/Summary** <br>So deaktivieren Sie die Fehlerberichterstattung: **serverweroptin/Disable** |
| Teilnehmen am Programm zur Verbesserung der Benutzerfreundlichkeit |                                                     So überprüfen Sie die aktuelle Einstellung: **serverceipoptin/Query "aus** <br>So aktivieren Sie CEIP: **serverceipoptin/enable** <br>So deaktivieren Sie CEIP: **serverceipoptin/Disable**                                                      |

### <a name="services-processes-and-performance"></a>Dienste, Prozesse und Leistung

|                               Aufgabe                               |                                                                                                                                                                                                             Befehl                                                                                                                                                                                                              |
|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                    Auflisten der laufenden Dienste                     |                                                                                                                                                                                                  **SC-Abfrage** oder **net Start**                                                                                                                                                                                                   |
|                         Starten eines Diensts                          |                                                                                                                                                                                 **SC Start \<dienst Name @ no__t-2** oder **net Start \<dienst Name @ no__t-5**                                                                                                                                                                                  |
|                          Beenden eines Diensts                          |                                                                                                                                                                                  **SC Beendigung \<dienst Name @ no__t-2** oder **net-\<Service-Name @ no__t-5**                                                                                                                                                                                   |
| Abrufen einer Liste mit ausgeführten Anwendungen und zugehörigen Prozessen |                                                                                                                                                                                                           **tasklist**                                                                                                                                                                                                           |
|                        Starten des Task-Managers                        |                                                                                                                                                                                                           **von "taskmgr**                                                                                                                                                                                                            |
|    Erstellen und Verwalten von Ereignis Ablauf Verfolgungs Sitzungen und Leistungs Protokollen    | So erstellen Sie einen Counter, eine Ablauf Verfolgung, eine Sammlung von Konfigurationsdaten oder eine API: **logman erstellen** <br>So Fragen Sie die Datensammler Eigenschaften ab: **Logman Query** <br>So starten oder verhindern Sie die Datensammlung: **logman Start @ no__t-1Stoppt** <br>So löschen Sie einen Collector: **logman delete** <br> So aktualisieren Sie die Eigenschaften eines Sammlers: **logman update** <br>So importieren Sie einen Datensammler Satz aus einer XML-Datei oder exportieren ihn in eine XML-Datei: **logman Import @ no__t-1export** |

### <a name="event-logs"></a>Ereignisprotokolle

|Aufgabe|Befehl| 
|----|-------|
|Auflisten von Ereignisprotokollen|**wevtutil El**| 
|Ereignisse in einem angegebenen Protokoll Abfragen|**wevtutil QE/f: Text \<log Name @ no__t-2**| 
|Exportieren eines Ereignis Protokolls|**wevtutil EPL \<log Name @ no__t-2**| 
|Löschen eines Ereignis Protokolls|**wevtutil cl \<log Name @ no__t-2**| 


### <a name="disk-and-file-system"></a>Datenträger- und Dateisystem

|                   Aufgabe                   |                        Befehl                        |
|------------------------------------------|-------------------------------------------------------|
|          Verwalten von Datenträgerpartitionen          | Führen Sie **DiskPart/?** aus, um eine komplette Liste der Befehle zu erhalten.  |
|           Verwalten von Software-RAID           | Führen Sie **Diskraid/?** aus, um eine komplette Liste der Befehle zu erhalten.  |
|        Verwalten von Volumebereitstellungspunkten        | Eine komplette Liste der Befehle erhalten Sie, wenn Sie " **mountvol/?** " ausführen.  |
|           Defragmentieren eines Volumes            |  Führen Sie **Defragmentierung/?** aus, um eine komplette Liste der Befehle zu erhalten.   |
| Konvertieren eines Volumes in das NTFS-Dateisystem |        **Konvertieren von \< Volume Letter @ no__t-2/FS: NTFS**         |
|              Komprimieren einer Datei              |  Führen Sie **Compact/?** aus, um eine komplette Liste der Befehle zu erhalten.  |
|          Verwalten geöffneter Dateien           | Führen Sie **openfiles/?** aus, um eine komplette Liste der Befehle zu erhalten. |
|          Verwalten von VSS-Ordnern          | Führen Sie **vssadmin/?** aus, um eine komplette Liste der Befehle zu erhalten.  |
|        Verwalten des Dateisystems        |  Führen Sie für eine komplette Liste der Befehle den Befehl " **f** " aus.   |
|    Übernehmen des Besitzes für eine Datei oder einen Ordner    |  Führen Sie **icacls/?** aus, um eine komplette Liste der Befehle zu erhalten.   |
 
### <a name="hardware"></a>Hardware

|Aufgabe|Befehl| 
|----|-------|
|Hinzufügen eines Treibers für ein neues Hardwaregerät|Kopieren Sie den Treiber in einen Ordner unter "% HomeDrive% \\ @ no__t-1driver Folder @ no__t-2". Führen Sie **PnPUtil-i-a% HOMEDRIVE% \\ @ no__t-2driver Folder @ no__t-3 @ no__t-4 @ no__t-5driver\>.inf** aus.|
|Entfernen eines Treibers für ein Hardwaregerät|Um eine Liste geladener Treiber zu erhalten, führen Sie **SC Query Type = Driver**aus. Führen Sie dann **SC DELETE \<service_name @ no__t-2** aus.|
