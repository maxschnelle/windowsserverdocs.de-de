---
title: bitsadmin complete
description: 'Windows-Befehls Thema für **bigsadmin Complete** : schließt den Auftrag ab. Die heruntergeladenen Dateien stehen Ihnen erst zur Verfügung, wenn Sie diesen Schalter verwenden.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5e86677-8f7b-43b3-929e-97706c57e7f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d5a1dc5dbbf2d5b3207b5423f338e0caf4412599
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381819"
---
# <a name="bitsadmin-complete"></a>bitsadmin complete

Schließt den Auftrag ab. Die heruntergeladenen Dateien stehen Ihnen erst zur Verfügung, wenn Sie diesen Schalter verwenden. Verwenden Sie diesen Schalter, nachdem der Auftrag in den übertragenen Zustand wechselt. Andernfalls sind nur die Dateien verfügbar, die erfolgreich übertragen wurden.

## <a name="syntax"></a>Syntax

```
bitsadmin /complete <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele

Wenn der Status des Auftrags übertragen wird, hat Bits erfolgreich alle Dateien im Auftrag übertragen. Die Dateien sind jedoch erst verfügbar, wenn Sie den Schalter **/Complete** verwenden. Wenn für mehrere Aufträge *mydownloadjob* als Name verwendet wird, müssen Sie *mydownloadjob* durch die GUID des Auftrags ersetzen, um den Auftrag eindeutig zu identifizieren.
```
C:\>bitsadmin /complete myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)