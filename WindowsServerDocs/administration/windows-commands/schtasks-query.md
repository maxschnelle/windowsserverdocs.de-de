---
title: schtasks-Abfrage
description: Referenz Artikel für den Befehl "Schtasks", der alle Aufgaben auflistet, die für die Ausführung auf dem Computer geplant sind.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 09/16/2020
ms.openlocfilehash: c1bff666f762b21e8dbcf2bff59383d49cab6409
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91390748"
---
# <a name="schtasks-query"></a>schtasks-Abfrage

Listet alle Aufgaben auf, die für die Ausführung auf dem Computer geplant sind.

Syntax

```
schtasks [/query] [/fo {TABLE | LIST | CSV}] [/nh] [/v] [/s <computer> [/u [<domain>\]<user> [/p <password>]]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /Query "aus | Gibt optional den Namen des Vorgangs an. Wenn Sie diese Abfrage ohne Parameter verwenden, wird eine Abfrage durchführen. |
| /FO `<format>` | Gibt das Ausgabeformat an. Gültige Werte sind " *Table*", " *List*" oder " *CSV*". |
| /nh | Entfernt Spaltenüberschriften aus der Tabellen Anzeige. Dieser Parameter ist mit den *Tabellen* -oder *CSV* -Ausgabeformaten gültig. |
| /v | Fügt die erweiterten Eigenschaften der Aufgabe der Anzeige hinzu. Dieser Parameter ist mit den Ausgabeformaten *List* oder *CSV* gültig. |
| /s `<computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (mit oder ohne umgekehrte Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| /u `[<domain>]` | Führt diesen Befehl mit den Berechtigungen des angegebenen Benutzerkontos aus. Standardmäßig wird der Befehl mit den Berechtigungen des aktuellen Benutzers auf dem lokalen Computer ausgeführt. Das angegebene Benutzerkonto muss ein Mitglied der Gruppe "Administratoren" auf dem Remote Computer sein. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden. |
| /p `<password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. Wenn Sie den **/u** -Parameter ohne den **/p** -Parameter oder das Password-Argument verwenden, werden Sie von schtasks aufgefordert, ein Kennwort einzugeben. Die Parameter **/u** und **/p** sind nur gültig, wenn Sie **/s**verwenden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Aufgaben aufzulisten, die für den lokalen Computer geplant sind:

```
schtasks
schtasks /query
```

Diese Befehle führen zu demselben Ergebnis und können austauschbar verwendet werden.

Geben Sie Folgendes ein, um eine detaillierte Anzeige der Aufgaben auf dem lokalen Computer anzufordern:

```
schtasks /query /fo LIST /v
```

Dieser Befehl verwendet den **/v** -Parameter, um eine ausführliche (ausführliche) Anzeige anzufordern, und den **/FO List** -Parameter, um die Anzeige als Liste für das einfache lesen zu formatieren. Mit diesem Befehl können Sie überprüfen, ob eine von Ihnen erstellte Aufgabe das gewünschte Wiederholungsmuster aufweist.

Geben Sie Folgendes ein, um eine Liste der Tasks anzufordern, die für einen Remote Computer geplant sind, und um die Tasks zu einer durch Trennzeichen getrennten Protokolldatei auf dem lokalen Computer hinzuzufügen:

```
schtasks /query /s Reskit16 /fo csv /nh >> \\svr01\data\tasklogs\p0102.csv
```

Sie können dieses Befehls Format verwenden, um Aufgaben zu erfassen und zu verfolgen, die für mehrere Computer geplant sind. Dieser Befehl verwendet den **/s** -Parameter zum Identifizieren des Remote Computers *Reskit16*, den **/FO** -Parameter, um das Format anzugeben, und den **/NH** -Parameter, um die Spaltenüberschriften zu unterdrücken. Das **>>** anfügebsymbol leitet die Ausgabe an das Aufgaben Protokoll weiter, *p0102.csv*auf dem lokalen Computer, *Svr01*. Da der Befehl auf dem Remote Computer ausgeführt wird, muss der Pfad des lokalen Computers voll qualifiziert sein.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [schtasks-Änderungs Befehl](schtasks-change.md)

- [Befehl "schtasks create"](schtasks-create.md)

- [Befehl "Schtasks löschen"](schtasks-delete.md)

- [schtasks-Befehl "Ende"](schtasks-end.md)

- [Befehl "Schtasks ausführen"](schtasks-run.md)