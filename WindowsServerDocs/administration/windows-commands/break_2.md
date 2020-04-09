---
title: break
description: Windows-Befehle Thema für break_2, das ein Schattenkopievolume von VSS trennt und als reguläres Volume verfügbar macht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: de2b6c95-1c2e-4a43-bec5-341a9014371b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6683c44c84f4baae5f016f7df62d5bd6591cff70
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848253"
---
# <a name="break"></a>break

Trennt ein Schattenkopievolume von VSS und ermöglicht es als reguläres Volume. Auf das Volume kann dann mithilfe eines Laufwerk Buchstabens (sofern zugewiesen) oder eines Volumenamens zugegriffen werden. Bei Verwendung ohne Parameter zeigt **break** die Hilfe an der Eingabeaufforderung an.

> [!NOTE]
> Dieser Befehl ist nur für Hardware Schatten Kopien nach dem Import relevant.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
break [writable] <SetID>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|beschreibbaren|Aktiviert den Lese-/Schreibzugriff auf dem Volume.|
|\<>|Gibt die ID des schattenkopiessets an.|

## <a name="remarks"></a>Hinweise

-   Verfügbar gemachte Volumes, wie die Schatten Kopien, von denen Sie stammen, sind standardmäßig schreibgeschützt.
-   Der Alias der Schattenkopiekennung, der durch den Befehl " **Metadaten laden** " als Umgebungsvariable gespeichert wird, kann *im Parameter "* Parameter" verwendet werden.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um eine Schatten Kopie mit dem Aliasnamen Alias1 zugänglich als beschreibbares Volume im Betriebssystem zu erstellen:
```
break writable %Alias1%
```

> [!NOTE]
> Der Zugriff auf das Volume erfolgt direkt an den Hardware Anbieter, ohne dass das Volume eine Schatten Kopie aufweist.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)