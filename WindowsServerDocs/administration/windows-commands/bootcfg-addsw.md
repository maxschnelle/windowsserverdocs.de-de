---
title: bootcfg addsw
description: Windows-Befehle Thema **Bootcfg Addsw** -Optionen zum Laden von Betriebssystem für einen angegebenen Betriebssystem-Eintrag hinzugefügt.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d8389293-ecd9-42f0-b84b-b9ead4cf52e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 768e9c5bcf8a5d272927d013ff4accf5c3237219
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862871"
---
# <a name="bootcfg-addsw"></a>bootcfg addsw

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Fügt Betriebssystem Ladeoptionen für einen angegebenen Betriebssystem-Eintrag hinzu.

## <a name="syntax"></a>Syntax
```
bootcfg /addsw [/s <computer> [/u <Domain>\<User> /p <Password>]] [/mm <MaximumRAM>] [/bv] [/so] [/ng] /id <OSEntryLineNum>
```
## <a name="parameters"></a>Parameter
|Begriff|Definition|
|----|-------|
|/s <computer>|Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer.|
|/u <Domain>\\<User>|Führt den Befehl mit den Berechtigungen des Benutzers gemäß <User> oder <Domain> \\ <User>. Der Standardwert ist die Berechtigungen von der aktuell angemeldete Benutzer auf dem Computer, die der Befehl ausgegeben wird.|
|/p <Password>|Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.|
|/mm <MaximumRAM>|Gibt die Höchstmenge an Arbeitsspeicher, in Megabyte an, die das Betriebssystem verwenden können. Der Wert muss gleich oder größer als 32 MB sein.|
|/bv|Fügt der **/basevideo** Option aus, um den angegebenen <OSEntryLineNum>, leiten das Betriebssystem für den installierten Grafikkartentreiber VGA-Modus zu verwenden.|
|/so|Fügt der **/SOS** Option aus, um den angegebenen *BSEintragZeilenNr*, leiten das Betriebssystem auf den Namen der Gerätetreiber anzuzeigen, während diese geladen werden.|
|/ng|Fügt der **/noguiboot** Option aus, um den angegebenen <OSEntryLineNum>, deaktivieren die Statusanzeige, die vor dem STRG + ALT + ENTF Anmeldung Eingabeaufforderung angezeigt.|
|/ ID <OSEntryLineNum>|Gibt die Zeilennummer der Betriebssystem-Eintrag im Abschnitt [Betriebssysteme] der Datei "Boot.ini", die Optionen für das Betriebssystem laden hinzugefügt werden. Die erste Zeile nach der [Betriebssysteme] Header im Abschnitt ist 1.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="BKMK_examples"></a>Beispiele für
Die folgenden Beispiele zeigen Informationen zur Verwendung der **Bootcfg/Addsw** Befehl:
```
bootcfg /addsw /mm 64 /id 2 
bootcfg /addsw /so /id 3 
bootcfg /addsw /so /ng /s srvmain /u hiropln /id 2 
bootcfg /addsw /ng /id 2 
bootcfg /addsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilensyntax](command-line-syntax-key.md)
