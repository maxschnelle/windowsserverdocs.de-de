---
title: mountvol
description: Referenz Artikel für den Befehl "mountvol", der einen Volumebereitstellungspunkt erstellt, löscht oder auflistet.
ms.topic: reference
ms.assetid: fea8ad4d-f04a-4aaa-a3e5-75931e867b39
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4da7562bd50072dc91538bd08b5462222857830d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640138"
---
# <a name="mountvol"></a>mountvol

Erstellt, löscht oder listet einen volumeeinstellungspunkt auf. Sie können auch Volumes verknüpfen, ohne einen Laufwerk Buchstaben zu erfordern.

## <a name="syntax"></a>Syntax

```
mountvol [<drive>:]<path volumename>
mountvol [<drive>:]<path> /d
mountvol [<drive>:]<path> /l
mountvol [<drive>:]<path> /p
mountvol /r
mountvol [/n|/e]
mountvol <drive>: /s
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `[<drive>:]<path>` | Gibt das vorhandene NTFS-Verzeichnis an, in dem sich der Einstellungspunkt befinden soll. |
| `<volumename>` | Gibt den Volumenamen an, der das Ziel des Bereitstellungs Punkts ist. Der Volumename verwendet die folgende Syntax, wobei *GUID* eine Globally Unique Identifier ist: `\\?\volume\{GUID}\` . Die Klammern `{ }` sind erforderlich. |
| /d | Entfernt den volumeeinstellungspunkt aus dem angegebenen Ordner. |
| /l | Listet den Namen des bereitgestellten Volumes für den angegebenen Ordner auf. |
| /p | Der Volumebereitstellungspunkt wird aus dem angegebenen Verzeichnis entfernt, die Bereitstellung des Basis Volumes wird aufgehoben, und das Basis Volume wird offline geschaltet. Wenn das Volume von anderen Prozessen verwendet wird, schließt **mountvol** alle geöffneten Handles, bevor das Volume getrennt wird. |
| /r | Entfernt Volumes für das Volumebereitstellungspunkt und die Registrierungs Einstellungen für Volumes, die sich nicht mehr im System befinden, sodass Sie nicht automatisch bereitgestellt werden und ihre früheren Volumebereitstellungspunkte beim Hinzufügen wieder zum System erhalten. |
| /n | Deaktiviert die automatische Einbindung neuer Basisvolumes. Neue Volumes werden nicht automatisch bereitgestellt, wenn Sie dem System hinzugefügt werden. |
| /e | Aktiviert die automatische Einbindung neuer Basisvolumes erneut. |
| /s | Stellt die EFI-Systempartition auf dem angegebenen Laufwerk bereit. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Hinweise

- Wenn Sie die Bereitstellung des Volumes aufheben, während Sie den **/p** -Parameter verwenden, wird in der Volumeliste angezeigt, dass das Volume erst bereitgestellt wird, wenn ein volumeeinstellungspunkt

- Wenn das Volume über mehrere Einfügepunkte verfügt, verwenden Sie **/d** , um die zusätzlichen Einfügepunkte vor der Verwendung von **/p**zu entfernen. Sie können das Basisvolume erneut einbinden, indem Sie einen Volumebereitstellungspunkt zuweisen.

- Wenn Sie den volumespeicherplatz erweitern müssen, ohne eine Festplatte neu zu formatieren oder zu ersetzen, können Sie einen Einfügungs Pfad einem anderen Volume hinzufügen. Der Vorteil der Verwendung eines Volumes mit mehreren einstellungenpfaden besteht darin, dass Sie mit einem einzelnen Laufwerk Buchstaben (z. b.) auf alle lokalen Volumes zugreifen können `C:` . Sie müssen sich nicht merken, welches Volume welchem Laufwerk Buchstaben entspricht – obwohl Sie trotzdem lokale Volumes einbinden und Ihnen Laufwerk Buchstaben zuweisen können.

## <a name="examples"></a>Beispiele

Geben Sie zum Erstellen eines Einfügepunkts Folgendes ein:

```
mountvol \sysmount \\?\volume\{2eca078d-5cbc-43d3-aff8-7e8511f60d0e}\
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
