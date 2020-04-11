---
title: Netsh-Befehlssyntax, Kontexte und Formatierung
description: Du kannst in diesem Thema erfahren, wie du Netsh-Kontexte und Unterkontexte eingibst, die Syntax und Befehlsformatierung von Netsh-Dateien verstehst und wie du Netsh-Befehle auf lokalen und Remotecomputern mit Windows Server 2016 oder Windows 10 ausführen kannst.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 8cb9b59f-0255-4261-b49a-562c5ea50ee0
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 061d7252d5a7bbe09d3dca245d9b77ed20a4dedf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854763"
---
# <a name="netsh-command-syntax-contexts-and-formatting"></a>Netsh-Befehlssyntax, Kontexte und Formatierung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Du kannst in diesem Thema erfahren, wie du Netsh-Kontexte und Unterkontexte eingibst, die Syntax und Befehlsformatierung von Netsh-Dateien verstehst und wie du Netsh-Befehle auf lokalen und Remotecomputern ausführen kannst.

Netsh ist ein Befehlszeilen-Skripthilfsprogramm, mit dem die Netzwerkkonfiguration eines Computers angezeigt oder geändert werden kann, die aktuell ausgeführt wird. Netsh-Befehle können durch Eingabe von Befehlen an der Netsh-Eingabeaufforderung ausgeführt und in Batchdateien oder Skripts verwendet werden. Remotecomputer und der lokale Computer können mithilfe von Netsh-Befehlen konfiguriert werden.

Netsh bietet auch eine Skriptingfunktion, mit der Sie eine Gruppe von Befehlen im Batchmodus für einen bestimmten Computer ausführen können. Mit Netsh können Sie ein Konfigurationsskript als Textdatei zu Archivierungszwecken oder für die Konfiguration anderer Computer speichern.

## <a name="netsh-contexts"></a>Netsh-Kontexte

Netsh interagiert mit anderen Betriebssystemkomponenten unter Verwendung von Dateien der Dynamic\-Link Library \(DLL\). 

Jede DLL des Netsh-Hilfsprogramms bietet einen umfangreichen Satz von Features, die als *Kontext* bezeichnet werden, d. h. eine Gruppe von Befehlen, die für eine Netzwerkserverrolle oder -funktion spezifisch sind. Diese Kontexte erweitern die Funktionalität von Netsh durch die Bereitstellung von Konfigurations- und Überwachungsunterstützung für mindestens einen Dienst, ein Hilfsprogramm oder Protokoll. So stellt z. B. „Dhcpmon.dll“ Netsh den Kontext und den Satz von Befehlen zur Verfügung, die zur Konfiguration und Verwaltung von DHCP-Servern erforderlich sind.

### <a name="obtain-a-list-of-contexts"></a>Abrufen einer Liste von Kontexten

Du kannst eine Liste von Netzh-Kontexten abrufen, indem du entweder die Eingabeaufforderung oder Windows PowerShell auf einem Computer mit Windows Server 2016 oder Windows 10 öffnest. Gib den Befehl **netsh** ein und drücke die EINGABETASTE. Gib **/?** ein und drücke dann die EINGABETASTE.

Es folgt eine Beispielausgabe für diese Befehle auf einem Computer mit Windows Server 2016 Datacenter.

>    ```
>   PS C:\Windows\system32> netsh
>   netsh>/?
>    
>    The following commands are available:
>    
>    Commands in this context:
>    ..            - Goes up one context level.
>    ?             - Displays a list of commands.
>    abort         - Discards changes made while in offline mode.
>    add           - Adds a configuration entry to a list of entries.
>    advfirewall   - Changes to the `netsh advfirewall' context.
>    alias         - Adds an alias.
>    branchcache   - Changes to the `netsh branchcache' context.
>    bridge        - Changes to the `netsh bridge' context.
>    bye           - Exits the program.
>    commit        - Commits changes made while in offline mode.
>    delete        - Deletes a configuration entry from a list of entries.
>    dhcpclient    - Changes to the `netsh dhcpclient' context.
>    dnsclient     - Changes to the `netsh dnsclient' context.
>    dump          - Displays a configuration script.
>    exec          - Runs a script file.
>    exit          - Exits the program.
>    firewall      - Changes to the `netsh firewall' context.
>    help          - Displays a list of commands.
>    http          - Changes to the `netsh http' context.
>    interface     - Changes to the `netsh interface' context.
>    ipsec         - Changes to the `netsh ipsec' context.
>    ipsecdosprotection - Changes to the `netsh ipsecdosprotection' context.
>    lan           - Changes to the `netsh lan' context.
>    namespace     - Changes to the `netsh namespace' context.
>    netio         - Changes to the `netsh netio' context.
>    offline       - Sets the current mode to offline.
>    online        - Sets the current mode to online.
>    popd          - Pops a context from the stack.
>    pushd         - Pushes current context on stack.
>    quit          - Exits the program.
>    ras           - Changes to the `netsh ras' context.
>    rpc           - Changes to the `netsh rpc' context.
>    set           - Updates configuration settings.
>    show          - Displays information.
>    trace         - Changes to the `netsh trace' context.
>    unalias       - Deletes an alias.
>    wfp           - Changes to the `netsh wfp' context.
>    winhttp       - Changes to the `netsh winhttp' context.
>    winsock       - Changes to the `netsh winsock' context.
>    
>    The following sub-contexts are available:
>     advfirewall branchcache bridge dhcpclient dnsclient firewall http interface ipsec ipsecdosprotection lan namespace netio ras rpc trace wfp winhttp winsock
>    
>    To view help for a command, type the command, followed by a space, and then type ?.
>    ```

### <a name="subcontexts"></a>Unterkontexte

Netsh-Kontexte können sowohl Befehle als auch zusätzliche Kontexte enthalten, die als *Unterkontexte* bezeichnet werden. Innerhalb des Routing-Kontextes kannst du z. B. zu den Unterkontexten „IP“ und „IPv6“ wechseln.

Um eine Liste von Befehlen und Unterkontexten anzuzeigen, die du innerhalb eines Kontexts verwenden kannst, gibst du an der Netsh-Eingabeaufforderung den Kontextnamen und dann entweder **/?** oder **help** ein. Um z. B. eine Liste von Unterkontexten und Befehlen anzuzeigen, die du im Routing-Kontext verwenden kannst, gib an der Netsh-Eingabeaufforderung \(d. h. **netsh&gt;** \) eine der folgenden Optionen ein:

**routing /?**

**routing help**

Gib den Kontextpfad des gewünschten Befehls an der Netsh-Eingabeaufforderung ein, um Aufgaben in einem anderen Kontext auszuführen, ohne den aktuellen Kontext zu wechseln. Um z. B. eine Schnittstelle namens „LAN-Verbindung“ im IGMP-Kontext hinzuzufügen, ohne zuerst in den IGMP-Kontext zu wechseln, gib an der Netsh-Eingabeaufforderung Folgendes ein:

**routing ip igmp add interface „LAN-Verbindung“ startupqueryinterval=21**

## <a name="running-netsh-commands"></a>Ausführen von Netsh-Befehlen

Zum Ausführen eines Netsh-Befehls ist es erforderlich, Netsh von der Eingabeaufforderung aus zu starten, indem du **netsh** eingibst und dann die EINGABETASTE drückst. Als nächstes kannst du zu dem Kontext wechseln, der den gewünschten Befehl enthält. Die verfügbaren Kontexte hängen von den installierten Netzwerkkomponenten ab. Wenn du z. B. **dhcp** an der Netsh-Eingabeaufforderung eingibst und die EINGABETASTE drückst, wechselt Netsh zum Kontext „DHCP-Server“. Wenn DHCP nicht installiert ist, wird die folgende Meldung angezeigt:

**Der folgende Befehl wurde nicht gefunden: dhcp.**

## <a name="formatting-legend"></a>Formatierungslegende

Du kannst die folgende Formatierungslegende verwenden, um die richtige Netsh-Befehlssyntax zu interpretieren und zu verwenden, wenn du den Befehl an der Netsh-Eingabeaufforderung oder in einer Batchdatei oder einem Skript ausführst.

- *Kursiver* Text kennzeichnet Informationen, die bei der Eingabe des Befehls bereitgestellt werden müssen. Wenn ein Befehl z. B. einen Parameter namens -*Benutzername* (UserName) aufweist, musst du den tatsächlichen Benutzernamen eingeben.
- **Fett** formatierter Text kennzeichnet Informationen, die genau so eingegeben werden müssen, wie sie während der Eingabe des Befehls angezeigt werden.
- Text, auf den Auslassungspunkte \(...\) folgen, kennzeichnet Parameter, die mehrmals in einer Befehlszeile wiederholt werden können.
- Text zwischen eckigen Klammern [&nbsp;] kennzeichnet optionale Elemente.
- Text zwischen geschweiften Klammern {&nbsp;} mit Optionen, die durch eine Pipe getrennt sind, bietet eine Reihe von Auswahlmöglichkeiten, aus denen du nur eine auswählen darfst, z. B. `{enable|disable}`.
- Text, der mit der Schriftart Courier formatiert ist, stellt einen Code oder eine Programmausgabe dar.

## <a name="running-netsh-commands-from-the-command-prompt-or-windows-powershell"></a>Ausführen von Netsh-Befehlen über die Eingabeaufforderung oder Windows PowerShell

Um Network Shell zu starten und Netsh an der Eingabeaufforderung oder in Windows PowerShell einzugeben, kannst du den folgenden Befehl verwenden.

### <a name="netsh"></a>Netsh

Netsh ist ein Befehlszeilen-Skripthilfsprogramm, mit dem die Netzwerkkonfiguration eines aktuell aktiven Computers entweder lokal oder remote angezeigt oder geändert werden kann. Bei Verwendung ohne Parameter öffnet **netsh** die Netsh.exe-Eingabeaufforderung \(d. h. **netsh&gt;** \).

#### <a name="syntax"></a>Syntax

**netsh**\[ **-a**&nbsp;*Aliasdatei*\] \[ **-c**&nbsp;*Kontext* \] \[ **-r**&nbsp;*Remotecomputer*\] \[ **-u** \[ *Domänenname\\* \] *Benutzername* \] \[ **-p**&nbsp;*Kennwort* | \*\] \[{*Netsh-Befehl* |  **-f**&nbsp;*Skriptdatei*}\]

##### <a name="parameters"></a>Parameter

**`-a`**

Optional. Gibt an, dass du nach der Ausführung von *Aliasdatei* zur **Netsh**-Eingabeaufforderung zurückkehrst.

**`AliasFile`**

Optional. Gibt den Namen der Textdatei an, die mindestens einen **Netsh**-Befehl enthält.

**`-c`**

Optional. Gibt an, dass Netsh in den angegebenen **Netsh**-Kontext wechselt.

**`Context`**

Optional. Gibt den **Netsh-** Kontext an, der eingegeben werden soll. 

**`-r`**

Optional. Gibt an, dass der Befehl auf einem Remotecomputer ausgeführt werden soll.

> [!IMPORTANT]
> Wenn du einige Netsh-Befehle remote auf einem anderen Computer mit dem Parameter **netsh -r** verwendest, muss der Remoteregistrierungsdienst auf dem Remotecomputer ausgeführt werden. Wenn er nicht ausgeführt wird, zeigt Windows die Fehlermeldung „Netzwerkpfad nicht gefunden“ an.

***`RemoteComputer`***

Optional. Gibt den Remotecomputer an, den du konfigurieren möchtest.

**`-u`**

Optional. Gibt an, dass du den Netsh-Befehl unter einem Benutzerkonto ausführen willst.

***`DomainName\\`***

Optional. Gibt die Domäne an, in der sich das Benutzerkonto befindet. Der Standardwert ist die lokale Domäne, wenn *Domänenname\\* nicht angegeben ist.

***`UserName`***

Optional. Gibt den Namen des Benutzerkontos an.

**`-p`**

Optional. Gibt an, dass du ein Kennwort für das Benutzerkonto bereitstellen möchtest.

***`Password`***

Optional. Gibt das Kennwort für das Benutzerkonto an, das du mit **-u** *Benutzername* angegeben hast.

***`NetshCommand`***

Optional. Gibt den **Netsh**-Befehl an, den du ausführen möchtest.

**`-f`**

Optional. Beendet **Netsh** nach Ausführung des Skripts, das du mit *Skriptdatei* bestimmst.

***`ScriptFile`***

Optional. Gibt das Skript an, dass du ausführen möchtest.

**`/?`**

Optional. Zeigt die Hilfe an der Netsh-Eingabeaufforderung an.

> [!NOTE]
> Wenn du **`-r`** gefolgt von einem anderen Befehl angibst, führt **Netsh** den Befehl auf dem Remotecomputer aus und kehrt dann zur „Cmd.exe“-Eingabeaufforderung zurück. Wenn du **`-r`** ohne einen anderen Befehl angibst, wird **Netsh** im Remotemodus geöffnet. Das Verfahren ist ähnlich wie die Verwendung von **set machine** an der Netsh-Eingabeaufforderung. Wenn du **`-r`** verwendest, legst du den Zielcomputer nur für die aktuelle Instanz von **Netsh** fest. Nachdem du **Netsh** beendet und erneut eingegeben hast, wird der Zielcomputer als lokaler Computer zurückgesetzt. Du kannst **Netsh**-Befehle auf einem Remotecomputer ausführen, indem du einen in WINS gespeicherten Computernamen, einen UNC-Namen, einen vom DNS-Server aufzulösenden Internetnamen oder eine IP-Adresse angibst.

**Eingeben von Parameterzeichenfolgenwerten für Netsh-Befehle**

In der gesamten Netsh-Befehlsreferenz gibt es Befehle, die Parameter enthalten, für die ein Zeichenfolgenwert erforderlich ist.

Wenn ein Zeichenfolgenwert Leerzeichen zwischen den Zeichen enthält, z. B. Zeichenfolgenwerte, die aus mehr als einem Wort bestehen, musst du den Zeichenfolgenwert in Anführungszeichen setzen. Verwende z. B. für einen Parameter namens **interface** mit dem Zeichenfolgenwert **Drahtlosnetzwerkverbindung** entsprechende Anführungszeichen um den Zeichenfolgenwert herum:

**`interface="Wireless Network Connection"`**

