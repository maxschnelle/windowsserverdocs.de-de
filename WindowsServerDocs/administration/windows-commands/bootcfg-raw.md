---
title: bootcfg raw
description: 'Windows-Befehls Thema für **Bootcfg raw** : Fügt dem Betriebssystem Eintrag im Abschnitt **[Betriebssysteme]** der Datei "Boot. ini" die Optionen für das Betriebssystem laden hinzu, die als Zeichenfolge angegeben werden.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3458749-b0a0-460f-a022-3ff199a71f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fb5c052f85f54656c54a9e534f867d287407d2d4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379896"
---
# <a name="bootcfg-raw"></a>bootcfg raw

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt einem Betriebssystem Eintrag im Abschnitt **[Betriebssysteme]** der Datei "Boot. ini" die Optionen für das Betriebssystem laden hinzu, die als Zeichenfolge angegeben sind.

## <a name="syntax"></a>Syntax
```
bootcfg /raw [/s <computer> [/u <Domain>\<User> /p <Password>]] <OSLoadOptionsString> [/id <OSEntryLineNum>] [/a]
```
## <a name="parameters"></a>Parameter

|         Begriff          |                                                                                                            Definition                                                                                                             |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /s <computer>     |                                                        Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                                         |
| /u <Domain> \\ @ no__t-2  |               Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch <User> oder <Domain> @ no__t-2 @ no__t-3 angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird.                |
|     /p <Password>     |                                                                       Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                                       |
| <OSLoadOptionsString> | Gibt die Betriebssystem-Lade Optionen an, die dem Betriebssystem Eintrag hinzugefügt werden sollen. Mit diesen Lade Optionen werden alle vorhandenen, dem Betriebssystem Eintrag zugeordneten Lade Optionen ersetzt. Es wird keine Überprüfung <OSLoadOptions> ausgeführt. |
| /ID <OSEntryLineNum>  |                       Gibt die Betriebssystem-Eintrags Zeilennummer im Abschnitt [Betriebssysteme] der zu aktualisierenden Datei "Boot. ini" an. Die erste Zeile nach der Abschnitts Kopfzeile [Betriebssystem] ist 1.                       |
|          /a           |                                                       Gibt an, dass die hinzugefügten Betriebssystem Optionen an alle vorhandenen Betriebssystem Optionen angefügt werden sollen.                                                        |
|          /?           |                                                                                               Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                |

##### <a name="remarks"></a>Hinweise
- **Bootcfg raw** wird zum Hinzufügen von Text am Ende eines Betriebssystem Eintrags verwendet, wobei alle vorhandenen Betriebssystem-Eintrags Optionen überschrieben werden. Dieser Text sollte gültige Lade Optionen für das Betriebssystem enthalten, wie z. b. **/Debug**, **/fastdetect**, **/NoDebug**, **/Baudrate**, **/crashdebug**und **/SOS**. Der folgende Befehl fügt z. b. " **/Debug/fastdetect**" am Ende des ersten Betriebssystem Eintrags hinzu und ersetzt alle vorherigen Betriebssystem-Eintrags Optionen:
  ```
  bootcfg /raw "/debug /fastdetect" /id 1
  ```
  ## <a name="BKMK_examples"></a>Beispiele
  In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **Bootcfg/raw** verwenden können:
  ```
  bootcfg /raw "/debug /sos" /id 2
  bootcfg /raw /s srvmain /u maindom\hiropln /p p@ssW23 "/crashdebug " /id 2
  ```
  #### <a name="additional-references"></a>Weitere Verweise
  [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
