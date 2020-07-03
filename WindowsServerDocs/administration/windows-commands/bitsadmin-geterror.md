---
title: bitsadmin geterror
description: Referenz Artikel für den bizadmin getError-Befehl, mit dem ausführliche Fehlerinformationen für den angegebenen Auftrag abgerufen werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cbe5bca1-d2dd-4ce6-903f-f85de4a2ec6a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1d729b946df4af33da3a55ff8051c59fbb5d7efe
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928309"
---
# <a name="bitsadmin-geterror"></a>bitsadmin geterror

Ruft ausführliche Fehlerinformationen für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /geterror <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

Zum Abrufen der Fehlerinformationen für den Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /geterror myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
