---
title: bitsadmin setreplyfilename
description: Windows-Befehls Thema für BITSAdmin * treplyfilename, das den Pfad der Datei angibt, in der die Serverantwort enthalten ist.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c26d3342-0533-40b1-a13e-e09678232b25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fd45174a7deac89cc943fb19d544e372c0198139
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849183"
---
# <a name="bitsadmin-setreplyfilename"></a>bitsadmin setreplyfilename

Gibt den Pfad der Datei an, die die Serverantwort enthält.

**Bits 1,2 und früher**: nicht unterstützt.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetReplyFileName <Job> <Path>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Path|Speicherort für die Serverantwort|

## <a name="remarks"></a>Hinweise

Nur für Upload-Antwort-Aufträge gültig.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Antwort Dateiname für den Auftrag mit dem Namen *mydownloadjob*festgelegt.
```
C:\>bitsadmin /SetReplyFileName myDownloadJob c:\reply
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)