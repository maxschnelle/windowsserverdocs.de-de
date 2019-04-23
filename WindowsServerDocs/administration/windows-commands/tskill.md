---
title: tskill
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 08986e6a-6900-4ece-85a1-8f73b14db1b3 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 59958481a7c832aca7bc25d7d4d3ebbf4e8ef80c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835041"
---
# <a name="tskill"></a>tskill

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Beendet einen Prozess auf einem Remotedesktop-Sitzungshost (rd Session Host)-Server in einer Sitzung ausgeführt.
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
tskill {<ProcessID> | <ProcessName>} [/server:<ServerName>] [/id:<SessionID> | /a] [/v]
```

## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|\<Prozess-ID >|Gibt die ID des Prozesses, die Sie beenden möchten.|
|\<ProcessName >|Gibt den Namen des Prozesses, die Sie beenden möchten. Dieser Parameter kann Platzhalterzeichen enthalten.|
|/server:\<ServerName>|Gibt an, der Terminalserver, der die den Prozess enthält, den Sie beenden möchten. Wenn **/Server** nicht angegeben ist, wird der aktuelle RD Session Host-Server verwendet wird.|
|/id:\<SessionID>|Beendet den Prozess, der in der angegebenen Sitzung ausgeführt wird.|
|/a|Beendet den Prozess, der in allen Sitzungen ausgeführt wird.|
|/v|Zeigt Informationen zu den Aktionen, die ausgeführt wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Sie können **Tskill** beendet nur die Prozesse, die zu Ihnen gehören, es sei denn, Sie Administrator sind. Administratoren haben vollen Zugriff auf alle **Tskill** Funktionen und können end-Prozesse, die in anderen benutzersitzungen ausgeführt werden.
-   Wenn alle Prozesse, die in einer Sitzung ausgeführt werden zu beenden, wird auch die Sitzung beendet.
-   Bei Verwendung der *ProcessName* und die **/Server: *** ServerName* Parameter auch Geben Sie die **/ID: *** SessionID* oder   **/a** Parameter.

## <a name="BKMK_examples"></a>Beispiele für
-   Um den Prozess 6543 zu beenden, geben Sie Folgendes ein:
    ```
    tskill 6543
    ```
-   Um den Prozess "Explorer" auf 5-Sitzung zu beenden, geben Sie Folgendes ein:
    ```
    tskill explorer /id:5
    ```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[Remotedesktopdienste &#40;Terminaldienste&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
