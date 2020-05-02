---
title: cmdkey
description: Referenz Thema zum cmdkey-Befehl, mit dem gespeicherte Benutzernamen und Kenn Wörter oder Anmelde Informationen erstellt, aufgelistet und gelöscht werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5fcd68ee-a14a-4b71-9300-c3f5c5d31e8e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4005707785101fcc1fb0030ffe895668bd65f730
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82712156"
---
# <a name="cmdkey"></a>cmdkey

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dient zum Erstellen, Auflisten und Löschen gespeicherter Benutzernamen, Kennwörter oder Anmeldeinformationen.

## <a name="syntax"></a>Syntax

```
cmdkey [{/add:<targetname>|/generic:<targetname>}] {/smartcard | /user:<username> [/pass:<password>]} [/delete{:<targetname> | /ras}] /list:<targetname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| ---------- | ----------- |
| /Add`<targetname>` | Fügt der Liste einen Benutzernamen und ein Kennwort hinzu.<p>Erfordert den-Parameter `<targetname>` , der den Computer-oder Domänen Namen identifiziert, dem dieser Eintrag zugeordnet wird. |
| /generisch`<targetname>` | Fügt der Liste generische Anmelde Informationen hinzu.<p>Erfordert den-Parameter `<targetname>` , der den Computer-oder Domänen Namen identifiziert, dem dieser Eintrag zugeordnet wird. |
| /smartcard | Ruft die Anmelde Informationen von einer Smartcard ab. Wenn auf dem System mehr als eine Smartcard gefunden wird, wenn diese Option verwendet wird, werden von **cmdkey** Informationen zu allen verfügbaren Smartcards angezeigt, und der Benutzer wird aufgefordert, das zu verwendende Zertifikat anzugeben. |
| /User`<username>` | Gibt den Namen des Benutzers oder des Kontos an, der mit diesem Eintrag gespeichert werden soll. Wenn `<username>` nicht angegeben wird, wird Sie angefordert. |
|Tage`<password>` | Gibt das Kennwort an, das mit diesem Eintrag gespeichert werden soll. Wenn `<password>` nicht angegeben wird, wird Sie angefordert. Kenn Wörter werden nicht angezeigt, nachdem Sie gespeichert wurden. |
| /delete{:`<targetname>` | shof | Löscht einen Benutzernamen und ein Kennwort aus der Liste. Wenn `<targetname>` angegeben wird, wird dieser Eintrag gelöscht. Wenn `/ras` angegeben wird, wird der gespeicherte Remote Zugriffs Eintrag gelöscht. |
| /List`<targetname>` | Zeigt die Liste der gespeicherten Benutzernamen und Anmelde Informationen an. Wenn `<targetname>` nicht angegeben ist, werden alle gespeicherten Benutzernamen und Anmelde Informationen aufgelistet. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Liste aller gespeicherten Benutzernamen und Anmelde Informationen anzuzeigen:

```
cmdkey /list
```

Geben Sie Folgendes ein, um einen Benutzernamen und ein Kennwort für den Benutzer *Mikedan* zum Zugreifen auf den Computer *Server01* mit dem Kennwort " *Kleo*"

```
cmdkey /add:server01 /user:mikedan /pass:Kleo
```

Geben Sie Folgendes ein, um einen Benutzernamen und ein Kennwort für den Benutzer *Mikedan* für den Zugriff auf den Computer *Server01* und die Aufforderung zur Eingabe des Kennworts einzugeben

```
cmdkey /add:server01 /user:mikedan
```

Geben Sie Folgendes ein, um Anmelde Informationen zu löschen, die durch Remote Zugriff gespeichert werden:

```
cmdkey /delete /ras
```

Geben Sie Folgendes ein, um die für *Server01*gespeicherten Anmelde Informationen zu löschen:

```
cmdkey /delete:server01
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
