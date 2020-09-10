---
title: bitsadmin getvalidationstate
description: Referenz Artikel für den Befehl BITSAdmin getvalidationstate, der den Status der Inhalts Überprüfung der angegebenen Datei innerhalb des Auftrags meldet.
ms.topic: reference
ms.assetid: 6ada3f1f-9967-4262-9d22-ed641e23f516
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5f85f006efa18baa95a491b84e365e707cdf225c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631554"
---
# <a name="bitsadmin-getvalidationstate"></a>bitsadmin getvalidationstate

Meldet den Status der Inhalts Überprüfung der angegebenen Datei innerhalb des Auftrags.

## <a name="syntax"></a>Syntax

```
bitsadmin /getvalidationstate <job> <file_index>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
