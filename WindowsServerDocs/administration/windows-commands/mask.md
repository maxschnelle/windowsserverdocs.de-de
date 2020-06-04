---
title: mask
description: Referenz Thema für den Mask-Befehl, mit dem Hardware Schatten Kopien entfernt werden, die mit dem Import-Befehl importiert wurden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bf301474-d74a-44e7-9fad-c8a11e7ca3bd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ee01bb74b1fef1bb31a266c01a9e9bde7743691d
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354630"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)