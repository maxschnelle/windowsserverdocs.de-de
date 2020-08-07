---
title: bitsadmin getreplydata
description: Referenz Artikel für den BITSAdmin getreplydata-Befehl, der die Upload-Antwort-Daten des Servers im Hexadezimal Format für den Auftrag abruft.
ms.topic: article
ms.assetid: 819f97d5-b255-4b2d-9f63-0daa73915434
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ab9f774c7b31576e18de3ec5db9b5a72427ecdaa
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893896"
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

| Parameter | BESCHREIBUNG |
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
