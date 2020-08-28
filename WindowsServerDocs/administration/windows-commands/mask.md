---
title: mask
description: Referenz Artikel für den Mask-Befehl, mit dem Hardware Schatten Kopien entfernt werden, die mit dem Import-Befehl importiert wurden.
ms.topic: reference
ms.assetid: bf301474-d74a-44e7-9fad-c8a11e7ca3bd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c5d8f86de3019e47da3aff56aa370972de3288fa
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037868"
---
# <a name="mask"></a>mask

Entfernt Hardware Schatten Kopien, die mithilfe des **Import** -Befehls importiert wurden.

## <a name="syntax"></a>Syntax

```
mask <shadowsetID>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Shadow-TID | Entfernt Schatten Kopien, die zur angegebenen Schattenkopiesatz-ID gehören. |

#### <a name="remarks"></a>Bemerkungen

- Anstelle von *Shadow* TID*können Sie einen vorhandenen Alias oder eine Umgebungsvariable verwenden. Verwenden **Sie hinzufügen** ohne Parameter, um vorhandene Aliase anzuzeigen.

### <a name="examples"></a>Beispiele

Um die importierte Schatten Kopie *% Import_1%* zu entfernen, geben Sie Folgendes ein:

```
mask %Import_1%
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)