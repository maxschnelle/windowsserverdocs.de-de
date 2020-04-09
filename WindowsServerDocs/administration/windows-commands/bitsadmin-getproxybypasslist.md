---
title: bitsadmin getproxybypasslist
description: Windows-Befehls Thema für **bigsadmin getproxybypasslist**, das die Proxy Umgehungs Liste für den angegebenen Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 50959be3-7014-4bc9-9a7b-68f1ff94a94a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9cd81aaef22c4173f198b765246b78b3d3bae136
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850533"
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

## <a name="remarks"></a>Hinweise

Die Umgehungs Liste enthält die Hostnamen oder IP-Adressen, die nicht über einen Proxy weitergeleitet werden sollen. Die Liste kann `<local>` enthalten, um auf alle Server im gleichen LAN zu verweisen. Die Liste kann ein Semikolon (;) oder durch Leerzeichen voneinander getrennt.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Proxy Umgehungs Liste für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getproxybypasslist myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)