---
title: bitsadmin replaceremoteprefix
description: Referenz Artikel für den Befehl bizadmin REPLACEREMOTEPREFIX, der die Remote-URL für alle Dateien im Auftrag von *oldprefix* in *newprefix*ändert, wenn erforderlich.
ms.topic: reference
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 21c1ede5b05a80ba80b1bd470065e914fb353c3c
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89026328"
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
