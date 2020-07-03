---
title: Remove-drivergroup
description: Referenz Artikel zu Remove-drivergroup, mit dem eine Treiber Gruppe von einem Server entfernt wird.
ms.prod: windows-server
ms.topic: article
ms.assetid: 1fefe9df-9782-433c-8abe-3f1a35e50da2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: baeeac57c04113e1e9dfc8e9d02fc40518a6689b
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932433"
---
# <a name="remove-drivergroup"></a>Remove-drivergroup

Entfernt eine Treiber Gruppe von einem Server.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Remove-DriverGroup /DriverGroup:<Group Name> [/Server:<Server name>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/DriverGroup:\<Group Name>|Gibt den Namen der zu entfernenden Treiber Gruppe an.|
|[/Server:\<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|

## <a name="examples"></a>Beispiele

Geben Sie eine der folgenden Informationen ein, um eine Treiber Gruppe zu entfernen:
```
WDSUTIL /Remove-DriverGroup /DriverGroup:PrinterDrivers
```
```
WDSUTIL /Remove-DriverGroup /DriverGroup:PrinterDrivers /Server:MyWdsServer
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)