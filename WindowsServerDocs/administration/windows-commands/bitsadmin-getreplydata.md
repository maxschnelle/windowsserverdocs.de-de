---
title: bitsadmin getreplydata
description: Referenz Artikel für den BITSAdmin getreplydata-Befehl, der die Upload-Antwort-Daten des Servers im Hexadezimal Format für den Auftrag abruft.
ms.topic: reference
ms.assetid: 819f97d5-b255-4b2d-9f63-0daa73915434
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e00a17e4633c9b065d03684cb0c953d1f6db811
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031338"
---
# <a name="bitsadmin-getreplydata"></a>bitsadmin getreplydata

Ruft die Upload-Antwort-Daten des Servers im Hexadezimal Format für den Auftrag ab.

> [!NOTE]
> Dieser Befehl wird von Bits 1,2 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /getreplydata <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

Zum Abrufen der Upload-Antwort-Daten für den Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /getreplydata myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
