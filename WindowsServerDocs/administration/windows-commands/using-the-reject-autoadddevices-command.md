---
title: Mithilfe des Befehls Reject-AutoaddDevices
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ea25a4b2-5fad-4360-9c47-c2c9df7ea31f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: af46aec7c8f02b3600983b66bd1b0ac6f5dd1dcc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852561"
---
# <a name="using-the-reject-autoadddevices-command"></a>Mithilfe des Befehls Reject-AutoaddDevices

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Lehnt die Computer, auf denen administrative Genehmigung aussteht. Wenn die Richtlinie zum automatischen hinzufügen aktiviert ist, ist die Zustimmung des Administrators erforderlich, vor dem unbekannten Computer (diejenigen, die nicht vorab bereitgestellt wurden), ein Abbild installieren können. Sie können diese Richtlinie mithilfe der **PXE-Antwort** s der Seite mit Servereigenschaften auf der Registerkarte.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Reject-AutoaddDevices [/Server:<Server name>] /RequestId:<Request ID or ALL>
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
|/RequestId:<Request ID &#124; ALL>|Gibt an, die Anforderungs-ID, die die ausstehenden Computer zugewiesen. Geben Sie zum Ablehnen aller ausstehenden Computern **alle**.|
## <a name="BKMK_examples"></a>Beispiele für
Um einen einzelnen Computer ablehnen möchten, geben Sie Folgendes ein:
```
wdsutil /Reject-AutoaddDevices /RequestId:12
```
Zum Ablehnen aller Computer, geben Sie Folgendes ein:
```
wdsutil /verbose /Reject-AutoaddDevices /Server:MyWDSServer /RequestId:ALL
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Approve-AutoaddDevices](using-the-approve-autoadddevices-command.md)
[mit dem Befehl Delete-AutoaddDevices](using-the-delete-autoadddevices-command.md) 
 [ Mithilfe des Befehls Get-AutoaddDevices](using-the-get-autoadddevices-command.md)
