---
title: bitsadmin cancel
description: Referenz Artikel für den Befehl bizadmin Cancel, der den Auftrag aus der Übertragungs Warteschlange entfernt und alle dem Auftrag zugeordneten temporären Dateien löscht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7374b544-6a16-4d3e-872c-dcf4c02ad89d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 35173fe8b2e4f3888fa3a365ca25da35b8153eb4
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928360"
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
