---
title: bootcfg debug
description: Windows-Befehle Thema **Bootcfg Debug** – hinzufügt oder ändert die Debugeinstellungen für einen bestimmten Betriebssystemeintrag.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 27768788e7f14445137331523c62151fcf3b6b2d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879021"
---
# <a name="bootcfg-debug"></a>bootcfg debug

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Hinzufügen oder Ändern der Einstellungen zum Debuggen für einen bestimmten Betriebssystemeintrag.

## <a name="syntax"></a>Syntax
```
bootcfg /debug {ON | OFF | edit}[/s <computer> [/u <Domain>\<User> /p <Password>]] [/port {COM1 | COM2 | COM3 | COM4}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|{ON &#124; OFF&#124; edit}|Gibt den Wert für das Debuggen.<br /><br />**ON** -ermöglicht Unterstützung für Remotedebuggen durch die Option "/ Debug" in den angegebenen <OSEntryLineNum>.<br /><br />**OFF** -deaktiviert Unterstützung für Remotedebuggen, indem die Option "/ Debug" aus dem angegebenen <OSEntryLineNum>.<br /><br />**Bearbeiten Sie** -können Sie Änderungen an den Port und der Baudrate Rate-Einstellungen, durch Ändern der Werte, die mit der Option "/ Debug" für den angegebenen verbundene <OSEntryLineNum>.|
|/s <computer>|Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer.|
|/u <Domain>\\<User>|Führt den Befehl mit den Berechtigungen des Benutzers gemäß <User> oder <Domain> \\ <User>. Der Standardwert ist die Berechtigungen von der aktuell angemeldete Benutzer auf dem Computer, die der Befehl ausgegeben wird.|
|/p <Password>|Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.|
|/port {COM1 &#124; COM2 &#124; COM3 &#124; COM4}|Gibt den COM-Port für das Debuggen verwendet werden. Verwenden Sie nicht die **/a-Station** -Parameters, wenn das Debuggen wird deaktiviert.|
|/baud {9600&#124; 19200&#124; 38400&#124; 57600&#124; 115200}|Gibt an, die Baudrate für das Debuggen verwendet werden. Verwenden Sie nicht die **/Baud** -Parameters, wenn das Debuggen wird deaktiviert.|
|/ ID <OSEntryLineNum>|Gibt die Zeilennummer der Betriebssystem-Eintrag im Abschnitt [Betriebssysteme] der Datei "Boot.ini", die die Debugoptionen hinzugefügt werden. Die erste Zeile nach der [Betriebssysteme] Header im Abschnitt ist 1.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
##### <a name="remarks"></a>Hinweise
-   Wenn Port 1394-debugging erforderlich ist, verwenden Sie [Bootcfg dbg1394](bootcfg-dbg1394.md).
## <a name="BKMK_examples"></a>Beispiele für
Die folgenden Beispiele zeigen Informationen zur Verwendung der **Bootcfg "/ Debug"** Befehl:
```
bootcfg /debug on /port com1 /id 2 
bootcfg /debug edit /port com2 /baud 19200 /id 2 
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /debug off /id 2
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilensyntax](command-line-syntax-key.md)
