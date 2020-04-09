---
title: bitsadmin setdisplayname
description: Windows-Befehls Thema für bizadmin setdisplayname, mit dem der Anzeige Name des angegebenen Auftrags festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 601c5b406132e70fb7d4facb97329f7456002bb4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849543"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname

Legt den anzeigen amen des angegebenen Auftrags fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetDisplayName <Job> <DisplayName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|DisplayName|Text, der für den anzeigen amen des angegebenen Auftrags verwendet wird.|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird der Anzeige Name für den Auftrag mit dem Namen *mydownloadjob* auf *myDownloadJob2*festgelegt.
```
C:\>bitsadmin /SetDisplayName myDownloadJob Download Music Job
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)