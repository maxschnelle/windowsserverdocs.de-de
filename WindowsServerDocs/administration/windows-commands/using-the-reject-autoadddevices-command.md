---
title: Ablehnen-AutoAddDevices
description: Windows-Befehls Artikel für ablehnen-AutoAddDevices, bei dem Computer abgelehnt werden, für die die administrative Genehmigung aussteht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea25a4b2-5fad-4360-9c47-c2c9df7ea31f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 39bdddbbc169a0a0810fcc67e95224360858b728
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830653"
---
# <a name="reject-autoadddevices"></a>Ablehnen-AutoAddDevices

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Weist Computer zurück, für die die administrative Genehmigung aussteht. Wenn die Richtlinie zum automatischen hinzufügen aktiviert ist, ist eine administrative Genehmigung erforderlich, bevor unbekannte Computer (die nicht vorab bereitgestellt werden) ein Abbild installieren können. Sie können diese Richtlinie mithilfe der Registerkarte **PXE-Antwort** auf der Seite Server s-Eigenschaften aktivieren.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Reject-AutoaddDevices [/Server:<Server name>] /RequestId:<Request ID or ALL>
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/RequestId: < Anforderungs- &#124; ID alle >|Gibt die Anforderungs-ID an, die dem ausstehenden Computer zugewiesen ist. Geben Sie **alle**ausstehenden Computer an, um alle ausstehenden Computer abzulehnen.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Um einen einzelnen Computer abzulehnen, geben Sie Folgendes ein:
```
wdsutil /Reject-AutoaddDevices /RequestId:12
```
Geben Sie Folgendes ein, um alle Computer abzulehnen:
```
wdsutil /verbose /Reject-AutoaddDevices /Server:MyWDSServer /RequestId:ALL
```
## <a name="additional-references"></a>Weitere Verweise
- Der [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls "genehmigen-AutoAddDevices](using-the-approve-autoadddevices-command.md) "
mithilfe des Befehls " [Delete-AutoAddDevices](using-the-delete-autoadddevices-command.md) "
[mithilfe des Befehls "Get-AutoAddDevices](using-the-get-autoadddevices-command.md) ".
