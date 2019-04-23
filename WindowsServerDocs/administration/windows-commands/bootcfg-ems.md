---
title: bootcfg ems
description: Windows-Befehle Thema **Bootcfg Ems** -ermöglicht es dem Benutzer hinzufügen oder ändern die Einstellungen für die Umleitung der Emergency Management Services-Konsole auf einem Remotecomputer befindet.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 97f0126fdfa4d800692a044d33e3de0f0d4c6cdb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861641"
---
# <a name="bootcfg-ems"></a>bootcfg ems

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ermöglicht es dem Benutzer hinzufügen oder ändern die Einstellungen für die Umleitung der Emergency Management Services-Konsole mit einem Remotecomputer aus. Durch Aktivieren der Emergency Management Services können Sie Hinzufügen einer "Redirect = Portnummer" Zeile zum Abschnitt [Bootloader] der Datei "Boot.ini" und eine Redirect-Option, um die Zeile mit dem angegebenen Betriebssystem aus. Die Emergency Management Services-Feature ist nur auf Servern aktiviert.

## <a name="syntax"></a>Syntax
```
bootcfg /ems {ON | OFF | edit} [/s <computer> [/u <Domain>\<User> /p <Password>]] [/port {COM1 | COM2 | COM3 | COM4 | BIOSSET}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|{ON &#124; OFF&#124; edit}|Gibt den Wert für die Emergency Management Services-Umleitung.<br /><br />**ON** -ermöglicht die remote-Ausgabe für den angegebenen <OSEntryLineNum>. Fügt eine Redirect-Option in den angegebenen <OSEntryLineNum> und eine Umleitung = com<X> auf den Abschnitt [Bootloader] festlegen. Der Wert von com<X> wird festgelegt, indem die **/a-Station** Parameter.<br /><br />**OFF** -Ausgabe mit einem Remotecomputer deaktiviert. Entfernt die Redirect-Option aus der angegebenen <OSEntryLineNum> und den umleitungs-= com<X> aus dem Abschnitt [Bootloader] festlegen.<br /><br />**Bearbeiten Sie** -können Sie Änderungen an den Porteinstellungen durch Ändern der umleitungs = com<X> im Abschnitt [Bootloader] festlegen. Der Wert von com<X> wird auf dem angegebenen Wert zurückgesetzt, die **/a-Station** Parameter.|
|/s <computer>|Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer.|
|/u <Domain>\\<User>|Führt den Befehl mit den Berechtigungen des Benutzers gemäß <User> oder <Domain> \\ <User>. Der Standardwert ist die Berechtigungen von der aktuell angemeldete Benutzer auf dem Computer, die der Befehl ausgegeben wird.|
|/p <Password>|Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.|
|/port {COM1 &#124; COM2 &#124; COM3 &#124; COM4 &#124; BIOSSET}|Gibt den COM-Port für die Umleitung verwendet werden. **BIOSSET** leitet Emergency Management Services zum Abrufen der BIOS-Einstellungen, um zu bestimmen, welcher Port für die Umleitung verwendet werden soll. Verwenden Sie nicht die **/a-Station** -Parameters, wenn die Remoteverwaltung der Ausgabe wird deaktiviert.|
|/baud {9600 &#124; 19200 &#124; 38400&#124; 57600 &#124; 115200}|Gibt an, die Baudrate für die Umleitung verwendet werden. Verwenden Sie nicht die **/Baud** -Parameters, wenn die Remoteverwaltung der Ausgabe wird deaktiviert.|
|/ ID <OSEntryLineNum>|Gibt die Zeilennummer der Betriebssystem-Eintrag, die die Emergency Management Services-Option im Abschnitt [Betriebssysteme] der Datei "Boot.ini" hinzugefügt wird. Die erste Zeile nach der [Betriebssysteme] Header im Abschnitt ist 1. Dieser Parameter ist erforderlich, wenn die Emergency Management Services-Wert, um festgelegt ist **ON** oder **OFF**.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="BKMK_examples"></a>Beispiele für
Die folgenden Beispiele zeigen Informationen zur Verwendung der **Bootcfg/EMS** Befehl:
```
bootcfg /ems on /port com1 /baud 19200 /id 2 
bootcfg /ems on /port biosset /id 3 
bootcfg /s srvmain /ems off /id 2 
bootcfg /ems edit /port com2 /baud 115200 
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /ems off /id 2
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilensyntax](command-line-syntax-key.md)
