---
title: bootcfg delete
description: 'Thema "Windows-Befehle" für **bootcfg DELETE** : Löscht einen Betriebssystem Eintrag im Abschnitt "Betriebssysteme" der Datei "Boot. ini".'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71382e29-9b39-41c8-9c23-cf0ff829440a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d2298c07af32e66a2ffcebb85ec780da762be58
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380008"
---
# <a name="bootcfg-delete"></a>bootcfg delete

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht einen Betriebssystem Eintrag im Abschnitt [Betriebssysteme] der Datei "Boot. ini".

## <a name="syntax"></a>Syntax
```
bootcfg /delete [/s <computer> [/u <Domain>\<User> /p <Password>]] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>Parameter

|         Begriff         |                                                                                             Definition                                                                                              |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                         Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                          |
| /u <Domain>\\<User>  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch <User>oder <Domain>\\<User>angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
|    /p <Password>     |                                                        Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                        |
| /ID <OSEntryLineNum> |        Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der zu löschenden Datei "Boot. ini" an. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1.        |
|          /?          |                                                                                Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                 |

## <a name="BKMK_examples"></a>Beispiele
In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **bootcfg/DELETE**verwenden können:
```
bootcfg /delete /id 1
bootcfg /delete /s srvmain /u maindom\hiropln /p p@ssW23 /id 3
```
#### <a name="additional-references"></a>Weitere Verweise
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
