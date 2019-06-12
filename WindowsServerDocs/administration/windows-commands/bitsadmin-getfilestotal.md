---
title: bitsadmin getfilestotal
description: Windows-Befehle Thema **Bitsadmin Getfilestotal** -Ruft die Anzahl der Dateien in den angegebenen Auftrag ab.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: b5f6d32b3410b182c510cf40b9def5370efafdc4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435118"
---
# <a name="bitsadmin-getfilestotal"></a>bitsadmin getfilestotal



Ruft die Anzahl der Dateien in den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetFilesTotal <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft die Anzahl der Dateien, die im Auftrag enthaltenen *MyDownloadJob*.
```
C:\>bitsadmin /GetFilesTotal myDownloadJob
```

# #

[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md) Siehe auch