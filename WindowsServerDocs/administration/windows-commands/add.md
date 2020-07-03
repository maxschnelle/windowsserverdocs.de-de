---
title: add
description: Referenz Artikel für den Befehl "hinzufügen", mit dem Volumes zu der Gruppe von Volumes hinzugefügt werden, die als Schatten kopiert werden sollen, oder um Aliase zur Alias Umgebung hinzuzufügen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 47efce7a-86d2-4872-ae31-baa108757afd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7b409b0355f4e112773c3f847466586fe3c84654
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924070"
---
# <a name="add"></a>add

Fügt Volumes zu dem Satz von Volumes hinzu, die als Schatten kopiert werden sollen, oder fügt der Alias Umgebung Aliase hinzu. Bei Verwendung ohne Unterbefehle listet **Add** die aktuellen Volumes und Aliase auf.

> [!NOTE]
> Aliase werden erst zur Alias Umgebung hinzugefügt, wenn die Schatten Kopie erstellt wird. Aliase, die Sie sofort benötigen, sollten mit **Add-Alias**hinzugefügt werden.

## <a name="syntax"></a>Syntax

```
add
add volume <volume> [provider <providerid>]
add alias <aliasname> <aliasvalue>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ----------- |
| Volume | Fügt ein Volume zum Schattenkopiesatz hinzu. Dies ist der Satz von Volumes, auf die Schatten kopiert werden soll. Syntax und Parameter finden [Sie unter Volume hinzufügen](add-volume.md) . |
| alias | Fügt der Alias Umgebung den angegebenen Namen und Wert hinzu. Informationen finden [Sie unter Add-Alias](add-alias.md) für Syntax und Parameter. |
| /? | Zeigt die Hilfe in der Befehlszeile an. |

## <a name="examples"></a>Beispiele

Zum Anzeigen der hinzugefügten Volumes und der Aliase, die sich derzeit in der Umgebung befinden, geben Sie Folgendes ein:

```
add
```

Die folgende Ausgabe zeigt, dass Laufwerk C dem Schattenkopiesatz hinzugefügt wurde:

```
Volume c: alias System1    GUID \\?\Volume{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}\
1 volume in Shadow Copy Set.
No Diskshadow aliases in the environment.
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)