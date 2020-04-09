---
title: bootcfg default
description: Windows-Befehls Thema für BOOTCFG Default, das den Betriebssystem Eintrag angibt, der als Standard festgelegt werden soll.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e21824d7-8278-41d7-a2c5-ce09803d513a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 517cf444a5517b3d612266b57b428e47ac60d4ef
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848564"
---
# <a name="bootcfg-default"></a>bootcfg default

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Gibt den Betriebssystem Eintrag an, der als Standard festgelegt werden soll.

## <a name="syntax"></a>Syntax
```
bootcfg /default [/s <computer> [/u <Domain>\<User> /p <Password>]] [/id <OSEntryLineNum>]
```
### <a name="parameters"></a>Parameter

|      Parameter       |                                                                                             Beschreibung                                                                                              |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                          Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                          |
| /u <Domain>\\<User>  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch <User> oder <Domain>\\<User>angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
|    /p <Password>     |                                                        Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                         |
| /ID <OSEntryLineNum> | Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der Datei "Boot. ini" an, die als Standard festgelegt werden soll. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1.  |
|          /?          |                                                                                 Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                 |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **bootcfg/Standard:** verwenden können:
```
bootcfg /default /id 2
bootcfg /default /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```
## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
