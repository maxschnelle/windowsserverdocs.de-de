---
title: telnet
description: Referenz Artikel für den Telnet-Befehl, der mit einem Computer kommuniziert, auf dem der Telnet-Server Dienst ausgeführt wird.
ms.topic: reference
ms.assetid: b70a6156-9413-4300-84ce-a34c467e2b4e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: cf4fa5754aec18662800f4536afd16a427ca0952
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91717927"
---
# <a name="telnet"></a>telnet

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kommuniziert mit einem Computer, auf dem der Telnet-Server Dienst ausgeführt wird. Wenn Sie diesen Befehl ohne Parameter ausführen, können Sie den Telnet-Kontext eingeben, wie von der Telnet-Eingabeaufforderung (**Microsoft Telnet>**) angegeben. Über die Telnet-Eingabeaufforderung können Sie den Computer, auf dem der Telnet-Client ausgeführt wird, mit Telnet-Befehlen verwalten.

> [!IMPORTANT]
> Sie müssen die Telnet-Client Software installieren, bevor Sie diesen Befehl ausführen können. Weitere Informationen finden Sie unter [Installieren von Telnet](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754293(v=ws.10)).

## <a name="syntax"></a>Syntax

```
telnet [/a] [/e <escapechar>] [/f <filename>] [/l <username>] [/t {vt100 | vt52 | ansi | vtnt}] [<host> [<port>]] [/?]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /a | Versucht die automatische Anmeldung. Identisch mit der Option **/l** , mit der Ausnahme, dass der Name des aktuell angemeldeten Benutzers verwendet wird. |
| /e `<escapechar>` | Gibt das Escapezeichen an, mit dem die Telnet-Client Eingabeaufforderung eingegeben wird. |
| /f `<filename>` | Gibt den Dateinamen für die Client seitige Protokollierung an. |
| /l `<username>` | Gibt den Benutzernamen für die Anmeldung auf dem Remote Computer an. |
| /t `{vt100 | vt52 | ansi | vtnt}` | Gibt den Terminaltyp an. Unterstützte Terminal Typen sind **VT100**, **VT52**, **ANSI**und **VTNT**. |
| `<host> [<port>]` | Gibt den Hostnamen oder die IP-Adresse des Remote Computers an, mit dem eine Verbindung hergestellt werden soll, und optional den zu verwendenden TCP-Port (standardmäßig TCP-Port 23). |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um mit Telnet eine Verbindung mit dem Computer herzustellen, auf dem der Telnet-Server Dienst unter *Telnet.Microsoft.com*

```
telnet telnet.microsoft.com
```

Wenn Sie zum Herstellen einer Verbindung mit dem Computer, auf dem der Telnet-Server Dienst unter *Telnet.Microsoft.com auf dem TCP-Port 44* ausgeführt wird, und die Sitzungs Aktivität in einer lokalen Datei namens *telnetlog.txt*verwenden möchten, geben Sie Folgendes ein

```
telnet /f telnetlog.txt telnet.microsoft.com 44
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Installieren von Telnet](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754293(v=ws.10))

- [Technische Referenz für Telnet](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754987(v=ws.10))
