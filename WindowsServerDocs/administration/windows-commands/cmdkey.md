---
title: cmdkey
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: dc2b12cb53eef930d05c1e291de5574a8ba94306
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379307"
---
# <a name="cmdkey"></a>cmdkey

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dient zum Erstellen, Auflisten und Löschen gespeicherter Benutzernamen, Kennwörter oder Anmeldeinformationen.

## <a name="syntax"></a>Syntax
```
cmdkey [{/add:<TargetName>|/generic:<TargetName>}] {/smartcard|/user:<UserName> [/pass:<Password>]} [/delete{:<TargetName>|/ras}] /list:<TargetName>
```
## <a name="parameters"></a>Parameter

|             Parameter             |                                                                                    Beschreibung                                                                                     |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         /Add: <TargetName>          | Fügt der Liste einen Benutzernamen und ein Kennwort hinzu.<br /><br />Erfordert den-Parameter <TargetName>, mit dem der Computer-oder Domänen Name identifiziert wird, dem dieser Eintrag zugeordnet wird. |
|       /generisch: <TargetName>        |   Fügt der Liste generische Anmelde Informationen hinzu.<br /><br />Erfordert den-Parameter <TargetName>, mit dem der Computer-oder Domänen Name identifiziert wird, dem dieser Eintrag zugeordnet wird.    |
|             /smartcard             |                                                                    Ruft die Anmelde Informationen von einer Smartcard ab.                                                                     |
|          /User: <UserName>          |                                 Gibt den Namen des Benutzers oder des Kontos an, der mit diesem Eintrag gespeichert werden soll. Wenn der *Benutzername* nicht angegeben wird, wird er angefordert.                                  |
|          /Pass: <Password>          |                                       Gibt das Kennwort an, das mit diesem Eintrag gespeichert werden soll. Wenn kein *Kennwort* angegeben wird, wird es angefordert.                                        |
| /DELETE{: <TargetName> &#124; /RAS} |  Löscht einen Benutzernamen und ein Kennwort aus der Liste. Wenn *TargetName* angegeben ist, wird dieser Eintrag gelöscht. Wenn/RAS angegeben wird, wird der gespeicherte Remote Zugriffs Eintrag gelöscht.   |
|         /List: <TargetName>         |                  Zeigt die Liste der gespeicherten Benutzernamen und Anmelde Informationen an. Wenn *TargetName* nicht angegeben wird, werden alle gespeicherten Benutzernamen und Anmelde Informationen aufgelistet.                   |
|                 /?                 |                                                                        Zeigt die Hilfe an der Eingabeaufforderung an.                                                                        |

## <a name="remarks"></a>Hinweise
- Wenn auf dem System mehr als eine Smartcard gefunden wird, wenn die Befehlszeilenoption/Smartcard verwendet wird, werden von **cmdkey** Informationen zu allen verfügbaren Smartcards angezeigt, und der Benutzer wird aufgefordert, die zu verwendende Option anzugeben.
- Kenn Wörter werden nicht angezeigt, nachdem Sie gespeichert wurden.
  ## <a name="BKMK_examples"></a>Beispiele
  Geben Sie Folgendes ein, um eine Liste aller gespeicherten Benutzernamen und Anmelde Informationen anzuzeigen:
  ```
  cmdkey /list
  ```
  Geben Sie Folgendes ein, um einen Benutzernamen und ein Kennwort für den Benutzer Mikedan zum Zugreifen auf den Computer Server01 mit dem Kennwort "Kleo"
  ```
  cmdkey /add:server01 /user:mikedan /pass:Kleo
  ```
  Geben Sie Folgendes ein, um einen Benutzernamen und ein Kennwort für den Benutzer Mikedan für den Zugriff auf den Computer Server01 und die Aufforderung zur Eingabe des Kennworts einzugeben
  ```
  cmdkey /add:server01 /user:mikedan
  ```
  Geben Sie Folgendes ein, um die Anmelde Informationen zu löschen, die der Remote Zugriff gespeichert hat:
  ```
  cmdkey /delete /ras
  ```
  Um die für Server01 gespeicherten Anmelde Informationen zu löschen, geben Sie Folgendes ein:
  ```
  cmdkey /delete:Server01
  ```
  ## <a name="additional-references"></a>Weitere Verweise
  [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
