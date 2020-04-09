---
title: bitsadmin getowner
description: Windows-Befehls Thema für bizadmin **GetOwner**, der den Besitzer des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5203f84c-a879-4f31-ae3e-7ea74bd63ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3e622c3759c9ec20867c693539c4481c70aa4f26
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850563"
---
# <a name="bitsadmin-getowner"></a>bitsadmin getowner

Zeigt den anzeigen Amen oder die GUID des Besitzers des angegebenen Auftrags an.

## <a name="syntax"></a>Syntax

```
bitsadmin /getowner <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Besitzer des Auftrags mit dem Namen *mydownloadjob*angezeigt.

```
C:\>bitsadmin /getowner myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)