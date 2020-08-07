---
title: bitsadmin sethttpmethod
description: Referenz Artikel für den Befehl "bizadmin sethttpmethod", der das zu verwendende HTTP-Verb festlegt.
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 9b782ea4f07113541ce62eaef63ac8047141e766
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881044"
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
