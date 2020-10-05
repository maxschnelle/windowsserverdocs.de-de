---
title: WDSUTIL Get-AutoAddDevices
description: Referenz Artikel zu "WDSUTIL Get-AutoAddDevices", in dem alle Computer angezeigt werden, die sich in der Datenbank zum automatischen Hinzufügen auf einem Windows-Bereitstellungsdiensteserver befinden.
ms.topic: reference
ms.assetid: 24b4b688-55b0-4bd9-a2f5-7ef4b3dfe2f2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c7d5be85ce29a41714d70d8bdfa11e3afa1661d6
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730284"
---
# <a name="wdsutil-get-autoadddevices"></a>WDSUTIL Get-AutoAddDevices

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt alle Computer an, die sich auf einem Windows-Bereitstellungsdiensteserver in der Datenbank automatisch hinzufügen befinden.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices | ApprovedDevices}
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/DeviceType: {pdingdevices &#124; rejecteddevices &#124; approveddevices}|Gibt den Typ des zurück zugebende Computers an.<p>-   Mit " **pdingdevices** " werden alle Computer in der Datenbank mit dem Status "Ausstehend" zurückgegeben.<br />-   **Rejecteddevices** gibt alle Computer in der Datenbank zurück, die den Status "abgelehnt" aufweisen.<br />-   **Approveddevices** gibt alle Computer in der Datenbank zurück, die den Status "genehmigt" aufweisen.|
## <a name="examples"></a>Beispiele
Wenn Sie alle genehmigten Computer anzeigen möchten, geben Sie Folgendes ein:
```
wdsutil /Get-AutoaddDevices /Devicetype:ApprovedDevices
```
Wenn Sie alle abgelehnten Computer anzeigen möchten, geben Sie Folgendes ein:
```
wdsutil /verbose /Get-AutoaddDevices /Devicetype:RejectedDevices /Server:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL DELETE-AutoAddDevices-Befehl](wdsutil-delete-autoadddevices.md)
- [Befehl "WDSUTIL genehmigen-AutoAddDevices"](wdsutil-approve-autoadddevices.md)
- [WDSUTIL ablehnen-AutoAddDevices-Befehl](wdsutil-reject-autoadddevices.md)
