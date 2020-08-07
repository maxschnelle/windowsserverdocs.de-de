---
title: mask
description: Referenz Artikel für den Mask-Befehl, mit dem Hardware Schatten Kopien entfernt werden, die mit dem Import-Befehl importiert wurden.
ms.topic: article
ms.assetid: bf301474-d74a-44e7-9fad-c8a11e7ca3bd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a893d32dca90169d51a04db66b3dc796cbc69a46
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886519"
---
# <a name="mask"></a>mask

Entfernt Hardware Schatten Kopien, die mithilfe des **Import** -Befehls importiert wurden.

## <a name="syntax"></a>Syntax

```
mask <shadowsetID>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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