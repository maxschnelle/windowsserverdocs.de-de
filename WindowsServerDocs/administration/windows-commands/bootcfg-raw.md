---
title: bootcfg raw
description: Referenz Artikel zum Befehl "unformatierte bootcfg", mit dem Betriebssystem-Lade Optionen, die als Zeichenfolge angegeben werden, einem Betriebssystem Eintrag im Abschnitt "Betriebssystem" der Boot.ini Datei hinzugefügt werden.
ms.topic: article
ms.assetid: e3458749-b0a0-460f-a022-3ff199a71f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9cba66ccebeacd21d337e04c97d935bd2c260b24
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880554"
---
# <a name="bootcfg-raw"></a>bootcfg raw

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt einem Betriebssystem Eintrag im Abschnitt [Betriebssysteme] der Boot.ini Datei die als Zeichenfolge angegebenen Betriebssystem-Lade Optionen hinzu. Dieser Befehl überschreibt alle vorhandenen Optionen für den Betriebssystem Eintrag.

## <a name="syntax"></a>Syntax

```
bootcfg /raw [/s <computer> [/u <domain>\<user> /p <password>]] <osloadoptionsstring> [/id <osentrylinenum>] [/a]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `/s <computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| `/u <domain>\<user>`  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der von oder angegeben wird `<user>` `<domain>\<user>` . Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
| `/p <password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| `<osloadoptionsstring>` | Gibt die Betriebssystem-Lade Optionen an, die dem Betriebssystem Eintrag hinzugefügt werden sollen. Diese Lade Optionen ersetzen alle vorhandenen Lade Optionen, die dem Betriebssystem Eintrag zugeordnet sind. Es gibt keine Validierung für den- `<osloadoptions>` Parameter.
| `/id <osentrylinenum>` | Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der Boot.ini Datei an, der die Betriebssystem-Lade Optionen hinzugefügt werden. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1. |
| /a | Gibt an, welche Betriebssystem Optionen an vorhandene Betriebssystem Optionen angefügt werden sollen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Dieser Text sollte gültige Lade Optionen für das Betriebssystem enthalten, wie z. b. **/Debug**, **/fastdetect**, **/NoDebug**, **/Baudrate**, **/crashdebug**und **/SOS**.

Um **/Debug/fastdetect** am Ende des ersten Betriebssystem Eintrags hinzuzufügen, ersetzen Sie alle vorherigen Betriebssystem-Eintrags Optionen:

```
bootcfg /raw /debug /fastdetect /id 1
```

So verwenden Sie den Befehl **Bootcfg/raw** :

```
bootcfg /raw /debug /sos /id 2
bootcfg /raw /s srvmain /u maindom\hiropln /p p@ssW23 /crashdebug  /id 2
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [BOOTCFG-Befehl](bootcfg.md)
