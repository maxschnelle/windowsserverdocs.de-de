---
title: bitsadmin getdisplayname
description: Referenz Artikel für den Befehl bizadmin GetDisplayName, der den anzeigen amen des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b0e768f377b9faa23eb59645cbecdc129f1e573
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923046"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname

Ruft den anzeigen amen des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getdisplayname <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
