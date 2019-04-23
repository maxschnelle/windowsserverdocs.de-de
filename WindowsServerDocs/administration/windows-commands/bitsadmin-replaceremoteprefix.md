---
title: bitsadmin replaceremoteprefix
description: Windows-Befehle Thema **Bitsadmin Replaceremoteprefix** -alle Dateien im Auftrag, deren remote-URL beginnt mit *OldPrefix* geändert werden, um verwenden *NewPrefix*.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 3d3eba4f62842fa7f862cd4eaea6830e6a08397a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868131"
---
# <a name="bitsadmin-replaceremoteprefix"></a>bitsadmin replaceremoteprefix



Alle Dateien im Auftrag, deren remote-URL beginnt mit *OldPrefix* geändert werden, um verwenden *NewPrefix*.

## <a name="syntax"></a>Syntax

```
bitsadmin /ReplaceRemotePrefix <Job> <OldPrefix> <NewPrefix
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|OldPrefix|Vorhandene URL-Präfix|
|NewPrefix|Neue URL-Präfix|

## <a name="BKMK_examples"></a>Beispiele für

Im folgende Beispiel ändert sich alle Dateien im Auftrag mit dem Namen *MyDownloadJob* , deren remote-URL mit beginnt *http://stageserver* zu *http://prodserver*.
```
C:\>bitsadmin /ReplaceRemotePrefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>Weitere Informationen

[Befehlszeilensyntax](command-line-syntax-key.md)