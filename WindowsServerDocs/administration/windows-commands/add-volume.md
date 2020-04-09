---
title: Volume hinzufügen
description: Windows-Befehls Thema zum **Hinzufügen**eines Volumes, mit dem dem Schattenkopiesatz Volumes hinzugefügt werden
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b7d4d35d-8bda-46d2-8df5-eb598cecaaba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 806ab273dbb63eb7341520f56a07691fe3fac214
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851353"
---
# <a name="add-volume"></a>Volume hinzufügen

Fügt dem Schattenkopiesatz Volumes hinzu, bei denen es sich um den Satz von Volumes handelt, die gespiegelt werden sollen. Dieser Befehl ist erforderlich, um Schatten Kopien zu erstellen. Wenn **Sie** ohne Parameter verwendet wird, wird in der Eingabeaufforderung Hilfe angezeigt.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
add volume <Volume> [provider <ProviderID>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
| `<Volume>` | Gibt ein Volume an, das dem Schattenkopiesatz hinzugefügt wird. Für die Erstellung von Schatten Kopien ist mindestens ein Volume erforderlich.|
| `[provider \<ProviderID>]` | Gibt die Anbieter-ID eines registrierten Anbieters an, der zum Erstellen der Schatten Kopie verwendet werden soll. Wenn der **Anbieter** nicht angegeben wird, wird der Standardanbieter verwendet.|

## <a name="remarks"></a>Hinweise

-   Volumes werden nacheinander hinzugefügt.

-   Jedes Mal, wenn ein Volume hinzugefügt wird, wird es geprüft, um sicherzustellen, dass VSS die Erstellung von Schatten Kopien dieses Volumes unterstützt. Diese primäre Prüfung kann jedoch durch spätere Verwendung des **Set Context** -Befehls ungültig gemacht werden.

-   Wenn eine Schatten Kopie erstellt wird, wird der Alias von einer Umgebungsvariablen mit der Schatten-ID verknüpft, sodass der Alias für die Skripterstellung verwendet werden kann.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Um die aktuelle Liste der registrierten Anbieter anzuzeigen, geben Sie an der `DISKSHADOW>` Eingabeaufforderung Folgendes ein:

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

Um das Laufwerk C dem Schattenkopiesatz hinzuzufügen und einen Alias namens system1 zuzuweisen, geben Sie Folgendes ein:

```
add volume c: alias System1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)