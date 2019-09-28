---
title: bitsadmin setpriority
description: 'Windows-Befehls Thema für **bitadmin SetPriority** : legt die Priorität des angegebenen Auftrags fest.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 60564350928f917ca1861684e042304d5d380426
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380436"
---
# <a name="bitsadmin-setpriority"></a>bitsadmin setpriority



Legt die Priorität des angegebenen Auftrags fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetPriority <Job> <Priority>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Priority|Einer der folgenden Werte:</br>-VORDERGRUND</br>-HOCH</br>-NORMAL</br>-NIEDRIG|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird die Priorität für den Auftrag mit dem Namen *mydownloadjob* auf Normal festgelegt.
```
C:\>bitsadmin /SetPriority myDownloadJob NORMAL
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)