---
title: add alias
description: Referenz Artikel für den Befehl Alias hinzufügen, der Aliase zur Alias Umgebung hinzufügt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5fe12f5d-11e9-4f3d-b7f9-40b26c8685e5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 405c04b17b32477654f0349c04c6059cf246f804
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924127"
---
# <a name="add-alias"></a>add alias

Fügt Aliase zur Alias Umgebung hinzu. Bei Verwendung ohne Parameter zeigt **Add Alias** die Hilfe an der Eingabeaufforderung an. Aliase werden in der Metadatendatei gespeichert und mit dem Befehl " **Metadaten laden** " geladen.

## <a name="syntax"></a>Syntax

```
add alias <aliasname> <aliasvalue>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<aliasname>` | Gibt den Namen des Alias an. |
| `<aliasvalue>` | Gibt den Wert des Alias an. |
| `? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Um alle Schatten, einschließlich der Aliase, aufzulisten, geben Sie Folgendes ein:

```
list shadows all
```

Der folgende Auszug zeigt eine Schatten Kopie, der der Standardalias ( *VSS_SHADOW_x*) zugewiesen wurde:

```
* Shadow Copy ID = {ff47165a-1946-4a0c-b7f4-80f46a309278}
%VSS_SHADOW_1%
```

Wenn Sie dieser Schatten Kopie einen neuen Alias mit dem Namen *system1* zuweisen möchten, geben Sie Folgendes ein:

```
add alias System1 %VSS_SHADOW_1%
```

Alternativ können Sie den Alias mithilfe der Schattenkopiekennung zuweisen:

```
add alias System1 {ff47165a-1946-4a0c-b7f4-80f46a309278}
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Metadaten laden"](load-metadata.md)
