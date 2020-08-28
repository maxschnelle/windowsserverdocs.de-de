---
title: Get-AutoAddDevices
description: Referenz Artikel zu Get-AutoAddDevices, in dem alle Computer angezeigt werden, die sich in der Datenbank zum automatischen Hinzufügen auf einem Windows-Bereitstellungsdiensteserver befinden.
ms.topic: reference
ms.assetid: 24b4b688-55b0-4bd9-a2f5-7ef4b3dfe2f2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f449ddb58bb4e5f28a3cee02e9c769d363baf3b7
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89035898"
---
# <a name="get-autoadddevices"></a>Get-AutoAddDevices

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt alle Computer an, die sich auf einem Windows-Bereitstellungsdiensteserver in der Datenbank automatisch hinzufügen befinden.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices | ApprovedDevices}
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
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
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-delete-autoadddevices-command.md) 
 Delete-AutoAddDevices [Verwenden des Befehls](using-the-approve-autoadddevices-command.md) 
 "genehmigen-AutoAddDevices" [Verwenden des ablehnen-AutoAddDevices-Befehls](using-the-reject-autoadddevices-command.md)
