---
title: Remove-drivergroupfilter
description: Windows-Befehls Thema für Remove-drivergroupfilter, das eine Filterregel aus einer Treiber Gruppe auf einem Server entfernt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 837bd5d4-c79d-4714-942d-9875bd8e61dc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 08914b66c37d327ddef2a50d2f98adcfdbb88ffe
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830493"
---
# <a name="remove-drivergroupfilter"></a>Remove-drivergroupfilter



Entfernt eine Filterregel aus einer Treiber Gruppe auf einem Server.

## <a name="syntax"></a>Syntax

```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:<Group Name> [/Server:<Server name>] /FilterType:<Filter Type>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/DriverGroup:\<Gruppen Name >|Gibt den Namen der Treiber Gruppe an.|
|[/Server:\<Server Name >]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|[/FILTERTYPE:\<FilterType >]|Gibt den Typ des Filters an, der aus der Gruppe entfernt werden soll. \<FilterType > kann eine der folgenden sein:</br>**Biosvendor**</br>**Biosversion**</br>**Chassistype**</br>**Manufacturer**</br>**UUID**</br>**OsVersion**</br>**Odition**</br>**OSLanguage**|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Um einen Filter zu entfernen, geben Sie einen der folgenden Informationen ein:
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer
```
```
WDSUTIL /Remove-DriverGroupFilter /DriverGroup:PrinterDrivers /FilterType:Manufacturer /FilterType:OSLanguage
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)