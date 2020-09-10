---
title: bitsadmin listfiles
description: Referenz Artikel für den Befehl bizadmin listFiles, der die Dateien im angegebenen Auftrag auflistet.
ms.topic: reference
ms.assetid: ad0d1eaa-3bd8-45e5-8f72-4da7366f0d59
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 702c2d3d3370275373a91aef63aa82f7e84bcf14
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631513"
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
