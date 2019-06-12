---
title: bootcfg query
description: Windows-Befehle Thema **Bootcfg Abfrage** -Abfragen und zeigt [Bootloader] und [Betriebssysteme] Abschnitt Einträge aus der Datei "Boot.ini".
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4cacfd1-10a6-4a11-b0c5-f8abde72bfc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e79acc100a9ec9955f2692a3c6ee812d0310b687
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434729"
---
# <a name="bootcfg-query"></a>bootcfg query

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Fragt ab und zeigt das [Startladeprogramm] und [Betriebssysteme] Abschnitt Einträge aus der Datei "Boot.ini".

## <a name="syntax"></a>Syntax
```
bootcfg /query [/s <computer> [/u <Domain>\<User> /p <Password>]]
```
## <a name="parameters"></a>Parameter

|        Begriff         |                                                                                             Definition                                                                                              |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>    |                                         Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer.                                          |
| /u <Domain>\\<User> | Führt den Befehl mit den Berechtigungen des Benutzers gemäß <User>oder <Domain> \\ <User>. Der Standardwert ist die Berechtigungen von der aktuell angemeldete Benutzer auf dem Computer, die der Befehl ausgegeben wird. |
|    /p <Password>    |                                                        Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.                                                        |
|         /?          |                                                                                Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                 |

##### <a name="remarks"></a>Hinweise
- Folgendes ist ein Beispiel für **Bootcfg/query** Ausgabe:
  ```
  Boot Loader Settings
  ----------
  timeout: 30
  default: multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
  Boot Entries
  ------
  Boot entry ID:   1
  Friendly Name:   ""
  path:            multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
  OS Load Options: /fastdetect /debug /debugport=com1:
  ```
- Die Boot-Loader-Einstellungen-Teil der **Bootcfg Abfrage** Ausgabe zeigt jeden Eintrag im Abschnitt "[Bootloader]" der Datei "Boot.ini".
- Die Starteinträge Teil der **Bootcfg Abfrage** Ausgabe zeigt die folgende Details für die einzelnen Betriebssystem-Einträge im Abschnitt [Betriebssysteme] der Datei "Boot.ini": Starteintrags-ID, Anzeigename, Pfad und Optionen für Betriebssystem laden.
  ## <a name="BKMK_examples"></a>Beispiele für
  Die folgenden Beispiele zeigen Informationen zur Verwendung der **Bootcfg/query** Befehl:
  ```
  bootcfg /query
  bootcfg /query /s srvmain /u maindom\hiropln /p p@ssW23
  bootcfg /query /u hiropln /p p@ssW23
  ```
  #### <a name="additional-references"></a>Zusätzliche Referenzen
  [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
