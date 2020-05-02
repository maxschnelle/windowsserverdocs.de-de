---
title: Remove-drivergroupfilter
description: Referenz Thema für Remove-drivergroupfilter, das eine Filterregel aus einer Treiber Gruppe auf einem Server entfernt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 837bd5d4-c79d-4714-942d-9875bd8e61dc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dd6fcbc8f87539ac687927b9e58ed15edb524ef6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720411"
---
# <a name="remove-drivergroupfilter"></a>Remove-drivergroupfilter



Entfernt eine Filterregel aus einer Treiber Gruppe auf einem Server.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type>
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/DriverGroup:\<Gruppen Name>|Gibt den Namen der Treiber Gruppe an.|
|[/Server:\<Server Name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|[/FILTERTYPE:\<FilterType->]|Gibt den Typ des Filters an, der aus der Gruppe entfernt werden soll. \<Ein Filter Type-> kann eines der folgenden sein:</br>**Biosvendor**</br>**Biosversion**</br>**ChassisType**</br>**Hersteller**</br>**UUID**</br>**OsVersion**</br>**Odition**</br>**OSLanguage**|

## <a name="examples"></a>Beispiele

Um einen Filter zu entfernen, geben Sie einen der folgenden Informationen ein:
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer
```
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /FilterType:OSLanguage
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)