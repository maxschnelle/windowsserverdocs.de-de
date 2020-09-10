---
title: bitsadmin makecustomheaderswriteonly
description: Referenz Artikel für den bizadmin-Befehl makecustomheadersschreiteonly, mit dem die benutzerdefinierten HTTP-Header eines Auftrags schreibgeschützt werden.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 03/01/2019
ms.openlocfilehash: 0eee6cc2fd8c825f02f7e01750be743b10beb73e
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631485"
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
