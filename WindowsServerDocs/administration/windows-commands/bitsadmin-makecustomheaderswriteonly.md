---
title: bitsadmin makecustomheaderswriteonly
description: Referenz Artikel für den bizadmin-Befehl makecustomheadersschreiteonly, mit dem die benutzerdefinierten HTTP-Header eines Auftrags schreibgeschützt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 3a97054bb9e8156de23e07d18d9806e04c59e967
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926520"
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
