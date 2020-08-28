---
title: bitsadmin getvalidationstate
description: Referenz Artikel für den Befehl BITSAdmin getvalidationstate, der den Status der Inhalts Überprüfung der angegebenen Datei innerhalb des Auftrags meldet.
ms.topic: reference
ms.assetid: 6ada3f1f-9967-4262-9d22-ed641e23f516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 173bbaad6508ec3ae8100232fda598fe7a422296
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89028638"
---
# <a name="bitsadmin-getvalidationstate"></a>bitsadmin getvalidationstate

Meldet den Status der Inhalts Überprüfung der angegebenen Datei innerhalb des Auftrags.

## <a name="syntax"></a>Syntax

```
bitsadmin /getvalidationstate <job> <file_index>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| file_index | Beginnt bei 0. |

## <a name="examples"></a>Beispiele

So rufen Sie den Status der Inhalts Überprüfung der Datei 2 innerhalb des Auftrags mit dem Namen *mydownloadjob*ab

```
bitsadmin /getvalidationstate myDownloadJob 1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
