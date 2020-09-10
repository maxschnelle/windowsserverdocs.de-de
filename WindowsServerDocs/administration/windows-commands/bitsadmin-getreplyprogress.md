---
title: bitsadmin getreplyprogress
description: Referenz Artikel für den Befehl "BITSAdmin getreplyprogress", der die Größe und den Fortschritt des Servers "Upload-Reply" abruft.
ms.topic: reference
ms.assetid: 7f7cb0b4-ad95-44fd-a35d-0ddf5fc0b0d0
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7dffacb53044175b8c65d3832863d17d59853b3a
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631691"
---
# <a name="bitsadmin-getreplyprogress"></a>bitsadmin getreplyprogress

Ruft die Größe und den Fortschritt des Server Uploads-Antwort-Vorgangs ab.

> [!NOTE]
> Dieser Befehl wird von Bits 1,2 und früheren Versionen nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /getreplyprogress <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie den Upload-Antwort-Status für den Auftrag *mydownloadjob*ab:

```
bitsadmin /getreplyprogress myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
