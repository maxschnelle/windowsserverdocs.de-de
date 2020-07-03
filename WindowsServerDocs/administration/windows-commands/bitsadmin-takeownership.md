---
title: bitsadmin takeownership
description: Referenz Artikel für den Befehl bizadmin TakeOwnership, mit dem ein Benutzer mit Administratorrechten den Besitz des angegebenen Auftrags übernimmt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc406d1d5f7c9553082f85f3315ab7622f6bc7db
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927464"
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
