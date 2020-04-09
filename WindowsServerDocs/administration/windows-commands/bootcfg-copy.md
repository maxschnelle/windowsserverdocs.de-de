---
title: bootcfg copy
description: Windows-Befehls Thema für bootcfg Copy, das eine Kopie eines vorhandenen Start Eintrags erstellt, dem Sie Befehlszeilenoptionen hinzufügen können.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2a236c2a-8675-444d-b695-9cbc9aff643b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5194418a07aece4f15a84c3eccbc044431a865b9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848683"
---
# <a name="bootcfg-copy"></a>bootcfg copy

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt eine Kopie eines vorhandenen Start Eintrags, dem Sie Befehlszeilenoptionen hinzufügen können.

## <a name="syntax"></a>Syntax
```
bootcfg /copy [/s <computer> [/u <Domain>\<User> /p <Password>]] [/d <Description>] [/id <OSEntryLineNum>]
```
### <a name="parameters"></a>Parameter

|      Parameter       |                                                                                             Beschreibung                                                                                             |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                         Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                          |
| /u <Domain>\\<User>  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch <User>oder <Domain>\\<User>angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
|    /p <Password>     |                                                        Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                        |
|   /d <Description>   |                                                                    Gibt die Beschreibung für den neuen Betriebssystem Eintrag an.                                                                    |
| /ID <OSEntryLineNum> |         Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der zu kopierenden Datei Boot. ini an. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1.         |
|          /?          |                                                                                Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                 |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
In den folgenden Beispielen wird veranschaulicht, wie Sie den Befehl **bootcfg/Copy** zum Kopieren des Start Eintrags 1 und zum Eingeben von \abc Server\\ als Beschreibung verwenden können:
```
bootcfg /copy /d \ABC Server\ /id 1
```
## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
