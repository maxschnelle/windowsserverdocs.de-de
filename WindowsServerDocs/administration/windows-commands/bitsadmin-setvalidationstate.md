---
title: bizadmin setvalidationstate
description: Windows-Befehls Thema für BITSAdmin setvalidationstate, mit dem der Inhalts Überprüfungs Zustand der angegebenen Datei innerhalb des Auftrags festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e8fc8e8c-171c-4681-8057-6986b018e576
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de6480596b55b3a483076297f32ce52a975915db
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849113"
---
# <a name="bitsadmin-setvalidationstate"></a>bizadmin setvalidationstate

Legt den Inhalts Überprüfungs Zustand der angegebenen Datei innerhalb des Auftrags fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetValidationState <Job> <file index> <true|false> 
```

### <a name="parameters"></a>Parameter

| Parameter  |          Beschreibung           |
|------------|--------------------------------|
|    Auftrag     | Der Anzeige Name oder GUID des Auftrags. |
| Datei index |         Beginnt bei 0          |
|    True    |             False              |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Inhalts Überprüfungs Zustand von Datei 2 für den Auftrag *MyJob*auf true festgelegt.
```
C:\>bitsadmin /SetValidationState myJob 2 TRUE 
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)