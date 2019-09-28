---
title: Verwenden des Remove-drivergroup-Befehls
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1fefe9df-9782-433c-8abe-3f1a35e50da2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d22ae4e191c2110a0b8d4cc50c24c2f3ec4a7e60
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362932"
---
# <a name="using-the-remove-drivergroup-command"></a>Verwenden des Remove-drivergroup-Befehls



entfernt eine Treiber Gruppe von einem Server.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Remove-DriverGroup /DriverGroup:<Group Name> [/Server:<Server name>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/DriverGroup: \<gruppenname >|Gibt den Namen der zu entfernenden Treiber Gruppe an.|
|[/Server: \<Server Name >]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|

## <a name="BKMK_examples"></a>Beispiele

Geben Sie eine der folgenden Informationen ein, um eine Treiber Gruppe zu entfernen:
```
WDSUTIL /Remove-DriverGroup /DriverGroup:PrinterDrivers
```
```
WDSUTIL /Remove-DriverGroup /DriverGroup:PrinterDrivers /Server:MyWdsServer
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)