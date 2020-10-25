---
title: Copy-drivergroup
description: Referenz Artikel für den Befehl Copy-drivergroup, mit dem eine vorhandene Treiber Gruppe auf dem Server dupliziert wird, einschließlich der Filter, Treiber Pakete und aktivierten/deaktivierten Status.
ms.topic: reference
ms.assetid: 0aaf6fa5-8b5b-4a1e-ae9b-8b5c6d89f571
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 924f6181e424dad88a33f1421098e658275d1fa3
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524915"
---
# <a name="copy-drivergroup"></a>Copy-drivergroup

Dupliziert eine vorhandene Treiber Gruppe auf dem Server, einschließlich der Filter, Treiber Pakete und aktivierten/deaktivierten Status.

## <a name="syntax"></a>Syntax

```
wdsutil /Copy-DriverGroup [/Server:<Server name>] /DriverGroup:<Source Groupname> /GroupName:<New Groupname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| Servers`<Servername>` | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
| /DriverGroup:`<Source Groupname>` | Gibt den Namen der Quell Treiber Gruppe an. |
| GroupName`<New Groupname>` | Gibt den Namen der neuen Treiber Gruppe an. |

## <a name="examples"></a>Beispiele

Um eine Treiber Gruppe zu kopieren, geben Sie Folgendes ein:

```
wdsutil /Copy-DriverGroup /Server:MyWdsServer /DriverGroup:PrinterDrivers /GroupName:X86PrinterDrivers
```

```
wdsutil /Copy-DriverGroup /DriverGroup:PrinterDrivers /GroupName:ColorPrinterDrivers
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
