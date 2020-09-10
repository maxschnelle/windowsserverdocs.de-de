---
title: bitsadmin sethelpertoken
description: Referenz Artikel für den BITSAdmin sethelpertoken-Befehl, mit dem das primäre Token der aktuellen Eingabeaufforderung (oder ggf. ein beliebiges Token des lokalen Benutzerkontos) als Hilfsobjekt für das Bits-Übertragungs Auftrag festgelegt wird.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: a691d010aa112f1ac609077be6a6968f79d73c72
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630910"
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

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| `<username@domain>` `<password>` | (Optional) Die Anmelde Informationen des lokalen Benutzerkontos, für die das Token verwendet werden soll. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
