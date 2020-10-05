---
title: WDSUTIL ablehnen-AutoAddDevices
description: Referenz Artikel für "WDSUTIL ablehnen-AutoAddDevices", bei dem Computer abgelehnt werden, für die die administrative Genehmigung aussteht.
ms.topic: reference
ms.assetid: ea25a4b2-5fad-4360-9c47-c2c9df7ea31f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2cb970ce6b51933e72f208f6fbcc50bcb7b3164b
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730161"
---
# <a name="wdsutil-reject-autoadddevices"></a>WDSUTIL ablehnen-AutoAddDevices

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
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [Befehl "WDSUTIL genehmigen-AutoAddDevices"](wdsutil-approve-autoadddevices.md)
- [WDSUTIL DELETE-AutoAddDevices-Befehl](wdsutil-delete-autoadddevices.md)
- [Befehl "WDSUTIL Get-AutoAddDevices"](wdsutil-get-autoadddevices.md)
