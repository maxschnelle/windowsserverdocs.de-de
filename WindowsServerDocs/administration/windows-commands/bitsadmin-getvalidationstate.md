---
title: bitsadmin getvalidationstate
description: Referenz Artikel für den Befehl BITSAdmin getvalidationstate, der den Status der Inhalts Überprüfung der angegebenen Datei innerhalb des Auftrags meldet.
ms.topic: article
ms.assetid: 6ada3f1f-9967-4262-9d22-ed641e23f516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b44fd90e2a35f5daf382cf506f7f68ae3c3ff1d9
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893812"
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
