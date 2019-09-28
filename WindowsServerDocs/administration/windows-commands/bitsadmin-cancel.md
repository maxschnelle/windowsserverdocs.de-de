---
title: bitsadmin cancel
description: 'Windows-Befehls Thema für **bitadmin Abbrechen** : entfernt den Auftrag aus der Übertragungs Warteschlange und löscht alle temporären Dateien, die dem Auftrag zugeordnet sind.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7374b544-6a16-4d3e-872c-dcf4c02ad89d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 77e46d787359af43a37faba5d844bfec09730454
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381803"
---
# <a name="bitsadmin-cancel"></a>bitsadmin cancel

Entfernt den Auftrag aus der Übertragungs Warteschlange und löscht alle temporären Dateien, die dem Auftrag zugeordnet sind.

## <a name="syntax"></a>Syntax

```
bitsadmin /cancel <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Auftrag *mydownloadjob* aus der Übertragungs Warteschlange entfernt.
```
C:\>bitsadmin /cancel myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)