---
title: bitsadmin getproxybypasslist
description: Referenz Artikel für den Befehl bizadmin getproxybypasslist, der die Proxy Umgehungs Liste für den angegebenen Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 50959be3-7014-4bc9-9a7b-68f1ff94a94a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 67e6e4a54bb8c4929acbbaa47c78e33bab95a283
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926830"
---
# <a name="bitsadmin-getproxybypasslist"></a>bitsadmin getproxybypasslist

Ruft die Proxy Umgehungs Liste für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getproxybypasslist <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

### <a name="remarks"></a>Hinweise

Die Umgehungs Liste enthält die Hostnamen oder IP-Adressen, die nicht über einen Proxy weitergeleitet werden sollen. Die Liste kann enthalten `<local>` , um auf alle Server im gleichen LAN zu verweisen. Die Liste kann ein Semikolon (;) oder durch Leerzeichen voneinander getrennt.

## <a name="examples"></a>Beispiele

Zum Abrufen der Proxy Umgehungs Liste für den Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /getproxybypasslist myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
