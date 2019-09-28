---
title: bizadmin setvalidationstate
description: 'Windows-Befehls Thema für **BITSAdmin setvalidationstate** : legt den Inhalts Überprüfungs Zustand der angegebenen Datei innerhalb des Auftrags fest.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 37d7fa3a8a91abf1e7b6ac5a51b6cebd78984a91
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380399"
---
# <a name="bitsadmin-setvalidationstate"></a>bizadmin setvalidationstate



Legt den Inhalts Überprüfungs Zustand der angegebenen Datei innerhalb des Auftrags fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetValidationState <Job> <file index> <true|false> 
```

## <a name="parameters"></a>Parameter

| Parameter  |          Beschreibung           |
|------------|--------------------------------|
|    Auftrag     | Der Anzeige Name oder GUID des Auftrags. |
| Datei index |         Beginnt bei 0          |
|    True    |             False              |

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Inhalts Überprüfungs Zustand von Datei 2 für den Auftrag *MyJob*auf true festgelegt.
```
C:\>bitsadmin /SetValidationState myJob 2 TRUE 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)