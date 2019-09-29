---
title: bootcfg debug
description: 'Windows-Befehls Thema für **bootcfg Debug** : fügt die Debugeinstellungen für einen angegebenen Betriebssystem Eintrag hinzu oder ändert Sie.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28afa5fb-a236-46e2-b1a4-a3c43a49c437
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f6659cf2bfdf83b1b2fe6f6c811365775526768a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380051"
---
# <a name="bootcfg-debug"></a>bootcfg debug

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt die Debugeinstellungen für einen angegebenen Betriebssystem Eintrag hinzu oder ändert Sie.

## <a name="syntax"></a>Syntax
```
bootcfg /debug {ON | OFF | edit}[/s <computer> [/u <Domain>\<User> /p <Password>]] [/port {COM1 | COM2 | COM3 | COM4}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>Parameter

|                           Parameter                           |                                                                                                                                                                                                                    Beschreibung                                                                                                                                                                                                                    |
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                  {ON &#124; from&#124; Edit}                   | Gibt den Wert für das Debuggen an.<br /><br />**On** : aktiviert die Unterstützung für Remote Debugging durch Hinzufügen der/Debug-Option zum angegebenen <OSEntryLineNum>.<br /><br />**Off** : deaktiviert die Unterstützung für Remote Debugging, indem die/Debug-Option aus dem angegebenen <OSEntryLineNum> entfernt wird.<br /><br />**Bearbeiten** : ermöglicht Änderungen an den Einstellungen für Port und Baudrate durch Ändern der Werte, die mit der Option/Debug für die angegebene <OSEntryLineNum> verknüpft sind. |
|                         /s <computer>                         |                                                                                                                                                                Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                                                                                                                                                 |
|                      /u <Domain> @ no__t-1 @ no__t-2                      |                                                                                                                       Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch <User> oder <Domain> @ no__t-2 @ no__t-3 angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird.                                                                                                                        |
|                         /p <Password>                         |                                                                                                                                                                               Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                                                                                                                                               |
|       /Port {COM1 &#124; COM2 &#124; COM3 &#124; COM4}        |                                                                                                                                                                Gibt den COM-Port an, der für das Debugging verwendet werden soll. Verwenden Sie den **/Port** -Parameter nicht, wenn das Debuggen deaktiviert wird.                                                                                                                                                                |
| /Baud {9600&#124; 19200&#124; 38400&#124; 57600&#124; 115200} |                                                                                                                                                               Gibt die Baudrate an, die für das Debugging verwendet werden soll. Verwenden Sie den **/Baud** -Parameter nicht, wenn das Debuggen deaktiviert wird.                                                                                                                                                                |
|                     /ID <OSEntryLineNum>                      |                                                                                                               Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der Datei "Boot. ini" an, der die Debugoptionen hinzugefügt werden. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1.                                                                                                                |
|                              /?                               |                                                                                                                                                                                                       Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                        |

##### <a name="remarks"></a>Hinweise
- Wenn 1394-Port-Debugging erforderlich ist, verwenden Sie [bootcfg dbg1394](bootcfg-dbg1394.md).
  ## <a name="BKMK_examples"></a>Beispiele
  In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **bootcfg/Debug**verwenden können:
  ```
  bootcfg /debug on /port com1 /id 2 
  bootcfg /debug edit /port com2 /baud 19200 /id 2 
  bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /debug off /id 2
  ```
  #### <a name="additional-references"></a>Weitere Verweise
  [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
