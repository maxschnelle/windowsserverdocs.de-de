---
title: bitsadmin sethelpertoken
description: Referenz Artikel für den BITSAdmin sethelpertoken-Befehl, mit dem das primäre Token der aktuellen Eingabeaufforderung (oder ggf. ein beliebiges Token des lokalen Benutzerkontos) als Hilfsobjekt für das Bits-Übertragungs Auftrag festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 21dee45610823cd70e8b7209ec99e080746316f9
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927782"
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

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| `<username@domain>` `<password>` | Dies ist optional. Die Anmelde Informationen des lokalen Benutzerkontos, für die das Token verwendet werden soll. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
