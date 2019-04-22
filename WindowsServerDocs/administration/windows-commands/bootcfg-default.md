---
title: bootcfg default
description: Windows-Befehle Thema **Bootcfg Standard** -gibt an, den Betriebssystemeintrag als Standard festgelegt werden soll.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e21824d7-8278-41d7-a2c5-ce09803d513a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aa19c787182584e941850bb38e6c4e8006790fca
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823151"
---
# <a name="bootcfg-default"></a>bootcfg default

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Gibt den Betriebssystemeintrag als Standard festgelegt werden soll.

## <a name="syntax"></a>Syntax
```
bootcfg /default [/s <computer> [/u <Domain>\<User> /p <Password>]] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/s <computer>|Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer.|
|/u <Domain>\\<User>|Führt den Befehl mit den Berechtigungen des Benutzers gemäß <User> oder <Domain> \\ <User>. Der Standardwert ist die Berechtigungen von der aktuell angemeldete Benutzer auf dem Computer, die der Befehl ausgegeben wird.|
|/p <Password>|Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.|
|/ ID <OSEntryLineNum>|Gibt die Zeilennummer der Betriebssystem-Eintrag im Abschnitt [Betriebssysteme] der Datei "Boot.ini" als Standard festgelegt werden soll. Die erste Zeile nach der [Betriebssysteme] Header im Abschnitt ist 1.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="BKMK_examples"></a>Beispiele für
Die folgenden Beispiele zeigen Informationen zur Verwendung der **Bootcfg/Standard**Befehl:
```
bootcfg /default /id 2
bootcfg /default /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilensyntax](command-line-syntax-key.md)
