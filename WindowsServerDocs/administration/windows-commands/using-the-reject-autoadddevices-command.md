---
title: Ablehnen-AutoAddDevices
description: Referenz Thema für ablehnen-AutoAddDevices, bei dem Computer abgelehnt werden, für die die administrative Genehmigung aussteht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea25a4b2-5fad-4360-9c47-c2c9df7ea31f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7e377d4e2d4aecea2e0ba3af023af39ab7695c0a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725923"
---
# <a name="reject-autoadddevices"></a>Ablehnen-AutoAddDevices

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Weist Computer zurück, für die die administrative Genehmigung aussteht. Wenn die Richtlinie zum automatischen hinzufügen aktiviert ist, ist eine administrative Genehmigung erforderlich, bevor unbekannte Computer (die nicht vorab bereitgestellt werden) ein Abbild installieren können. Sie können diese Richtlinie mithilfe der Registerkarte **PXE-Antwort** auf der Seite Server s-Eigenschaften aktivieren.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Reject-AutoaddDevices [/Server:<Server name>] /RequestId:<Request ID or ALL>
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/RequestId: <Anforderungs-ID &#124; alle>|Gibt die Anforderungs-ID an, die dem ausstehenden Computer zugewiesen ist. Geben Sie **alle**ausstehenden Computer an, um alle ausstehenden Computer abzulehnen.|
## <a name="examples"></a>Beispiele
Um einen einzelnen Computer abzulehnen, geben Sie Folgendes ein:
```
wdsutil /Reject-AutoaddDevices /RequestId:12
```
Geben Sie Folgendes ein, um alle Computer abzulehnen:
```
wdsutil /verbose /Reject-AutoaddDevices /Server:MyWDSServer /RequestId:ALL
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
mithilfe des Befehls "[genehmigen-AutoAddDevices](using-the-approve-autoadddevices-command.md)
" mithilfe des Befehls "[Delete-AutoAddDevices](using-the-delete-autoadddevices-command.md)
"[mithilfe des Befehls "Get-AutoAddDevices](using-the-get-autoadddevices-command.md) "
