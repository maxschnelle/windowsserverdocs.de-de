---
title: Netsh-Befehlssyntax, Kontexte und Formatierung
description: Sie können in diesem Thema verwenden, um zu erfahren, wie geben Netsh-Kontexten und Unterkontexte, zu verstehen, Netsh-Syntax und Befehl formatieren und das Netsh-Befehle auf lokalen Computern und Remotecomputern ausgeführt wird, auf denen Windows Server 2016 oder Windows 10 ausgeführt werden.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 8cb9b59f-0255-4261-b49a-562c5ea50ee0
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: adb1546bc21b3209a362fd61feab0d3ee6810a66
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812170"
---
# <a name="netsh-command-syntax-contexts-and-formatting"></a>Netsh-Befehlssyntax, Kontexte und Formatierung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um zu erfahren, wie geben Netsh-Kontexten und Unterkontexte, zu verstehen, Netsh-Syntax und die Formatierung der Befehl, und wie Sie Netsh-Befehle auf lokalen Computern und Remotecomputern ausführen.

Netsh ist ein Befehlszeilen-skripthilfsprogramm, mit dem Sie anzeigen oder ändern die Netzwerkkonfiguration eines Computers, der derzeit ausgeführt wird. Netsh-Befehle können ausgeführt werden, indem Sie Befehle eingeben, an der Eingabeaufforderung Netsh ein, und sie können in Batch-Dateien oder Skripts verwendet werden. Remote-Computern und dem lokalen Computer können mithilfe von Netsh-Befehle konfiguriert werden.

Netsh bietet auch eine Skriptingfunktion, mit der Sie eine Gruppe von Befehlen im Batchmodus für einen bestimmten Computer ausführen können. Mit Netsh können Sie ein Konfigurationsskript als Textdatei zu Archivierungszwecken oder für die Konfiguration anderer Computer speichern.

## <a name="netsh-contexts"></a>Netsh-Kontexten

Netsh interagiert mit anderen Komponenten des Betriebssystems mithilfe von dynamischen\-Link Library \(DLL\) Dateien. 

Jede Netsh-Hilfsprogramm-DLL bietet eine Breite Palette von Features mit dem Namen einer *Kontext*, dies ist eine Gruppe von spezifischen Befehlen für ein Netzwerk-Serverrolle oder-Funktion. Diese Kontexte erweitern die Funktionalität von Netsh, durch die Konfiguration und Unterstützung für Dienste, Hilfsprogramme oder Protokolle zu überwachen. Beispielsweise bietet Dhcpmon.dll Netsh mit dem Kontext und eine Reihe von Befehlen, die zum Konfigurieren und Verwalten von DHCP-Servern.

### <a name="obtain-a-list-of-contexts"></a>Abrufen einer Liste von Kontexten

Sie erhalten eine Liste der Netsh-Kontexten, öffnen Sie auf einem Computer unter Windows Server 2016 oder Windows 10-Eingabeaufforderung oder in Windows PowerShell. Geben Sie den Befehl **Netsh** und drücken Sie EINGABETASTE. Typ **/?** , und drücken Sie dann die EINGABETASTE.

Es folgt die Beispielausgabe für diese Befehle auf einem Computer unter Windows Server 2016 Datacenter.

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

### <a name="subcontexts"></a>Folgende Unterkontexte

Netsh-Kontext können sowohl Befehle als auch zusätzliche Kontexten aufgerufen enthalten *Unterkontexte*. Innerhalb des Kontexts Routing können Sie z. B. um die IP- und IPv6-Unterkontexte ändern.

Klicken Sie zum Anzeigen einer Liste von Befehlen und Unterkontexte, mit denen Sie in einem Kontext, an der Eingabeaufforderung Netsh Geben Sie den Kontext ein, und geben Sie dann entweder **/?** oder **Hilfe**. Beispielsweise, um das Anzeigen einer Liste von untergeordneten Kontexten und Befehle, mit denen Sie in den Routing-Kontext, an der Eingabeaufforderung Netsh \(, also **Netsh&gt;** \), geben Sie einen der folgenden:

**Routing /?**

**routing help**

Geben Sie zum Ausführen von Aufgaben in einem anderen Kontext, ohne von den aktuellen Kontext ändern zu müssen, die Kontextpfad des Befehls, die Sie an der Eingabeaufforderung Netsh verwenden möchten. Geben Sie z. B. zum Hinzufügen einer Schnittstelle, die mit dem Namen "LAN-Verbindung" im IGMP-Kontext, ohne zuerst auf den IGMP-Kontext, an der Eingabeaufforderung Netsh:

**Igmp für IP-Weiterleitung hinzufügen Schnittstelle "LAN-Verbindung" Startupqueryinterval = 21**

## <a name="running-netsh-commands"></a>Ausführen von Netsh-Befehlen

Führen Sie einen netch-Befehl müssen Sie Netsh über die Eingabeaufforderung starten, indem Sie eingeben **Netsh** und dann die EINGABETASTE drücken. Als Nächstes können Sie in den Kontext ändern, die den Befehl enthält, die, den Sie verwenden möchten. Die Kontexte, die verfügbar sind, hängt von der Netzwerkkomponenten, die Sie installiert haben. Angenommen, Sie geben ein **Dhcp** an die Netsh-Eingabeaufforderung, und drücken Sie die EINGABETASTE, Netsh ändert sich in den Kontext des DHCP-Server. Wenn Sie nicht DHCP installiert haben, wird jedoch die folgende Meldung angezeigt:

**Der folgende Befehl wurde nicht gefunden: Dhcp.**

## <a name="formatting-legend"></a>Formatierungslegende

Sie können die folgende formatierungslegende interpretieren und Verwenden der richtigen Netsh-Befehlssyntax beim Ausführen des Befehls an der Eingabeaufforderung Netsh oder in einer Batchdatei oder einem Skript verwenden.

- Text in *Kursiv* sind Informationen, die Sie angeben müssen, während Sie den Befehl eingeben. Wenn ein Befehl einen Parameter Namens - enthält z. B.*Benutzername*, müssen Sie den tatsächlichen Benutzernamen eingeben.
- Text in **fett** sind Informationen, die Sie genau wie dargestellt, während der Eingabe des Befehls eingeben müssen.
- Text von einem Auslassungszeichen gefolgt \(... \) ist ein Parameter, die in einer Befehlszeile mehrmals wiederholt werden kann.
- Text, der zwischen Klammern [&nbsp;] ist ein optionales Element.
- Text, der in geschweiften Klammern {&nbsp;} Auswahlmöglichkeiten, getrennt durch einen senkrechten Strich bietet eine Reihe von Auswahlmöglichkeiten, aus dem Sie nur eine, wie z. B. auswählen müssen `{enable|disable}`.
- Mit der Schriftart Courier formatierter Text ist, Code oder Programmausgabe.

## <a name="running-netsh-commands-from-the-command-prompt-or-windows-powershell"></a>Ausführen von Netsh-Befehle über die Eingabeaufforderung oder die Windows PowerShell

Starten die Network Shell aus, und geben Netsh an der Eingabeaufforderung oder in Windows PowerShell, können Sie den folgenden Befehl verwenden.

### <a name="netsh"></a>netsh

Netsh ist ein Befehlszeilen-skripthilfsprogramm, mit dem Sie entweder lokal oder Remote anzeigen oder ändern die Netzwerkkonfiguration eines aktuell ausgeführten Computers. Ohne Parameter verwendet **Netsh** öffnet der Netsh.exe-Eingabeaufforderung \(, also **Netsh&gt;** \).

#### <a name="syntax"></a>Syntax

**Netsh** \[ **– ein**&nbsp;*Aliasdatei* \] \[ **- C** &nbsp;  *Kontext* \] \[ **- R**&nbsp;*RemoteComputer* \] \[ **- u** \[ *DomainName\\*  \] *Benutzername* \] \[ **-p** &nbsp; *Kennwort*  |  \* \] \[{*netsh-Befehl* |  **-f** &nbsp; *ScriptFile*}\]

#### <a name="parameters"></a>Parameter

**`-a`**

Dies ist optional. Gibt an, dass Sie nach Rückkehr der **Netsh** Eingabeaufforderung nach der Ausführung *Aliasdatei*.

**`AliasFile`**

Optional. Gibt den Namen der Textdatei, die eine oder mehrere enthält **Netsh** Befehle.

**`-c`**

Optional. Gibt an, Netsh gibt das angegebene **Netsh** Kontext.

**`Context`**

Optional. Gibt an, die **Netsh** Kontext, die Sie eingeben möchten. 

**`-r`**

Optional. Gibt an, dass den Befehl auf einem Remotecomputer ausgeführt werden sollen.

> [!IMPORTANT]
> Bei Verwendung einiger Netsh-Befehle Remote auf einem anderen Computer mit der **Netsh – R** Parameter, der Remoteregistrierungsdienst muss ausgeführt werden auf dem Remotecomputer. Wenn er nicht ausgeführt wird, zeigt Windows eine Fehlermeldung "Netzwerk Pfad nicht gefunden".

***`RemoteComputer`***

Optional. Gibt den remote-Computer, den Sie konfigurieren möchten.

**`-u`**

Optional. Gibt an, dass der Befehl "Netsh" unter einem Benutzerkonto ausgeführt werden soll.

***`DomainName\\`***

Dies ist optional. Gibt die Domäne, wo sich das Benutzerkonto befindet. Der Standardwert ist der lokalen Domäne aus, wenn *DomainName\\*  nicht angegeben ist.

***`UserName`***

Optional. Gibt den Namen des Benutzerkontos an.

**`-p`**

Optional. Gibt an, dass Sie ein Kennwort für das Benutzerkonto angeben möchten.

***`Password`***

Optional. Gibt das Kennwort für das Benutzerkonto an, die mit angegebenen **-u** *Benutzername*.

***`NetshCommand`***

Optional. Gibt an, die **Netsh** -Befehl, der ausgeführt werden soll.

**`-f`**

Dies ist optional. Beendet **Netsh** nach dem Ausführen des Skripts, die Sie festlegen, mit *ScriptFile*.

***`ScriptFile`***

Optional. Gibt an, das Skript, das Sie ausführen möchten.

**`/?`**

Dies ist optional. Zeigt die Hilfe an der Eingabeaufforderung Netsh.

> [!NOTE]
> Bei Angabe von **`-r`** gefolgt von einem anderen Befehl **Netsh** führt den Befehl auf dem Remotecomputer, und sendet Sie an der Eingabeaufforderung von Cmd.exe zurück. Bei Angabe von **`-r`** ohne einen weiteren Befehl **Netsh** im Remotemodus wird geöffnet. Der Prozess ist vergleichbar mit der Verwendung **Satz Computer** an der Eingabeaufforderung Netsh. Bei Verwendung von **`-r`** , festlegen, dass der Zielcomputer für die aktuelle Instanz von **Netsh** nur. Nach dem Beenden und erneut ein **Netsh**, der Zielcomputer wird als dem lokalen Computer zurückgesetzt. Sie können ausführen **Netsh** Befehle auf einem Remotecomputer durch Angabe eines Computers Namen in WINS gespeichert, einen UNC-Namen, den Internetnamen eines, um die von den DNS-Server oder eine IP-Adresse aufgelöst werden.

**Eingeben von Parameterwerten der Zeichenfolge für die Netsh-Befehle**

In der Netsh-Befehlsreferenz stehen Befehle, die Parameter enthalten, für die ein Zeichenfolgenwert erforderlich ist.

In die Groß-/Kleinschreibung, der einen Zeichenfolgenwert enthält, in denen Leerzeichen zwischen den Zeichen, z. B. Werte, die aus mehr als ein Wort, bestehen es erforderlich ist, dass Sie den Zeichenfolgenwert in Anführungszeichen setzen. Z. B. für einen Parameter namens **Schnittstelle** mit einem Zeichenfolgenwert des **Drahtlosnetzwerkverbindung**, verwenden Sie den Zeichenfolgenwert in Anführungszeichen einschließen:

**`interface="Wireless Network Connection"`**

