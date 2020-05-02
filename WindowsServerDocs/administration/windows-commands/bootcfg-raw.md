---
title: bootcfg raw
description: Referenz Thema für den BOOTCFG Raw-Befehl, mit dem Betriebssystem-Lade Optionen, die als Zeichenfolge angegeben werden, einem Betriebssystem Eintrag im Abschnitt "Betriebssystem" der Datei "Boot. ini" hinzugefügt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e3458749-b0a0-460f-a022-3ff199a71f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b9127b278a41bb8f1f36f7b45c544bf09f5c4ff7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82708957"
---
# <a name="bootcfg-raw"></a>bootcfg raw

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt einem Betriebssystem Eintrag im Abschnitt [Betriebssysteme] der Datei "Boot. ini" die Optionen für das Betriebssystem laden hinzu, die als Zeichenfolge angegeben sind. Dieser Befehl überschreibt alle vorhandenen Optionen für den Betriebssystem Eintrag.

## <a name="syntax"></a>Syntax

```
bootcfg /raw [/s <computer> [/u <domain>\<user> /p <password>]] <osloadoptionsstring> [/id <osentrylinenum>] [/a]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `/s <computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer. |
| `/u <domain>\<user>`  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der `<user>` von `<domain>\<user>`oder angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
| `/p <password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| `<osloadoptionsstring>` | Gibt die Betriebssystem-Lade Optionen an, die dem Betriebssystem Eintrag hinzugefügt werden sollen. Diese Lade Optionen ersetzen alle vorhandenen Lade Optionen, die dem Betriebssystem Eintrag zugeordnet sind. Es gibt keine Validierung für den `<osloadoptions>` -Parameter.
| `/id <osentrylinenum>` | Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der Datei Boot. ini an, der die Betriebssystem-Lade Optionen hinzugefügt werden. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1. |
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [BOOTCFG-Befehl](bootcfg.md)
