---
title: schtasks löschen
description: Referenz Artikel für den Befehl "schtasks delete", mit dem eine geplante Aufgabe aus dem Zeitplan gelöscht wird.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 09/16/2020
ms.openlocfilehash: a5b090ac9520aeae5e603e0c47c0c225b8bd0eff
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91390765"
---
# <a name="schtasks-delete"></a>schtasks löschen

Löscht eine geplante Aufgabe aus dem Zeitplan. Mit diesem Befehl wird das Programm, das vom Task ausgeführt wird, nicht gelöscht, oder ein ausgeführten Programm wird unterbrochen

## <a name="syntax"></a>Syntax

```
schtasks /delete /tn {<taskname> | *} [/f] [/s <computer> [/u [<domain>\]<user> [/p <password>]]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /TN `{<taskname> | *}` | Identifiziert den zu löschenden Task. Wenn Sie verwenden `*` , werden mit diesem Befehl alle Aufgaben gelöscht, die für den Computer geplant sind, und nicht nur die vom aktuellen Benutzer geplanten Tasks. |
| /f | Unterdrückt die Bestätigungsmeldung. Der Task wird ohne Warnung gelöscht. |
| /s `<computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (mit oder ohne umgekehrte Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| /u `[<domain>]` | Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos aus. Standardmäßig wird der Befehl mit den Berechtigungen des aktuellen Benutzers auf dem lokalen Computer ausgeführt. Das angegebene Benutzerkonto muss ein Mitglied der Gruppe "Administratoren" auf dem Remote Computer sein. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden. |
| /p `<password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. Wenn Sie den **/u** -Parameter ohne den **/p** -Parameter oder das Password-Argument verwenden, werden Sie von schtasks aufgefordert, ein Kennwort einzugeben. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

, Um den Task " *Mail starten* " aus dem Zeitplan eines Remote Computers zu löschen.

```
schtasks /delete /tn Start Mail /s Svr16
```

Dieser Befehl verwendet den **/s** -Parameter, um den Remote Computer zu identifizieren.

So löschen Sie alle Aufgaben aus dem Zeitplan des lokalen Computers, einschließlich der von anderen Benutzern geplanten Tasks.

```
schtasks /delete /tn * /f
```

Dieser Befehl verwendet den **/TN &#42;** -Parameter, um alle Aufgaben auf dem Computer darzustellen, und den **/f** -Parameter, um die Bestätigungsmeldung zu unterdrücken.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [schtasks-Änderungs Befehl](schtasks-change.md)

- [Befehl "schtasks create"](schtasks-create.md)

- [schtasks-Befehl "Ende"](schtasks-end.md)

- [schtasks-Abfragebefehl](schtasks-query.md)

- [Befehl "Schtasks ausführen"](schtasks-run.md)
