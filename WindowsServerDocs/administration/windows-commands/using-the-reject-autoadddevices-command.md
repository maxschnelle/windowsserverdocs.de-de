---
title: Ablehnen-AutoAddDevices
description: Referenz Artikel zu ablehnen-AutoAddDevices, bei dem Computer abgelehnt werden, für die die administrative Genehmigung aussteht.
ms.topic: article
ms.assetid: ea25a4b2-5fad-4360-9c47-c2c9df7ea31f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7b6b134b89040982325d55822583475fe91044cd
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896354"
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
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-approve-autoadddevices-command.md) 
 "genehmigen-AutoAddDevices" [Verwenden des Befehls](using-the-delete-autoadddevices-command.md) 
 Delete-AutoAddDevices [Verwenden des Befehls Get-AutoAddDevices](using-the-get-autoadddevices-command.md)
