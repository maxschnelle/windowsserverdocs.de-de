---
title: mldg
description: Referenz Artikel für den Befehl "msg", der eine Nachricht an einen Benutzer auf einem Remotedesktop-Sitzungshost Server sendet
ms.topic: reference
ms.assetid: 9501cf3e-568e-4982-9987-8daecc6c17ff
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 34b51bb82fdac6b847d69b4d59a345777054839f
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639637"
---
# <a name="msg"></a>mldg

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet eine Nachricht an einen Benutzer auf einem Remotedesktop-Sitzungshost Server.

> [!NOTE]
> Zum Senden einer Nachricht müssen Sie über eine spezielle Zugriffsberechtigung für eine Nachricht verfügen.

## <a name="syntax"></a>Syntax

```
msg {<username> | <sessionname> | <sessionID>| @<filename> | *} [/server:<servername>] [/time:<seconds>] [/v] [/w] [<message>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<username>` | Gibt den Namen des Benutzers an, der die Nachricht empfangen soll. Wenn Sie keinen Benutzer oder eine Sitzung angeben, wird mit diesem Befehl eine Fehlermeldung angezeigt. Wenn eine Sitzung angegeben wird, muss Sie aktiv sein. |
| `<sessionname>` | Gibt den Namen der Sitzung an, die die Nachricht empfangen soll. Wenn Sie keinen Benutzer oder eine Sitzung angeben, wird mit diesem Befehl eine Fehlermeldung angezeigt. Wenn eine Sitzung angegeben wird, muss Sie aktiv sein. |
| `<sessionID>` | Gibt die numerische ID der Sitzung an, deren Benutzer eine Nachricht erhalten soll. |
| `@<filename>` | Identifiziert eine Datei, die eine Liste von Benutzernamen, Sitzungs Namen und Sitzungs-IDs enthält, die Sie empfangen möchten. |
| * | Sendet die Nachricht an alle Benutzernamen im System. |
| /server:`<servername>` | Gibt den Remotedesktop-Sitzungshost Server an, dessen Sitzung oder Benutzer die Nachricht empfangen soll. Wenn nicht angegeben, verwendet **/Server** den Server, auf dem Sie zurzeit angemeldet sind. |
| /Time`<seconds>` | Gibt die Zeitspanne an, zu der die gesendete Nachricht auf dem Bildschirm des Benutzers angezeigt wird. Wenn das Zeitlimit erreicht ist, wird die Meldung nicht mehr angezeigt. Wenn kein Zeit Limit festgelegt ist, verbleibt die Nachricht auf dem Bildschirm des Benutzers, bis der Benutzer die Meldung sieht und auf **OK**klickt. |
| /v | Zeigt Informationen zu den Aktionen an, die ausgeführt werden. |
| /w | Wartet auf eine Bestätigung des Benutzers, dass die Nachricht empfangen wurde. Verwenden Sie diesen Parameter mit `/time:<*seconds*>` , um eine mögliche lange Verzögerung zu vermeiden, wenn der Benutzer nicht sofort antwortet. Die Verwendung dieses Parameters mit **/v** ist ebenfalls hilfreich. |
| `<message>` | Gibt den Text der Nachricht an, die Sie senden möchten. Wenn keine Meldung angegeben ist, werden Sie aufgefordert, eine Meldung einzugeben. Um eine Nachricht zu senden, die in einer Datei enthalten ist, geben Sie das Symbol kleiner als (<) gefolgt vom Dateinamen ein. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Um eine Nachricht mit dem Namen zu senden, sehen *wir uns heute* für alle Sitzungen für *User1*den folgenden Typ an:

```
msg User1 Let's meet at 1PM today
```

Um dieselbe Nachricht an Session *modeM02*zu senden, geben Sie Folgendes ein:

```
msg modem02 Let's meet at 1PM today
```

Geben Sie Folgendes ein, um die Nachricht an alle Sitzungen zu senden, die in der Datei *userlist*enthalten sind:

```
msg @userlist Let's meet at 1PM today
```

Geben Sie Folgendes ein, um die Nachricht an alle angemeldeten Benutzer zu senden:

```
msg * Let's meet at 1PM today
```

Geben Sie Folgendes ein, um die Nachricht mit einem Timeout der Bestätigung (z. b. 10 Sekunden) an alle Benutzer zu senden:

```
msg * /time:10 Let's meet at 1PM today
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
