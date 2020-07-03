---
title: Copy-drivergroup
description: Referenz Artikel für "Copy-drivergroup", mit dem eine vorhandene Treiber Gruppe auf dem Server dupliziert wird, einschließlich der Filter, Treiber Pakete und aktivierten/deaktivierten Status.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0aaf6fa5-8b5b-4a1e-ae9b-8b5c6d89f571
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d9be90f065cc76e16b7b45135c60b5206c7bf581
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934078"
---
# <a name="copy-drivergroup"></a>Copy-drivergroup

Dupliziert eine vorhandene Treiber Gruppe auf dem Server, einschließlich der Filter, Treiber Pakete und aktivierten/deaktivierten Status.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Copy-DriverGroup [/Server:<Server name>] /DriverGroup:<Source Group Name> /GroupName:<New Group Name>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[/Server:\<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/DriverGroup:\<Source Group Name>|Gibt den Namen der Quell Treiber Gruppe an.|
|GroupName\<New Group Name>|Gibt den Namen der neuen Treiber Gruppe an.|

## <a name="examples"></a>Beispiele

Geben Sie eine der folgenden Informationen ein, um eine Treiber Gruppe zu kopieren:
```
WDSUTIL /Copy-DriverGroup /Server:MyWdsServer /DriverGroup:PrinterDrivers /GroupName:X86PrinterDrivers
```
```
WDSUTIL /Copy-DriverGroup /DriverGroup:PrinterDrivers /GroupName:ColorPrinterDrivers
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)