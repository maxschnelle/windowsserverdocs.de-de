---
title: mask
description: Referenz Artikel für den Mask-Befehl, mit dem Hardware Schatten Kopien entfernt werden, die mit dem Import-Befehl importiert wurden.
ms.topic: reference
ms.assetid: bf301474-d74a-44e7-9fad-c8a11e7ca3bd
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ee0e4207a7c5cf6ad81ece39e9134881ad3c0239
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633710"
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

#### <a name="remarks"></a>Hinweise

- Anstelle von *Shadow* TID*können Sie einen vorhandenen Alias oder eine Umgebungsvariable verwenden. Verwenden **Sie hinzufügen** ohne Parameter, um vorhandene Aliase anzuzeigen.

### <a name="examples"></a>Beispiele

Um die importierte Schatten Kopie *% Import_1%* zu entfernen, geben Sie Folgendes ein:

```
mask %Import_1%
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)