---
title: bitsadmin fortsetzen
description: 'Windows-Befehls Thema für **bigsadmin Resume** : aktiviert einen neuen oder angehaltenen Auftrag in der Übertragungs Warteschlange.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c7540a9-a11a-4910-923a-2a2a61cbf11d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1393e959980b72de09c546ced763a506d334b56c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380767"
---
# <a name="bitsadmin-resume"></a>bitsadmin fortsetzen



Aktiviert einen neuen oder angehaltenen Auftrag in der Übertragungs Warteschlange.

## <a name="syntax"></a>Syntax

```
bitsadmin /Resume <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Auftrag mit dem Namen *mydownloadjob*fortgesetzt.
```
C:\>bitsadmin /Resume myDownloadJob
```
Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)