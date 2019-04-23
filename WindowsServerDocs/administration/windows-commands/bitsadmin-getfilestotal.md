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
ms.openlocfilehash: 21240cfa1f0fa1f8e8fc3d2acf83f5df80812816
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857461"
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

##

[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md) Siehe auch