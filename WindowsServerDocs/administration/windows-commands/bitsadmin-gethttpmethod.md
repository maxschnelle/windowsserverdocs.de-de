---
title: bitsadmin gethttpmethod
description: Referenz Artikel für den bizadmin gethttpmethod-Befehl, der das HTTP-Verb abruft, das mit dem Auftrag verwendet wird.
ms.topic: reference
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 5bbd2509cabea7ae68240a31cee78d9ffd3ac5e0
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033528"
---
# <a name="bitsadmin-gethttpmethod"></a>bitsadmin gethttpmethod

Ruft das HTTP-Verb ab, das mit dem Auftrag verwendet werden soll.

## <a name="syntax"></a>Syntax

```
bitsadmin /gethttpmethod <Job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie das HTTP-Verb für die Verwendung mit dem Auftrag *mydownloadjob*ab:

```
bitsadmin /gethttpmethod myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
