---
title: break
description: 'Windows-Befehls Thema für **break_2** : hebt die Zuordnung eines Schattenkopievolumes zu VSS auf und ermöglicht es als reguläres Volume.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de2b6c95-1c2e-4a43-bec5-341a9014371b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a5789e3442152c705b3197bf1ce5e63dc782a15c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379777"
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

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|beschreibbaren|Aktiviert den Lese-/Schreibzugriff auf dem Volume.|
|\<> TID|Gibt die ID des schattenkopiessets an.|

## <a name="remarks"></a>Hinweise

-   Verfügbar gemachte Volumes, wie die Schatten Kopien, von denen Sie stammen, sind standardmäßig schreibgeschützt.
-   Der Alias der Schattenkopiekennung, der durch den Befehl " **Metadaten laden** " als Umgebungsvariable gespeichert wird, kann *im Parameter "* Parameter" verwendet werden.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Schatten Kopie mit dem Aliasnamen Alias1 zugänglich als beschreibbares Volume im Betriebssystem zu erstellen:
```
break writable %Alias1%
```

> [!NOTE]
> Der Zugriff auf das Volume erfolgt direkt an den Hardware Anbieter, ohne dass das Volume eine Schatten Kopie aufweist.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)