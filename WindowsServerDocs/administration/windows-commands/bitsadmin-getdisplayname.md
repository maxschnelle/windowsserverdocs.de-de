---
title: bitsadmin getdisplayname
description: Referenz Thema für den bizadmin GetDisplayName-Befehl, der den anzeigen amen des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f7c92fdb7c743c1a4c71f076764f5d1da2d95a6f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718030"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname

Ruft den anzeigen amen des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getdisplayname <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie den anzeigen Amen für den Auftrag mit dem Namen *mydownloadjob*ab

```
bitsadmin /getdisplayname myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
