---
title: WDSUTIL DELETE-AutoAddDevices
description: Referenz Artikel zu "WDSUTIL DELETE-AutoAddDevices", mit dem Computer gelöscht werden, die aus der Datenbank zum automatischen Hinzufügen ausstehend, abgelehnt oder genehmigt wurden.
ms.topic: reference
ms.assetid: 8dcaca6a-212e-4c36-98e3-00938eef6b9c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 98c5aa38fd5394d4060cf9eba874d1be5cef845b
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730389"
---
# <a name="wdsutil-delete-autoadddevices"></a>WDSUTIL DELETE-AutoAddDevices

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
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [Befehl "WDSUTIL genehmigen-AutoAddDevices"](wdsutil-approve-autoadddevices.md)
- [Befehl "WDSUTIL Get-AutoAddDevices"](wdsutil-get-autoadddevices.md)
- [WDSUTIL ablehnen-AutoAddDevices-Befehl](wdsutil-reject-autoadddevices.md)
