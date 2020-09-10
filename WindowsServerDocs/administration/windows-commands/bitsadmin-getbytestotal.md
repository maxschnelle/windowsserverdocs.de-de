---
title: bitsadmin getbytestotal
description: Referenz Artikel für den bizadmin GetBytesTotal-Befehl, der die Größe des angegebenen Auftrags abruft.
ms.topic: reference
ms.assetid: 784e0bfa-7b09-4262-9104-adbc9beb479b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 50b926b8d89e402ef4fd9e58896963edd3c368c9
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89632342"
---
# <a name="bitsadmin-getbytestotal"></a>bitsadmin getbytestotal

Ruft die Größe des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getbytestotal <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
