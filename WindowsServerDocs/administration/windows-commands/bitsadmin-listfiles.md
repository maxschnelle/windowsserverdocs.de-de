---
title: bitsadmin listfiles
description: Referenz Artikel für den Befehl bizadmin listFiles, der die Dateien im angegebenen Auftrag auflistet.
ms.topic: article
ms.assetid: ad0d1eaa-3bd8-45e5-8f72-4da7366f0d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a5dcd9092f2d9a8d150496e4cf89595537885d62
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893681"
---
# <a name="bitsadmin-listfiles"></a>bitsadmin listfiles

Listet die Dateien im angegebenen Auftrag auf.

## <a name="syntax"></a>Syntax

```
bitsadmin /listfiles <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie die Liste der Dateien für den Auftrag mit dem Namen *mydownloadjob*ab:

```
bitsadmin /listfiles myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
