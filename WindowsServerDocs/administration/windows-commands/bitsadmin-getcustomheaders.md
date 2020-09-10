---
title: bitsadmin getcustomheaders
description: Referenz Artikel für den Befehl "bipadmin getcustomheaders", der die benutzerdefinierten HTTP-Header aus dem Auftrag abruft.
ms.topic: reference
ms.assetid: 1f0d38d3-e865-4474-81e8-773d65c3d1cc
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ec061c9e7f195d463525031bcbefc97913d69083
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632198"
---
# <a name="bitsadmin-getcustomheaders"></a>bitsadmin getcustomheaders

Ruft die benutzerdefinierten HTTP-Header aus dem Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getcustomheaders <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
