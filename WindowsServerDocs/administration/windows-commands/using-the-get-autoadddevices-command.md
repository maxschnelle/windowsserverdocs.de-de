---
title: Mithilfe des Befehls Get-AutoaddDevices
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 337c8e76923fe243982ba9c10d18f2e5a5e7d9ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885741"
---
# <a name="using-the-get-autoadddevices-command"></a>Mithilfe des Befehls Get-AutoaddDevices

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt alle Computer, die in der Datenbank zum automatischen hinzufügen auf einem Windows-Bereitstellungsdienste-Server befinden.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices | ApprovedDevices}
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
|/Devicetype:{PendingDevices &#124; RejectedDevices &#124; ApprovedDevices}|Gibt den Typ des Computers zurückgegeben.<br /><br />-   **PendingDevices** enthält alle Computer in der Datenbank, die den Status ausstehend aufweisen.<br />-   **RejectedDevices** , dass Status abgelehnt haben alle Computer in der Datenbank zurückgegeben.<br />-   **ApprovedDevices** , dass der Status genehmigt haben alle Computer in der Datenbank zurückgegeben.|
## <a name="BKMK_examples"></a>Beispiele für
Um alle genehmigten Computern anzuzeigen, geben Sie Folgendes ein:
```
wdsutil /Get-AutoaddDevices /Devicetype:ApprovedDevices
```
Um alle abgelehnten Computer anzuzeigen, geben Sie Folgendes ein:
```
wdsutil /verbose /Get-AutoaddDevices /Devicetype:RejectedDevices /Server:MyWDSServer
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl Delete-AutoaddDevices](using-the-delete-autoadddevices-command.md)
[mithilfe des Befehls Approve-AutoaddDevices](using-the-approve-autoadddevices-command.md) 
 [ Mithilfe des Befehls Reject-AutoaddDevices](using-the-reject-autoadddevices-command.md)
