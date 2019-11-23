---
title: Verwenden des Befehls Delete-AutoAddDevices
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8dcaca6a-212e-4c36-98e3-00938eef6b9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5e914506f731685b17117b359359f60ea91992dc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363545"
---
# <a name="using-the-delete-autoadddevices-command"></a>Verwenden des Befehls Delete-AutoAddDevices

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

löscht Computer, die aus der Datenbank zum automatischen Hinzufügen ausstehend, abgelehnt oder genehmigt wurden. In dieser Datenbank werden Informationen zu diesen Computern auf dem-Server gespeichert.
## <a name="syntax"></a>Syntax
```
wdsutil /delete-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices |ApprovedDevices}
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/DeviceType: {pdingdevices &#124; rejecteddevices &#124;approveddevices}|Gibt den Typ des Computers an, der aus der Datenbank gelöscht werden soll. Dies kann einer der folgenden drei Typen sein:<br /><br />-   von " **pdingdevices** " werden alle Computer in der Datenbank mit dem Status "Ausstehend" zurückgegeben.<br />-   **rejecteddevices** gibt alle Computer in der Datenbank zurück, die den Status "abgelehnt" aufweisen.<br />-   **approveddevices** werden alle Computer mit dem Status "genehmigt" zurückgegeben.|
## <a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um alle abgelehnten Computer zu löschen:
```
wdsutil /delete-AutoaddDevices /Devicetype:RejectedDevices
```
Geben Sie Folgendes ein, um alle genehmigten Computer zu löschen:
```
wdsutil /verbose /delete-AutoaddDevices /Server:MyWDSServer /Devicetype:ApprovedDevices
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls "genehmigen-AutoAddDevices](using-the-approve-autoadddevices-command.md) "
mithilfe des Befehls " [Get-AutoAddDevices](using-the-get-autoadddevices-command.md) "
[mit dem Befehl "ablehnen-AutoAddDevices](using-the-reject-autoadddevices-command.md) ".
