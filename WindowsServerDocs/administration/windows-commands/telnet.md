---
title: telnet
description: Referenz Artikel für Telnet, der mit einem Computer kommuniziert, auf dem der Telnet-Server Dienst ausgeführt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b70a6156-9413-4300-84ce-a34c467e2b4e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a5f588328deb51109ee9139b6e7dfaad8f0166dc
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934219"
---
# <a name="telnet"></a>telnet

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kommuniziert mit einem Computer, auf dem der Telnet-Server Dienst ausgeführt wird.

## <a name="syntax"></a>Syntax
```
telnet [/a] [/e <EscapeChar>] [/f <FileName>] [/l <UserName>] [/t {vt100 | vt52 | ansi | vtnt}] [<Host> [<Port>]] [/?]
```
#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/a|versuchen Sie die automatische Anmeldung. Identisch mit der Option/l, mit der Ausnahme, dass der Name des aktuell angemeldeten Benutzers verwendet wird.|
|/e\<EscapeChar>|Escapezeichen für die Eingabe der Telnet-Client Eingabeaufforderung.|
|/f \<FileName>|Der für die Client seitige Protokollierung verwendete Dateiname.|
|/l\<UserName>|Gibt den Benutzernamen für die Anmeldung auf dem Remote Computer an.|
|/t {VT100 &#124; VT52 &#124; ANSI &#124; VTNT}|Gibt den Terminaltyp an. Unterstützte Terminal Typen sind VT100, vt52, ANSI und VTNT.|
|\<Host> [\<Port>]|Gibt den Hostnamen oder die IP-Adresse des Remote Computers an, mit dem eine Verbindung hergestellt werden soll, und optional den zu verwendenden TCP-Port (standardmäßig TCP-Port 23).|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an. Alternativ können Sie/h. eingeben.|

## <a name="remarks"></a>Hinweise
-   Sie müssen die Telnet-Client Software installieren, bevor Sie diesen Befehl ausführen können. Weitere Informationen finden Sie unter [Installieren von Telnet](https://technet.microsoft.com/library/cc754293(v=ws.10).aspx).
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
-   [Installieren von Telnet](https://technet.microsoft.com/library/cc754293(v=ws.10).aspx)
-   [Technische Referenz für Telnet](https://technet.microsoft.com/library/cc754987(v=ws.10).aspx)
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
