---
title: bitsadmin replaceremoteprefix
description: Windows-Befehls Thema für **bitionadmin REPLACEREMOTEPREFIX** -alle Dateien im Auftrag, deren Remote-URL mit *oldprefix* beginnt, werden so geändert, dass *newprefix*verwendet wird.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ee896a337b571487797967d3ce0bf1f1b17e7507
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380800"
---
# <a name="bitsadmin-replaceremoteprefix"></a>bitsadmin replaceremoteprefix

Alle Dateien im Auftrag, deren Remote-URL mit *oldprefix* beginnt, werden so geändert, dass Sie *newprefix*verwendet.

## <a name="syntax"></a>Syntax

```
bitsadmin /ReplaceRemotePrefix <Job> <OldPrefix> <NewPrefix
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Oldprefix|Bestehendes URL-Präfix|
|Newprefix|Neues URL-Präfix|

## <a name="examples"></a>Beispiele

Im folgenden Beispiel werden alle Dateien in einem Auftrag mit dem Namen *mydownloadjob* geändert, deren Remote-URL mit *http://stageserver* auf *http://prodserver* beginnt.

```
C:\>bitsadmin /ReplaceRemotePrefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>Weitere Informationen

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)