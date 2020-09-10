---
title: bootcfg debug
description: Referenz Artikel für den bootcfg-Debugbefehl, mit dem die Debugeinstellungen für einen angegebenen Betriebssystem Eintrag hinzugefügt oder geändert werden.
ms.topic: reference
ms.assetid: 28afa5fb-a236-46e2-b1a4-a3c43a49c437
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 385bdd6ebadb4cb3eb9b48e1b920325db996dc38
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630248"
---
# <a name="bootcfg-debug"></a>bootcfg debug

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt die Debugeinstellungen für einen angegebenen Betriebssystem Eintrag hinzu oder ändert Sie.

>[!NOTE]
> Wenn Sie versuchen, Port 1394 zu debuggen, verwenden Sie stattdessen den [bootcfg dbg1394](bootcfg-dbg1394.md) -Befehl.

## <a name="syntax"></a>Syntax

```
bootcfg /debug {on | off | edit}[/s <computer> [/u <domain>\<user> /p <password>]] [/port {COM1 | COM2 | COM3 | COM4}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <osentrylinenum>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `{on | off | edit}` | Gibt den Wert für das Port Debuggen an, einschließlich:<ul><li>**auf.** Aktiviert die Unterstützung für Remote Debugging durch Hinzufügen der/Debug-Option zum angegebenen `<osentrylinenum>` .</li><li>**abgeschrieben.** Deaktiviert die Unterstützung für Remote Debugging, indem die/Debug-Option aus dem angegebenen entfernt wird <osentrylinenum> .</li><li>**Bearbeiten.** Ermöglicht Änderungen an den Einstellungen für Port und Baudrate durch Ändern der Werte, die mit der/Debug-Option für das angegebene verknüpft sind <osentrylinenum> .</li></ul> |
| `/s <computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| `/u <domain>\<user>`  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der von oder angegeben wird `<user>` `<domain>\<user>` . Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
| `/p <password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| `/port {COM1 | COM2 | COM3 | COM4}` |  Gibt den COM-Port an, der für das Debugging verwendet werden soll. Verwenden Sie diesen Parameter nicht, wenn das Debuggen deaktiviert ist. |
| `/baud {9600 | 19200 | 38400 | 57600 | 115200}` | Gibt die Baudrate an, die für das Debugging verwendet werden soll. Verwenden Sie diesen Parameter nicht, wenn das Debuggen deaktiviert ist. |
| `/id <osentrylinenum>` | Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der Boot.ini Datei an, der die Betriebssystem-Lade Optionen hinzugefügt werden. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

So verwenden Sie den Befehl **bootcfg/Debug** :

```
bootcfg /debug on /port com1 /id 2
bootcfg /debug edit /port com2 /baud 19200 /id 2
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /debug off /id 2
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [BOOTCFG-Befehl](bootcfg.md)
