---
title: Bitsadmin setvalidationstate
description: Windows-Befehle Thema **Bitsadmin Setvalidationstate** -legt den Status der Überprüfung des Inhalts der angegebenen Datei innerhalb des Auftrags fest.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8fc8e8c-171c-4681-8057-6986b018e576
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a832e8f3d21681f67a4486df33c387e5a8456718
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434874"
---
# <a name="bitsadmin-setvalidationstate"></a>Bitsadmin setvalidationstate



Legt den Status der Überprüfung des Inhalts der angegebenen Datei innerhalb des Auftrags fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetValidationState <Job> <file index> <true|false> 
```

## <a name="parameters"></a>Parameter

| Parameter  |          Beschreibung           |
|------------|--------------------------------|
|    Auftrag     | Anzeigenamen oder die GUID des Auftrags |
| Datei-index |         Beginnt bei 0          |
|    True    |             False              |

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird den Status der Überprüfung des Inhalts der Datei 2 auf "true" für den Auftrag mit dem Namen *MyJob*.
```
C:\>bitsadmin /SetValidationState myJob 2 TRUE 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)