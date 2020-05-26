---
title: add alias
description: Referenz Thema für den Befehl Alias hinzufügen, mit dem Aliase zur Alias Umgebung hinzugefügt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5fe12f5d-11e9-4f3d-b7f9-40b26c8685e5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 66301a39a1e969e270b42b5ce92a73392a134357
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83819660"
---
# <a name="add-alias"></a>add alias

Fügt Aliase zur Alias Umgebung hinzu. Bei Verwendung ohne Parameter zeigt **Add Alias** die Hilfe an der Eingabeaufforderung an. Aliase werden in der Metadatendatei gespeichert und mit dem Befehl " **Metadaten laden** " geladen.

## <a name="syntax"></a>Syntax

```
add alias <aliasname> <aliasvalue>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Metadaten laden"](load-metadata.md)
