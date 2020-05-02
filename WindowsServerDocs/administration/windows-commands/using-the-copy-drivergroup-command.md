---
title: Copy-drivergroup
description: Referenz Thema für "Copy-drivergroup", das eine vorhandene Treiber Gruppe auf dem Server dupliziert, einschließlich der Filter, Treiber Pakete und aktivierten/deaktivierten Status.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0aaf6fa5-8b5b-4a1e-ae9b-8b5c6d89f571
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc157e9ef6d07a45efe2a19221fb3a046b2f65c1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721011"
---
# <a name="copy-drivergroup"></a>Copy-drivergroup

Dupliziert eine vorhandene Treiber Gruppe auf dem Server, einschließlich der Filter, Treiber Pakete und aktivierten/deaktivierten Status.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Copy-DriverGroup [/Server:<Server name>] /DriverGroup:<Source Group Name> /GroupName:<New Group Name>
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|[/Server:\<Server Name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/DriverGroup:\<Quell Gruppen Name>|Gibt den Namen der Quell Treiber Gruppe an.|
|/GroupName:\<neuer Gruppen Name>|Gibt den Namen der neuen Treiber Gruppe an.|

## <a name="examples"></a>Beispiele

Geben Sie eine der folgenden Informationen ein, um eine Treiber Gruppe zu kopieren:
```
WDSUTIL /Copy-DriverGroup /Server:MyWdsServer /DriverGroup:PrinterDrivers /GroupName:X86PrinterDrivers
```
```
WDSUTIL /Copy-DriverGroup /DriverGroup:PrinterDrivers /GroupName:ColorPrinterDrivers
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)