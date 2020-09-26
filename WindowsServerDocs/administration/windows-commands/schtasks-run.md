---
title: schtasks ausführen
description: Referenz Artikel für den Befehl "Schtasks ausführen", der
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 09/16/2020
ms.openlocfilehash: 9304e41c21899ce49bd6d4d4409ae3b47d3746aa
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91390741"
---
# <a name="schtasks-run"></a>schtasks ausführen

Startet eine geplante Aufgabe sofort. Der Ausführungs Vorgang ignoriert den Zeitplan, verwendet jedoch den Programmdatei Speicherort, das Benutzerkonto und das Kennwort, die in der Aufgabe gespeichert sind, um den Task sofort auszuführen. Das Ausführen einer Aufgabe wirkt sich nicht auf den Task Zeitplan aus und ändert nicht die nächste Ausführungszeit, die für den Task geplant ist.

## <a name="syntax"></a>Syntax

```
schtasks /run /tn <taskname> [/s <computer> [/u [<domain>\]<user> [/p <password>]]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /TN `<taskname>` | Gibt die zu startende Aufgabe an. Dieser Parameter ist erforderlich. |
| /s `<computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (mit oder ohne umgekehrte Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| /u `[<domain>]` | Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos aus. Standardmäßig wird der Befehl mit den Berechtigungen des aktuellen Benutzers auf dem lokalen Computer ausgeführt. Das angegebene Benutzerkonto muss ein Mitglied der Gruppe "Administratoren" auf dem Remote Computer sein. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden. |
| /p `<password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. Wenn Sie den **/u** -Parameter ohne den **/p** -Parameter oder das Password-Argument verwenden, werden Sie von schtasks aufgefordert, ein Kennwort einzugeben. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Verwenden Sie diesen Vorgang, um Ihre Aufgaben zu testen. Wenn eine Aufgabe nicht ausgeführt wird, überprüfen Sie das Taskplaner-Dienst Transaktionsprotokoll `<Systemroot>\SchedLgU.txt` auf Fehler.

- Um einen Task Remote auszuführen, muss die Aufgabe auf dem Remote Computer geplant werden. Wenn Sie den Task ausführen, wird er nur auf dem Remote Computer ausgeführt. Um zu überprüfen, ob eine Aufgabe auf einem Remote Computer ausgeführt wird, verwenden Sie den Task-Manager oder das Taskplaner-Dienst Transaktionsprotokoll `<Systemroot>\SchedLgU.txt` .

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den *Sicherheits Skript* Task zu starten:

```
schtasks /run /tn Security Script
```

Geben Sie Folgendes ein, um den *Aktualisierungs* Task auf einem Remote Computer (SVR01) zu starten:

```
schtasks /run /tn Update /s Svr01
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [schtasks-Änderungs Befehl](schtasks-change.md)

- [Befehl "schtasks create"](schtasks-create.md)

- [Befehl "Schtasks löschen"](schtasks-delete.md)

- [schtasks-Befehl "Ende"](schtasks-end.md)

- [schtasks-Abfragebefehl](schtasks-query.md)