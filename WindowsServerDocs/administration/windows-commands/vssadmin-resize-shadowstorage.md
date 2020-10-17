---
title: vssadmin resize shadowstorage
description: Eine Beschreibung des Befehls vssadmin Größe ShadowStorage, der die maximale Speicherplatz Größe, die für den schattenkopiespeicherspeicher verwendet werden kann, ändert.
ms.topic: reference
author: JasonGerend
ms.author: jgerend
ms.date: 03/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: 704130890d68c271e74a9163ba4ae76dcfb1a516
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156144"
---
# <a name="vssadmin-resize-shadowstorage"></a>vssadmin resize shadowstorage

> Gilt für: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Ändert die maximale Speicherplatz Größe, die für den schattenkopiespeicherspeicher verwendet werden kann.

Die minimale Menge an Speicherplatz, die zum Speichern von Schatten Kopien verwendet werden kann, kann mit dem Registrierungs Wert **MinDiffAreaFileSize** angegeben werden. Weitere Informationen finden Sie unter [MinDiffAreaFileSize](/windows/win32/backup/registry-keys-for-backup-and-restore#mindiffareafilesize).

> [!WARNING]
> Die Größe der Speicher Zuordnung kann dazu führen, dass Schatten Kopien ausgeblendet werden.

## <a name="syntax"></a>Syntax

```
vssadmin resize shadowstorage /for=<ForVolumeSpec> /on=<OnVolumeSpec> [/maxsize=<MaxSizeSpec>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /for =`<ForVolumeSpec>` | Gibt das Volume an, für das die maximale Speicherplatz Größe geändert werden soll. |
| /on =`<OnVolumeSpec>` | Gibt das Speicher Volume an. |
| [/MaxSize = `<MaxSizeSpec>` ] | Gibt die maximale Menge an Speicherplatz an, die zum Speichern von Schatten Kopien verwendet werden kann. Wenn für **/MaxSize**kein Wert angegeben wird, gibt es keine Beschränkung für die Menge des Speicherplatzes, der verwendet werden kann.<p>Der **maxsizespec** -Wert muss 1 MB oder größer sein und muss in einer der folgenden Einheiten ausgedrückt werden: KB, MB, GB, TB, PB oder EB. Wenn keine Einheit angegeben ist, verwendet **maxsizespec** standardmäßig bytes. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Größe der Schatten Kopie von Volume C auf Volume D mit einer maximalen Größe von 900 MB zu ändern:

```
vssadmin resize shadowstorage /For=C: /On=D: /MaxSize=900MB
```

Geben Sie Folgendes ein, um die Größe der Schatten Kopie von Volume C auf Volume D ohne maximale Größe zu ändern:

```
vssadmin resize shadowstorage /For=C: /On=D: /MaxSize=UNBOUNDED
```

Um die Größe der Schatten Kopie von Volume C um 20% zu ändern, geben Sie Folgendes ein:

```
vssadmin resize shadowstorage /For=C: /On=C: /MaxSize=20%
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [vssadmin-Befehl](vssadmin.md)
