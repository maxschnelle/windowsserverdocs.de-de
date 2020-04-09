---
title: bitsadmin geterror
description: Windows-Befehls Thema für **bizadmin getError**, das ausführliche Fehlerinformationen für den angegebenen Auftrag abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cbe5bca1-d2dd-4ce6-903f-f85de4a2ec6a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c65b072bb190e3e516b917c310942146bb3f3d2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850703"
---
# <a name="bitsadmin-geterror"></a>bitsadmin geterror

Ruft ausführliche Fehlerinformationen für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /geterror <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden die Fehlerinformationen für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /geterror myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)