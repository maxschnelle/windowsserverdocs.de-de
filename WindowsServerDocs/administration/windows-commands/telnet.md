---
title: telnet
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b70a6156-9413-4300-84ce-a34c467e2b4e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6439a91d82d6d199666629e333d8130bf65a384b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858561"
---
# <a name="telnet"></a>telnet

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Kommuniziert mit einem Computer mit dem Telnet-Server-Dienst. 
## <a name="syntax"></a>Syntax
```
telnet [/a] [/e <EscapeChar>] [/f <FileName>] [/l <UserName>] [/t {vt100 | vt52 | ansi | vtnt}] [<Host> [<Port>]] [/?]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/a|Automatische Anmeldung. Identisch mit/l option außer verwendet derzeit angemeldeten auf s Benutzernamen.|
|/ e \<EscapeChar >|Escape-Zeichen verwendet, um die Telnet-Client-Eingabeaufforderung einzugeben.|
|/f \<FileName>|Der Dateiname für die clientseitigen Protokollierung verwendet.|
|/ l \<Benutzername >|Gibt den Benutzernamen ein, auf dem Remotecomputer mit anmelden.|
|/t {vt100 &#124; vt52 &#124; ansi &#124; vtnt}|Gibt den Typ der Terminaldienste. Unterstützte terminal Typen sind vt100, vt52, Ansi und gesendet.|
|\<Host> [\<Port>]|Gibt den Hostnamen oder die IP-Adresse des Remotecomputers auf das Herstellen einer Verbindung mit und optional den zu verwendenden TCP-Port (Standardmäßig wird TCP-Port 23).|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an. Alternativ können Sie/h eingeben.|

## <a name="remarks"></a>Hinweise
-   Sie müssen die Telnet-Client-Software installieren, bevor Sie diesen Befehl ausführen können. Weitere Informationen finden Sie unter [installieren Telnet](https://technet.microsoft.com/library/cc754293(v=ws.10).aspx).
-   Können Sie Telnet ohne Parameter, geben Sie den Telnet-Kontext, angegeben durch die Telnet-Aufforderung ausführen (**Microsoft Telnet >**). Der Telnet-Eingabeaufforderung können Sie Telnet-Befehle zum Verwalten des Computers, der Telnetclient ausgeführt wird.

## <a name="BKMK_Examples"></a>Beispiele für
Verwenden Sie für die Verbindung an den Computer mit dem Telnet-Server-Dienst auf telnet.microsoft.com Telnet.
```
telnet telnet.microsoft.com
```
Verwenden Sie eine Verbindung mit Computer, auf den Telnet-Server-Dienst auf telnet.microsoft.com TCP-Port 44 ausgeführt, und melden Sie sich die Session-Aktivität in einer lokalen Datei namens telnetlog.txt telnet
```
telnet /f telnetlog.txt telnet.microsoft.com 44
```

## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Installieren von telnet](https://technet.microsoft.com/library/cc754293(v=ws.10).aspx)
-   [Telnet-technische Referenz](https://technet.microsoft.com/library/cc754987(v=ws.10).aspx)
-   [Befehlszeilensyntax](command-line-syntax-key.md)
