---
title: Unterbefehl Set-Server
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da55c29d-a94a-4d73-877b-af480f906ca0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: abc3fe23558f077e0ba9ac69f2641e3b8c9cde4f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858381"
---
# <a name="subcommand-set-server"></a>Unterbefehl: Set-Server

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Konfiguriert die Einstellungen für einen Windows-Bereitstellungsdienste-Server.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Set-Server [/Server:<Server name>]
    [/Authorize:{Yes | No}]
    [/RogueDetection:{Yes | No}]
    [/AnswerClients:{All | Known | None}]
    [/Responsedelay:<time in seconds>]
    [/AllowN12forNewClients:{Yes | No}]
    [/ArchitectureDiscovery:{Yes | No}]
    [/resetBootProgram:{Yes | No}]
    [/DefaultX86X64Imagetype:{x86 | x64 | Both}]
    [/UseDhcpPorts:{Yes | No}]
    [/DhcpOption60:{Yes | No}]
    [/RpcPort:<Port number>]
    [/PxepromptPolicy 
        [/Known:{OptIn | Noprompt | OptOut}]
        [/New:{OptIn | Noprompt | OptOut}] 
    [/BootProgram:<Relative path>]
         /Architecture:{x86 | ia64 | x64}
    [/N12BootProgram:<Relative path>]
         /Architecture:{x86 | ia64 | x64}
    [/BootImage:<Relative path>]
         /Architecture:{x86 | ia64 | x64}
    [/PreferredDC:<DC Name>]
    [/PreferredGC:<GC Name>]
    [/PrestageUsingMAC:{Yes | No}]
    [/NewMachineNamingPolicy:<Policy>]
    [/NewMachineOU]
         [/type:{Serverdomain | Userdomain | UserOU | Custom}]
         [/OU:<Domain name of OU>]
    [/DomainSearchOrder:{GCOnly | DCFirst}]
    [/NewMachineDomainJoin:{Yes | No}]
    [/OSCMenuName:<Name>]
    [/WdsClientLogging]
         [/Enabled:{Yes | No}]
         [/LoggingLevel:{None | Errors | Warnings | Info}]
    [/WdsUnattend]
         [/Policy:{Enabled | Disabled}]
         [/CommandlinePrecedence:{Yes | No}]
         [/File:<path>]
             /Architecture:{x86 | ia64 | x64}
    [/AutoaddPolicy]
         [/Policy:{AdminApproval | Disabled}]
         [/PollInterval:{time in seconds}]
         [/MaxRetry:{Retries}]
         [/Message:<Message>]
         [/RetentionPeriod]
             [/Approved:<time in days>]
             [/Others:<time in days>]
    [/AutoaddSettings]
         /Architecture:{x86 | ia64 | x64}
         [/BootProgram:<Relative path>]
         [/ReferralServer:<Server name>
         [/WdsClientUnattend:<Relative path>]
         [/BootImage:<Relative path>]
         [/User:<Owner>]
         [/JoinRights:{JoinOnly | Full}]
         [/JoinDomain:{Yes | No}]
    [/BindPolicy]
         [/Policy:{Include | Exclude}]
         [/add]
              /address:<IP or MAC address>
              /addresstype:{IP | MAC}
         [/remove]
              /address:<IP or MAC address>
              /addresstype:{IP | MAC}
    [/RefreshPeriod:<time in seconds>]
    [/BannedGuidPolicy]
         [/add]
              /Guid:<GUID>
         [/remove]
             /Guid:<GUID>
    [/BcdRefreshPolicy]
         [/Enabled:{Yes | No}]
         [/RefreshPeriod:<time in minutes>]
    [/Transport]
         [/ObtainIpv4From:{Dhcp | Range}]
             [/start:<start IP address>]
             [/End:<End IP address>]
         [/ObtainIpv6From:Range]
             [/start:<start IP address>]
             [/End:<End IP address>]
         [/startPort:<start Port>
             [/EndPort:<start Port>
        [/Profile:{10Mbps | 100Mbps | 1Gbps | Custom}]
        [/MulticastSessionPolicy]
             [/Policy:{None | AutoDisconnect | Multistream}]
                 [/Threshold:<Speed in KBps>]
                 [/StreamCount:{2 | 3}]
                 [/Fallback:{Yes | No}]    
        [/forceNative]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
|[/Authorize:{Yes &#124; No}]|Gibt an, ob dieser Server in das Dynamic Host Control Protocol (DHCP) zu autorisieren.|
|[/RogueDetection:{Yes &#124; No}]|Aktiviert oder deaktiviert die DHCP-Rogue-Erkennung.|
|[/ AnswerClients: {alle &#124; bezeichnet &#124; None}]|Gibt an, welche Clients, die diesem Server beantwortet werden sollen. Wenn Sie diesen Wert, um festlegen **bezeichnet**, ein Computer in active Directory-Domänendienste (AD DS) vorab bereitgestellt werden muss, bevor sie vom Windows-Bereitstellungsdienste-Server beantwortet wird.|
|[/ Responsedelay:<time in seconds>]|Die Zeitspanne, die der Server für die Beantwortung eines startenden Clients gewartet wird. Diese Einstellung gilt nicht für vorab bereitgestellten Computern.|
|[/AllowN12forNewClients:{Yes &#124; No}]|für Windows Server 2008 gibt an, dass unbekannte Clients nicht die Taste F12 drücken hat, um einen Netzwerkstart zu initiieren. Bekannte Clients erhalten die Boot-Anwendung, die für den Computer angegeben, oder, wenn nicht angegeben ist, wird die Boot-Anwendung für angegebene der Architektur.<br /><br />für Windows Server 2008 R2, wurde diese Option mit dem folgenden Befehl ersetzt: Wdsutil/AutoAddPolicy pxepromptpolicy /New:Noprompt|
|[/ArchitectureDiscovery:{Yes &#124; No}]|Aktiviert oder deaktiviert die Ermittlung der Architektur. Dies ermöglicht die Ermittlung von X64-basierte Clients, die nicht ihrer Architektur ordnungsgemäß übertragen werden.|
|[/resetBootProgram:{Yes &#124; No}]|Bestimmt, ob der Startpfad für einen Client gelöscht wird, die gerade gestartet wurde, ohne ein Drücken der Taste F12.|
|[/DefaultX86X64Imagetype: {x86 &#124; x64 &#124; Both}]|Steuert, welche Startimages werden X64-basierte Clients angezeigt.|
|[/UseDhcpPorts:{Yes &#124; No}]|Gibt an, und zwar unabhängig davon, ob der PXE-Server versuchen, eine Bindung mit dem DHCP-Port, TCP-port 67. Wenn DHCP und Windows-Bereitstellungsdienste auf demselben Computer ausgeführt werden, sollten Sie diese Option festlegen, um **keine** So aktivieren Sie die DHCP-Server an den Port verwenden, und legen Sie die **/DhcpOption60** Parameter **Ja**. Die Standardeinstellung für diesen Wert **Ja**.|
|[/DhcpOption60:{Yes &#124; No}]|Gibt an, ob der DHCP-Option 60 für PXE-Unterstützung konfiguriert werden soll. Wenn DHCP und Windows-Bereitstellungsdienste auf demselben Server ausführen, legen Sie diese Option, um **Ja** und legen Sie die **/UseDhcpPorts** option **keine**. Die Standardeinstellung für diesen Wert **keine**.|
|[/RpcPort:<Port number>]|Gibt an, die TCP-Portnummer verwendet werden, um Clientanforderungen zu bedienen.|
|[/PxepromptPolicy]|Konfiguriert wie bekannte (Staging) und neue Clients initiieren Sie einen PXE-Start. Diese Option gilt nur für Windows Server 2008 R2. Sie haben die Einstellungen, die mithilfe der folgenden Optionen festlegen:<br /><br />-[/ Bekannte: {OptIn&#124;"OptOut"&#124;Noprompt}]-legt die Richtlinie für die vorab bereitgestellte Clients.<br />-[/ New: {OptIn&#124;"OptOut"&#124;Noprompt}]-legt die Richtlinie für neue Clients.<br /><br />**OptIn** bedeutet, dass der Client in der Reihenfolge nach PXE-Start eine Taste zu drücken muss, andernfalls es wird ein Fallback auf den nächsten Startgerät.<br /><br />**Noprompt** bedeutet, dass der Client wird immer PXE-Start.<br /><br />**"OptOut"** bedeutet, dass der Client werden PXE-Start, es sei denn, die Esc-Taste gedrückt wird.|
|[/BootProgram:<Relative path>] /Architecture:{x86 &#124; ia64 &#124; x64}|Gibt den relativen Pfad zum die Boot-Anwendung im Ordner "RemoteInstall" (z. B. **boot\x86\pxeboot.n12**), und gibt die Architektur des Programms starten.|
|[/N12BootProgram:<Relative path>] /Architecture:{x86 &#124; ia64 &#124; x64}|Gibt den relativen Pfad für das Startprogramm, das Drücken der Taste F12 nicht erforderlich ist (z. B. **boot\x86\pxeboot.n12**), und gibt die Architektur des Programms starten.|
|[/BootImage:<Relative path>] /Architecture:{x86 &#124; ia64 &#124; x64}|Gibt den relativen Pfad zum Startabbild, das Starten von Clients erhalten, und gibt die Architektur des Startabbilds an. Sie können dies für jede Architektur angeben.|
|[/PreferredDC:<DC Name>]|Gibt den Namen des Domänencontrollers, die Windows-Bereitstellungsdienste verwenden soll. Dies kann entweder den NetBIOS-Namen oder den FQDN sein.|
|[/PreferredGC:<GC Name>]|Gibt den Namen der vom globalen Katalogserver, den Windows-Bereitstellungsdienste verwenden soll. Dies kann entweder den NetBIOS-Namen oder den FQDN sein.|
|[/PrestageUsingMAC:{Yes &#124; No}]|Gibt an, ob Windows Deployment Services, Erstellung von Computerkonten in AD DS die MAC-Adresse statt auf die GUID/UUID verwenden sollten, um den Computer zu identifizieren.|
|[/NewMachineNamingPolicy:<Policy>]|Gibt das Format, das beim Generieren von Computernamen für Clients verwendet werden. Informationen über das Format für die Verwendung <policy>mit der rechten Maustaste auf den Server im Mmc-Snap-in, klicken Sie auf **Eigenschaften**, und zeigen Sie die **Verzeichnisdienste** Registerkarte. Z. B. **/NewMachineNamingPolicy: % 61Username % #**.|
|[/NewMachineOU]|Verwendet, um den Speicherort in AD DS angeben, unter der Clientcomputerkonten erstellt werden. Sie geben Sie mithilfe der folgenden Optionen an.<br /><br />-[/ type: Serverdomain &#124; Userdomain &#124; Benutzerorganisationseinheit an &#124; benutzerdefinierte] Gibt den Typ des Speicherorts. **Serverdomain** Konten in derselben Domäne wie der Windows-Bereitstellungsdienste-Server erstellt. **UserDomain** Konten in derselben Domäne wie der Benutzer, die beim Ausführen der Installation erstellt. **Benutzerorganisationseinheit an** Konten in der Organisationseinheit des Benutzers beim Ausführen der Installation erstellt. **Benutzerdefinierte** können Sie einen benutzerdefinierten Speicherort angeben (Sie müssen auch angeben, einen Wert für **OU** mit dieser Option).<br />-[/ OU:<Domain name of OU>]: bei Angabe von **benutzerdefinierte** für die **/type** können diese Option gibt die Organisationseinheit, in dem Computerkonten erstellt werden soll.|
|[/DomainSearchOrder:{GCOnly &#124; DCFirst}]|Gibt die Richtlinie für die Suche von Computerkonten in AD DS (globalen Katalog oder Domänencontroller).|
|[/NewMachineDomainJoin:{Yes &#124; No}]|Gibt an, und zwar unabhängig davon, ob ein Computer, der in AD DS nicht bereits vorab bereitgestellt wird während der Installation mit der Domäne verknüpft werden soll. Die Standardeinstellung ist **Ja**.|
|[/WdsClientLogging]|Gibt den Protokolliergrad für den Server an.<br /><br />-[/ Aktiviert: {Yes &#124; No}]: aktiviert oder deaktiviert die Protokollierung von Windows-Bereitstellungsdienste-Client-Aktionen.<br />-[/ LoggingLevel: {None &#124; Fehler &#124; Warnungen &#124; Info}-legt den Protokolliergrad fest. **Keine** entspricht dem Deaktivieren der Protokollierung. **Fehler** wird von die untersten Ebene der Protokollierung und gibt an, dass nur Fehler protokolliert werden. **Warnungen** enthält Warnungen und Fehler. **Info** ist die höchste Ebene der Protokollierung und enthält Fehler, Warnungen und Informationsereignisse.|
|[/WdsUnattend]|Diese Einstellungen steuern das Verhalten für die unbeaufsichtigte Installation von Windows-Bereitstellungsdienste-Client. Sie haben die Einstellungen, die mithilfe der folgenden Optionen festlegen:<br /><br />-[/ Policy: {aktiviert &#124; deaktiviert}]: Gibt an, ob für die unbeaufsichtigte Installation verwendet wird.<br />-[/ CommandlinePrecedence: {Yes &#124; No}]: Gibt an, ob die Datei "Autounattend.xml" (falls vorhanden, auf dem Client) oder eine unbeaufsichtigte Setupdatei, die direkt an dem Windows-Bereitstellungsdienste-Client mit der Option/Unattend in Verbindung übergeben wurde anstelle von verwendet wird für die unbeaufsichtigte Installation Bilddatei während einer Clientinstallation. Die Standardeinstellung ist **keine**.<br />-[/ File:<Relative path> Architecture: {X86 &#124; ia64 &#124; X64}]: Gibt den Dateinamen, den Pfad und die Architektur der Datei für die unbeaufsichtigte Installation.|
|[/AutoaddPolicy]|Diese Einstellungen steuern die Richtlinie zum automatischen hinzufügen. Sie definieren die Einstellungen, die mithilfe der folgenden Optionen:<br /><br />-[/ Policy: {AdminApproval &#124; deaktiviert}]- **AdminApprove** bewirkt, dass alle unbekannten Computer einer Warteschlange, hinzugefügt werden, in dem der Administrator dann überprüfen Sie die Liste von Computern und genehmigen oder ablehnen kann jeder Anforderung als geeignet. **Deaktivierte** gibt an, dass keine weitere Aktion ausgeführt wird, wenn ein Unbekannter Computer startet mit dem Server versucht.<br />-[/ Sein Abfrageintervall: {Time in Sekunden}]: Gibt das Intervall (in Sekunden), in dem das Netzwerkstartprogramm sollte die Windows-Bereitstellungsdienste-Server Abfragen.<br />-[/ MaxRetry: <Number>]: Gibt an, wie oft das Netzwerkstartprogramm muss die Windows-Bereitstellungsdienste-Server eine Abfrage durchführen. Dieser Wert zusammen mit **/PollInterval**, bestimmt, wie lange das Netzwerkstartprogramm für einen Administrator zum Genehmigen oder Ablehnen des Computers, bevor ein Timeout gewartet wird. Z. B. eine **MaxRetry** Wert 10 und ein **sein Abfrageintervall** Vlue von 60 würde angeben, dass der Client den Server 10-Mal abrufen soll 60 Sekunden zwischen den Versuchen gewartet. Aus diesem Grund wird der Client Timeout nach 10 Minuten (10 x 60 Sekunden = 10 Minuten).<br />-[/ Message: <Message>]: Gibt die Meldung, die an den Client auf der dialogfeldseite für Network Boot Program angezeigt wird.<br />-[/RetentionPeriod]: Gibt die Anzahl der Tage, die ein Computer im Status "Ausstehend" sein kann, bevor diese automatisch gelöscht werden.<br />-[/ Genehmigt: <time in days>]: Gibt die Beibehaltungsdauer für die genehmigte Computer. Sie müssen diesen Parameter verwenden die **/RetentionPeriod** Option.<br />-[/ Andere: <time in days>]: Gibt die Beibehaltungsdauer für nicht genehmigte Computer ("abgelehnt" oder "Ausstehend"). Sie müssen diesen Parameter verwenden die **/RetentionPeriod** Option.|
|[/AutoaddSettings]|Gibt an, die Standardeinstellungen, die auf jedem Computer angewendet werden. Sie definieren die Einstellungen, die mithilfe der folgenden Optionen:<br /><br />-Architecture: {X86 &#124; ia64 &#124; X64}-gibt die Architektur.<br />-[/ BootProgram: <Relative path>]: Gibt an, die Boot-Anwendung, die an den genehmigte Computer gesendet. Wenn kein Boot-Programm angegeben ist, wird der Standardwert für die Architektur des Computers (wie angegeben, auf dem Server) verwendet werden.<br />-[/ WdsClientUnattend: <Relative path>]-legt den relativen Pfad zur Datei für die unbeaufsichtigte Installation, die der genehmigte Client erhalten soll.<br />-[/ ReferralServer: <Server name>]: Gibt an, die Windows-Bereitstellungsdienste-Server, die vom Client verwendet wird, um Bilder herunterzuladen.<br />-[/ BootImage: <Relative path>]: Gibt das Startabbild an, die der genehmigte Client empfangen wird.<br />-[/ Benutzer: < Domäne\Benutzer &#124; User@Domain>]-Berechtigungen für das Computerkonto-Objekt, das dem angegebenen Benutzer die erforderlichen Rechte für den Beitritt zur Domäne geben festgelegt.<br />-[JoinRights: {JoinOnly &#124; vollständige}]: Gibt den Typ der Rechte für den Benutzer zugewiesen werden. **JoinOnly** muss der Administrator das Computerkonto zurückgesetzt werden, bevor der Benutzer den Computer der Domäne beitreten kann. **Vollständige** erhalten Sie Vollzugriff für den Benutzer, einschließlich des rechts, um den Computer der Domäne zu verknüpfen.<br />-[/ JoinDomain: {Ja &#124; No}]: Gibt an, und zwar unabhängig davon, ob der Computer der Domäne als dieses Konto während einer Installation von Windows-Bereitstellungsdienste hinzugefügt werden soll. Die Standardeinstellung ist **Ja**.|
|[/BindPolicy]|Konfiguriert die Netzwerkschnittstellen für den PXE-Anbieter für das Lauschen an. Sie definieren die Richtlinie mithilfe der folgenden Optionen:<br /><br />-[/ Policy: {Include &#124; ausschließen}]-legt die Richtlinie zur Schnittstelle binden, die Adressen in der Schnittstellenliste ein- oder ausgeschlossen.<br />-[/ add] - Fügt eine Schnittstelle zur Liste hinzu. Sie müssen auch/addressType "und" Address angeben.<br />-[/ Remove]: entfernt eine Schnittstelle aus der Liste. Sie müssen auch/addressType "und" Address angeben.<br />- / Adresse:<IP or MAC address> – gibt an, die IP- oder MAC-Adresse der Schnittstelle zum Hinzufügen oder entfernen.<br />-/ addressType: {IP &#124; MAC}-gibt den Typ der Adresse angegeben wird, der **/Adresse** Option.|
|[/RefreshPeriod: <seconds>]|Gibt Häufigkeit (in Sekunden), dem Server führt die Einstellungen werden aktualisiert.|
|[/BannedGuidPolicy]|Verwaltet die Liste der gesperrten GUIDs, die mithilfe der folgenden Optionen:<br /><br />-[/ add] /Guid:<GUID> -fügt die angegebene GUID der Liste der gesperrten GUIDs. Jeder Client mit dieser GUID wird stattdessen durch die MAC-Adresse identifiziert werden.<br />-[/ Remove] /Guid:<GUID> – entfernt die angegebene GUID aus der Liste der gesperrten GUIDs.|
|[/BcdRefreshPolicy]|Konfiguriert die Einstellungen für die Aktualisierung des Bcd-Dateien, die mithilfe der folgenden Optionen:<br /><br />-[/ Aktiviert: {Ja &#124; No}]: Gibt an, die BCD-Datei Aktualisieren der Richtlinie. Wenn **/aktiviert** nastaven NA hodnotu **Ja**, Bcd-Dateien in das angegebene Zeitintervall aktualisiert werden.<br />-[/ RefreshPeriod:<time in minutes>]: Gibt das Zeitintervall, in der Bcd Dateien aktualisiert werden.|
|[/Transport]|Konfiguriert die folgenden Optionen:<br /><br /><ul><li>[/ ObtainIpv4From: {Dhcp &#124; Bereich}]: Gibt die Quelle der IPv4-Adressen.<br /><br /><ul><li>[/ start: <starting Ipv4 address>]: Gibt den Anfang des IP-Adressbereichs. Diese Option ist erforderlich und nur gültig, wenn **/ObtainIpv4From** nastaven NA hodnotu **Bereich**</li><li>[/ End: <Ending Ipv4 address>]: Gibt das Ende des IP-Adressbereichs. Diese Option ist erforderlich und nur gültig, wenn **/ObtainIpv4From** nastaven NA hodnotu **Bereich**.</li></ul></li><li>[/ ObtainIpv6From:Range] [/ start:<start IP address>] [/ End:<End IP address>] Gibt die Quelle der IPv6-Adressen. Diese Option gilt nur für Windows Server 2008 R2 und der einzige unterstützte Wert ist der Bereich.</li><li>[/ Startport-Wert: <starting port>]: Gibt den Anfang der Portbereich.</li><li>[/ Endport-Wert: <Ending port>]: Gibt das Ende der Portbereich.</li><li>[/ Profile: {10 Mbit/s &#124; 100 Mbit/s &#124; 1 Gbit/s &#124; benutzerdefinierte}]: Gibt an, das Netzwerkprofil verwendet werden. Diese Option ist nur von unterstützten Forservers unter Windows Server 2008.</li><li>[/MulticastSessionPolicy]  Konfiguriert die ODX-Einstellungen für Multicastübertragungen an. Dieser Befehl ist nur für Windows Server 2008 R2 verfügbar.<br /><br /><ul><li>[/ Policy: {None &#124; automatischen Verbindungsabbruch &#124; Zusatzkopie}]-Gewusst wie: Behandeln von langsamen Clients bestimmt. Keine bedeutet, dass alle Clients in einer Sitzung mit derselben Geschwindigkeit zu halten. Automatischen Verbindungsabbruch bedeutet, dass alle Clients, die unter der angegebenen /Threshold fällt getrennt werden. Zusatzkopie bedeutet, dass es sich bei Clients in mehreren Sitzungen laut /StreamCount getrennt werden.</li><li>[/ Schwellenwert:<Speed in KBps>]: /Policy:AutoDisconnect, diese Option legt die minimale Übertragungsrate in Kbit/s. Clients, die unter dieser Rate fällt werden von Multicastübertragungen getrennt.</li><li>[/ StreamCount: {2 &#124; 3}] [/ Fallback: {Yes &#124; No}]-für /Policy:Multistream, diese Option bestimmt die Anzahl der Sitzungen. 2 steht für zwei Sitzungen (schnellsten bzw. langsamsten) 3 bedeutet, dass drei Sitzungen (Fast "langsam," Mittel ",").</li><li>[/ Fallback: {Yes&#124; No}]-bestimmt, ob Clients, die getrennt sind, mit die Übertragung mit einer anderen Methode, (wenn vom Client unterstützt) fortfahren. Wenn Sie den WDS-Clients verwenden, der Computer erfolgt ein Fallback auf Unicasting. Einen Fallbackmechanismus unterstützt Wdsmcast.exe nicht. Diese Option gilt auch für Clients, die keine Zusatzkopie unterstützen. In diesem Fall wird der Computer auf eine andere Methode anstelle der Wechsel zu einer langsameren übertragungssitzung zurückgreifen.</li></ul></li></ul>|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie Folgendes ein, um den Server für mit einer Verzögerung von 4 Minuten, nur bekannten Clients zu beantworten:
```
wdsutil /Set-Server /AnswerClients:Known /Responsedelay:4
```
Um die Boot-Anwendung und die Architektur für den Server festzulegen, geben Sie Folgendes ein:
```
wdsutil /Set-Server /BootProgram:boot\x86\pxeboot.n12 /Architecture:x86
```
Um die Protokollierung auf dem Server aktivieren, geben Sie Folgendes ein:
```
wdsutil /Set-Server /WdsClientLogging /Enabled:Yes /LoggingLevel:Warnings
```
So aktivieren Sie für die unbeaufsichtigte Installation auf dem Server als auch die Architektur und die Client für die unbeaufsichtigte Installation, Typ:
```
wdsutil /Set-Server /WdsUnattend /Policy:Enabled /File:WDSClientUnattend \unattend.xml /Architecture:x86
```
Um den Pre-Boot Execution Environment (PXE) Server versucht, die zum Binden an TCP-Ports 67 und 60 festzulegen, geben Sie Folgendes ein:
```
wdsutil /Set-server /UseDhcpPorts:No /DhcpOption60:Yes
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Disable-Server-Befehl](using-the-disable-server-command.md)
[mit dem Enable-Server-Befehl](using-the-enable-server-command.md)
[mithilfe der Get-Server-Befehl](using-the-get-server-command.md)
[mithilfe des Befehls Initialize-Server](using-the-initialize-server-command.md)
[Unterbefehl: Start-Server](subcommand-start-server.md) 
 [ Unterbefehl: Stop-Server](subcommand-stop-server.md)
[die Uninitialize-Server-Option](the-uninitialize-server-option.md)
