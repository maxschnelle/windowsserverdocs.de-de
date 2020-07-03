---
title: bitsadmin sethttpmethod
description: Referenz Artikel für den Befehl "bizadmin sethttpmethod", der das zu verwendende HTTP-Verb festlegt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 86d4749de294871a05176239cc1265974d8a7590
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927753"
---
# <a name="bitsadmin-sethttpmethod"></a>bitsadmin sethttpmethod

Legt das zu verwendende HTTP-Verb fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /sethttpmethod <job> <httpmethod>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| HttpMethod | Das zu verwendende HTTP-Verb. Weitere Informationen zu verfügbaren Verben finden Sie unter [Methoden Definitionen](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html). |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
