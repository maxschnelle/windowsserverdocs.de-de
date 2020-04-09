---
title: DELETE-AutoAddDevices
description: Windows-Befehls Artikel für "Delete-AutoAddDevices", mit dem Computer gelöscht werden, die aus der Datenbank zum automatischen Hinzufügen ausstehend, abgelehnt oder genehmigt wurden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8dcaca6a-212e-4c36-98e3-00938eef6b9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 29df0bd92859e9ee0b5b5bedfbd2e66173059cb5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831663"
---
# <a name="delete-autoadddevices"></a>DELETE-AutoAddDevices

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Löscht Computer, die aus der Datenbank zum automatischen Hinzufügen ausstehend, abgelehnt oder genehmigt wurden. In dieser Datenbank werden Informationen zu diesen Computern auf dem-Server gespeichert.

## <a name="syntax"></a>Syntax
```
wdsutil /delete-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices |ApprovedDevices}
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/DeviceType: {pdingdevices &#124; rejecteddevices &#124;approveddevices}|Gibt den Typ des Computers an, der aus der Datenbank gelöscht werden soll. Dies kann einer der folgenden drei Typen sein:<p>-   von " **pdingdevices** " werden alle Computer in der Datenbank mit dem Status "Ausstehend" zurückgegeben.<br />-   **rejecteddevices** gibt alle Computer in der Datenbank zurück, die den Status "abgelehnt" aufweisen.<br />-   **approveddevices** werden alle Computer mit dem Status "genehmigt" zurückgegeben.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
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
[mithilfe des Befehls "genehmigen-AutoAddDevices](using-the-approve-autoadddevices-command.md) "
mithilfe des Befehls " [Get-AutoAddDevices](using-the-get-autoadddevices-command.md) "
[mit dem Befehl "ablehnen-AutoAddDevices](using-the-reject-autoadddevices-command.md) ".
