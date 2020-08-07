---
title: bitsadmin complete
description: Referenz Artikel für den Befehl "bizadmin Complete", mit dem der Auftrag abgeschlossen wird.
ms.topic: article
ms.assetid: a5e86677-8f7b-43b3-929e-97706c57e7f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 43c3296520b5843643c10d204d89f4f2f2bf98d8
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894601"
---
# <a name="bitsadmin-complete"></a>bitsadmin complete

Schließt den Auftrag ab. Verwenden Sie diesen Schalter, nachdem der Auftrag in den übertragenen Zustand wechselt. Andernfalls sind nur die Dateien verfügbar, die erfolgreich übertragen wurden.

## <a name="syntax"></a>Syntax

```
bitsadmin /complete <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
