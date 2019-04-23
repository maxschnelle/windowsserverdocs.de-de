---
title: bootcfg raw
description: Windows-Befehle Thema **Bootcfg unformatierten** -Fügt Betriebssystem Ladeoptionen angegeben werden, als eine Zeichenfolge, die ein Betriebssystem-Eintrag in der **[Betriebssysteme]** -Abschnitt der Datei "Boot.ini".
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3458749-b0a0-460f-a022-3ff199a71f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a68c59eb3a7018ba8a7c0c96b594f0ed68d914b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841601"
---
# <a name="bootcfg-raw"></a>bootcfg raw

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Fügt der Betriebssystem-Ladeoptionen angegeben werden, als eine Zeichenfolge, die ein Betriebssystem-Eintrag in der **[Betriebssysteme]** -Abschnitt der Datei "Boot.ini".

## <a name="syntax"></a>Syntax
```
bootcfg /raw [/s <computer> [/u <Domain>\<User> /p <Password>]] <OSLoadOptionsString> [/id <OSEntryLineNum>] [/a]
```
## <a name="parameters"></a>Parameter
|Begriff|Definition|
|----|-------|
|/s <computer>|Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer.|
|/u <Domain> \\<User>|Führt den Befehl mit den Berechtigungen des Benutzers gemäß <User> oder <Domain> \\ <User>. Der Standardwert ist die Berechtigungen von der aktuell angemeldete Benutzer auf dem Computer, die der Befehl ausgegeben wird.|
|/p <Password>|Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.|
|<OSLoadOptionsString>|Gibt die Betriebssystem-Load-Optionen den Betriebssystemeintrag hinzu. Diese Optionen laden ersetzt alle vorhandenen Ladeoptionen den Betriebssystemeintrag zugeordnet. Keine Überprüfung des <OSLoadOptions> erfolgt.|
|/ ID <OSEntryLineNum>|Gibt die Zeilennummer der Betriebssystem-Eintrag im Abschnitt [Betriebssysteme] der Datei "Boot.ini" zu aktualisieren. Die erste Zeile nach der [Betriebssysteme] Header im Abschnitt ist 1.|
|/a|Gibt an, dass die Betriebssystemoptionen hinzugefügt wird an alle vorhandenen Betriebssystemoptionen angefügt werden sollen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
##### <a name="remarks"></a>Hinweise
-   **unformatierte BOOTCFG** wird verwendet, um den Text am Ende einen Betriebssystemeintrag, überschreiben alle vorhandenen Optionen hinzufügen. Dieser Text muss gültige OS Ladeoptionen enthalten, z. B. **/debug**, **/fastdetect**, **/nodebug**, **/Baudrate**, **/ Crashdebug**, und **/SOS**. Der folgende Befehl fügt beispielsweise "**/debug/fastdetect**" am Ende der erste Eintrag des Betriebssystems, ersetzen Sie alle vorherigen Optionen:
    ```
    bootcfg /raw "/debug /fastdetect" /id 1
    ```
## <a name="BKMK_examples"></a>Beispiele für
Die folgenden Beispiele zeigen Informationen zur Verwendung der **Bootcfg / raw** Befehl:
```
bootcfg /raw "/debug /sos" /id 2
bootcfg /raw /s srvmain /u maindom\hiropln /p p@ssW23 "/crashdebug " /id 2
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilensyntax](command-line-syntax-key.md)
