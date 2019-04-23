---
title: bitsadmin getmodificationtime
description: Windows-Befehle Thema **Bitsadmin Getmodificationtime** -Ruft die letzte des Auftrags Änderung oder Daten erfolgreich übertragen wurde.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e543945e-92c4-491e-8c2d-344f8a3e342d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4257f0ae4868b2f18221ab99268384f778c4bbbe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837021"
---
# <a name="bitsadmin-getmodificationtime"></a>bitsadmin getmodificationtime



Ruft die letzte Änderung des Auftrags wurde oder die Daten wurde erfolgreich übertragen.

## <a name="syntax"></a>Syntax

```
bitsadmin /GetModificationTime <Job>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel ruft den Zeitpunkt der letzten Änderung für den Auftrag mit dem Namen *MyDownloadJob*.
```
C:\>bitsadmin /GetModificationTime myDownloadJob
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)