---
title: Alias hinzufügen
description: 'Windows-Befehls Artikel zum **Hinzufügen von Alias** : fügt Aliase zur Alias Umgebung hinzu.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5fe12f5d-11e9-4f3d-b7f9-40b26c8685e5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f2834376e497f54eadf1d9077e74f9c398202c5a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382818"
---
# <a name="add-alias"></a>Alias hinzufügen



Fügt Aliase zur Alias Umgebung hinzu. Bei Verwendung ohne Parameter zeigt **Add Alias** die Hilfe an der Eingabeaufforderung an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
add alias <AliasName> <AliasValue>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<aliasname >|Gibt den Namen des Alias an.|
|\<aliasvalue >|Gibt den Wert des Alias an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Aliase werden in der Metadatendatei gespeichert und mit dem Befehl " **Metadaten laden** " geladen.

## <a name="BKMK_examples"></a>Beispiele

Um alle Schatten, einschließlich der Aliase, aufzulisten, geben Sie Folgendes ein:
```
list shadows all
```
Der folgende Auszug zeigt eine Schatten Kopie, der der Standardalias VSS_SHADOW_x zugewiesen wurde:
```
* Shadow Copy ID = {ff47165a-1946-4a0c-b7f4-80f46a309278}
%VSS_SHADOW_1%
```
Wenn Sie dieser Schatten Kopie einen neuen Alias mit dem Namen system1 zuweisen möchten, geben Sie Folgendes ein:
```
add alias System1 %VSS_SHADOW_1%
```
Alternativ können Sie den Alias mithilfe der Schattenkopiekennung zuweisen:
```
add alias System1 {ff47165a-1946-4a0c-b7f4-80f46a309278}
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)