---
title: bitadmin-Eingabetoken
description: 'Windows-Befehls Thema für **BITSAdmin sethelpertoken** : legt das primäre Token der aktuellen Eingabeaufforderung (oder ggf. ein beliebiges Token eines beliebigen lokalen Benutzerkontos) als Hilfsobjekt des Bits-Übertragungs Auftrags fest.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 91c03366998168dad9ab4530ef36a5020b8ad6ec
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380567"
---
# <a name="bitsadmin-sethelpertoken"></a>bitadmin-Eingabetoken

Legt das primäre Token der aktuellen Eingabeaufforderung (oder ggf. ein beliebiges Token eines beliebigen lokalen Benutzerkontos) als [Hilfsobjekt](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs)des Bits-Übertragungs Auftrags fest.

**Bits 3,0 und früher**: nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetHelperToken <Job> [\<username@domain\> \<password\>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|\<username@domain\> \<Kennwort\>|Optional&mdash;die Anmelde Informationen eines lokalen Benutzerkontos, dessen Token verwendet werden soll.|

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
