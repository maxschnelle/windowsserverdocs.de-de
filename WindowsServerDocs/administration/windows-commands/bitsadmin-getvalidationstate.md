---
title: Bitsadmin getvalidationstate
description: 'Windows-Befehle Thema **Bitsadmin Getvalidationstate** -meldet den Status der Überprüfung des Inhalts der angegebenen Datei innerhalb des Auftrags. '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ada3f1f-9967-4262-9d22-ed641e23f516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8abff3fc9fddb9cff1758739fdc540a9c945efe2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879161"
---
# <a name="bitsadmin-getvalidationstate"></a>Bitsadmin getvalidationstate



Meldet den Status der Überprüfung des Inhalts der angegebenen Datei innerhalb des Auftrags an.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetValidationState <Job> <file index> 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|Datei-index|Beginnt bei 0|

## <a name="BKMK_examples"></a>Beispiele für

Im folgende Beispiel ruft den Status der Überprüfung des Inhalts der Datei "2" innerhalb des Auftrags, der mit dem Namen *MyJob*.
```
C:\>bitsadmin /GetValidationState myJob 1
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)