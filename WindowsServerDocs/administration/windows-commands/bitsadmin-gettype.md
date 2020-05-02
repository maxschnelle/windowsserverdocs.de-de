---
title: bitsadmin gettype
description: Referenz Thema für den bizadmin GetType-Befehl, der den Auftragstyp des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 151f9b8e81229a666111ebcd20f060d84160445a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717478"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
