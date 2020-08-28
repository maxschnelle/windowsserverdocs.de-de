---
title: bitsadmin cancel
description: Referenz Artikel für den Befehl bizadmin Cancel, der den Auftrag aus der Übertragungs Warteschlange entfernt und alle dem Auftrag zugeordneten temporären Dateien löscht.
ms.topic: reference
ms.assetid: 7374b544-6a16-4d3e-872c-dcf4c02ad89d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da7a858603875affc7acc8bcb60d02451a641690
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024434"
---
# <a name="bitsadmin-cancel"></a>bitsadmin cancel

Entfernt den Auftrag aus der Übertragungs Warteschlange und löscht alle temporären Dateien, die dem Auftrag zugeordnet sind.

## <a name="syntax"></a>Syntax

```
bitsadmin /cancel <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So entfernen Sie den Auftrag " *mydownloadjob* " aus der Übertragungs Warteschlange:

```
bitsadmin /cancel myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
