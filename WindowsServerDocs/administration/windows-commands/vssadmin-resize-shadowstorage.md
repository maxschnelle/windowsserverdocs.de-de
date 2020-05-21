---
title: Vssadmin residieren von ShadowStorage
description: Eine Beschreibung des Befehls vssadmin Größe shadowstorage.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 03/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: e32fe419899c0f553f36976ecee95fb3a922f1a6
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436625"
---
# <a name="vssadmin-resize-shadowstorage"></a>Vssadmin residieren von ShadowStorage

> Gilt für: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Ändert die maximale Speicherplatz Größe, die für den schattenkopiespeicherspeicher verwendet werden kann.

Die minimale Menge an Speicherplatz, die zum Speichern von Schatten Kopien verwendet werden kann, kann mit dem Registrierungs Wert **MinDiffAreaFileSize** angegeben werden. Weitere Informationen finden Sie unter [MinDiffAreaFileSize](https://docs.microsoft.com/windows/win32/backup/registry-keys-for-backup-and-restore#mindiffareafilesize).

> [!WARNING]
> Die Größe der Speicher Zuordnung kann dazu führen, dass Schatten Kopien ausgeblendet werden.

## <a name="syntax"></a>Syntax

```cmd
vssadmin resize shadowstorage /for=<ForVolumeSpec> /on=<OnVolumeSpec> [/maxsize=<MaxSizeSpec>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
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

## <a name="additional-references"></a>Zusätzliche Referenzen

* [Befehlszeilen-Syntax Schlüssel](https://docs.microsoft.com/windows-server/administration/windows-commands/command-line-syntax-key)
* [Vssadmin](vssadmin.md)
