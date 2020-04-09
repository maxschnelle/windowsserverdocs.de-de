---
title: BI-admin-Cache und ' abtexpirationtime '
description: Windows-Befehls Thema für **bitadmin-Cache und setexpirationtime**, die die Ablaufzeit des Caches festlegen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 00ea6e4e-b707-4b31-88dd-b61a78565c8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bf283a0a8b94fd55c591609e3dcd1d127a2be81a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850883"
---
>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="bitsadmin-cache-and-setexpirationtime"></a>BI-admin-Cache und ' abtexpirationtime '

Legt die Ablaufzeit für den Cache fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /cache /setexpirationtime secs
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Sekunden | Die Anzahl der Sekunden bis zum Ablauf des Caches. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel läuft der Cache in 60 Sekunden ab.

```
C:\>bitsadmin /cache / setexpirationtime 60
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
