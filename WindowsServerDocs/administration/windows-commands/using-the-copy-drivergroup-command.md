---
title: Mithilfe des Befehls der kopieren-DriverGroup
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0aaf6fa5-8b5b-4a1e-ae9b-8b5c6d89f571
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68d9c6f4ca78991bb4c286042a6172211161dd1e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842081"
---
# <a name="using-the-copy-drivergroup-command"></a>Mithilfe des Befehls der kopieren-DriverGroup



Dupliziert die vorhandene Treibergruppe auf dem Server, einschließlich Filter, Treiberpakete und aktivierten/deaktivierten Status.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Copy-DriverGroup [/Server:<Server name>] /DriverGroup:<Source Group Name> /GroupName:<New Group Name>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[/ Server:\<Servername >]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet.|
|/ DriverGroup:\<Quellgruppe-Name >|Gibt den Namen der Treiber Quellgruppe.|
|/ GroupName:\<neuen Gruppennamen ein >|Gibt den Namen der neuen Gruppe "Treiber".|

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie eine der folgenden Schritte aus, um eine Treibergruppe zu kopieren:
```
WDSUTIL /Copy-DriverGroup /Server:MyWdsServer /DriverGroup:PrinterDrivers /GroupName:X86PrinterDrivers
```
```
WDSUTIL /Copy-DriverGroup /DriverGroup:PrinterDrivers /GroupName:ColorPrinterDrivers
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)