---
title: bitsadmin Beschreibung
description: Windows-Befehle Thema **Bitsadmin Setdescription** -legt die Beschreibung des angegebenen Auftrags fest.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8e3323c20eebc8ba633ccfd478daa0753e506f46
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830751"
---
# <a name="bitsadmin-setdescription"></a>bitsadmin Beschreibung



Legt die Beschreibung des angegebenen Auftrags fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetDescription <Job> <Description>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|Beschreibung|Text zur Beschreibung des Auftrags verwendet.|

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft die Beschreibung für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /SetDescription myDownloadJob "Music Downloads"
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)