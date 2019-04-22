---
title: bitsadmin überwachen
description: Windows-Befehle Thema **Bitsadmin Monitor** -überwacht die Aufträge in der Übertragungswarteschlange, die der aktuelle Benutzer besitzt.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 2c4620d5c8e46cb8bfcb6b9c83261d57781abea5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814591"
---
# <a name="bitsadmin-monitor"></a>bitsadmin überwachen



Überwacht die Aufträge in der Übertragungswarteschlange, die der aktuelle Benutzer besitzt.

## <a name="syntax"></a>Syntax

```
bitsadmin /Monitor [/allusers] [/refresh <Seconds>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|ALLUSERS|Optional – überwacht die Aufträge für alle Benutzer.|
|Aktualisieren|Optional – aktualisiert die Daten in einem Intervall von angegebenen *Sekunden*. Das standardmäßige Aktualisierungsintervall beträgt fünf Sekunden.|

## <a name="remarks"></a>Hinweise

Sie benötigen Administratorrechte, um Sie verwenden die **Allusers** Parameter.

Verwenden Sie STRG + C, um die Aktualisierung zu beenden.

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird die Übertragungswarteschlange für Aufträge im Besitz des aktuellen Benutzers überwacht und aktualisiert die Informationen, alle 60 Sekunden.
```
C:\>bitsadmin /Monitor /refesh 60
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)