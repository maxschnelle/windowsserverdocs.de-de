---
title: Remove-drivergroupfilter
description: Referenz Artikel zu Remove-drivergroupfilter, mit dem eine Filterregel aus einer Treiber Gruppe auf einem Server entfernt wird.
ms.topic: reference
ms.assetid: 837bd5d4-c79d-4714-942d-9875bd8e61dc
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ed154b0ef50ebf36b716ad93d30768739b39ffb5
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730155"
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
|/DriverGroup:\<Group Name>|Gibt den Namen der Treiber Gruppe an.|
|[/Server:\<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|[/FILTERTYPE: \<FilterType> ]|Gibt den Typ des Filters an, der aus der Gruppe entfernt werden soll. \<FilterType> kann eines der folgenden sein:</br>**Biosvendor**</br>**Biosversion**</br>**ChassisType**</br>**Manufacturer**</br>**UUID**</br>**OsVersion**</br>**Odition**</br>**OSLanguage**|

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