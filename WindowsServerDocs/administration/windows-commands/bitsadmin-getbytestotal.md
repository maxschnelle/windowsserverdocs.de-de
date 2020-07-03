---
title: bitsadmin getbytestotal
description: Referenz Artikel für den bizadmin GetBytesTotal-Befehl, der die Größe des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 784e0bfa-7b09-4262-9104-adbc9beb479b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cc153ae373152461ed127dde76c934da86be8d6b
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923136"
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

## <a name="examples"></a>Beispiele

So rufen Sie die Größe des Auftrags mit dem Namen *mydownloadjob*ab

```
bitsadmin /getbytestotal myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
