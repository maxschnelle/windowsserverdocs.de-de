---
title: bitsadmin getbytestotal
description: Windows-Befehls Thema für **bizadmin GetBytesTotal**, das die Größe des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 784e0bfa-7b09-4262-9104-adbc9beb479b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 84e3e0311ead0eb79f9247d4f06844ece5f20fa2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850783"
---
# <a name="bitsadmin-getbytestotal"></a>bitsadmin getbytestotal

Ruft die Größe des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getbytestotal <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Größe des Auftrags mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getbytestotal myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)