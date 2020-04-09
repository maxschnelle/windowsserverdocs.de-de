---
title: BI-admin getmaxdownloadtime
description: Windows-Befehls Thema für **bistiadmin getmaxdownloadtime**, das das Download Timeout in Sekunden abruft.
ms.prod: windows-servemr
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cdce64f6-7125-489d-be3c-4af1dfc8c46a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8b6e4a45da76d5ba39edae151454ad7f28a74085
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850633"
---
# <a name="bitsadmin-getmaxdownloadtime"></a>BI-admin getmaxdownloadtime

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft das Download Timeout in Sekunden ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getmaxdownloadtime <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die maximale Downloadzeit für den Auftrag mit dem Namen *mydownloadjob* in Sekunden abgerufen.

```
C:\>bitsadmin /getmaxdownloadtime myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
