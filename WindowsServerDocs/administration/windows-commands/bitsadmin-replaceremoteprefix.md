---
title: bitsadmin replaceremoteprefix
description: Referenz Artikel für den Befehl bizadmin REPLACEREMOTEPREFIX, der die Remote-URL für alle Dateien im Auftrag von *oldprefix* in *newprefix*ändert, wenn erforderlich.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2453ac4c223baa049980578c81d9bc6539baac7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927977"
---
# <a name="bitsadmin-replaceremoteprefix"></a>bitsadmin replaceremoteprefix

Ändert die Remote-URL für alle Dateien im Auftrag bei Bedarf von *oldprefix* in *newprefix*.

## <a name="syntax"></a>Syntax

```
bitsadmin /replaceremoteprefix <job> <oldprefix> <newprefix>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| oldprefix | Vorhandenes URL-Präfix. |
| newprefix | Neues URL-Präfix. |

## <a name="examples"></a>Beispiele

Um die Remote-URL für alle Dateien im Auftrag mit dem Namen *mydownloadjob*zu ändern, von *http://stageserver* auf *http://prodserver* .

```
bitsadmin /replaceremoteprefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>Zusätzliche Informationen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
