---
title: Bitsadmin getpriority
description: Windows-Befehle Thema **Bitsadmin Getpriority** -Ruft die Priorität des angegebenen Auftrags.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 6be2461ed87b75144367b1bd74376381e4674b66
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841441"
---
# <a name="bitsadmin-getpriority"></a>Bitsadmin getpriority

Ruft die Priorität des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetPriority <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="remarks"></a>Hinweise

Die Priorität ist entweder **VORDERGRUND**, **hohe**, **NORMAL**, **niedrig**, oder **unbekannte**.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft die Priorität für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /GetPriority myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)
