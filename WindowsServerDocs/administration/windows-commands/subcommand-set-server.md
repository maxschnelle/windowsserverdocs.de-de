---
title: Unterbefehls Satz-Server
description: Referenz Artikel für den Unterbefehl set-Server, der die Einstellungen für einen Windows-Bereitstellungsdiensteserver konfiguriert hat.
ms.topic: article
ms.assetid: da55c29d-a94a-4d73-877b-af480f906ca0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aa9a40be9b2af534ddf80b03e2c56ac06b533a75
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882135"
---
# <a name="subcommand-set-server"></a>Unterbefehl: Set-Server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konfiguriert die Einstellungen für einen Windows-Bereitstellungsdiensteserver.

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
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|[/Authorize-Endpunkt: {yes &#124; No}]|Gibt an, ob dieser Server in Dynamic Host Control Protocol (DHCP) autorisiert werden soll.|
|[/RogueDetection: {yes &#124; No}]|Aktiviert oder deaktiviert die nicht autorisierte DHCP-Erkennung.|
|[/AnswerClients: {all &#124; known &#124; none}]|Gibt an, welche Clients von diesem Server beantwortet werden. Wenn Sie diesen Wert auf **bekannt**festlegen, muss ein Computer vorab in den Active Directory-Domänen Diensten (AD DS) bereitgestellt werden, bevor er vom Windows-Bereitstellungsdiensteserver beantwortet wird.|
|[/ResponseDelay: <time in seconds> ]|Die Zeitspanne, die der Server wartet, bevor er einen Start Client beantwortet. Diese Einstellung gilt nicht für vorab bereitgestellte Computer.|
|[/AllowN12forNewClients: {yes &#124; No}]|gibt für Windows Server 2008 an, dass unbekannte Clients die Taste F12 nicht drücken müssen, um einen Netzwerkstart zu initiieren. Bekannte Clients erhalten das Start Programm, das für den Computer angegeben wird, oder, falls nicht angegeben, das für die Architektur angegebene Start Programm.<p>für Windows Server 2008 R2 wurde diese Option durch den folgenden Befehl ersetzt: WDSUTIL/Set-Server/PxepromptPolicy/neue: noprompt|
|[/ArchitectureDiscovery: {yes &#124; No}]|Aktiviert oder deaktiviert die Architektur Ermittlung. Dadurch wird die Ermittlung von x64-basierten Clients ermöglicht, die ihre Architektur nicht ordnungsgemäß übertragen.|
|[/resetBootProgram: {yes &#124; No}]|Bestimmt, ob der Start Pfad für einen Client gelöscht wird, der gerade gestartet wurde, ohne dass eine F12-Taste gedrückt werden muss.|
|[/DefaultX86X64Imagetype: {x86 &#124; x64 &#124; beide}]|Steuert, welche Start Abbilder x64-basierten Clients angezeigt werden.|
|[/UseDhcpPorts: {yes &#124; No}]|Gibt an, ob der PXE-Server versuchen soll, eine Bindung zum DHCP-Port, TCP-Port 67, herzustellen. Wenn die DHCP-und Windows-Bereitstellungs Dienste auf dem gleichen Computer ausgeführt werden, sollten Sie diese Option auf **Nein** festlegen, damit der DHCP-Server den Port verwenden kann, und den **/DhcpOption60** -Parameter auf **Yes**festlegen. Die Standardeinstellung für diesen Wert ist **Ja**.|
|[/DhcpOption60: {yes &#124; No}]|Gibt an, ob die DHCP-Option 60 für PXE-Unterstützung konfiguriert werden soll. Wenn die DHCP-und Windows-Bereitstellungs Dienste auf demselben Server ausgeführt werden, legen Sie diese Option auf **Ja** fest, und legen Sie die **/UseDhcpPorts** -Option auf **Nein**fest. Die Standardeinstellung für diesen Wert ist **Nein**.|
|[/RpcPort: <Port number> ]|Gibt die TCP-Portnummer an, die zum Dienst von Client Anforderungen verwendet werden soll.|
|[/PxepromptPolicy]|Konfiguriert, wie bekannte (vorab bereitgestellte) und neue Clients einen PXE-Start initiieren. Diese Option gilt nur für Windows Server 2008 R2. Sie legen die Einstellungen mithilfe der folgenden Optionen fest:<p>-[/Known: {optin&#124;OptOut&#124;noprompt}]: legt die Richtlinie für vorab bereitgestellte Clients fest.<br />-[/Neue: {optin&#124;OptOut&#124;noprompt}]: legt die Richtlinie für neue Clients fest.<p>**Optin** bedeutet, dass der Client eine Taste drücken muss, um PXE-Start zu starten. andernfalls wird auf das nächste Startgerät zurückgegriffen.<p>**Noprompt** bedeutet, dass der Client immer per PXE gestartet wird.<p>**OptOut** bedeutet, dass der Client PXE startet, es sei denn, die ESC-Taste wird gedrückt.|
|[/BootProgram: <Relative path> ] /Architecture: {x86 &#124; ia64 &#124; x64}|Gibt den relativen Pfad zum Start Programm im Ordner "RemoteInstall" (z. b. **boot\x86\pxeboot.n12**) an und gibt die Architektur des Start Programms an.|
|[/N12BootProgram: <Relative path> ] /Architecture: {x86 &#124; ia64 &#124; x64}|Gibt den relativen Pfad zum Start Programm an, für das die Taste F12 nicht gedrückt werden muss (z. b. **boot\x86\pxeboot.n12**), und gibt die Architektur des Start Programms an.|
|[/Bootimage: <Relative path> ] /Architecture: {x86 &#124; ia64 &#124; x64}|Gibt den relativen Pfad zum Start Abbild an, das von Start Clients empfangen werden soll, und gibt die Architektur des Start Abbilds an. Dies kann für jede Architektur angegeben werden.|
|[/PreferredDC: <DC Name> ]|Gibt den Namen des Domänen Controllers an, den die Windows-Bereitstellungs Dienste verwenden sollen. Dabei kann es sich entweder um den NetBIOS-Namen oder den voll qualifizierten Namen handeln.|
|[/PreferredGC: <GC Name> ]|Gibt den Namen des globalen Katalog Servers an, der von den Windows-Bereitstellungs Diensten verwendet werden soll. Dabei kann es sich entweder um den NetBIOS-Namen oder den voll qualifizierten Namen handeln.|
|[/PrestageUsingMAC: {yes &#124; No}]|Gibt an, ob die Windows-Bereitstellungs Dienste beim Erstellen von Computer Konten in AD DS die Mac-Adresse anstelle der GUID/UUID verwenden sollten, um den Computer zu identifizieren.|
|[/NewMachineNamingPolicy: <Policy> ]|Gibt das Format an, das beim Erstellen von Computernamen für Clients verwendet werden soll. Informationen zu dem für zu verwendenden Format erhalten <policy> Sie, indem Sie im MMC-Snap-in mit der rechten Maustaste auf den Server klicken, auf **Eigenschaften**klicken und die Registerkarte **Verzeichnisdienste** anzeigen. Beispiel **:/NewMachineNamingPolicy:% 61Username% #**.|
|[/NewMachineOU]|Wird verwendet, um den Speicherort in AD DS anzugeben, auf dem Client Computer Konten erstellt werden. Sie geben den Speicherort mit den folgenden Optionen an.<p>-[/Type: ServerDomain &#124; UserDomain &#124; UserOU &#124; Custom] gibt den Typ des Speicher Orts an. Server **Domain** erstellt Konten in derselben Domäne wie der Windows-Bereitstellungsdiensteserver. **User Domain** erstellt Konten in derselben Domäne wie der Benutzer, der die Installation ausführt. **UserOU** erstellt Konten in der Organisationseinheit des Benutzers, der die Installation ausführt. Mit **Custom** können Sie einen benutzerdefinierten Speicherort angeben (Sie müssen auch mit dieser Option einen Wert für **/OU** angeben).<br />-[/Ou: <Domain name of OU> ]: Wenn Sie für die **/Type** -Option **Benutzer** definiert angeben, gibt diese Option die Organisationseinheit an, in der Computer Konten erstellt werden sollen.|
|[/DomainSearchOrder: {ginly &#124; DCFirst}]|Gibt die Richtlinie zum Durchsuchen von Computer Konten in AD DS an (globaler Katalog oder Domänen Controller).|
|[/NewMachineDomainJoin: {yes &#124; No}]|Gibt an, ob ein Computer, der nicht bereits in AD DS vorab bereitgestellt ist, während der Installation der Domäne beitreten soll. Der Standardwert für diese Einstellung ist **Ja**.|
|/WdsClientLogging|Gibt den Protokolliergrad für den Server an.<p>-[/Enabled: {yes &#124; No}]: aktiviert oder deaktiviert die Protokollierung von Client Aktionen der Windows-Bereitstellungs Dienste.<br />-[/LoggingLevel: {None &#124; Errors &#124; Warnungen &#124; Info}-legt den Protokolliergrad fest. **None** entspricht der Deaktivierung der Protokollierung. **Fehler** ist die niedrigste Protokollierungsebene und zeigt an, dass nur Fehler protokolliert werden. **Warnungen** enthalten sowohl Warnungen als auch Fehler. **Info** ist die höchste Protokollierungsebene und umfasst Fehler, Warnungen und Informations Ereignisse.|
|/WdsUnattend|Diese Einstellungen steuern das Verhalten der unbeaufsichtigten Installation des Windows-Bereitstellungsdiensteclient. Sie legen die Einstellungen mithilfe der folgenden Optionen fest:<p>-[/Policy: {aktivierte &#124; deaktiviert}]: Hiermit wird angegeben, ob eine unbeaufsichtigte Installation verwendet wird.<br />-[/CommandlinePrecedence: {yes &#124; No}]: Hiermit wird angegeben, ob eine Autounattend.xml Datei (sofern auf dem Client vorhanden) oder eine unbeaufsichtigte Setup Datei, die direkt an den Windows-Bereitstellungsdiensteclient mit der Option/unattend weitergeleitet wurde, während einer Client Installation anstelle einer Abbild Datei für die unbeaufsichtigte Installation verwendet wird. Die Standardeinstellung ist " **Nein**".<br />-[/File: <Relative path> /Architecture: {x86 &#124; ia64 &#124; x64}]: gibt den Dateinamen, den Pfad und die Architektur der Datei für die unbeaufsichtigte Installation an.|
|[/AutoaddPolicy]|Diese Einstellungen steuern die Richtlinie zum automatischen Hinzufügen. Sie definieren die Einstellungen mithilfe der folgenden Optionen:<p>-[/Policy: {adminapproval &#124; deaktiviert}]: " **admingenehmigen** " bewirkt, dass alle unbekannten Computer einer ausstehenden Warteschlange hinzugefügt werden. der Administrator kann dann die Liste der Computer überprüfen und die einzelnen Anforderungen entsprechend genehmigen oder ablehnen. **Deaktiviert** gibt an, dass keine weiteren Aktionen ausgeführt werden, wenn ein unbekannter Computer versucht, auf dem Server zu starten.<br />-[/PollInterval: {Time in seconds}]: Hiermit wird das Intervall (in Sekunden) angegeben, in dem das Netzwerkstart Programm den Windows-Bereitstellungsdiensteserver abrufen soll.<br />-[/MaxRetry:]: Hiermit wird angegeben, wie <Number> oft das Netzwerkstart Programm den Windows-Bereitstellungsdiensteserver abrufen soll. Mit diesem Wert wird zusammen mit **/PollInterval**bestimmt, wie lange das Netzwerkstart Programm darauf wartet, dass ein Administrator den Computer vor dem Timeout genehmigt oder ablehnt. Beispielsweise würde ein **maxretry** -Wert von 10 und eine **PollInterval** -vlue von 60 angeben, dass der Client den Server 10 Mal abrufen soll und 60 Sekunden zwischen den versuchen wartet. Daher wird für den Client nach 10 Minuten ein Timeout gemeldet (10 x 60 Sekunden = 10 Minuten).<br />-[/Message: <Message> ]: gibt die Meldung an, die dem Client auf der Dialogfeld Seite des Netzwerkstart Programms angezeigt wird.<br />-[/RetentionPeriod]: gibt die Anzahl der Tage an, die ein Computer sich im Zustand "Ausstehend" befinden kann, bevor er automatisch bereinigt wird.<br />-[/Approved: <time in days> ]: gibt die Beibehaltungs Dauer für genehmigte Computer an. Sie müssen diesen Parameter mit der **/RetentionPeriod** -Option verwenden.<br />-[/Others: <time in days> ]: gibt die Beibehaltungs Dauer für nicht genehmigte Computer an (abgelehnt oder ausstehend). Sie müssen diesen Parameter mit der **/RetentionPeriod** -Option verwenden.|
|[/AutoaddSettings]|Gibt die Standardeinstellungen an, die auf die einzelnen Computer angewendet werden sollen. Sie definieren die Einstellungen mithilfe der folgenden Optionen:<p>-/Architecture: {x86 &#124; ia64 &#124; x64}-gibt die Architektur an.<br />-[/BootProgram: <Relative path> ]: gibt das Start Programm an, das an den genehmigten Computer gesendet wird. Wenn kein Start Programm angegeben ist, wird der Standardwert für die Architektur des Computers verwendet (wie auf dem Server angegeben).<br />-[/WdsClientUnattend: <Relative path> ]: legt den relativen Pfad zur Datei für die unbeaufsichtigte Installation fest, die der genehmigte Client empfangen soll.<br />-[/ReferralServer: <Server name> ]: gibt den Windows-Bereitstellungsdiensteserver an, den der Client zum Herunterladen von Images verwendet.<br />-[/Bootimage: <Relative path> ]: gibt das Start Abbild an, das der genehmigte Client empfängt.<br />-[/User: <Domäne \ Benutzer &#124; User@Domain>]: legt Berechtigungen für das Computer Konto Objekt fest, um dem angegebenen Benutzer die erforderlichen Rechte zum Hinzufügen des Computers zur Domäne zu übergeben.<br />-[JoinRights: {joinonly &#124; Full}]: gibt den Typ der Rechte an, die dem Benutzer zugewiesen werden sollen. Für **joinonly** muss der Administrator das Computer Konto zurücksetzen, bevor der Benutzer den Computer der Domäne hinzufügen kann. **Full** bietet vollen Zugriff auf den Benutzer, einschließlich der Berechtigung, den Computer der Domäne hinzuzufügen.<br />-[/JoinDomain: {yes &#124; No}]: Hiermit wird angegeben, ob der Computer während der Installation der Windows-Bereitstellungs Dienste der Domäne als dieses Computer Konto beitreten soll. Der Standardwert für diese Einstellung ist **Ja**.|
|/BindPolicy|Konfiguriert die Netzwerkschnittstellen, die der PXE-Anbieter lauschen soll. Sie definieren die Richtlinie mit den folgenden Optionen:<p>-[/Policy: {include &#124; Exclude}]: legt fest, dass die Schnittstellen Bindungs Richtlinie die Adressen in der Schnittstellen Liste einschließt oder ausschließt.<br />-[/Add]-fügt der Liste eine Schnittstelle hinzu. Sie müssen auch/AddressType und/Address. angeben.<br />-[/remove]: entfernt eine Schnittstelle aus der Liste. Sie müssen auch/AddressType und/Address. angeben.<br />-/Address:: <IP or MAC address> gibt die IP-oder Mac-Adresse der Schnittstelle an, die hinzugefügt oder entfernt werden soll.<br />-/AddressType: {IP &#124; Mac}-gibt den Adresstyp an, der in der **/Address** -Option angegeben ist.|
|[/RefreshPeriod: <seconds> ]|Gibt an, wie oft (in Sekunden) der Server seine Einstellungen aktualisiert.|
|[/BannedGuidPolicy]|Verwaltet die Liste der gesperrten GUIDs mithilfe der folgenden Optionen:<p>-[/Add]/GUID: <GUID> Fügt der Liste der gesperrten GUIDs die angegebene GUID hinzu. Jeder Client mit dieser GUID wird stattdessen durch seine MAC-Adresse identifiziert.<br />-[/remove]/GUID: <GUID> entfernt die angegebene GUID aus der Liste der gesperrten GUIDs.|
|/BcdRefreshPolicy|Konfiguriert die Einstellungen zum Aktualisieren von BCD-Dateien mithilfe der folgenden Optionen:<p>-[/Enabled: {yes &#124; No}]: gibt die Richtlinie zum Aktualisieren von BCD an. Wenn **/Enabled** auf " **Yes**" festgelegt ist, werden BCD-Dateien im angegebenen Zeitintervall aktualisiert.<br />-[/RefreshPeriod: <time in minutes> ]: gibt das Zeitintervall an, in dem BCD-Dateien aktualisiert werden.|
|/Transport|Konfiguriert die folgenden Optionen:<p><ul><li>[/ObtainIpv4From: {DHCP &#124; Range}]: gibt die Quelle der IPv4-Adressen an.<p><ul><li>[/Start: <starting Ipv4 address> ] : Gibt den Anfang des IP-Adress Bereichs an. Diese Option ist erforderlich und nur gültig, wenn **/ObtainIpv4From** auf **Range** festgelegt ist.</li><li>[/End: <Ending Ipv4 address> ] : Gibt das Ende des IP-Adress Bereichs an. Diese Option ist nur erforderlich und gültig, wenn **/ObtainIpv4From** auf **Range**festgelegt ist.</li></ul></li><li>[/ObtainIpv6From: Bereich] [/Start: <start IP address> ] [/End: <End IP address> ]  Gibt die Quelle von IPv6-Adressen an. Diese Option gilt nur für Windows Server 2008 R2, und der einzige unterstützte Wert ist Range.</li><li>[/startPort: <starting port> ] : Gibt den Anfang des Port Bereichs an.</li><li>[/EndPort: <Ending port> ] : Gibt das Ende des Port Bereichs an.</li><li>[/Profile: {10 Mbit/s &#124; 100 Mbit/s &#124; 1Gbit/s &#124; Custom}]: gibt das zu verwendende Netzwerk Profil an. Diese Option wird nur unterstützt, auf denen Windows Server 2008 ausgeführt wird.</li><li>[/MulticastSessionPolicy]  Konfiguriert die Übertragungs Einstellungen für Multicast Übertragungen. Dieser Befehl ist nur für Windows Server 2008 R2 verfügbar.<p><ul><li>[/Policy: {None &#124; Autodisconnect &#124; Multistream}]-bestimmt, wie langsame Clients behandelt werden. "None" bedeutet, dass alle Clients in einer Sitzung mit derselben Geschwindigkeit aufbewahrt werden. Autodisconnect bedeutet, dass alle Clients, die unterhalb des angegebenen/Threshold ablegen, getrennt werden. Multistream bedeutet, dass Clients in mehrere Sitzungen unterteilt werden, wie von/StreamCount. angegeben.</li><li>[/Threshold: <Speed in KBps> ] -bei/Policy: Autodisconnect wird durch diese Option die minimale Übertragungsrate in Kbit/s festgelegt. Clients, die diese Rate unterhalb dieses Satzes ablegen, werden von Multicast Übertragungen getrennt.</li><li>[/StreamCount: {2 &#124; 3}] [/Fallback: {Yes &#124; No}]-für/Policy: Multistream legt diese Option die Anzahl der Sitzungen fest. 2 bedeutet, dass zwei Sitzungen (schnell und langsam) 3 drei Sitzungen (langsam, Mittel, schnell) bedeuten.</li><li>[/Fallback: {Yes&#124; No}]: bestimmt, ob Clients, die getrennt sind, die Übertragung mit einer anderen Methode fortsetzen (sofern vom Client unterstützt). Wenn Sie den WDS-Client verwenden, erfolgt ein Fall Back des Computers auf Unicasting. Wdsmcast.exe unterstützt keinen Fall Back Mechanismus. Diese Option gilt auch für Clients, die Multistream nicht unterstützen. In diesem Fall wird der Computer auf eine andere Methode zurückgreifen, anstatt zu einer langsameren Übertragungs Sitzung zu wechseln.</li></ul></li></ul>|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um festzulegen, dass der Server nur auf bekannte Clients antwortet, mit einer Antwort Verzögerung von 4 Minuten:
```
wdsutil /Set-Server /AnswerClients:Known /Responsedelay:4
```
Geben Sie Folgendes ein, um das Start Programm und die Architektur für den Server festzulegen:
```
wdsutil /Set-Server /BootProgram:boot\x86\pxeboot.n12 /Architecture:x86
```
Zum Aktivieren der Protokollierung auf dem Server geben Sie Folgendes ein:
```
wdsutil /Set-Server /WdsClientLogging /Enabled:Yes /LoggingLevel:Warnings
```
Geben Sie Folgendes ein, um die unbeaufsichtigte Installation auf dem Server sowie die Architektur und die Datei für die unbeaufsichtigte Client Installation zu aktivieren:
```
wdsutil /Set-Server /WdsUnattend /Policy:Enabled /File:WDSClientUnattend \unattend.xml /Architecture:x86
```
Geben Sie Folgendes ein, um den PXE-Server (Pre-Boot Execution Environment) für die Bindung an die TCP-Ports 67 und 60 festzulegen:
```
wdsutil /Set-server /UseDhcpPorts:No /DhcpOption60:Yes
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-disable-server-command.md) 
 "deaktivierte Server" [Verwenden des Befehls](using-the-enable-server-command.md) 
 "Enable-Server" [Verwenden des Befehls](using-the-get-server-command.md) 
 Get-Server [Verwenden des Befehls](using-the-initialize-server-command.md) 
 "Initialize-Server" [Unterbefehl: Start-Server](subcommand-start-server.md) 
 [Unterbefehl: "Ende-Server](subcommand-stop-server.md) 
 " [Die Option "nicht initialisieren-Server](the-uninitialize-server-option.md) "
