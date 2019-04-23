---
title: bootcfg rmsw
description: Windows-Befehle Thema **Bootcfg Rmsw** - operating System Ladeoptionen für einen bestimmten Betriebssystemeintrag entfernt.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fd7e4248-880e-4e2b-929e-87f8d44b9a63
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 65a8ba452911eb1b46a748d4e9d639ed102421b6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878821"
---
# <a name="bootcfg-rmsw"></a>bootcfg rmsw

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Optionen zum Laden von Betriebssystem für einen angegebenen Betriebssystem-Eintrag wird entfernt.

## <a name="syntax"></a>Syntax
```
bootcfg /rmsw [/s <computer> [/u <Domain>\<User> [/p <Password>]]] [/mm] [/bv] [/so] [/ng] /id <OSEntryLineNum>
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/s <computer>|Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer.|
|/u <Domain>\\<User>|Führt den Befehl mit den Berechtigungen des Benutzers gemäß <User> oder <Domain> \\ <User>. Der Standardwert ist die Berechtigungen von der aktuell angemeldete Benutzer auf dem Computer, die der Befehl ausgegeben wird.|
|/p <Password>|Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.|
|/mm|Entfernt die Option/maxmem und seine zugeordnete maximale Speicherwert aus der angegebenen <OSEntryLineNum>. Die/maxmem-Option gibt die Höchstmenge an Arbeitsspeicher, die das Betriebssystem verwenden können.|
|/bv|Entfernt die Option/basevideo aus dem angegebenen <OSEntryLineNum>. Die Option/basevideo weist das Betriebssystem für den installierten Grafikkartentreiber VGA-Modus zu verwenden.|
|/so|Entfernt die Option/SOS aus dem angegebenen <OSEntryLineNum>. Die Option/SOS weist das Betriebssystem auf den Namen der Gerätetreiber anzuzeigen, während diese geladen werden.|
|/ng|Entfernt die Option/noguiboot aus dem angegebenen <OSEntryLineNum>. Die Option/noguiboot deaktiviert die Statusanzeige, die vor dem STRG + ALT + del-anmeldeaufforderung angezeigt wird.|
|/ ID <OSEntryLineNum>|Gibt die Zeilennummer der Betriebssystem-Eintrag im Abschnitt [Betriebssysteme] der Datei "Boot.ini", die aus der der Betriebssystem-Ladeoptionen entfernt werden. Die erste Zeile nach der [Betriebssysteme] Header im Abschnitt ist 1.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="BKMK_examples"></a>Beispiele für
Die folgenden Beispiele zeigen Informationen zur Verwendung der **Bootcfg/Rmsw**Befehl:
```
bootcfg /rmsw /mm 64 /id 2 
bootcfg /rmsw /so /id 3 
bootcfg /rmsw /so /ng /s srvmain /u hiropln /id 2 
bootcfg /rmsw /ng /id 2 
bootcfg /rmsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2       
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilensyntax](command-line-syntax-key.md)
