---
title: bitsadmin addfileset
description: Windows-Befehle Thema **Bitsadmin Addfileset** – der angegebene Auftrag ein oder mehrere Dateien hinzugefügt.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: f8f6ff32dfa6042272c68647477d77183ce9cb76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889441"
---
# <a name="bitsadmin-addfileset"></a>bitsadmin addfileset

Fügt eine oder mehrere Dateien zum angegebenen Auftrag hinzu.

## <a name="syntax"></a>Syntax

```
bitsadmin /addfileset <Job> <TextFile>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|TextFile|Eine Textdatei, die jede, die Zeile, deren einer und einen lokalen Dateinamen enthält.</br>Hinweis: Die Namen sind durch Leerzeichen getrennt. Zeilen, die mit dem Zeichen # beginnen, werden als Kommentar behandelt.|

## <a name="BKMK_examples"></a>Beispiele für

```
C:\>bitsadmin /addfileset files.txt
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)