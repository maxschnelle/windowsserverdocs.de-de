---
title: WDSUTIL DELETE-AutoAddDevices
description: Referenz Artikel für den Befehl WDSUTIL DELETE-AutoAddDevices, mit dem Computer gelöscht werden, die aus der Datenbank zum automatischen Hinzufügen ausstehend, abgelehnt oder genehmigt wurden.
ms.topic: reference
ms.assetid: 8dcaca6a-212e-4c36-98e3-00938eef6b9c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 610b57c7db49c5d8cf354502634cf82212d52c19
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524815"
---
# <a name="wdsutil-delete-autoadddevices"></a>WDSUTIL DELETE-AutoAddDevices

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht Computer, die aus der Datenbank zum automatischen Hinzufügen ausstehend, abgelehnt oder genehmigt wurden. In dieser Datenbank werden Informationen zu diesen Computern auf dem-Server gespeichert.

## <a name="syntax"></a>Syntax

```
wdsutil /delete-AutoaddDevices [/Server:<Servername>] /Devicetype:{PendingDevices | RejectedDevices |ApprovedDevices}
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| [/Server:`<Servername>`] | Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
| Den DeviceType "`{PendingDevices|RejectedDevices|ApprovedDevices}` | Gibt den Typ des Computers an, der aus der Datenbank gelöscht werden soll. Bei diesem Typ kann es sich um " **pdingdevices**" handeln, bei der alle Computer in der Datenbank mit dem Status "Ausstehend", " **rejecteddevices**" zurückgegeben werden. Hiermit werden alle Computer in der Datenbank zurückgegeben, die den Status "abgelehnt" aufweisen **, und es**werden alle Computer mit dem Status "genehmigt" zurückgegeben. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle abgelehnten Computer zu löschen:

```
wdsutil /delete-AutoaddDevices /Devicetype:RejectedDevices
```

Geben Sie Folgendes ein, um alle genehmigten Computer zu löschen:

```
wdsutil /verbose /delete-AutoaddDevices /Server:MyWDSServer /Devicetype:ApprovedDevices
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "WDSUTIL genehmigen-AutoAddDevices"](wdsutil-approve-autoadddevices.md)

- [Befehl "WDSUTIL Get-AutoAddDevices"](wdsutil-get-autoadddevices.md)

- [WDSUTIL ablehnen-AutoAddDevices-Befehl](wdsutil-reject-autoadddevices.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
