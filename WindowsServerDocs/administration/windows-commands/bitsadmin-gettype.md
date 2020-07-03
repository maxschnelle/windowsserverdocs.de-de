---
title: bitsadmin gettype
description: Referenz Artikel für den bizadmin GetType-Befehl, der den Auftragstyp des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c7224add1b503d9ec50e84879a47442c12447e5d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926647"
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

#### <a name="output"></a>Ausgabe

Die zurückgegebenen Ausgabewerte können wie folgt lauten:

| Typ | Beschreibung |
| --------------- | ----------- |
| Download | Der Auftrag ist ein Download. |
| Hochladen | Der Auftrag ist ein Upload. |
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
