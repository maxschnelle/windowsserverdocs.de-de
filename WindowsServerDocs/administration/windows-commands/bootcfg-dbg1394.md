---
title: bootcfg dbg1394
description: Windows-Befehle Thema **Bootcfg dbg1394** -Debugport 1394 konfiguriert, für einen bestimmten Betriebssystemeintrag
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35724697-90dd-4dbe-85b0-337fbd369dcc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b36d22cea5b7b0c0e1768736d6c80c67b3c733f9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857651"
---
# <a name="bootcfg-dbg1394"></a>bootcfg dbg1394

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Konfiguriert die 1394 Port für einen bestimmten Betriebssystemeintrag Debuggen.

## <a name="syntax"></a>Syntax
```
bootcfg /dbg1394 {ON | OFF}[/s <computer> [/u <Domain>\<User> /p <Password>]] [/ch <Channel>] /id <OSEntryLineNum>
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|{ON &#124; OFF}|Gibt den Wert für das Debuggen von 1394 Port.<br /><br />-   **ON** -ermöglicht Unterstützung für Remotedebuggen durch die Option/dbg1394 mit dem angegebenen <OSEntryLineNum>.<br />-   **OFF** -deaktiviert Unterstützung für Remotedebuggen, indem die Option/dbg1394 aus dem angegebenen <OSEntryLineNum>.|
|/s <computer>|Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer.|
|/u <Domain>\\<User>|Führt den Befehl mit den Berechtigungen des Benutzers gemäß <User> oder <Domain> \\ <User>. Der Standardwert ist die Berechtigungen von der aktuell angemeldete Benutzer auf dem Computer, die der Befehl ausgegeben wird.|
|/p <Password>|Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.|
|/ CH Kanal|Gibt an, der Kanal für das Debuggen verwenden. Gültige Werte sind ganze Zahlen zwischen 1 und 64. Verwenden Sie nicht die **/ch** <Channel> -Parameters, wenn Port 1394-debugging deaktiviert wird.|
|/ ID <OSEntryLineNum>|Gibt die Zeilennummer der Betriebssystem-Eintrag im Abschnitt [Betriebssysteme] der Datei "Boot.ini", die die Optionen Debuggen 1394 hinzugefügt werden. Die erste Zeile nach der [Betriebssysteme] Header im Abschnitt ist 1.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="BKMK_examples"></a>Beispiele für
Die folgenden Beispiele zeigen Informationen zur Verwendung der **Bootcfg/dbg1394**Befehl:
```
bootcfg /dbg1394 /id 2 
bootcfg /dbg1394 on /ch 1 /id 3 
bootcfg /dbg1394 edit /ch 8 /id 2 
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /dbg1394 off /id 2
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilensyntax](command-line-syntax-key.md)
