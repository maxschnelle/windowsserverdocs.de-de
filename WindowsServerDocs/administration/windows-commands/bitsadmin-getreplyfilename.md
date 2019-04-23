---
title: bitsadmin getreplyfilename
description: Windows-Befehle Thema **Bitsadmin Getreplyfilename** -Ruft den Pfad der Datei, das die Serverantwort enthält.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85447184-1732-4816-a365-2e3599551bf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 46130700e9ac7e2d0076b368712e5dcb3f02ba2f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862151"
---
# <a name="bitsadmin-getreplyfilename"></a>bitsadmin getreplyfilename

Ruft den Pfad der Datei, die die Serverantwort enthält.

**BITS-Version 1.2 und früher**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetReplyFileName <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="remarks"></a>Hinweise

Gilt nur für den Upload-Antwort-Aufträge.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft den Dateinamen der Antwort für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /GetReplyFileName myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)