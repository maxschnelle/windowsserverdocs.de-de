---
title: bitsadmin takeownership
description: Referenz Artikel für den Befehl bizadmin TakeOwnership, mit dem ein Benutzer mit Administratorrechten den Besitz des angegebenen Auftrags übernimmt.
ms.topic: article
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b7e37b4508681af58ab07458507101647a0906ff
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880983"
---
# <a name="bitsadmin-takeownership"></a>bitsadmin takeownership

Ermöglicht einem Benutzer mit Administratorrechten, den Besitz des angegebenen Auftrags zu übernehmen.

## <a name="syntax"></a>Syntax

```
bitsadmin /takeownership <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
