---
title: bitsadmin sethelpertoken
description: Referenz Artikel für den BITSAdmin sethelpertoken-Befehl, mit dem das primäre Token der aktuellen Eingabeaufforderung (oder ggf. ein beliebiges Token des lokalen Benutzerkontos) als Hilfsobjekt für das Bits-Übertragungs Auftrag festgelegt wird.
ms.topic: reference
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 37adfc2145089a871dca819745160794ed93a68e
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028528"
---
# <a name="bitsadmin-sethelpertoken"></a>bitsadmin sethelpertoken

Legt das primäre Token der aktuellen Eingabeaufforderung (oder ggf. ein beliebiges Token eines beliebigen lokalen Benutzerkontos) als [Hilfsobjekt](/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)des Bits-Übertragungs Auftrags fest.

> [!NOTE]
> Dieser Befehl wird von Bits 3,0 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /sethelpertoken <job> [<user_name@domain> <password>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| `<username@domain>` `<password>` | Optional. Die Anmelde Informationen des lokalen Benutzerkontos, für die das Token verwendet werden soll. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
