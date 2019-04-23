---
title: bitsadmin Liste
description: Windows-Befehle Thema **Bitsadmin Liste** -Listet die Übertragungsaufträge, die im Besitz des aktuellen Benutzers.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f0b88001b9c4ae01b57006ffeef66dec0348ca77
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873861"
---
# <a name="bitsadmin-list"></a>bitsadmin Liste



Listet die Übertragungsaufträge, die im Besitz des aktuellen Benutzers.

## <a name="syntax"></a>Syntax

```
bitsadmin /List [/allusers][/verbose]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/Allusers|Optional – Listet die Aufträge für alle Benutzer|
|/ Verbose|Optional: enthält ausführliche Informationen für jeden Auftrag.|

## <a name="remarks"></a>Hinweise

Sie benötigen Administratorrechte, um den /allusers-Parameter verwenden

## <a name="BKMK_examples"></a>Beispiele für

Im folgende Beispiel ruft Informationen zu den Aufträgen, die im Besitz des aktuellen Benutzers ab.
```
C:\>bitsadmin /List 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)