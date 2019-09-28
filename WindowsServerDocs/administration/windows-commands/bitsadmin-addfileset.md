---
title: bitsadmin addfileset
description: Windows-Befehls Thema für **bitadmin ADDFILESET** -fügt dem angegebenen Auftrag eine oder mehrere Dateien hinzu.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 464f2da151d5a7bfffde286e52d9158560d48dcc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381991"
---
# <a name="bitsadmin-addfileset"></a>bitsadmin addfileset

Fügt dem angegebenen Auftrag eine oder mehrere Dateien hinzu.

## <a name="syntax"></a>Syntax

```
bitsadmin /addfileset <Job> <TextFile>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|Textfile|Eine Textdatei, in der jede Zeile einen Remote-und einen lokalen Dateinamen enthält.</br>Hinweis: Die Namen sind durch Leerzeichen getrennt. Zeilen, die mit einem #-Zeichen beginnen, werden als Kommentar behandelt.|

## <a name="BKMK_examples"></a>Beispiele

```
C:\>bitsadmin /addfileset files.txt
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)