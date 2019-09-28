---
title: msg
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 42a614f313d1e68dbf78d19a498563b541c52be1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373433"
---
# <a name="msg"></a>msg

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet eine Nachricht an einen Benutzer auf einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host).
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
msg {<UserName> | <SessionName> | <SessionID>| @<FileName> | *} [/server:<ServerName>] [/time:<Seconds>] [/v] [/w] [<Message>]
```

## <a name="parameters"></a>Parameter

|      Parameter       |                                                                                                                               Beschreibung                                                                                                                               |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      <UserName>      |                                                                                                  Gibt den Namen des Benutzers an, der die Nachricht empfangen soll.                                                                                                   |
|    <SessionName>     |                                                                                                 Gibt den Namen der Sitzung an, die die Nachricht empfangen soll.                                                                                                 |
|     <SessionID>      |                                                                                            Gibt die numerische ID der Sitzung an, deren Benutzer eine Nachricht erhalten soll.                                                                                            |
|     @<FileName>      |                                                                         Identifiziert eine Datei, die eine Liste von Benutzernamen, Sitzungs Namen und Sitzungs-IDs enthält, die Sie empfangen möchten.                                                                         |
|          \*          |                                                                                                           Sendet die Nachricht an alle Benutzernamen im System.                                                                                                            |
| /server:<ServerName> |                                              Gibt den RD-Sitzungs Host Server an, dessen Sitzung oder Benutzer die Nachricht empfangen soll. Wenn nicht angegeben, verwendet **/Server** den Server, auf dem Sie zurzeit angemeldet sind.                                              |
|   /Time: <Seconds>    | Gibt die Zeitspanne an, zu der die gesendete Nachricht auf dem Bildschirm des Benutzers angezeigt wird. Wenn das Zeitlimit erreicht ist, wird die Meldung nicht mehr angezeigt. Wenn kein Zeit Limit festgelegt ist, verbleibt die Nachricht auf dem Bildschirm des Benutzers, bis der Benutzer die Meldung sieht und auf **OK**klickt. |
|          /v          |                                                                                                         Zeigt Informationen zu den Aktionen an, die ausgeführt werden.                                                                                                         |
|          /w          |         Wartet auf eine Bestätigung des Benutzers, dass die Nachricht empfangen wurde. Verwenden Sie diesen Parameter mit **/Time:** <*Sekunden*>, um eine mögliche lange Verzögerung zu vermeiden, wenn der Benutzer nicht sofort antwortet. Die Verwendung dieses Parameters mit **/v** ist ebenfalls hilfreich.          |
|      <Message>       |                  Gibt den Text der Nachricht an, die Sie senden möchten. Wenn keine Meldung angegeben ist, werden Sie aufgefordert, eine Meldung einzugeben. Um eine Nachricht zu senden, die in einer Datei enthalten ist, geben Sie das Symbol kleiner als (<) gefolgt vom Dateinamen ein.                  |
|          /?          |                                                                                                                  Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                   |

## <a name="remarks"></a>Hinweise
-   Wenn Sie keinen Benutzer oder eine Sitzung angeben, wird von **msg** eine Fehlermeldung angezeigt. Wenn eine Sitzung angegeben wird, muss Sie aktiv sein.
-   Der Benutzer muss über eine Nachrichten Zugriffsberechtigung verfügen, um eine Nachricht zu senden.

## <a name="BKMK_examples"></a>Beispiele
-   Geben Sie Folgendes ein, um die Nachricht mit dem Titel "Wir können heute um 1 Uhr an allen Sitzungen für User1" zu senden:
    ```
    msg User1 Let's meet at 1PM today
    ```
-   Um dieselbe Nachricht an Session modeM02 zu senden, geben Sie Folgendes ein:
    ```
    msg modem02 Let's meet at 1PM today
    ```
-   Geben Sie Folgendes ein, um die Nachricht an Sitzung 12 zu senden:
    ```
    msg 12 Let's meet at 1PM today
    ```
-   Geben Sie Folgendes ein, um die Nachricht an alle Sitzungen zu senden, die in der Datei userlist enthalten sind:
    ```
    msg @userlist Let's meet at 1PM today
    ```
-   Geben Sie Folgendes ein, um die Nachricht an alle angemeldeten Benutzer zu senden:
    ```
    msg * Let's meet at 1PM today
    ```
-   Geben Sie Folgendes ein, um die Nachricht mit einem Timeout der Bestätigung (z. b. 10 Sekunden) an alle Benutzer zu senden:
    ```
    msg * /time:10 Let's meet at 1PM today
    ```

#### <a name="additional-references"></a>Weitere Verweise
-  [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-  [Remotedesktopdienste &#40;Befehlsreferenz&#41; für terminaldienstedienste](remote-desktop-services-terminal-services-command-reference.md)
