---
title: bizadmin-Setup Methode
description: Windows-Befehls Thema für **bitadmin sethttpmethod**, mit dem das zu verwendende HTTP-Verb festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: d349dcad7bdf6a6fc566ed961c3160836d7f49da
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122965"
---
# <a name="bitsadmin-sethttpmethod"></a>bizadmin-Setup Methode

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