---
title: bitsadmin takeownership
description: Referenz Artikel für den Befehl bizadmin TakeOwnership, mit dem ein Benutzer mit Administratorrechten den Besitz des angegebenen Auftrags übernimmt.
ms.topic: reference
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a4998ce3c28c839bb035a04c5472aae7c98b4eac
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630569"
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
