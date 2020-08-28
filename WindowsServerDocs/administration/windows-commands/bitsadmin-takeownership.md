---
title: bitsadmin takeownership
description: Referenz Artikel für den Befehl bizadmin TakeOwnership, mit dem ein Benutzer mit Administratorrechten den Besitz des angegebenen Auftrags übernimmt.
ms.topic: reference
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b0df40e336ecc282e4b1a1774d7b5848f37a1a7a
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033378"
---
# <a name="bitsadmin-takeownership"></a>bitsadmin takeownership

Ermöglicht einem Benutzer mit Administratorrechten, den Besitz des angegebenen Auftrags zu übernehmen.

## <a name="syntax"></a>Syntax

```
bitsadmin /takeownership <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ---------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

Um den Besitz des Auftrags mit dem Namen *mydownloadjob*zu übernehmen:

```
bitsadmin /takeownership myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
