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
ms.openlocfilehash: 27cf04e8745aeab5cd1f2ce379c8506be642fea2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381613"
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

# #

[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) Siehe auch