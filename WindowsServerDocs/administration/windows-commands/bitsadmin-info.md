---
title: bitsadmin Informationen
description: Windows-Befehls Thema für **bizadmin-Informationen**, die zusammenfassende Informationen zum angegebenen Auftrag anzeigen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b9d8b840e39620db01c44001d9cb7d593be2be5d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850343"
---
# <a name="bitsadmin-info"></a>bitsadmin Informationen

Zeigt zusammenfassende Informationen zum angegebenen Auftrag an.

## <a name="syntax"></a>Syntax

```
bitsadmin /info <job> [/verbose]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| /verbose | Optional. Stellt ausführliche Informationen zu jedem Auftrag bereit. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden Informationen zum Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /info myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)