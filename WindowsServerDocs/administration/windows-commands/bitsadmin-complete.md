---
title: bitsadmin complete
description: Referenz Thema für den Befehl "bizadmin Complete", mit dem der Auftrag abgeschlossen wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a5e86677-8f7b-43b3-929e-97706c57e7f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6b61f3475afdb0e29e5777940e6426a04fe33e78
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718230"
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

So führen Sie den Auftrag *mydownloadjob* aus, nachdem er `TRANSFERRED` den Status erreicht hat:

```
bitsadmin /complete myDownloadJob
```

Wenn für mehrere Aufträge *mydownloadjob* als Name verwendet wird, müssen Sie die GUID des Auftrags verwenden, um Sie für den Abschluss eindeutig zu identifizieren.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
