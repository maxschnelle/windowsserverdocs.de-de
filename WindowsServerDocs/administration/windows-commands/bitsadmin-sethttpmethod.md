---
title: bitsadmin sethttpmethod
description: Referenz Artikel für den Befehl "bizadmin sethttpmethod", der das zu verwendende HTTP-Verb festlegt.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: 0c8d2357e35831db89365eabbe0b97cdec88b6aa
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630875"
---
# <a name="bitsadmin-sethttpmethod"></a>bitsadmin sethttpmethod

Legt das zu verwendende HTTP-Verb fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /sethttpmethod <job> <httpmethod>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| HttpMethod | Das zu verwendende HTTP-Verb. Weitere Informationen zu verfügbaren Verben finden Sie unter [Methoden Definitionen](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html). |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
