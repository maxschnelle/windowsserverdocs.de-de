---
title: bitsadmin gettype
description: Referenz Artikel für den bizadmin GetType-Befehl, der den Auftragstyp des angegebenen Auftrags abruft.
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3f0fe66256e59526b874aaf2ec8ae0193846a1da
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893827"
---
# <a name="bitsadmin-gettype"></a>bitsadmin gettype

Ruft den Auftragstyp des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /gettype <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

#### <a name="output"></a>Output

Die zurückgegebenen Ausgabewerte können wie folgt lauten:

| type | BESCHREIBUNG |
| --------------- | ----------- |
| Download | Der Auftrag ist ein Download. |
| Upload | Der Auftrag ist ein Upload. |
| Upload-Antwort | Der Auftrag ist ein Upload-Antwort-Vorgang. |
| Unknown | Der Auftrag weist einen unbekannten Typ auf. |

## <a name="examples"></a>Beispiele

So rufen Sie den Auftragstyp für den Auftrag mit dem Namen *mydownloadjob*ab

```
bitsadmin /gettype myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
