---
title: bitsadmin getproxybypasslist
description: Referenz Artikel für den Befehl bizadmin getproxybypasslist, der die Proxy Umgehungs Liste für den angegebenen Auftrag abruft.
ms.topic: article
ms.assetid: 50959be3-7014-4bc9-9a7b-68f1ff94a94a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 16cca14a47f086be65764da5441d915d2d28d2db
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894002"
---
# <a name="bitsadmin-getproxybypasslist"></a>bitsadmin getproxybypasslist

Ruft die Proxy Umgehungs Liste für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getproxybypasslist <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

### <a name="remarks"></a>Bemerkungen

Die Umgehungs Liste enthält die Hostnamen oder IP-Adressen, die nicht über einen Proxy weitergeleitet werden sollen. Die Liste kann enthalten `<local>` , um auf alle Server im gleichen LAN zu verweisen. Die Liste kann ein Semikolon (;) oder durch Leerzeichen voneinander getrennt.

## <a name="examples"></a>Beispiele

Zum Abrufen der Proxy Umgehungs Liste für den Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /getproxybypasslist myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
