---
title: bitsadmin makecustomheaderswriteonly
description: Referenz Artikel für den bizadmin-Befehl makecustomheadersschreiteonly, mit dem die benutzerdefinierten HTTP-Header eines Auftrags schreibgeschützt werden.
ms.topic: reference
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 4d31f51c2531079342e223752c626b0b7e8d19f8
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024264"
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

| Parameter | Beschreibung |
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
