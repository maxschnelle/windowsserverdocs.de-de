---
title: bitsadmin sethttpmethod
description: Referenz Thema für den bizadmin sethttpmethod-Befehl, der das zu verwendende HTTP-Verb festlegt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: daf1c23565bc4f398fd29e51aaaeef23b3b0d018
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719359"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
