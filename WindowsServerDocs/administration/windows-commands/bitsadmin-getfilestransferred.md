---
title: bitsadmin getfilestransferred
description: Windows-Befehle Thema **Bitsadmin Getfilestransferred** -Ruft die Anzahl der Dateien für den angegebenen Auftrag übertragen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e282815c-938b-4ac0-a09d-9baafb656dcb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5df7f2abfdad6780878b1f00da44c772eecf9fba
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822261"
---
# <a name="bitsadmin-getfilestransferred"></a>bitsadmin getfilestransferred



Ruft die Anzahl der Dateien, die für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetFilesTransferred <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für

Im folgende Beispiel ruft die Anzahl der Dateien, die im Auftrag *MyDownloadJob*.
```
C:\>bitsadmin /GetFilesTransferred myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)