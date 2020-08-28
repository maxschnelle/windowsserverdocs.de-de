---
title: bitsadmin gettype
description: Referenz Artikel für den bizadmin GetType-Befehl, der den Auftragstyp des angegebenen Auftrags abruft.
ms.topic: reference
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6edd13a6647852fd9491254864199895a07ce1f0
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024394"
---
# <a name="bitsadmin-gettype"></a>bitsadmin gettype

Ruft den Auftragstyp des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /gettype <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

#### <a name="output"></a>Output

Die zurückgegebenen Ausgabewerte können wie folgt lauten:

| Typ | BESCHREIBUNG |
| --------------- | ----------- |
| Download | Der Auftrag ist ein Download. |
| Upload | Der Auftrag ist ein Upload. |
| Upload-Antwort | Der Auftrag ist ein Upload-Antwort-Vorgang. |
| Unbekannt | Der Auftrag weist einen unbekannten Typ auf. |

## <a name="examples"></a>Beispiele

So rufen Sie den Auftragstyp für den Auftrag mit dem Namen *mydownloadjob*ab

```
bitsadmin /gettype myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
