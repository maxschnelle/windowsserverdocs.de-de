---
title: Volume hinzufügen
description: Referenz Thema für den Befehl "Volume hinzufügen", mit dem dem Schattenkopiesatz Volumes hinzugefügt werden
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b7d4d35d-8bda-46d2-8df5-eb598cecaaba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a8cfd3d8f7d9f008e3136d8f694dc00370b8b0f2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719211"
---
# <a name="add-volume"></a>Volume hinzufügen

Fügt dem Schattenkopiesatz Volumes hinzu, bei denen es sich um den Satz von Volumes handelt, die gespiegelt werden sollen. Wenn eine Schatten Kopie erstellt wird, wird der Alias von einer Umgebungsvariablen mit der Schatten-ID verknüpft, sodass der Alias für die Skripterstellung verwendet werden kann.

Volumes werden nacheinander hinzugefügt. Jedes Mal, wenn ein Volume hinzugefügt wird, wird es geprüft, um sicherzustellen, dass VSS die Erstellung von Schatten Kopien für dieses Volume unterstützt. Diese Überprüfung kann durch die spätere Verwendung des **Set Context** -Befehls ungültig gemacht werden.

Dieser Befehl ist erforderlich, um Schatten Kopien zu erstellen. Wenn **Sie** ohne Parameter verwendet wird, wird in der Eingabeaufforderung Hilfe angezeigt.

## <a name="syntax"></a>Syntax

```
add volume <volume> [provider <providerid>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<volume>` | Gibt ein Volume an, das dem Schattenkopiesatz hinzugefügt wird. Für die Erstellung von Schatten Kopien ist mindestens ein Volume erforderlich. |
| `[provider \<providerid>]` | Gibt die Anbieter-ID an, die ein registrierter Anbieter zum Erstellen der Schatten Kopie verwenden soll. Wenn der **Anbieter** nicht angegeben wird, wird der Standardanbieter verwendet. |

## <a name="examples"></a>Beispiele

Geben Sie an der `diskshadow>` Eingabeaufforderung Folgendes ein, um die aktuelle Liste der registrierten Anbieter anzuzeigen:

```
list providers
```

Die folgende Ausgabe zeigt einen einzelnen Anbieter, der standardmäßig verwendet wird:

```
* ProviderID: {b5946137-7b9f-4925-af80-51abd60b20d5}
        Type: [1] VSS_PROV_SYSTEM
        Name: Microsoft Software Shadow Copy provider 1.0
        Version: 1.0.0.7
        CLSID: {65ee1dba-8ff4-4a58-ac1c-3470ee2f376a}
1 provider registered.
```

Zum Hinzufügen von Laufwerk C: zum Schattenkopiesatz und Zuweisen eines Alias namens *system1*geben Sie Folgendes ein:

```
add volume c: alias System1
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Kontext Befehl festlegen](set-context.md)
