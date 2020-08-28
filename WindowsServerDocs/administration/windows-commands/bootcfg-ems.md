---
title: bootcfg ems
description: Referenz Artikel zum Befehl "bootcfg EMS", der es dem Benutzer ermöglicht, die Einstellungen für die Umleitung der Konsole der Notfall Verwaltungsdienste zu einem Remote Computer hinzuzufügen oder zu ändern.
ms.topic: reference
ms.assetid: 57abdc50-c64a-45f1-8470-3f8c3a51f743
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da374cc5b901be72c8ef3fed2a16d7d56c5d53fe
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89034458"
---
# <a name="bootcfg-ems"></a>bootcfg ems

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht es dem Benutzer, die Einstellungen für die Umleitung der Notfall Verwaltungsdienste-Konsole einem Remote Computer hinzuzufügen oder zu ändern. Wenn Sie die Notfall Verwaltungsdienste aktivieren, wird dem `redirect=Port#` Abschnitt [Boot Loader] der Boot.ini Datei eine Zeile hinzugefügt, zusammen mit der Option/Redirect für die angegebene Betriebssystem-Eingabezeile. Die Notfall Verwaltungsdienste-Funktion ist nur auf-Servern aktiviert.

## <a name="syntax"></a>Syntax

```
bootcfg /ems {on | off | edit}[/s <computer> [/u <domain>\<user> /p <password>]] [/port {COM1 | COM2 | COM3 | COM4 | BIOSSET}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <osentrylinenum>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `{on | off | edit}` | Gibt den Wert für die Umleitung der Notfall Verwaltungsdienste an, einschließlich:<ul><li>**auf.** Aktiviert die Remote Ausgabe für die angegebene `<osentrylinenum>` . Fügt dem angegebenen außerdem eine/Redirect-Option <osentrylinenum> und eine `redirect=com<X>` Einstellung zum [Boot Loader]-Abschnitt hinzu. Der Wert von `com<X>` wird durch den **/Port** -Parameter festgelegt.</li><li>**abgeschrieben.** Deaktiviert die Ausgabe auf einem Remote Computer. Entfernt auch die Option/Redirect für die angegebene <osentrylinenum> und die `redirect=com<X>` Einstellung aus dem Abschnitt [Boot Loader].</li><li>**Bearbeiten.** Ermöglicht Änderungen an den Port Einstellungen durch Ändern der `redirect=com<X>` Einstellung im Abschnitt [Boot Loader]. Der Wert von `com<X>` wird durch den **/Port** -Parameter festgelegt.</li></ul> |
| `/s <computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| `/u <domain>\<user>`  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der von oder angegeben wird `<user>` `<domain>\<user>` . Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
| `/p <password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| `/port {COM1 | COM2 | COM3 | COM4 | BIOSSET}` |  Gibt den COM-Port an, der für die Umleitung verwendet werden soll. Der BIOSSET-Parameter leitet Notfall Verwaltungsdienste zum Ermitteln der BIOS-Einstellungen ein, um zu bestimmen, welcher Port für die Umleitung verwendet werden soll. Verwenden Sie diesen Parameter nicht, wenn die Remote verwaltete Ausgabe deaktiviert ist. |
| `/baud {9600 | 19200 | 38400 | 57600 | 115200}` | Gibt die Baudrate an, die für die Umleitung verwendet werden soll. Verwenden Sie diesen Parameter nicht, wenn die Remote verwaltete Ausgabe deaktiviert ist. |
| `/id <osentrylinenum>` | Gibt die Betriebssystem-Zeilennummer an, der die Option "Notfall Verwaltungsdienste" im Abschnitt "[Betriebssysteme]" der Boot.ini Datei hinzugefügt wird. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1. Dieser Parameter ist erforderlich, wenn der Emergency Management Services-Wert **auf on** oder **Off**festgelegt ist. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

So verwenden Sie den Befehl **bootcfg/EMS** :

```
bootcfg /ems on /port com1 /baud 19200 /id 2
bootcfg /ems on /port biosset /id 3
bootcfg /s srvmain /ems off /id 2
bootcfg /ems edit /port com2 /baud 115200
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /ems off /id 2
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [BOOTCFG-Befehl](bootcfg.md)
