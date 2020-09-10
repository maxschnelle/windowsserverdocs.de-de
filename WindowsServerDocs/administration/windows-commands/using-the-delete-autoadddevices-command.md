---
title: DELETE-AutoAddDevices
description: Referenz Artikel zu "Delete-AutoAddDevices", mit dem Computer gelöscht werden, die aus der Datenbank zum automatischen Hinzufügen ausstehend, abgelehnt oder genehmigt wurden.
ms.topic: reference
ms.assetid: 8dcaca6a-212e-4c36-98e3-00938eef6b9c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9137c1f5888f4b60e19e1330feab57d678c3bfd1
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622092"
---
# <a name="delete-autoadddevices"></a>DELETE-AutoAddDevices

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht Computer, die aus der Datenbank zum automatischen Hinzufügen ausstehend, abgelehnt oder genehmigt wurden. In dieser Datenbank werden Informationen zu diesen Computern auf dem-Server gespeichert.

## <a name="syntax"></a>Syntax
```
wdsutil /delete-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices |ApprovedDevices}
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/DeviceType: {pdingdevices &#124; rejecteddevices &#124;approveddevices}|Gibt den Typ des Computers an, der aus der Datenbank gelöscht werden soll. Dies kann einer der folgenden drei Typen sein:<p>-   Mit " **pdingdevices** " werden alle Computer in der Datenbank mit dem Status "Ausstehend" zurückgegeben.<br />-   **Rejecteddevices** gibt alle Computer in der Datenbank zurück, die den Status "abgelehnt" aufweisen.<br />-   **Approveddevices** gibt alle Computer zurück, die den Status "genehmigt" aufweisen.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um alle abgelehnten Computer zu löschen:
```
wdsutil /delete-AutoaddDevices /Devicetype:RejectedDevices
```
Geben Sie Folgendes ein, um alle genehmigten Computer zu löschen:
```
wdsutil /verbose /delete-AutoaddDevices /Server:MyWDSServer /Devicetype:ApprovedDevices
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-approve-autoadddevices-command.md) 
 "genehmigen-AutoAddDevices" [Verwenden des Befehls](using-the-get-autoadddevices-command.md) 
 Get-AutoAddDevices [Verwenden des ablehnen-AutoAddDevices-Befehls](using-the-reject-autoadddevices-command.md)
