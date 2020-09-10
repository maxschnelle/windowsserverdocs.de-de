---
title: bitsadmin complete
description: Referenz Artikel für den Befehl "bizadmin Complete", mit dem der Auftrag abgeschlossen wird.
ms.topic: reference
ms.assetid: a5e86677-8f7b-43b3-929e-97706c57e7f1
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 88e8ac3920adb80dcc453317fbffe5fd661811fb
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632380"
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
