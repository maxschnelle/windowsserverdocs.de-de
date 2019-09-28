---
title: bitsadmin setreplyfilename
description: 'Windows-Befehls Thema für BITSAdmin-Server-Installations **Dateiname** : Geben Sie den Pfad der Datei an, die die Serverantwort enthält.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: a490b5bc565549d096b6f43f42758f77570fcb26
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380421"
---
# <a name="bitsadmin-setreplyfilename"></a>bitsadmin setreplyfilename

Geben Sie den Pfad der Datei an, die die Serverantwort enthält.

**Bits 1,2 und früher**: Nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetReplyFileName <Job> <Path>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Pfad|Speicherort für die Serverantwort|

## <a name="remarks"></a>Hinweise

Nur für Upload-Antwort-Aufträge gültig.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird der Antwort Dateiname für den Auftrag mit dem Namen *mydownloadjob*festgelegt.
```
C:\>bitsadmin /SetReplyFileName myDownloadJob c:\reply
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)