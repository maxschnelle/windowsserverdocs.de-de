---
title: Netsh-Befehlssyntax, Kontexte und Formatierung
description: In diesem Thema erfahren Sie, wie Sie netsh-Kontexte und-unter Kontexte eingeben, die Netsh-Syntax und Befehls Formatierung verstehen und Netsh-Befehle auf lokalen Computern und Remote Computern ausführen, auf denen Windows Server 2016 oder Windows 10 ausgeführt wird.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 8cb9b59f-0255-4261-b49a-562c5ea50ee0
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 815e59ca00d6450b8ef09a034434c4209c928e78
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405573"
---
# <a name="netsh-command-syntax-contexts-and-formatting"></a>Netsh-Befehlssyntax, Kontexte und Formatierung

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie netsh-Kontexte und-unter Kontexte eingeben, die Netsh-Syntax und Befehls Formatierung verstehen und Netsh-Befehle auf lokalen Computern und Remote Computern ausführen.

Netsh ist ein Befehlszeilen-Skript Hilfsprogramm, mit dem Sie die Netzwerkkonfiguration eines Computers anzeigen oder ändern können, der zurzeit ausgeführt wird. Netsh-Befehle können ausgeführt werden, indem Sie in der netsh-Eingabeaufforderung Befehle eingeben, die in Batch Dateien oder Skripts verwendet werden können. Remote Computer und der lokale Computer können mithilfe von Netsh-Befehlen konfiguriert werden.

Netsh bietet auch eine Skriptingfunktion, mit der Sie eine Gruppe von Befehlen im Batchmodus für einen bestimmten Computer ausführen können. Mit Netsh können Sie ein Konfigurationsskript als Textdatei zu Archivierungszwecken oder für die Konfiguration anderer Computer speichern.

## <a name="netsh-contexts"></a>Netsh-Kontexte

Netsh interagiert mit anderen Betriebssystemkomponenten mithilfe von Dynamic\-Link Library \(dll\) Dateien. 

Jede Netsh Helper-DLL bietet einen umfangreichen Satz von Features, die als *Kontext*bezeichnet werden. Dies ist eine Gruppe von Befehlen, die für eine Netzwerkserver Rolle oder ein Feature spezifisch sind. Diese Kontexte erweitern die Funktionalität von Netsh, indem Sie Konfigurations-und Überwachungs Unterstützung für einen oder mehrere Dienste, Hilfsprogramme oder Protokolle bereitstellen. Dhcpmon. dll bietet beispielsweise Netsh mit dem Kontext und dem Satz von Befehlen, die zum Konfigurieren und Verwalten von DHCP-Servern erforderlich sind.

### <a name="obtain-a-list-of-contexts"></a>Abrufen einer Liste von Kontexten

Sie können eine Liste der netsh-Kontexte abrufen, indem Sie entweder die Eingabeaufforderung oder Windows PowerShell auf einem Computer öffnen, auf dem Windows Server 2016 oder Windows 10 ausgeführt wird. Geben Sie den Befehl **netsh** ein, und drücken Sie EINGABETASTE. Geben Sie **/?** ein, und drücken Sie dann die EINGABETASTE.

Im folgenden finden Sie eine Beispielausgabe für diese Befehle auf einem Computer, auf dem Windows Server 2016 Datacenter ausgeführt wird.

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

### <a name="subcontexts"></a>Unter Kontexte

Netsh-Kontexte können sowohl Befehle als auch zusätzliche Kontexte enthalten, die als *unter Kontexte*bezeichnet werden. Beispielsweise können Sie im Routing Kontext zu den unter Kontexten IP und IPv6 wechseln.

Wenn Sie eine Liste der Befehle und unter Kontexte anzeigen möchten, die Sie in einem Kontext verwenden können, geben Sie an der netsh-Eingabeaufforderung den Kontext Namen ein, und geben Sie dann entweder **/?** ein. oder **Hilfe**. Wenn Sie z. b. eine Liste von unter Kontexten und Befehlen anzeigen möchten, die Sie im Routing Kontext verwenden können, geben Sie an der netsh-Eingabeaufforderung \(das heißt, **netsh&gt;** \)eine der folgenden Informationen ein:

**Routing/?**

**Routing Hilfe**

Um Aufgaben in einem anderen Kontext auszuführen, ohne den aktuellen Kontext zu ändern, geben Sie den Kontext Pfad des Befehls ein, den Sie an der netsh-Eingabeaufforderung verwenden möchten. Um beispielsweise eine Schnittstelle mit dem Namen "LAN-Verbindung" im IGMP-Kontext hinzuzufügen, ohne zuvor in den IGMP-Kontext zu wechseln, geben Sie an der netsh-Eingabeaufforderung Folgendes ein:

**Routing IP IGMP Add Interface "Local Area Connection" startupqueryinterval = 21**

## <a name="running-netsh-commands"></a>Ausführen von Netsh-Befehlen

Um einen netsh-Befehl auszuführen, müssen Sie netsh von der Eingabeaufforderung aus starten, indem Sie **netsh** eingeben und dann die EINGABETASTE drücken. Als nächstes können Sie in den Kontext wechseln, der den gewünschten Befehl enthält. Welche Kontexte verfügbar sind, hängt von den installierten Netzwerkkomponenten ab. Wenn Sie z. b. **DHCP** an der netsh-Eingabeaufforderung eingeben und die EINGABETASTE drücken, werden Änderungen am DHCP-Server Kontext von Netsh geändert. Wenn Sie DHCP nicht installiert haben, wird die folgende Meldung angezeigt:

**Der folgende Befehl wurde nicht gefunden: DHCP.**

## <a name="formatting-legend"></a>Legende formatieren

Sie können die folgende Formatierungs Legende verwenden, um die richtige Netsh-Befehlssyntax zu interpretieren und zu verwenden, wenn Sie den Befehl an der netsh-Eingabeaufforderung oder in einer Batchdatei oder einem Skript ausführen.

- Text in *kursiv* Schrift sind Informationen, die Sie beim Eingeben des Befehls angeben müssen. Wenn ein Befehl z. b. einen Parameter mit dem Namen-*username*hat, müssen Sie den tatsächlichen Benutzernamen eingeben.
- **Fett** formatierter Text sind Informationen, die Sie genau wie angezeigt eingeben müssen, wenn Sie den Befehl eingeben.
- Text gefolgt von einem Ellipsen \(...\) ist ein Parameter, der mehrmals in einer Befehlszeile wiederholt werden kann.
- Text zwischen eckigen Klammern [&nbsp;] ist ein optionales Element.
- Text zwischen geschweiften Klammern {&nbsp;}, wobei Auswahlmöglichkeiten durch eine Pipe getrennt sind, stellen eine Reihe von Optionen bereit, von denen Sie nur eine auswählen müssen, z. b. `{enable|disable}`.
- Text, der mit Courier Font formatiert wird, ist die Code-oder Programmausgabe.

## <a name="running-netsh-commands-from-the-command-prompt-or-windows-powershell"></a>Ausführen von Netsh-Befehlen über die Eingabeaufforderung oder Windows PowerShell

Um die Netzwerkshell zu starten und netsh an der Eingabeaufforderung oder in Windows PowerShell einzugeben, können Sie den folgenden Befehl verwenden.

### <a name="netsh"></a>netsh

Netsh ist ein Befehlszeilen-Skript Hilfsprogramm, mit dem Sie die Netzwerkkonfiguration eines derzeit ausgelaufenden Computers entweder lokal oder Remote anzeigen oder ändern können. Wenn Sie ohne Parameter verwendet wird, öffnet **netsh** die Eingabeaufforderung netsh. exe \(das heißt, **netsh&gt;** \).

#### <a name="syntax"></a>Syntax

**netsh**\[ **-a**&nbsp;*aliasfile*\] \[ **-c**&nbsp;*Kontext* \] \[ **-r**&nbsp;*Remotecomputer*\] \[ **-u** \[ *Domain Name\\* \] *username* \] \[ **-p**&nbsp;*Password* | \*\] \[{*netshcommand* |  **-f**&nbsp; *Scriptfile*}\]

#### <a name="parameters"></a>Parameter

**`-a`**

Optional. Gibt an, dass Sie nach dem Ausführen von *aliasfile*an die **netsh** -Eingabeaufforderung zurückgegeben werden.

**`AliasFile`**

Optional. Gibt den Namen der Textdatei an, die mindestens einen **netsh** -Befehl enthält.

**`-c`**

Optional. Gibt an, dass Netsh in den angegebenen **netsh** -Kontext gelangt.

**`Context`**

Optional. Gibt den **netsh** -Kontext an, den Sie eingeben möchten. 

**`-r`**

Optional. Gibt an, dass der Befehl auf einem Remote Computer ausgeführt werden soll.

> [!IMPORTANT]
> Wenn Sie einige Netsh-Befehle Remote auf einem anderen Computer mit dem **netsh – r** -Parameter verwenden, muss der Remote Registrierungsdienst auf dem Remote Computer ausgeführt werden. Wenn er nicht ausgeführt wird, zeigt Windows die Fehlermeldung "Netzwerkpfad nicht gefunden" an.

***`RemoteComputer`***

Optional. Gibt den Remote Computer an, den Sie konfigurieren möchten.

**`-u`**

Optional. Gibt an, dass Sie den Netsh-Befehl unter einem Benutzerkonto ausführen möchten.

***`DomainName\\`***

Optional. Gibt die Domäne an, in der sich das Benutzerkonto befindet. Der Standardwert ist die lokale Domäne, wenn *Domain Name\\* nicht angegeben ist.

***`UserName`***

Optional. Gibt den Namen des Benutzerkontos an.

**`-p`**

Optional. Gibt an, dass Sie ein Kennwort für das Benutzerkonto angeben möchten.

***`Password`***

Optional. Gibt das Kennwort für das Benutzerkonto an, das Sie mit dem *Benutzernamen* **-u** angegeben haben.

***`NetshCommand`***

Optional. Gibt den **netsh** -Befehl an, den Sie ausführen möchten.

**`-f`**

Optional. Beendet **netsh** , nachdem das Skript ausgeführt wurde, das Sie mit *scriptfile*festgelegt haben.

***`ScriptFile`***

Optional. Gibt das Skript an, das Sie ausführen möchten.

**`/?`**

Optional. Zeigt die Hilfe an der netsh-Eingabeaufforderung an.

> [!NOTE]
> Wenn Sie **`-r`** gefolgt von einem anderen Befehl angeben, führt **netsh** den Befehl auf dem Remote Computer aus und kehrt dann zur Eingabeaufforderung von "cmd. exe" zurück. Wenn Sie **`-r`** ohne einen anderen Befehl angeben, wird **netsh** im Remote Modus geöffnet. Der Prozess ähnelt der Verwendung von **Set Machine** an der netsh-Eingabeaufforderung. Wenn Sie **`-r`** verwenden, legen Sie den Bereitstellungs Zielcomputer nur für die aktuelle Instanz von **netsh** fest. Nachdem Sie **netsh**beendet und erneut eingegeben haben, wird der Zielcomputer als lokaler Computer zurückgesetzt. Sie können **netsh** -Befehle auf einem Remote Computer ausführen, indem Sie einen in WINS gespeicherten Computernamen, einen UNC-Namen, einen Internet Namen, der vom DNS-Server aufgelöst werden soll, oder eine IP-Adresse angeben.

**Eingeben von Parameter Zeichen folgen Werten für Netsh-Befehle**

Im gesamten Netsh-Befehls Verweis sind Befehle vorhanden, die Parameter enthalten, für die ein Zeichen folgen Wert erforderlich ist.

Wenn ein Zeichen folgen Wert Leerzeichen zwischen Zeichen enthält, z. b. Zeichen folgen Werte, die aus mehr als einem Wort bestehen, müssen Sie den Zeichen folgen Wert in Anführungszeichen einschließen. Verwenden Sie beispielsweise für einen Parameter mit dem Namen " **Interface** " mit dem Zeichen folgen Wert " **drahtlose Netzwerkverbindung**" Anführungszeichen um den Zeichen folgen Wert:

**`interface="Wireless Network Connection"`**

