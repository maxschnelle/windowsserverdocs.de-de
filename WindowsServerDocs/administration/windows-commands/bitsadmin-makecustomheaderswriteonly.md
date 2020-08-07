---
title: bitsadmin makecustomheaderswriteonly
description: Referenz Artikel für den bizadmin-Befehl makecustomheadersschreiteonly, mit dem die benutzerdefinierten HTTP-Header eines Auftrags schreibgeschützt werden.
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: b1e152ee51f3009a5cc1f5bf1b747e65e86e5e04
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893697"
---
# <a name="bitsadmin-makecustomheaderswriteonly"></a>bitsadmin makecustomheaderswriteonly

Schreiben Sie die benutzerdefinierten HTTP-Header eines Auftrags als schreibgeschützt.

> [!IMPORTANT]
> Diese Aktion kann nicht rückgängig gemacht werden.

## <a name="syntax"></a>Syntax

```
bitsadmin /makecustomheaderswriteonly <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

Zum Schreiben von benutzerdefinierten HTTP-Headern für den Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /makecustomheaderswriteonly myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
