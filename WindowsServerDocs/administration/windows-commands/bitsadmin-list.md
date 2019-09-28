---
title: bitsadmin Liste
description: 'Thema Windows-Befehle für die **bitadmin-Liste** : Listet die Übertragungs Aufträge auf, die sich im Besitz des aktuellen Benutzers befinden.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: bd4787f51dc2a7843ff6cf5c4f786658e530ad8f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381088"
---
# <a name="bitsadmin-list"></a>bitsadmin Liste



Listet die Übertragungs Aufträge auf, die sich im Besitz des aktuellen Benutzers befinden.

## <a name="syntax"></a>Syntax

```
bitsadmin /List [/allusers][/verbose]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ALLUSERS|Optional – listet Aufträge für alle Benutzer auf.|
|/Verbose|Optional – stellt ausführliche Informationen zu jedem Auftrag bereit.|

## <a name="remarks"></a>Hinweise

Sie müssen über Administratorrechte verfügen, um den/ALLUSERS-Parameter zu verwenden.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel werden Informationen zu Aufträgen abgerufen, die sich im Besitz des aktuellen Benutzers befinden.
```
C:\>bitsadmin /List 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)