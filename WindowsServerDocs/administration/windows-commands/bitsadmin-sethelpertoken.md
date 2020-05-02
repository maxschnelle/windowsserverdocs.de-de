---
title: bitsadmin sethelpertoken
description: Referenz Thema für den BITSAdmin sethelpertoken-Befehl, mit dem das primäre Token der aktuellen Eingabeaufforderung (oder ggf. ein beliebiges Token des lokalen Benutzerkontos) als Hilfsobjekt für das Bits-Übertragungs Auftrag festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: b125f95e262c2fd78f20266e3e2b6c80cea5a789
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719392"
---
# <a name="bitsadmin-sethelpertoken"></a>bitsadmin sethelpertoken

Legt das primäre Token der aktuellen Eingabeaufforderung (oder ggf. ein beliebiges Token eines beliebigen lokalen Benutzerkontos) als [Hilfsobjekt](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)des Bits-Übertragungs Auftrags fest.

> [!NOTE]
> Dieser Befehl wird von Bits 3,0 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /sethelpertoken <job> [<user_name@domain> <password>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| `<username@domain>` `<password>` | Optional. Die Anmelde Informationen des lokalen Benutzerkontos, für die das Token verwendet werden soll. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
