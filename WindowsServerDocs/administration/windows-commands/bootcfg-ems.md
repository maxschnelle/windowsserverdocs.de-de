---
title: bootcfg ems
description: 'Windows-Befehle-Thema für **bootcfg EMS** : ermöglicht dem Benutzer das Hinzufügen oder Ändern der Einstellungen für die Umleitung der Konsole der Notfall Verwaltungsdienste zu einem Remote Computer.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57abdc50-c64a-45f1-8470-3f8c3a51f743
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c0e761f3796121cc71be88d23e25371369a3ee90
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379963"
---
# <a name="bootcfg-ems"></a>bootcfg ems

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht es dem Benutzer, die Einstellungen für die Umleitung der Notfall Verwaltungsdienste-Konsole einem Remote Computer hinzuzufügen oder zu ändern. Wenn Sie die Notfall Verwaltungsdienste aktivieren, fügen Sie dem Abschnitt [Boot Loader] der Datei "Boot. ini" und der Option/Redirect für die angegebene Betriebssystem-Eingabezeile die Zeile "Redirect = Port #" hinzu. Die Notfall Verwaltungsdienste-Funktion ist nur auf-Servern aktiviert.

## <a name="syntax"></a>Syntax
```
bootcfg /ems {ON | OFF | edit} [/s <computer> [/u <Domain>\<User> /p <Password>]] [/port {COM1 | COM2 | COM3 | COM4 | BIOSSET}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>Parameter

|                            Parameter                             |                                                                                                                                                                                                                                                                                                                                                              Beschreibung                                                                                                                                                                                                                                                                                                                                                              |
|------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                    {ON &#124; from&#124; Edit}                    | Gibt den Wert für die Umleitung der Notfall Verwaltungsdienste an.<br /><br />**On** : aktiviert die Remote Ausgabe für die angegebene <OSEntryLineNum>. Fügt dem angegebenen <OSEntryLineNum> eine/Redirect-Option und die Einstellung Redirect = com<X> im Abschnitt [Boot Loader] hinzu. Der Wert von com-<X> wird durch den **/Port** -Parameter festgelegt.<br /><br />**Off** : deaktiviert die Ausgabe auf einem Remote Computer. entfernt die/Redirect-Option aus dem angegebenen <OSEntryLineNum> und die Einstellung Redirect = com<X> aus dem Abschnitt [Boot Loader].<br /><br />**Bearbeiten** : ermöglicht Änderungen an den Port Einstellungen durch Ändern der Einstellung Redirect = com<X> im Abschnitt [Boot Loader]. Der Wert der com-<X> wird auf den Wert zurückgesetzt, der durch den **/Port** -Parameter angegeben wird. |
|                          /s <computer>                           |                                                                                                                                                                                                                                                                                                          Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                                                                                                                                                                                                                                                                                           |
|                       /u <Domain>\\<User>                        |                                                                                                                                                                                                                                                                 Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch <User> oder <Domain>\\<User>angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird.                                                                                                                                                                                                                                                                  |
|                          /p <Password>                           |                                                                                                                                                                                                                                                                                                                         Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                                                                                                                                                                                                                                                                                         |
| /Port {COM1 &#124; COM2 &#124; COM3 &#124; COM4 &#124; BIOSSET}  |                                                                                                                                                                                                                              Gibt den COM-Port an, der für die Umleitung verwendet werden soll. **BIOSSET** leitet Notverwaltungsdienste an, um die BIOS-Einstellungen zu erhalten, um zu bestimmen, welcher Port für die Umleitung verwendet werden soll. Verwenden Sie den **/Port** -Parameter nicht, wenn die Remote verwaltete Ausgabe deaktiviert wird.                                                                                                                                                                                                                              |
| /Baud {9600 &#124; 19200 &#124; 38400&#124; 57600 &#124; 115200} |                                                                                                                                                                                                                                                                                               Gibt die Baudrate an, die für die Umleitung verwendet werden soll. Verwenden Sie den **/Baud** -Parameter nicht, wenn die Remote verwaltete Ausgabe deaktiviert wird.                                                                                                                                                                                                                                                                                               |
|                       /ID <OSEntryLineNum>                       |                                                                                                                                                                                              Gibt die Betriebssystem-Zeilennummer an, der die Option "Notfall Verwaltungsdienste" im Abschnitt "[Betriebssysteme]" der Datei "Boot. ini" hinzugefügt wird. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1. Dieser Parameter ist erforderlich, wenn der Emergency Management Services-Wert **auf on** oder **Off**festgelegt ist.                                                                                                                                                                                              |
|                                /?                                |                                                                                                                                                                                                                                                                                                                                                 Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                                                                                                                                                                  |

## <a name="BKMK_examples"></a>Beispiele
In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **bootcfg/EMS** verwenden können:
```
bootcfg /ems on /port com1 /baud 19200 /id 2 
bootcfg /ems on /port biosset /id 3 
bootcfg /s srvmain /ems off /id 2 
bootcfg /ems edit /port com2 /baud 115200 
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /ems off /id 2
```
#### <a name="additional-references"></a>Weitere Verweise
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
