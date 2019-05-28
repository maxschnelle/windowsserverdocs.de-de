---
title: Mithilfe des Befehls Add-DriverPackage /
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ac9e8d5-63ec-4ce8-86fc-85d28011050b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a7e96391ee8dce0b77f00f51d7cb78ff9b8bf242
ms.sourcegitcommit: 08eba714d3ceb5f2dfb5486d6b990da1aa4dcbdd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2019
ms.locfileid: "65564662"
---
# <a name="using-the-add-driverpackage-command"></a>Mithilfe des Befehls Add-DriverPackage /



Fügt einem Treiberpaket an den Server an.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Add-DriverPackage /InfFile:<Inf File path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>] [/Name:<Friendly Name>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|INF:\<Pfad der Inf-Datei >|Gibt den vollständigen Pfad der INF-Datei hinzufügen.|
|/ Server:\<Servername >|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet.|
|/ Architecture: {X86 | ia64 | x64}|Gibt die Architektur des Treiberpakets.|
|[/ DriverGroup:\<Gruppenname >]|Gibt den Namen der Gruppe "Treiber", der das Paket hinzugefügt werden soll.|
|[/ Name:\<angezeigter Name >]|Gibt den Anzeigenamen für das Treiberpaket an.|

## <a name="BKMK_examples"></a>Beispiele für

Um ein Treiberpaket hinzufügen möchten, geben Sie eine der folgenden:
```
WDSUTIL /verbose /Add-DriverPackage /InfFile:"C:\Temp\Display.inf"
```
```
WDSUTIL /Add-DriverPackage /Server:MyWDSServer /InfFile:"C:\Temp\Display.inf" /Architecture:x86 /DriverGroup:x86Drivers /Name:"Display Driver"
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

