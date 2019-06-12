---
title: tsdiscon
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13139674-7dee-4965-8cac-32f4928e8b9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a1b5fca329864ebed9eab66671a17493f0fc3ca8
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440910"
---
# <a name="tsdiscon"></a>tsdiscon

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Trennt eine-Sitzung von einem Server Remote Desktop Session Host (rd Session Host).
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
tsdiscon [<SessionID> | <SessionName>] [/server:<ServerName>] [/v]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|\<SessionId>|Gibt die ID der Sitzung zu trennen.|
|\<SessionName>|Gibt den Namen der Sitzung zu trennen.|
|/server:\<ServerName>|Gibt an, die Terminalserver, der die Sitzung enthält, die Sie trennen möchten. Andernfalls wird der aktuelle rd Session Host-Server verwendet.|
|/v|Zeigt Informationen zu den Aktionen, die ausgeführt wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Sie müssen über die Full Control-Berechtigung verfügen oder spezielle Zugriffsberechtigungen für ein anderer Benutzer trennen einer Sitzung trennen.
-   Wenn keine Sitzungs-ID oder ein Sitzungsname angegeben wird, **Tsdiscon** trennt die aktuelle Sitzung.
-   Alle Anwendungen, die ausgeführt wurden, wenn Sie die Sitzung getrennt werden automatisch ausgeführt, wenn Sie die Verbindung dieser Sitzung ohne Verlust von Daten wiederherstellen. Verwendung **-Sitzung zurücksetzen** um die ausgeführten Anwendungen der getrennten Sitzung zu beenden, aber denken Sie daran, dass dies in der Sitzung Datenverlust führen kann.
-   Die **/Server** Parameter ist erforderlich, nur bei Verwendung von **Tsdiscon** von einem Remoteserver.
-   Die konsolensitzung kann nicht getrennt werden.

## <a name="BKMK_examples"></a>Beispiele für
- Wenn die aktuelle Sitzung trennen möchten, geben Sie Folgendes ein:
  ```
  tsdiscon
  ```
- Wenn Sitzung 10 trennen möchten, geben Sie Folgendes ein:
  ```
  tsdiscon 10
  ```
- Wenn die Sitzung mit dem Namen TERM04 trennen möchten, geben Sie Folgendes ein:
  ```
  tsdiscon TERM04
  ```
  #### <a name="additional-references"></a>Weitere Verweise
  [Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
  [Remotedesktopdienste &#40;Terminaldienste&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
