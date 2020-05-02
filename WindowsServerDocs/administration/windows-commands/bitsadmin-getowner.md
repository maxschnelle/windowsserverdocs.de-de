---
title: bitsadmin getowner
description: Referenz Thema für den bizadmin-Befehl "GetOwner", der den Besitzer des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5203f84c-a879-4f31-ae3e-7ea74bd63ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2a345ea47232f1f4d6340e1341747c9dad92382b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717717"
---
# <a name="bitsadmin-getowner"></a>bitsadmin getowner

Zeigt den anzeigen Amen oder die GUID des Besitzers des angegebenen Auftrags an.

## <a name="syntax"></a>Syntax

```
bitsadmin /getowner <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So zeigen Sie den Besitzer des Auftrags mit dem Namen *mydownloadjob*an:

```
bitsadmin /getowner myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
