---
title: bitsadmin replaceremoteprefix
description: Referenz Artikel für den Befehl bizadmin REPLACEREMOTEPREFIX, der die Remote-URL für alle Dateien im Auftrag von *oldprefix* in *newprefix*ändert, wenn erforderlich.
ms.topic: reference
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 83c517a9126a3b78dfc919af5663e939aceee186
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631123"
---
# <a name="bitsadmin-replaceremoteprefix"></a>bitsadmin replaceremoteprefix

Ändert die Remote-URL für alle Dateien im Auftrag bei Bedarf von *oldprefix* in *newprefix*.

## <a name="syntax"></a>Syntax

```
bitsadmin /replaceremoteprefix <job> <oldprefix> <newprefix>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
