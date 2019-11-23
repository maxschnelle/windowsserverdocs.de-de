---
title: bootcfg copy
description: Windows-Befehls Thema für **bootcfg Copy** -erstellt eine Kopie eines vorhandenen Start Eintrags, dem Sie Befehlszeilenoptionen hinzufügen können.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 42a408443cbe6722c25780f7c27d70b05da7eb8e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380119"
---
# <a name="bootcfg-copy"></a>bootcfg copy

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt eine Kopie eines vorhandenen Start Eintrags, dem Sie Befehlszeilenoptionen hinzufügen können.

## <a name="syntax"></a>Syntax
```
bootcfg /copy [/s <computer> [/u <Domain>\<User> /p <Password>]] [/d <Description>] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>Parameter

|      Parameter       |                                                                                             Beschreibung                                                                                             |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                         Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                          |
| /u <Domain>\\<User>  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch <User>oder <Domain>\\<User>angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
|    /p <Password>     |                                                        Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                        |
|   /d <Description>   |                                                                    Gibt die Beschreibung für den neuen Betriebssystem Eintrag an.                                                                    |
| /ID <OSEntryLineNum> |         Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der zu kopierenden Datei Boot. ini an. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1.         |
|          /?          |                                                                                Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                 |

## <a name="BKMK_examples"></a>Beispiele
In den folgenden Beispielen wird veranschaulicht, wie Sie den Befehl **bootcfg/Copy** verwenden können, um Boot Entry 1 zu kopieren und "\abc Server\\" als Beschreibung einzugeben:
```
bootcfg /copy /d "\ABC Server\" /id 1
```
#### <a name="additional-references"></a>Weitere Verweise
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
