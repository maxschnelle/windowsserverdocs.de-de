---
title: bitsadmin getproxybypasslist
description: Referenz Thema für den bizadmin getproxybypasslist-Befehl, der die Proxy Umgehungs Liste für den angegebenen Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 50959be3-7014-4bc9-9a7b-68f1ff94a94a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3b4f37d09521c28d55104975ed754a10e8df011e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717662"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
