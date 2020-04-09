---
title: bitsadmin getfilestotal
description: Windows-Befehls Thema für **bizadmin getfilestotal**, das die Anzahl der Dateien im angegebenen Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c5de113e-f29c-4cd3-9392-0e300018d516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bad42a8bef57ca4c4a1411a12f20979e4a95d178
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850683"
---
# <a name="bitsadmin-getfilestotal"></a>bitsadmin getfilestotal

Ruft die Anzahl der Dateien im angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getfilestotal <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Anzahl der Dateien abgerufen, die im Auftrag mit dem Namen *mydownloadjob*enthalten sind.

```
C:\>bitsadmin /getfilestotal myDownloadJob
```

## <a name="see-also"></a>Weitere Informationen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
