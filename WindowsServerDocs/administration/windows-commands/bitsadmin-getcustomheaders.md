---
title: bitsadmin getcustomheaders
description: Referenz Artikel für den Befehl "bipadmin getcustomheaders", der die benutzerdefinierten HTTP-Header aus dem Auftrag abruft.
ms.topic: reference
ms.assetid: 1f0d38d3-e865-4474-81e8-773d65c3d1cc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 09bd1f43e54c6fbca39dffe7c89b978b2b0d2944
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033658"
---
# <a name="bitsadmin-getcustomheaders"></a>bitsadmin getcustomheaders

Ruft die benutzerdefinierten HTTP-Header aus dem Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getcustomheaders <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So erhalten Sie die benutzerdefinierten Header für den Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /getcustomheaders myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
