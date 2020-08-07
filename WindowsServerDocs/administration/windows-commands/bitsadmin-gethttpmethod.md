---
title: bitsadmin gethttpmethod
description: Referenz Artikel für den bizadmin gethttpmethod-Befehl, der das HTTP-Verb abruft, das mit dem Auftrag verwendet wird.
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: ea6f1b3896b11bfcc157ea54dc0470786d3dff1f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894222"
---
# <a name="bitsadmin-gethttpmethod"></a>bitsadmin gethttpmethod

Ruft das HTTP-Verb ab, das mit dem Auftrag verwendet werden soll.

## <a name="syntax"></a>Syntax

```
bitsadmin /gethttpmethod <Job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
