---
title: bitsadmin replaceremoteprefix
description: Referenz Thema für den bizadmin REPLACEREMOTEPREFIX-Befehl, der die Remote-URL für alle Dateien im Auftrag von *oldprefix* in *newprefix*ändert, je nach Bedarf.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 745d026513413db799e86df3422d5ee19c89274f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717038"
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

Um die Remote-URL für alle Dateien im Auftrag mit dem Namen *mydownloadjob*zu ändern, von *http://stageserver* auf *http://prodserver*.

```
bitsadmin /replaceremoteprefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>Zusätzliche Informationen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
