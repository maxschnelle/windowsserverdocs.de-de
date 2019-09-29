---
title: bitsadmin getcompletiontime
description: 'Thema Windows-Befehle für **bigsadmin getcompletiontime** : Ruft die Zeit ab, zu der der Auftrag das Übertragen von Daten abgeschlossen hat.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 190467d5f3a7b7244ed0d7ab3b75d4cbbf56c8d5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381745"
---
# <a name="bitsadmin-getcompletiontime"></a>bitsadmin getcompletiontime



Ruft den Zeitpunkt ab, zu dem der Auftrag die Datenübertragung abgeschlossen hat.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetCompletionTime <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird die Uhrzeit abgerufen, zu der der Auftrag mit dem Namen *mydownloadjob* die Datenübertragung abgeschlossen hat.
```
C:\>bitsadmin /GetCompletionTime myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)