---
title: bitsadmin getbytestotal
description: Referenz Thema für den bizadmin GetBytesTotal-Befehl, der die Größe des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 784e0bfa-7b09-4262-9104-adbc9beb479b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f844e1d3689c42a2c533921797d15dbb946b551e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718153"
---
# <a name="bitsadmin-getbytestotal"></a>bitsadmin getbytestotal

Ruft die Größe des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getbytestotal <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die Größe des Auftrags mit dem Namen *mydownloadjob*ab

```
bitsadmin /getbytestotal myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
