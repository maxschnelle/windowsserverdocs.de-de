---
title: bitadmin-Eingabetoken
description: Windows-Befehls Thema für BITSAdmin sethelpertoken, das das primäre Token der aktuellen Eingabeaufforderung (oder ggf. ein beliebiges Token des lokalen Benutzerkontos) als Hilfsobjekt für Bits-Übertragungs Aufträge festlegt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: a1e8fd0054cadf3bf06b6e5b7bdf5010b18781e1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849533"
---
# <a name="bitsadmin-sethelpertoken"></a>bitadmin-Eingabetoken

Legt das primäre Token der aktuellen Eingabeaufforderung (oder ggf. ein beliebiges Token eines beliebigen lokalen Benutzerkontos) als [Hilfsobjekt](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs)des Bits-Übertragungs Auftrags fest.

**Bits 3,0 und früher**: nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetHelperToken <Job> [\<username@domain\> \<password\>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|\<username@domain\> \<Kennwort\>|Optional&mdash;die Anmelde Informationen eines lokalen Benutzerkontos, dessen Token verwendet werden soll.|

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
