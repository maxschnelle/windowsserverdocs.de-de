---
title: bootcfg delete
description: Windows-Befehls Artikel zum Löschen von Bootcfg, mit dem ein Betriebssystem Eintrag im Abschnitt "Betriebssysteme" der Datei "Boot. ini" gelöscht wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 71382e29-9b39-41c8-9c23-cf0ff829440a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 01ec7a4dde1e22982f2cf0fa30245c33e09cc0ff
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848543"
---
# <a name="bootcfg-delete"></a>bootcfg delete

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht einen Betriebssystem Eintrag im Abschnitt [Betriebssysteme] der Datei "Boot. ini".

## <a name="syntax"></a>Syntax
```
bootcfg /delete [/s <computer> [/u <Domain>\<User> /p <Password>]] [/id <OSEntryLineNum>]
```
### <a name="parameters"></a>Parameter

|         Begriff         |                                                                                             Definition                                                                                              |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                         Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                          |
| /u <Domain>\\<User>  | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch <User>oder <Domain>\\<User>angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
|    /p <Password>     |                                                        Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                        |
| /ID <OSEntryLineNum> |        Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der zu löschenden Datei "Boot. ini" an. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1.        |
|          /?          |                                                                                Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                 |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **bootcfg/DELETE**verwenden können:
```
bootcfg /delete /id 1
bootcfg /delete /s srvmain /u maindom\hiropln /p p@ssW23 /id 3
```
## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
