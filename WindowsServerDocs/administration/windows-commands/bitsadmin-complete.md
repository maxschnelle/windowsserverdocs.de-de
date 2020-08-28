---
title: bitsadmin complete
description: Referenz Artikel für den Befehl "bizadmin Complete", mit dem der Auftrag abgeschlossen wird.
ms.topic: reference
ms.assetid: a5e86677-8f7b-43b3-929e-97706c57e7f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c21cd7919d49b2ac68c665dfd7043cbe55937e45
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89026688"
---
# <a name="bitsadmin-complete"></a>bitsadmin complete

Schließt den Auftrag ab. Verwenden Sie diesen Schalter, nachdem der Auftrag in den übertragenen Zustand wechselt. Andernfalls sind nur die Dateien verfügbar, die erfolgreich übertragen wurden.

## <a name="syntax"></a>Syntax

```
bitsadmin /complete <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="example"></a>Beispiel

So führen Sie den Auftrag *mydownloadjob* aus, nachdem er den Status erreicht hat `TRANSFERRED` :

```
bitsadmin /complete myDownloadJob
```

Wenn für mehrere Aufträge *mydownloadjob* als Name verwendet wird, müssen Sie die GUID des Auftrags verwenden, um Sie für den Abschluss eindeutig zu identifizieren.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
