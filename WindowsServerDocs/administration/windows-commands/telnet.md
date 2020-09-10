---
title: telnet
description: Referenz Artikel für Telnet, der mit einem Computer kommuniziert, auf dem der Telnet-Server Dienst ausgeführt wird.
ms.topic: reference
ms.assetid: b70a6156-9413-4300-84ce-a34c467e2b4e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9110bd2f3d4c701e46c8a52af48773f7d5a1026b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640810"
---
# <a name="telnet"></a>telnet

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kommuniziert mit einem Computer, auf dem der Telnet-Server Dienst ausgeführt wird.

## <a name="syntax"></a>Syntax
```
telnet [/a] [/e <EscapeChar>] [/f <FileName>] [/l <UserName>] [/t {vt100 | vt52 | ansi | vtnt}] [<Host> [<Port>]] [/?]
```
#### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|/a|versuchen Sie die automatische Anmeldung. Identisch mit der Option/l, mit der Ausnahme, dass der Name des aktuell angemeldeten Benutzers verwendet wird.|
|/e \<EscapeChar>|Escapezeichen für die Eingabe der Telnet-Client Eingabeaufforderung.|
|/f \<FileName>|Der für die Client seitige Protokollierung verwendete Dateiname.|
|/l \<UserName>|Gibt den Benutzernamen für die Anmeldung auf dem Remote Computer an.|
|/t {VT100 &#124; VT52 &#124; ANSI &#124; VTNT}|Gibt den Terminaltyp an. Unterstützte Terminal Typen sind VT100, vt52, ANSI und VTNT.|
|\<Host> [\<Port>]|Gibt den Hostnamen oder die IP-Adresse des Remote Computers an, mit dem eine Verbindung hergestellt werden soll, und optional den zu verwendenden TCP-Port (standardmäßig TCP-Port 23).|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an. Alternativ können Sie/h. eingeben.|

## <a name="remarks"></a>Hinweise
-   Sie müssen die Telnet-Client Software installieren, bevor Sie diesen Befehl ausführen können. Weitere Informationen finden Sie unter [Installieren von Telnet](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754293(v=ws.10)).
-   Sie können Telnet ohne Parameter ausführen, um den Telnet-Kontext einzugeben, der durch die Telnet-Eingabeaufforderung (**Microsoft Telnet>**) angegeben wird. Über die Telnet-Eingabeaufforderung können Sie den Computer, auf dem der Telnet-Client ausgeführt wird, mit Telnet-Befehlen verwalten.

## <a name="examples"></a>Beispiele
Verwenden Sie Telnet zum Herstellen einer Verbindung mit dem Computer, auf dem der Telnet-Server Dienst unter Telnet.Microsoft.com ausgeführt wird
```
telnet telnet.microsoft.com
```
Stellen Sie mithilfe von Telnet eine Verbindung mit dem Computer her, auf dem der Telnet-Server Dienst unter Telnet.Microsoft.com auf TCP-Port 44 ausgeführt wird, und protokollieren Sie die Sitzungs Aktivität in einer telnetlog.txt lokalen
```
telnet /f telnetlog.txt telnet.microsoft.com 44
```

## <a name="additional-references"></a>Weitere Verweise
-   [Installieren von Telnet](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754293(v=ws.10))
-   [Technische Referenz für Telnet](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754987(v=ws.10))
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
