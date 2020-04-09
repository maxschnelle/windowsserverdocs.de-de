---
title: bootcfg debug
description: Windows-Befehls Thema für bootcfg Debug, mit dem die Debugeinstellungen für einen angegebenen Betriebssystem Eintrag hinzugefügt oder geändert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 28afa5fb-a236-46e2-b1a4-a3c43a49c437
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de225e1bd0f8406a0b28e5af28fd29bceb8e713c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848633"
---
# <a name="bootcfg-debug"></a>bootcfg debug

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt die Debugeinstellungen für einen angegebenen Betriebssystem Eintrag hinzu oder ändert Sie.

## <a name="syntax"></a>Syntax
```
bootcfg /debug {ON | OFF | edit}[/s <computer> [/u <Domain>\<User> /p <Password>]] [/port {COM1 | COM2 | COM3 | COM4}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <OSEntryLineNum>]
```
### <a name="parameters"></a>Parameter

|                           Parameter                           |                                                                                                                                                                                                                    Beschreibung                                                                                                                                                                                                                    |
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                  {ON &#124; from&#124; Edit}                   | Gibt den Wert für das Debuggen an.<p>**On** : aktiviert die Unterstützung für Remote Debugging durch Hinzufügen der/Debug-Option zum angegebenen <OSEntryLineNum>.<p>**Off** : deaktiviert die Unterstützung für Remote Debugging, indem die/Debug-Option aus dem angegebenen <OSEntryLineNum>entfernt wird.<p>**Bearbeiten** : ermöglicht Änderungen an den Einstellungen für Port und Baudrate durch Ändern der Werte, die mit der Option/Debug für die angegebene <OSEntryLineNum>verknüpft sind. |
|                         /s <computer>                         |                                                                                                                                                                Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                                                                                                                                                 |
|                      /u <Domain>\\<User>                      |                                                                                                                       Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch <User> oder <Domain>\\<User>angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird.                                                                                                                        |
|                         /p <Password>                         |                                                                                                                                                                               Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                                                                                                                                               |
|       /Port {COM1 &#124; COM2 &#124; COM3 &#124; COM4}        |                                                                                                                                                                Gibt den COM-Port an, der für das Debugging verwendet werden soll. Verwenden Sie den **/Port** -Parameter nicht, wenn das Debuggen deaktiviert wird.                                                                                                                                                                |
| /Baud {9600&#124; 19200&#124; 38400&#124; 57600&#124; 115200} |                                                                                                                                                               Gibt die Baudrate an, die für das Debugging verwendet werden soll. Verwenden Sie den **/Baud** -Parameter nicht, wenn das Debuggen deaktiviert wird.                                                                                                                                                                |
|                     /ID <OSEntryLineNum>                      |                                                                                                               Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der Datei "Boot. ini" an, der die Debugoptionen hinzugefügt werden. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1.                                                                                                                |
|                              /?                               |                                                                                                                                                                                                       Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                        |

##### <a name="remarks"></a>Hinweise
- Wenn 1394-Port-Debugging erforderlich ist, verwenden Sie [bootcfg dbg1394](bootcfg-dbg1394.md).
  ## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
  In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **bootcfg/Debug**verwenden können:
  ```
  bootcfg /debug on /port com1 /id 2 
  bootcfg /debug edit /port com2 /baud 19200 /id 2 
  bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /debug off /id 2
  ```
  ## <a name="additional-references"></a>Weitere Verweise
  - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
