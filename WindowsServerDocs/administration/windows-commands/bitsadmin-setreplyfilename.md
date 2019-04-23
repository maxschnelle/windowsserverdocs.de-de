---
title: bitsadmin setreplyfilename
description: Windows-Befehle Thema **Bitsadmin Setreplyfilename** -Geben Sie den Pfad der Datei, die die Serverantwort enthält.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c26d3342-0533-40b1-a13e-e09678232b25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b86d4137f661e9953d6d397b2fbc890393bbd8a0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852871"
---
# <a name="bitsadmin-setreplyfilename"></a>bitsadmin setreplyfilename

Geben Sie den Pfad der Datei, die die Serverantwort enthält.

**BITS-Version 1.2 und früher**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetReplyFileName <Job> <Path>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|Pfad|Speicherort für die Antwort des Servers|

## <a name="remarks"></a>Hinweise

Gilt nur für den Upload-Antwort-Aufträge.

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird die Antwort Filename Pathfor der Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /SetReplyFileName myDownloadJob c:\reply
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)