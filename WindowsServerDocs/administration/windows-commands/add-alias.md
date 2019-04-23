---
title: alias hinzufügen
description: Windows-Befehle Thema **alias hinzufügen** -Aliase auf die Alias-Umgebung hinzugefügt.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 50de932ea0153546816face61f0852a08707ea85
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862221"
---
# <a name="add-alias"></a>alias hinzufügen



Fügt die Aliase der Alias-Umgebung hinzu. Wenn Sie ohne Angabe von Parametern **alias hinzufügen** zeigt die Hilfe an der Eingabeaufforderung.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
add alias <AliasName> <AliasValue>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<AliasName>|Gibt den Namen des Alias.|
|\<AliasValue>|Gibt den Wert des Alias.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Aliase werden in der Metadatendatei gespeichert und werden geladen, mit der **Laden von Metadaten** Befehl.

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie Folgendes ein, um ihre Aliase, einschließlich aller Schatten aufzulisten:
```
list shadows all
```
Der folgende Ausschnitt zeigt eine Schattenkopie, die Standardalias, VSS_SHADOW_x, zugewiesen wurde:
```
* Shadow Copy ID = {ff47165a-1946-4a0c-b7f4-80f46a309278}
%VSS_SHADOW_1%
```
Um einen neuen Alias mit dem Namen 1 diese Schattenkopie zuzuweisen, geben Sie Folgendes ein:
```
add alias System1 %VSS_SHADOW_1%
```
Alternativ können Sie den Alias zuweisen, mit der Schattenkopie-ID:
```
add alias System1 {ff47165a-1946-4a0c-b7f4-80f46a309278}
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)