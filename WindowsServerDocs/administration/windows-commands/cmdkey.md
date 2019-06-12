---
title: cmdkey
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5fcd68ee-a14a-4b71-9300-c3f5c5d31e8e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5c06a04fa6473bc30c3b354f049a55775d2308a0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434314"
---
# <a name="cmdkey"></a>cmdkey

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Dient zum Erstellen, Auflisten und Löschen gespeicherter Benutzernamen, Kennwörter oder Anmeldeinformationen.

## <a name="syntax"></a>Syntax
```
cmdkey [{/add:<TargetName>|/generic:<TargetName>}] {/smartcard|/user:<UserName> [/pass:<Password>]} [/delete{:<TargetName>|/ras}] /list:<TargetName>
```
## <a name="parameters"></a>Parameter

|             Parameter             |                                                                                    Beschreibung                                                                                     |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         / hinzufügen:<TargetName>          | Fügt einen Benutzernamen und ein Kennwort zur Liste hinzu.<br /><br />Muss der Parameter der <TargetName> identifiziert den Computer oder eine Domäne-Namen, der diesem Eintrag zugeordnet wird. |
|       / generisch:<TargetName>        |   generische Anmeldeinformationen und der Liste hinzugefügt.<br /><br />Muss der Parameter der <TargetName> identifiziert den Computer oder eine Domäne-Namen, der diesem Eintrag zugeordnet wird.    |
|             /smartcard             |                                                                    Ruft die Anmeldeinformationen von einer Smartcard ab.                                                                     |
|          / User:<UserName>          |                                 Gibt an, die Benutzer- oder Kontonamen, um mit diesem Eintrag zu speichern. Wenn *Benutzername* ist nicht angegeben wird, es wird angefordert werden.                                  |
|          /Pass:<Password>          |                                       Gibt das Kennwort ein, um mit diesem Eintrag zu speichern. Wenn *Kennwort* ist nicht angegeben wird, es wird angefordert werden.                                        |
| /delete{:<TargetName> &#124; /ras} |  Löscht einen Benutzernamen und Kennwort aus der Liste an. Wenn *TargetName* angegeben ist, dass Eintrag gelöscht werden. Wenn/RAS angegeben wird, werden die gespeicherten RAS-Eintrag gelöscht werden.   |
|         / List:<TargetName>         |                  Zeigt die Liste der gespeicherten Benutzernamen und Anmeldeinformationen. Wenn *TargetName* ist nicht angegeben wird, alle gespeicherten Benutzernamen und Anmeldeinformationen werden aufgelistet.                   |
|                 /?                 |                                                                        Zeigt die Hilfe an der Eingabeaufforderung an.                                                                        |

## <a name="remarks"></a>Hinweise
- Wenn mehr als eine Smartcard auf dem System gefunden wird, wenn die Befehlszeilenoption "/ Smartcard" verwendet wird, **Cmdkey** Informationen zu allen verfügbaren Smartcards angezeigt, und klicken Sie dann die Benutzer aufgefordert, welche angeben.
- Kennwörter werden nicht angezeigt werden, sobald diese gespeichert sind.
  ## <a name="BKMK_examples"></a>Beispiele für
  Zum Anzeigen einer Liste aller Benutzernamen und Anmeldeinformationen, die gespeichert werden, geben Sie Folgendes ein:
  ```
  cmdkey /list
  ```
  Um einen Benutzernamen und das Kennwort für den Benutzer Mikedan Access-Computer "SERVER01" mit dem Kennwort Kleo hinzuzufügen, geben Sie Folgendes ein:
  ```
  cmdkey /add:server01 /user:mikedan /pass:Kleo
  ```
  Zum Hinzufügen eines Benutzernamens und Kennworts für Benutzer Mikedan Zugriff auf Computer "SERVER01" und Aufforderung zur Kennworteingabe, wenn "SERVER01" zugegriffen wird, geben Sie Folgendes ein:
  ```
  cmdkey /add:server01 /user:mikedan
  ```
  Um die Anmeldeinformationen zu löschen, die Remotezugriff gespeichert wurde, geben Sie Folgendes ein:
  ```
  cmdkey /delete /ras
  ```
  Um die Anmeldeinformationen zu löschen, die für "SERVER01" gespeichert ist, geben Sie Folgendes ein:
  ```
  cmdkey /delete:Server01
  ```
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
