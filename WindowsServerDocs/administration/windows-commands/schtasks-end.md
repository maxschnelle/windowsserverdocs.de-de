---
title: schtasks beenden
description: Referenz Artikel für den Befehl "Schtasks beenden", der nur die Instanzen eines Programms stoppt, das von einer geplanten Aufgabe gestartet wurde.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 09/16/2020
ms.openlocfilehash: 7075c8689a39c7bc9eba917298678977916e29fa
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91390749"
---
# <a name="schtasks-end"></a>schtasks beenden

Beendet nur die Instanzen eines Programms, das von einer geplanten Aufgabe gestartet wurde. Um andere Prozesse zu beenden, müssen Sie den [taskkill](taskkill.md) -Befehl verwenden.

## <a name="syntax"></a>Syntax

```
schtasks /end /tn <taskname> [/s <computer> [/u [<domain>\]<user> [/p <password>]]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /TN `<taskname>` | Identifiziert den Task, der das Programm gestartet hat. Dieser Parameter ist erforderlich. |
| /s `<computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (mit oder ohne umgekehrte Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| /u `[<domain>]` | Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos aus. Standardmäßig wird der Befehl mit den Berechtigungen des aktuellen Benutzers auf dem lokalen Computer ausgeführt. Das angegebene Benutzerkonto muss ein Mitglied der Gruppe "Administratoren" auf dem Remote Computer sein. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden. |
| /p `<password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. Wenn Sie den **/u** -Parameter ohne den **/p** -Parameter oder das Password-Argument verwenden, werden Sie von schtasks aufgefordert, ein Kennwort einzugeben. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Instanz von Notepad.exe zu starten *, die von der Aufgabe* "Editor" gestartet wurde:

```
schtasks /end /tn "My Notepad"
```

Geben Sie Folgendes ein, um die Internet Explorer-Instanz zu unterbinden, die von der *internetton* -Aufgabe auf dem Remote Computer gestartet wurde, *Svr01*:

```
schtasks /end /tn InternetOn /s Svr01
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [schtasks-Änderungs Befehl](schtasks-change.md)

- [Befehl "schtasks create"](schtasks-create.md)

- [Befehl "Schtasks löschen"](schtasks-delete.md)

- [schtasks-Abfragebefehl](schtasks-query.md)

- [Befehl "Schtasks ausführen"](schtasks-run.md)