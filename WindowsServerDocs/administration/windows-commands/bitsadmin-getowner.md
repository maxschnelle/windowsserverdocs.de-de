---
title: bitsadmin getowner
description: Referenz Artikel für den Befehl "bizadmin GetOwner", der den Besitzer des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5203f84c-a879-4f31-ae3e-7ea74bd63ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f530952e510fdff1a30dfd7c6081e112d841f401
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926892"
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

## <a name="examples"></a>Beispiele

So zeigen Sie den Besitzer des Auftrags mit dem Namen *mydownloadjob*an:

```
bitsadmin /getowner myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
