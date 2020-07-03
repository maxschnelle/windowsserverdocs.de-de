---
title: mask
description: Referenz Artikel für den Mask-Befehl, mit dem Hardware Schatten Kopien entfernt werden, die mit dem Import-Befehl importiert wurden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bf301474-d74a-44e7-9fad-c8a11e7ca3bd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2839fce0a64f187c1445a5f6a4af6c5f0ebc9fb8
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922100"
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

#### <a name="remarks"></a>Hinweise

- Anstelle von *Shadow* TID*können Sie einen vorhandenen Alias oder eine Umgebungsvariable verwenden. Verwenden **Sie hinzufügen** ohne Parameter, um vorhandene Aliase anzuzeigen.

### <a name="examples"></a>Beispiele

Um die importierte Schatten Kopie *% Import_1%* zu entfernen, geben Sie Folgendes ein:

```
mask %Import_1%
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)