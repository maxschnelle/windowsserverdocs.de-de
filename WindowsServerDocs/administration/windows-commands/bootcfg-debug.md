---
title: bootcfg debug
description: Referenz Thema für den bootcfg-Debugbefehl, mit dem die Debugeinstellungen für einen angegebenen Betriebssystem Eintrag hinzugefügt oder geändert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 28afa5fb-a236-46e2-b1a4-a3c43a49c437
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c8059aaefd1b23b3e74f4c27ba96e322c44b5cb6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82709709"
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
| `{on | off | edit}` | Gibt den Wert für das Port Debuggen an, einschließlich:<ul><li>**auf.** Aktiviert die Unterstützung für Remote Debugging durch Hinzufügen der/Debug `<osentrylinenum>`-Option zum angegebenen.</li><li>**abgeschrieben.** Deaktiviert die Unterstützung für Remote Debugging, indem die/Debug-Option <osentrylinenum>aus dem angegebenen entfernt wird.</li><li>**Bearbeiten.** Ermöglicht Änderungen an den Einstellungen für Port und Baudrate durch Ändern der Werte, die mit der/Debug <osentrylinenum>-Option für das angegebene verknüpft sind.</li></ul> |
| `/s <computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer. |
| `/u <domain>\<user>`  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der `<user>` von `<domain>\<user>`oder angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
| `/p <password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| `/port {COM1 | COM2 | COM3 | COM4}` |  Gibt den COM-Port an, der für das Debugging verwendet werden soll. Verwenden Sie diesen Parameter nicht, wenn das Debuggen deaktiviert ist. |
| `/baud {9600 | 19200 | 38400 | 57600 | 115200}` | Gibt die Baudrate an, die für das Debugging verwendet werden soll. Verwenden Sie diesen Parameter nicht, wenn das Debuggen deaktiviert ist. |
| `/id <osentrylinenum>` | Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der Datei Boot. ini an, der die Betriebssystem-Lade Optionen hinzugefügt werden. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

So verwenden Sie den Befehl **bootcfg/Debug** :

```
bootcfg /debug on /port com1 /id 2
bootcfg /debug edit /port com2 /baud 19200 /id 2
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /debug off /id 2
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [BOOTCFG-Befehl](bootcfg.md)
