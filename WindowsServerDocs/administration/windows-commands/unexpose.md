---
title: unexpose
description: Referenz Artikel zum nicht verfügbar machen, das eine Schatten Kopie zurückgibt, die mit dem verfügbar gemachten Befehl verfügbar gemacht wurde.
ms.topic: reference
ms.assetid: 58dc7d0f-52e9-4587-9487-d3b4c3e52640
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 76e1666bd87a3304dcbe8de3025a0ec790cf83d7
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626579"
---
# <a name="unexpose"></a>unexpose

Macht eine Schatten Kopie verfügbar **, die mit dem verfügbar** gemachten Befehl verfügbar gemacht wurde. Die verfügbar gemachte Schatten Kopie kann durch die Schatten-ID, den Laufwerk Buchstaben, die Freigabe oder den Einfügepunkt angegeben werden.



## <a name="syntax"></a>Syntax

```
unexpose {<ShadowID> | <Drive:> | <Share> | <MountPoint>}
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<ShadowID>|Macht die von der angegebenen Schatten-ID angegebene Schatten Kopie nicht verfügbar.|
|\<Drive:>|Macht die Schatten Kopie verfügbar, die dem angegebenen Laufwerk Buchstaben zugeordnet ist (z. b. Laufwerk P).|
|\<Share>|Macht die der angegebenen Freigabe zugeordnete Schatten Kopie (z \\ \\ . b. *MachineName*) nicht verfügbar \) .|
|\<MountPoint>|Macht die für den angegebenen Einstellungspunkt zugeordnete Schatten Kopie (z. b. c:\shadowcopy) nicht verfügbar \) .|

## <a name="remarks"></a>Hinweise

-   Anstelle von *shadowid*können Sie einen vorhandenen Alias oder eine Umgebungsvariable verwenden. Verwenden **Sie hinzufügen** ohne Parameter, um vorhandene Aliase anzuzeigen.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die verfügbar machung der dem Laufwerk P zugeordneten Schatten Kopie anzuzeigen:
```
unexpose P:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)