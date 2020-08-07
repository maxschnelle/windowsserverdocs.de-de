---
title: Vssadmin residieren von ShadowStorage
description: Eine Beschreibung des Befehls vssadmin Größe shadowstorage.
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.date: 03/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0b49c85ab628de040cf58d47b4e4c694674ce6e7
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87892335"
---
# <a name="vssadmin-resize-shadowstorage"></a>Vssadmin residieren von ShadowStorage

> Gilt für: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Ändert die maximale Speicherplatz Größe, die für den schattenkopiespeicherspeicher verwendet werden kann.

Die minimale Menge an Speicherplatz, die zum Speichern von Schatten Kopien verwendet werden kann, kann mit dem Registrierungs Wert **MinDiffAreaFileSize** angegeben werden. Weitere Informationen finden Sie unter [MinDiffAreaFileSize](/windows/win32/backup/registry-keys-for-backup-and-restore#mindiffareafilesize).

> [!WARNING]
> Die Größe der Speicher Zuordnung kann dazu führen, dass Schatten Kopien ausgeblendet werden.

## <a name="syntax"></a>Syntax

```cmd
vssadmin resize shadowstorage /for=<ForVolumeSpec> /on=<OnVolumeSpec> [/maxsize=<MaxSizeSpec>]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---|---|
`/for=<ForVolumeSpec>`  | Gibt das Volume an, für das die maximale Speicherplatz Größe geändert werden soll.
`/on=<OnVolumeSpec>` | Gibt das Speicher Volume an.
`[/maxsize=<MaxSizeSpec>]` |  Gibt die maximale Menge an Speicherplatz an, die zum Speichern von Schatten Kopien verwendet werden kann. Wenn für/MAXSIZE kein Wert angegeben wird, gibt es keine Beschränkung für die Menge des Speicherplatzes, der verwendet werden kann.  <br> <br> Der maxsizespec-Wert muss 1 MB oder größer sein und muss in einer der folgenden Einheiten ausgedrückt werden: KB, MB, GB, TB, PB oder EB. Wenn keine Einheit angegeben ist, verwendet maxsizespec standardmäßig bytes.

## <a name="examples"></a>Beispiele

```cmd
vssadmin Resize ShadowStorage /For=C: /On=D: /MaxSize=900MB
vssadmin Resize ShadowStorage /For=C: /On=D: /MaxSize=UNBOUNDED
vssadmin Resize ShadowStorage /For=C: /On=C: /MaxSize=20%
```

## <a name="additional-references"></a>Weitere Verweise

* [Befehlszeilen-Syntax Schlüssel](./command-line-syntax-key.md)
* [Vssadmin](vssadmin.md)
