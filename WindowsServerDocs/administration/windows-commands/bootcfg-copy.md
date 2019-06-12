---
title: bootcfg copy
description: Windows-Befehle Thema **Bootcfg Kopie** -erstellt eine Kopie eines vorhandenen Starteintrags, die Sie hinzufügen können, das Befehlszeilenoptionen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a236c2a-8675-444d-b695-9cbc9aff643b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b76ecfe953d1a462e311fdaaeba35e8f962165c4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434863"
---
# <a name="bootcfg-copy"></a>bootcfg copy

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Erstellt eine Kopie eines vorhandenen Starteintrags, zu dem Sie Befehlszeilenoptionen hinzufügen können.

## <a name="syntax"></a>Syntax
```
bootcfg /copy [/s <computer> [/u <Domain>\<User> /p <Password>]] [/d <Description>] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>Parameter

|      Parameter       |                                                                                             Beschreibung                                                                                             |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                         Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer.                                          |
| /u <Domain>\\<User>  | Führt den Befehl mit den Berechtigungen des Benutzers gemäß <User>oder <Domain> \\ <User>. Der Standardwert ist die Berechtigungen von der aktuell angemeldete Benutzer auf dem Computer, die der Befehl ausgegeben wird. |
|    /p <Password>     |                                                        Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.                                                        |
|   /d <Description>   |                                                                    Gibt die Beschreibung für den neuen Betriebssystem-Eintrag.                                                                    |
| / ID <OSEntryLineNum> |         Gibt die Zeilennummer der Betriebssystem-Eintrag im Abschnitt [Betriebssysteme] die zu kopierende Datei "Boot.ini" an. Die erste Zeile nach der [Betriebssysteme] Header im Abschnitt ist 1.         |
|          /?          |                                                                                Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                 |

## <a name="BKMK_examples"></a>Beispiele für
Die folgenden Beispiele zeigen Informationen zur Verwendung der **Bootcfg startmenübeschreibung** Befehl aus, um Starteintrag 1 kopieren, und geben "\ABC Server\\" als Beschreibung:
```
bootcfg /copy /d "\ABC Server\" /id 1
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
