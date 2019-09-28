---
title: bitsadmin überwachen
description: 'Windows-Befehls Thema für den **bitadmin-Monitor** : überwacht Aufträge in der Übertragungs Warteschlange, die der aktuelle Benutzer besitzt.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2c424d27-e011-49c2-b579-a2c235467c39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fe4963349c7e17fc77500b5adfceafc48a20ac5f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381217"
---
# <a name="bitsadmin-monitor"></a>bitsadmin überwachen



Überwacht Aufträge in der Übertragungs Warteschlange, die der aktuelle Benutzer besitzt.

## <a name="syntax"></a>Syntax

```
bitsadmin /Monitor [/allusers] [/refresh <Seconds>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|ALLUSERS|Optional – überwacht Aufträge für alle Benutzer.|
|Aktualisieren|Optional – aktualisiert die Daten in einem durch *Sekunden*angegebenen Intervall. Das Standard Aktualisierungs Intervall beträgt 5 Sekunden.|

## <a name="remarks"></a>Hinweise

Sie müssen über Administratorrechte verfügen, um den **ALLUSERS** -Parameter zu verwenden.

Verwenden Sie STRG + C, um die Aktualisierung zu unterbinden.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird die Übertragungs Warteschlange für Aufträge überwacht, die im Besitz des aktuellen Benutzers sind, und die Informationen werden alle 60 Sekunden aktualisiert.
```
C:\>bitsadmin /Monitor /refesh 60
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)