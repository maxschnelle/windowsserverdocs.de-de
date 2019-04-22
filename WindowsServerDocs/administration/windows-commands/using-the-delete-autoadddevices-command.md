---
title: Verwenden den Befehl Delete-AutoaddDevices
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 8b3375418c5ce0b02e187e292cac5b168f0de5dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813501"
---
# <a name="using-the-delete-autoadddevices-command"></a>Verwenden den Befehl Delete-AutoaddDevices

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Löscht die Computer, Ausstehend, abgelehnt oder genehmigt, die aus der Datenbank zum automatischen hinzufügen. Diese Datenbank speichert Informationen über diese Computer, auf dem Server.
## <a name="syntax"></a>Syntax
```
wdsutil /delete-AutoaddDevices [/Server:<Server name>] /Devicetype:{PendingDevices | RejectedDevices |ApprovedDevices}
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
|/Devicetype:{PendingDevices &#124; RejectedDevices &#124;ApprovedDevices}|Gibt den Typ des Computers aus der Datenbank zu löschen. Dies kann einen der folgenden drei Typen sein:<br /><br />-   **PendingDevices** enthält alle Computer in der Datenbank, die den Status ausstehend aufweisen.<br />-   **RejectedDevices** , dass Status abgelehnt haben alle Computer in der Datenbank zurückgegeben.<br />-   **ApprovedDevices** werden alle Computer mit dem Status der Genehmigung.|
## <a name="BKMK_examples"></a>Beispiele für
Wenn Sie um alle abgelehnten Computer zu löschen, geben Sie Folgendes ein:
```
wdsutil /delete-AutoaddDevices /Devicetype:RejectedDevices
```
Um alle genehmigten Computern zu löschen, geben Sie Folgendes ein:
```
wdsutil /verbose /delete-AutoaddDevices /Server:MyWDSServer /Devicetype:ApprovedDevices
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Approve-AutoaddDevices](using-the-approve-autoadddevices-command.md)
[mit dem Befehl Get-AutoaddDevices](using-the-get-autoadddevices-command.md) 
 [Mithilfe des Befehls Reject-AutoaddDevices](using-the-reject-autoadddevices-command.md)
