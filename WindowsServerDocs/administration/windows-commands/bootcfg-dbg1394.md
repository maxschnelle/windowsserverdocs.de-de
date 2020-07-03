---
title: bootcfg dbg1394
description: Referenz Artikel für den Befehl Bootcfg dbg1394, der 1394-Port-Debugging für einen angegebenen Betriebssystem Eintrag konfiguriert
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 35724697-90dd-4dbe-85b0-337fbd369dcc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f1f71edbabbf85c301bec24138a805523975d3f6
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926341"
---
# <a name="bootcfg-dbg1394"></a>bootcfg dbg1394

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konfiguriert 1394-Port Debugging für einen angegebenen Betriebssystem Eintrag.

## <a name="syntax"></a>Syntax

```
bootcfg /dbg1394 {on | off}[/s <computer> [/u <domain>\<user> /p <password>]] [/ch <channel>] /id <osentrylinenum>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `{on | off}` | Gibt den Wert für 1394-Port Debugging an, einschließlich:<ul><li>**auf.** Aktiviert die Unterstützung für Remote Debugging durch Hinzufügen der/dbg1394-Option zum angegebenen `<osentrylinenum>` .</li><li>**abgeschrieben.** Deaktiviert die Unterstützung für Remote Debugging, indem die/dbg1394-Option aus dem angegebenen entfernt wird <osentrylinenum> .</li></ul> |
| `/s <computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| `/u <domain>\<user>`  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der von oder angegeben wird `<user>` `<domain>\<user>` . Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
| `/p <password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| `/ch <channel>` | Gibt den für das Debugging zu verwendenden Kanal an. Gültige Werte sind ganze Zahlen zwischen 1 und 64. Verwenden Sie diesen Parameter nicht, wenn 1394-Port-Debugging deaktiviert ist. |
| `/id <osentrylinenum>` | Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der Boot.ini Datei an, der die Betriebssystem-Lade Optionen hinzugefügt werden. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

So verwenden Sie den Befehl **bootcfg/dbg1394**:

```
bootcfg /dbg1394 /id 2
bootcfg /dbg1394 on /ch 1 /id 3
bootcfg /dbg1394 edit /ch 8 /id 2
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /dbg1394 off /id 2
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [BOOTCFG-Befehl](bootcfg.md)
