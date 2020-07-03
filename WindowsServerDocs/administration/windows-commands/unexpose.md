---
title: unexpose
description: Referenz Artikel zum nicht verfügbar machen, das eine Schatten Kopie zurückgibt, die mit dem verfügbar gemachten Befehl verfügbar gemacht wurde.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 58dc7d0f-52e9-4587-9487-d3b4c3e52640
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 02edb1f2c9331a22473123f0327dbc84cb05a865
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937301"
---
# <a name="unexpose"></a>unexpose

Macht eine Schatten Kopie verfügbar **, die mit dem verfügbar** gemachten Befehl verfügbar gemacht wurde. Die verfügbar gemachte Schatten Kopie kann durch die Schatten-ID, den Laufwerk Buchstaben, die Freigabe oder den Einfügepunkt angegeben werden.



## <a name="syntax"></a>Syntax

```
unexpose {<ShadowID> | <Drive:> | <Share> | <MountPoint>}
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
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