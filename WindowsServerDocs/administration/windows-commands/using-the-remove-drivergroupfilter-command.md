---
title: Verwenden den Befehl Remove-DriverGroupFilter
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 837bd5d4-c79d-4714-942d-9875bd8e61dc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a546ead7220273955368c582ac1e3f9b3f61c191
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883431"
---
# <a name="using-the-remove-drivergroupfilter-command"></a>Verwenden den Befehl Remove-DriverGroupFilter



Entfernt eine Filterregel aus einer Treibergruppe auf einem Server an.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ DriverGroup:\<Gruppenname >|Gibt den Namen der Gruppe "Treiber".|
|[/ Server:\<Servername >]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollqualifizierten Domänennamen sein. Wenn ein Servername nicht angegeben ist, wird der lokale Server verwendet.|
|[/FilterType:\<FilterType>]|Gibt den Typ des Filters, der aus der Gruppe entfernen. \<FilterType > kann eine der folgenden:</br>**BiosVendor**</br>**BiosVersion**</br>**ChassisType**</br>**Hersteller**</br>**Uuid**</br>**OsVersion**</br>**OsEdition**</br>**OsLanguage**|

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie einen der folgenden Schritte aus, um einen Filter zu entfernen:
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer
```
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /FilterType:OSLanguage
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)