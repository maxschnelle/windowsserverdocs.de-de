---
title: bitsadmin getcustomheaders
description: Referenz Artikel für den Befehl "bipadmin getcustomheaders", der die benutzerdefinierten HTTP-Header aus dem Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f0d38d3-e865-4474-81e8-773d65c3d1cc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7482c3eb4b259051ebd63677c70dbaabfb013314
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923075"
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
