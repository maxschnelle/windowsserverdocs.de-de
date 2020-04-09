---
title: Get-AutoAddDevices
description: Windows-Befehls Artikel für Get-AutoAddDevices, in dem alle Computer angezeigt werden, die sich in der Datenbank zum automatischen Hinzufügen auf einem Windows-Bereitstellungsdiensteserver befinden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 24b4b688-55b0-4bd9-a2f5-7ef4b3dfe2f2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b373fca81769ff1296d0e9a0788fe536c4fc3132
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831183"
---
# <a name="get-autoadddevices"></a>Get-AutoAddDevices

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt alle Computer an, die sich auf einem Windows-Bereitstellungsdiensteserver in der Datenbank automatisch hinzufügen befinden.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices | ApprovedDevices}
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/DeviceType: {pdingdevices &#124; rejecteddevices &#124; approveddevices}|Gibt den Typ des zurück zugebende Computers an.<p>-   von " **pdingdevices** " werden alle Computer in der Datenbank mit dem Status "Ausstehend" zurückgegeben.<br />-   **rejecteddevices** gibt alle Computer in der Datenbank zurück, die den Status "abgelehnt" aufweisen.<br />-   **approveddevices** werden alle Computer in der Datenbank mit dem Status "genehmigt" zurückgegeben.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
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
[mithilfe des Befehls "Delete-AutoAddDevices](using-the-delete-autoadddevices-command.md) "
mithilfe des Befehls " [genehmigen-AutoAddDevices](using-the-approve-autoadddevices-command.md) "
[mit dem Befehl "ablehnen-AutoAddDevices](using-the-reject-autoadddevices-command.md) ".
