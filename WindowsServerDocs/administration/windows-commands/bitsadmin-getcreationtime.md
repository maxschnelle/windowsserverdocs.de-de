---
title: bitsadmin getcreationtime
description: Windows-Befehle Thema **Bitsadmin Getcreationtime** -Ruft die Uhrzeit der Erstellung für den angegebenen Auftrag ab.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: be409cb5-ce72-41d9-aafa-edd4e230fd14
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d8cc0f02933c6a890ae8bf40361d859ad508b319
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858471"
---
# <a name="bitsadmin-getcreationtime"></a>bitsadmin getcreationtime



Ruft den Zeitpunkt der Erstellung für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetCreationTime <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft den Zeitpunkt der Erstellung des Auftrags namens *MyDownloadJob*.
```
C:\>bitsadmin /GetCreationTime myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)