---
title: bitsadmin getfilestotal
description: 'Windows-Befehls Thema für **bizadmin getfilestotal** : Ruft die Anzahl der Dateien im angegebenen Auftrag ab.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5de113e-f29c-4cd3-9392-0e300018d516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5c28d8e970bd7db896073bf8cddb168ffe9deff
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75946847"
---
# <a name="bitsadmin-getfilestotal"></a>bitsadmin getfilestotal



Ruft die Anzahl der Dateien im angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetFilesTotal <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird die Anzahl der Dateien abgerufen, die im Auftrag mit dem Namen *mydownloadjob*enthalten sind.
```
C:\>bitsadmin /GetFilesTotal myDownloadJob
```

## <a name="see-also"></a>Siehe auch

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
