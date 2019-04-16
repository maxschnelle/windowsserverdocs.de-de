---
title: Netsh-Befehl Syntax Kontexte und formatieren
description: Sie können in diesem Thema erfahren Sie, wie Sie geben Sie Netsh-Kontext und Unterkontexte, zu verstehen, Netsh-Syntax und Befehl formatieren und Netsh-Befehle auf lokalen Computern und Remotecomputern ausführen, auf denen Windows Server 2016 oder Windows 10 verwenden.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 8cb9b59f-0255-4261-b49a-562c5ea50ee0
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c7c16674b831431ff5bb1d0172cc2b2a939008f6
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="netsh-command-syntax-contexts-and-formatting"></a>Netsh-Befehl Syntax Kontexte und formatieren

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können in diesem Thema erfahren Sie, wie Sie geben Sie Netsh-Kontext und Unterkontexte, zu verstehen, Netsh-Syntax und Befehl formatieren und zum Ausführen von Netsh-Befehle auf lokalen Computern und Remotecomputern verwenden.

Netsh ist ein Befehlszeilen-skripthilfsprogramm, mit der Sie anzeigen oder ändern die Netzwerkkonfiguration eines Computers, der derzeit ausgeführt wird. Netsh-Befehle können durch Eingabe von Befehlen an der Eingabeaufforderung Netsh ausgeführt werden, und sie können in Batchdateien oder Skripts verwendet werden. Remote-Computer und dem lokalen Computer können mithilfe von Netsh-Befehle konfiguriert werden.

Netsh bietet auch eine Skriptingfunktion, mit der Sie eine Gruppe von Befehlen im Batchmodus für einen bestimmten Computer ausführen kann. Mit Netsh können Sie ein Konfigurationsskript in einer Textdatei zu Archivierungszwecken oder können Sie die Konfiguration anderer Computer speichern.

## <a name="netsh-contexts"></a>Netsh-Kontext

Netsh interagiert mit anderen Komponenten des Betriebssystems mithilfe von Dynamic\-Link Library \(DLL\) Dateien. 

Jede Netsh-Hilfsprogramm-DLL bietet einen umfangreichen Satz von Features, die Namen einer *Kontext*, ist eine Gruppe von spezifischen Befehlen für eine Netzwerk-Serverrolle oder ein Feature. Diese Kontexte erweitern die Funktionalität von Netsh durch die Konfiguration und Überwachung von Unterstützung für Dienste, Dienstprogramme oder Protokolle. Beispielsweise bietet Dhcpmon.dll Netsh mit dem Kontext und einen Satz von Befehlen, die zum Konfigurieren und Verwalten von DHCP-Servern erforderlich.

### <a name="obtain-a-list-of-contexts"></a>Abrufen einer Liste von Kontexten

Sie können eine Liste der Netsh-Kontext abrufen, indem Sie die Befehlszeile oder Windows PowerShell auf einem Computer unter Windows Server 2016 oder Windows 10 öffnen. Geben Sie den Befehl **Netsh** und drücken Sie die EINGABETASTE. Typ **/? **, und drücken Sie dann die EINGABETASTE.

Im folgenden sehen die Ausgabe von Beispiel für diese Befehle auf einem Computer unter Windows Server 2016 Datacenter.

    PS C:\Windows\system32> netsh
    netsh>/?
    
    The following commands are available:
    
    Commands in this context:
    ..            - Goes up one context level.
    ?             - Displays a list of commands.
    abort         - Discards changes made while in offline mode.
    add           - Adds a configuration entry to a list of entries.
    advfirewall   - Changes to the `netsh advfirewall' context.
    alias         - Adds an alias.
    branchcache   - Changes to the `netsh branchcache' context.
    bridge        - Changes to the `netsh bridge' context.
    bye           - Exits the program.
    commit        - Commits changes made while in offline mode.
    delete        - Deletes a configuration entry from a list of entries.
    dhcpclient    - Changes to the `netsh dhcpclient' context.
    dnsclient     - Changes to the `netsh dnsclient' context.
    dump          - Displays a configuration script.
    exec          - Runs a script file.
    exit          - Exits the program.
    firewall      - Changes to the `netsh firewall' context.
    help          - Displays a list of commands.
    http          - Changes to the `netsh http' context.
    interface     - Changes to the `netsh interface' context.
    ipsec         - Changes to the `netsh ipsec' context.
    ipsecdosprotection - Changes to the `netsh ipsecdosprotection' context.
    lan           - Changes to the `netsh lan' context.
    namespace     - Changes to the `netsh namespace' context.
    netio         - Changes to the `netsh netio' context.
    offline       - Sets the current mode to offline.
    online        - Sets the current mode to online.
    popd          - Pops a context from the stack.
    pushd         - Pushes current context on stack.
    quit          - Exits the program.
    ras           - Changes to the `netsh ras' context.
    rpc           - Changes to the `netsh rpc' context.
    set           - Updates configuration settings.
    show          - Displays information.
    trace         - Changes to the `netsh trace' context.
    unalias       - Deletes an alias.
    wfp           - Changes to the `netsh wfp' context.
    winhttp       - Changes to the `netsh winhttp' context.
    winsock       - Changes to the `netsh winsock' context.
    
    The following sub-contexts are available:
     advfirewall branchcache bridge dhcpclient dnsclient firewall http interface ipsec ipsecdosprotection lan namespace netio ras rpc trace wfp winhttp winsock
    
    To view help for a command, type the command, followed by a space, and then
     type ?.


### <a name="subcontexts"></a>Folgende Unterkontexte

Netsh-Kontext können enthalten, Befehle und zusätzliche Kontexten aufgerufen *Unterkontexte*. Im Kontext Routing können Sie z. B. auf die IP- und IPv6-Unterkontexte ändern.

Klicken Sie zum Anzeigen einer Liste von Befehlen und Unterkontexte, mit denen Sie in einem Kontext, an der Eingabeaufforderung Netsh, geben Sie den Kontext ein, und geben Sie entweder **/?** oder **Hilfe**. Beispielsweise, um eine Liste der Befehle, die Sie verwenden können und Unterkontexte im an der Eingabeaufforderung Netsh-Kontext Routing anzeigen \ (d. h. **Netsh&gt;**\), geben Sie einen der folgenden:

**Routing /?**

**Routing-Hilfe**

Geben Sie zum Ausführen von Aufgaben in einem anderen Kontext ohne Änderung von Ihrem aktuellen Kontext, den Kontextpfad des Befehls, die Sie an der Eingabeaufforderung Netsh verwenden möchten. Geben Sie z. B. zum Hinzufügen einer Schnittstelle, die mit dem Namen "LAN-Verbindung" im Zusammenhang mit IGMP, ohne zuerst auf den IGMP-Kontext, an der Eingabeaufforderung Netsh:

**Routing Ip Igmp hinzufügen Interface "LAN-Verbindung" Startupqueryinterval = 21**

## <a name="running-netsh-commands"></a>Netsh-Befehle ausführen

Um einen Netsh-Befehl ausführen, müssen Sie Netsh über die Befehlszeile starten, indem Sie die Eingabe **Netsh** und dann die EINGABETASTE drücken. Als Nächstes können Sie für den Kontext ändern, die mit dem Befehl enthält, den Sie verwenden möchten. Die Kontexte, die verfügbar sind, hängt von der Netzwerkkomponenten, die Sie installiert haben. Angenommen, Sie geben **Dhcp** an der Eingabeaufforderung Netsh und drücken Sie die EINGABETASTE, Netsh geändert wird, für den DHCP-Server-Kontext. Wenn Sie nicht DHCP installiert haben, wird jedoch die folgende Meldung angezeigt:

**Der folgende Befehl wurde nicht gefunden: Dhcp.**

## <a name="formatting-legend"></a>Formatierung

Sie können die folgende formatierungslegende zum Interpretieren und richtigen Netsh Befehlssyntax verwenden, wenn Sie den Befehl an der Eingabeaufforderung Netsh oder eine Batchdatei oder ein Skript ausführen.

- Text in *Kursiv* sind Informationen, die Sie angeben müssen, während Sie den Befehl eingeben. Wenn ein Befehl mit dem Namen - Parameter enthält z. B.*Benutzername*, geben Sie den jeweiligen Benutzernamen.
- Text in **fett** sind Informationen, die Sie genau wie dargestellt, während der Eingabe des Befehls eingeben müssen.
- Text, gefolgt von einer Ellipse \(...\) ist ein Parameter, der in einer Befehlszeile mehrmals wiederholt werden kann.
- Text, der zwischen Klammern [&nbsp;] ist optional.
- Text, der zwischen geschweiften Klammern {&nbsp;} Optionen voneinander getrennt durch einen senkrechten Strich bietet eine Reihe von Optionen, die von dem Sie nur eine, wie z. B. auswählen müssen `{enable|disable}`.
- Mit der Schriftart Courier formatierter Text ist Code oder Programmausgabe.

## <a name="running-netsh-commands-from-the-command-prompt-or-windows-powershell"></a>Netsh-Befehle an der Befehlszeile oder Windows PowerShell ausführen

Starten von Network Shell, und geben Netsh an der Eingabeaufforderung oder in Windows PowerShell, können Sie den folgenden Befehl verwenden.

### <a name="netsh"></a>Netsh

Netsh ist ein Befehlszeilen-skripthilfsprogramm, mit dem Sie lokal oder Remote anzeigen oder ändern die Netzwerkkonfiguration eines derzeit ausgeführten Computers. Ohne Parameter **Netsh** öffnet der Netsh.exe-Befehlszeile \ (d. h. **Netsh&gt;**\).

#### <a name="syntax"></a>Syntax

**netsh**\[ **-a**&nbsp;*AliasFile*\] \[ **-c**&nbsp;*Context* \] \[**-r**&nbsp;*RemoteComputer*\] \[ **-u** \[ *DomainName\\* \] *UserName* \] \[ **-p**&nbsp;*Password* | \*\] \[{*NetshCommand* | **-f**&nbsp;*ScriptFile*}\]

#### <a name="parameters"></a>Parameter

**`-a`**

Optional. Gibt an, dass Sie an zurückgegeben werden die **Netsh** Aufforderung nach der Ausführung *Aliasdatei*.

**`AliasFile`**

Optional. Gibt den Namen der Textdatei mit den enthält eine oder mehrere **Netsh** Befehle.

**`-c`**

Optional. Gibt an, Netsh wechselt in den angegebenen **Netsh** Kontext.

**`Context`**

Optional. Gibt die **Netsh** Kontext, die Sie eingeben möchten. 

**`-r`**

Optional. Gibt an, dass den Befehl auf einem Remotecomputer ausgeführt werden soll.

>[!IMPORTANT]
>Wenn Sie verwenden einige Netsh-Befehle Remote auf einem anderen Computer mit der **Netsh – R** -Parameter, der Remoteregistrierungsdienst muss ausgeführt werden auf dem Remotecomputer. Wenn sie nicht ausgeführt wird, zeigt Windows eine Fehlermeldung "Der Pfad nicht gefunden".

***`RemoteComputer`***

Optional. Gibt die remote-Computer, den Sie konfigurieren möchten.

**`-u`**

Optional. Gibt an, dass die Netsh-Befehl unter einem Benutzerkonto ausgeführt werden soll.

***`DomainName\\`***

Optional. Gibt die Domäne, in denen das Benutzerkonto befindet. Der Standardwert ist die lokale Domäne, wenn *DomainName\\* nicht angegeben ist.

***`UserName`***

Optional. Gibt den Namen des Benutzerkontos an.

**`-p`**

Optional. Gibt an, dass Sie ein Kennwort für das Benutzerkonto angeben möchten.

***`Password`***

Optional. Gibt das Kennwort für das Benutzerkonto, das die Angabe mit **-u** *Benutzername*.

***`NetshCommand`***

Optional. Gibt die **Netsh** Befehl, der ausgeführt werden soll.

**`-f`**

Optional. Beendet **Netsh** nach dem Ausführen des Skripts, die Sie mit festlegen *Skriptdatei*.

***`ScriptFile`***

Optional. Gibt das Skript an, das Sie ausführen möchten.

**`/?`**

Optional. Zeigt die Hilfe an der Eingabeaufforderung Netsh.

>[!NOTE]
>Wenn Sie angeben, ** `-r` ** gefolgt von einem anderen Befehl **Netsh** führt den Befehl auf dem Remotecomputer und dann in der Befehlszeile Cmd.exe zurück. Wenn Sie angeben, ** `-r` ** ohne einen anderen Befehl **Netsh** im Remotemodus wird geöffnet. Der Prozess ist vergleichbar mit der Verwendung **Satz Computer** an der Eingabeaufforderung Netsh. Bei Verwendung ** `-r` **, legen Sie den Zielcomputer für die aktuelle Instanz des **Netsh** nur. Nach dem Beenden und erneut eingeben **Netsh**, wird die Ziel-PC als dem lokalen Computer zurückgesetzt. Sie können ausführen **Netsh** Befehle auf einem Remotecomputer durch Angabe eines Computers Namen in WINS gespeichert, einen UNC-Namen, den Internetnamen eines, um über den DNS-Server oder eine IP-Adresse aufgelöst werden.

**Geben die Zeichenfolge Parameterwerte für Netsh-Befehle**

In der gesamten Netsh-Befehlsreferenz stehen Befehle, die Parameter enthalten, für die ein Zeichenfolgenwert erforderlich ist.

Im Fall einen Zeichenfolgenwert enthält, in denen Leerzeichen zwischen den Zeichen, z. B. Zeichenfolgenwerte, die aus mehreren Wörtern bestehen ist es erforderlich, dass Sie den Zeichenfolgenwert in Anführungszeichen einschließen. Z. B. für einen Parameter mit dem Namen **Schnittstelle** mit einem Zeichenfolgenwert **Wireless Network Connection**, verwenden Sie den Zeichenfolgenwert in Anführungszeichen einschließen:

**`interface="Wireless Network Connection"`**

