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
ms.openlocfilehash: 848c57736c3530e296cffb970237149b4634de67
ms.sourcegitcommit: d84dc3d037911ad698f5e3e84348b867c5f46ed8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266512"
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

## <a name="examples"></a>Beispiele

Im folgende Beispiel ändert sich alle Dateien im Auftrag mit dem Namen *MyDownloadJob* , deren remote-URL mit beginnt *http://stageserver* zu *http://prodserver* .
```
C:\>bitsadmin /ReplaceRemotePrefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>Weitere Informationen

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)