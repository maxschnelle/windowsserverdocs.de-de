---
title: Verwenden des Befehls Get-AutoAddDevices
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24b4b688-55b0-4bd9-a2f5-7ef4b3dfe2f2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fa30a8ebd73164dc3d8ab267c3deb0739aa4b700
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363250"
---
# <a name="using-the-get-autoadddevices-command"></a>Verwenden des Befehls Get-AutoAddDevices

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt alle Computer an, die sich auf einem Windows-Bereitstellungsdiensteserver in der Datenbank automatisch hinzufügen befinden.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices | ApprovedDevices}
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/DeviceType: {pdingdevices &#124; rejecteddevices &#124; approveddevices}|Gibt den Typ des zurück zugebende Computers an.<br /><br />-   von " **pdingdevices** " werden alle Computer in der Datenbank mit dem Status "Ausstehend" zurückgegeben.<br />-   **rejecteddevices** gibt alle Computer in der Datenbank zurück, die den Status "abgelehnt" aufweisen.<br />-   **approveddevices** werden alle Computer in der Datenbank mit dem Status "genehmigt" zurückgegeben.|
## <a name="BKMK_examples"></a>Beispiele
Wenn Sie alle genehmigten Computer anzeigen möchten, geben Sie Folgendes ein:
```
wdsutil /Get-AutoaddDevices /Devicetype:ApprovedDevices
```
Wenn Sie alle abgelehnten Computer anzeigen möchten, geben Sie Folgendes ein:
```
wdsutil /verbose /Get-AutoaddDevices /Devicetype:RejectedDevices /Server:MyWDSServer
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls "Delete-AutoAddDevices](using-the-delete-autoadddevices-command.md) "
mithilfe des Befehls " [genehmigen-AutoAddDevices](using-the-approve-autoadddevices-command.md) "
[mit dem Befehl "ablehnen-AutoAddDevices](using-the-reject-autoadddevices-command.md) ".
