---
title: bitsadmin getreplydata
description: Referenz Artikel für den BITSAdmin getreplydata-Befehl, der die Upload-Antwort-Daten des Servers im Hexadezimal Format für den Auftrag abruft.
ms.topic: reference
ms.assetid: 819f97d5-b255-4b2d-9f63-0daa73915434
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a15dc59d9487ed928954f8d5cbd47828c2b58291
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631723"
---
# <a name="bitsadmin-getreplydata"></a>bitsadmin getreplydata

Ruft die Upload-Antwort-Daten des Servers im Hexadezimal Format für den Auftrag ab.

> [!NOTE]
> Dieser Befehl wird von Bits 1,2 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /getreplydata <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

Zum Abrufen der Upload-Antwort-Daten für den Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /getreplydata myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
