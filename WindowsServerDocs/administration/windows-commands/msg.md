---
title: msg
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9501cf3e-568e-4982-9987-8daecc6c17ff
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68a393b57a255915b93759b4b26286ce4d838019
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437223"
---
# <a name="msg"></a>msg

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sendet eine Nachricht zu einem Benutzer auf einem Server Remote Desktop Session Host (rd Session Host).
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
msg {<UserName> | <SessionName> | <SessionID>| @<FileName> | *} [/server:<ServerName>] [/time:<Seconds>] [/v] [/w] [<Message>]
```

## <a name="parameters"></a>Parameter

|      Parameter       |                                                                                                                               Beschreibung                                                                                                                               |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      <UserName>      |                                                                                                  Gibt den Namen des Benutzers, der die Nachricht empfangen soll.                                                                                                   |
|    <SessionName>     |                                                                                                 Gibt den Namen der Sitzung, die die Nachricht empfangen soll.                                                                                                 |
|     <SessionID>      |                                                                                            Gibt an, die numerische ID der Sitzung, deren Benutzer eine Meldung angezeigt werden sollen.                                                                                            |
|     @<FileName>      |                                                                         Identifiziert eine Datei mit einer Liste von Benutzernamen, Namen und die Sitzungs-IDs, die die Nachricht empfangen werden sollen.                                                                         |
|          \*          |                                                                                                           Sendet die Nachricht an alle Benutzernamen auf dem System.                                                                                                            |
| /server:<ServerName> |                                              Gibt dem RD-Sitzungshostserver, deren Sitzung oder der Benutzer die Meldung angezeigt werden soll. Falls nicht angegeben, **/Server** verwendet der Server, auf die Sie derzeit angemeldet sind.                                              |
|   / Time:<Seconds>    | Gibt die Zeitspanne, die die Meldung, die Sie gesendet, die auf dem Bildschirm des Benutzers angezeigt wird. Wenn das Zeitlimit erreicht wird, verschwindet die Nachricht. Wenn keine zeitliche Begrenzung festgelegt ist, werden die Nachricht auf dem Bildschirm des Benutzers bleibt, bis der Benutzer die Meldung angezeigt, und klickt auf **OK**. |
|          /v          |                                                                                                         Zeigt Informationen zu den Aktionen, die ausgeführt wird.                                                                                                         |
|          /w          |         Wartet auf eine Bestätigung vom Benutzer, dass die Nachricht empfangen wurde. Verwenden Sie diesen Parameter mit **/Uhrzeit:** <*Sekunden*> um eine mögliche lange Verzögerung zu vermeiden, wenn der Benutzer nicht sofort reagiert. Dieser Parameter mit **/v** ist auch hilfreich.          |
|      <Message>       |                  Gibt den Text der Nachricht, die Sie senden möchten. Wenn keine Meldung angegeben wird, werden Sie aufgefordert werden, eine Nachricht eingeben. Geben Sie zum Senden einer Nachricht, die in einer Datei enthalten ist, das kleiner-als (<) gefolgt vom Namen Datei ein.                  |
|          /?          |                                                                                                                  Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                   |

## <a name="remarks"></a>Hinweise
-   Wenn Sie einen Benutzer nicht angeben oder eine Sitzung, **msg** wird eine Fehlermeldung angezeigt. Wenn Sie eine Sitzung angeben, muss es eine aktiv sein.
-   Die Benutzer benötigen spezielle Zugriffsberechtigung zum Senden einer Nachricht.

## <a name="BKMK_examples"></a>Beispiele für
-   Um die Nachricht mit dem Titel "Treffen wir uns noch heute 13 Uhr" zu allen Sitzungen für "user1" zu senden, geben Sie Folgendes ein:
    ```
    msg User1 Let's meet at 1PM today
    ```
-   Um die gleiche Nachricht an die Sitzung modeM02 senden zu können, geben Sie Folgendes ein:
    ```
    msg modem02 Let's meet at 1PM today
    ```
-   Geben Sie Folgendes ein, um das Senden der Nachricht an die Sitzung 12:
    ```
    msg 12 Let's meet at 1PM today
    ```
-   Um die Nachricht an alle Sitzungen, die in der Datei USERlist enthaltenen senden möchten, geben Sie Folgendes ein:
    ```
    msg @userlist Let's meet at 1PM today
    ```
-   Zum Senden der Nachricht an alle Benutzer angemeldet sind, geben Sie Folgendes ein:
    ```
    msg * Let's meet at 1PM today
    ```
-   Zum Senden der Nachricht an alle Benutzer, ein Timeout der Bestätigung (z. B. 10 Sekunden), geben Sie Folgendes ein:
    ```
    msg * /time:10 Let's meet at 1PM today
    ```

#### <a name="additional-references"></a>Zusätzliche Referenzen
-  [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-  [Remotedesktopdienste &#40;Terminaldienste&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
