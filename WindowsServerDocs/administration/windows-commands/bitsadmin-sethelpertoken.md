---
title: Bitsadmin sethelpertoken
description: Windows-Befehle Thema **Bitsadmin Sethelpertoken** -primäres Token von der aktuellen-Eingabeaufforderung (oder einer beliebigen lokalen des Benutzerkontos Token, wenn angegeben) als eine BITS-Übertragungsauftrag Helper Token festgelegt.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 558a1aca66a7b3ec447136ceff9237d13efe4ede
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853001"
---
# <a name="bitsadmin-sethelpertoken"></a>Bitsadmin sethelpertoken

Primäres Token von der aktuellen-Eingabeaufforderung (oder einer beliebigen lokalen des Benutzerkontos Token, wenn angegeben) als eine BITS-Übertragungsauftrag festgelegt [Helper-Token](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs).

**BITS 3.0 und früheren**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetHelperToken <Job> [\<username@domain\> \<password\>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Auftrags Anzeigenamen oder die GUID.|
|\<username@domain\> \<password\>|Optionale&mdash;die Anmeldeinformationen eines lokalen Benutzers Konto, dessen Token verwenden.|

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)
