---
title: Mithilfe des Befehls genehmigen-AutoaddDevices
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d76e8d3-ab35-429c-be7b-904f95d0782d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ce9824c45a00ccb9f1f9e357c7e3d36b2857f69
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886821"
---
# <a name="using-the-approve-autoadddevices-command"></a>Mithilfe des Befehls genehmigen-AutoaddDevices

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Genehmigt, Computer, auf denen administrative Genehmigung aussteht. Wenn die Richtlinie zum automatischen hinzufügen aktiviert ist, ist die Zustimmung des Administrators erforderlich, vor dem unbekannten Computer (diejenigen, die nicht vorab bereitgestellt wurden), ein Abbild installieren können. Sie können diese Richtlinie mithilfe der **PXE-Antwort** s der Seite mit Servereigenschaften auf der Registerkarte.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Approve-AutoaddDevices [/Server:<Server name>] /RequestId:{<Request ID>| ALL} [/MachineName:<Device name>] [/OU:<DN of OU>] 
[/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] [/WdsClientUnattend:<Relative path>] [/BootImagepath:<Relative path>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn Sie keinen Servernamen angeben, wird der lokale Server verwendet.|
|/RequestId:{Request ID &#124; ALL}|Gibt an, die Anforderungs-ID, die die ausstehenden Computer zugewiesen. Geben Sie **alle** alle ausstehenden Computer genehmigen.|
|[/MachineName:<Device name>]|Gibt den Namen des Computers hinzugefügt werden. Diese Option verwenden nicht, wenn alle Computer genehmigen.|
|[/OU:<DN of OU>]|Gibt den distinguished Name der Organisationseinheit (OU), in dem das Computerkontoobjekt erstellt werden soll. Zum Beispiel: **OU = MyOU, CN = Test, DC = Domain, DC = com**. Der Standardspeicherort ist der Container für die Standard-Computer.|
|[/User:<Domain\User &#124; User@Domain>]|Legt Berechtigungen für das Computerkontoobjekt dem angegebenen Benutzer die erforderlichen Rechte zuweisen.|
|[/JoinRights:{JoinOnly &#124; Full}]|Gibt den Typ der Rechte für den angegebenen Benutzer zugewiesen werden.<br /><br />-   **JoinOnly** muss der Administrator das Computerkonto zurückgesetzt werden, bevor der Benutzer den Computer der Domäne beitreten kann.<br />-   **Vollständige** erhalten Sie Vollzugriff für den Benutzer das Recht zum Beitritt zur Domäne gehört.|
|[/JoinDomain:{Yes &#124; No}]|Gibt an, und zwar unabhängig davon, ob der Computer der Domäne als dieses Computerkonto während Betriebssysteminstallation hinzugefügt werden soll. Der Standardwert ist **Ja**.|
|[/ReferralServer:<Server name>]|Gibt den Namen des Servers kontaktiert werden, um das Netzwerk-Startabbild an Programm und den Start mit Trivial File Transfer Protocol (Tftp) herunterzuladen.|
|[/BootProgram:<Relative path>]|Gibt an, der relative Pfad vom Ordner "RemoteInstall", um das Netzwerkstartprogramm an, dem diesem Computer erhalten soll. Zum Beispiel: **boot\x86\pxeboot.com**.|
|[/WdsClientUnattend:<Relative path>]|Gibt an, der relative Pfad vom Ordner "RemoteInstall" zur Datei für die unbeaufsichtigte Installation, die den Windows-Bereitstellungsdiensteclient automatisiert.|
|[/BootImagepath:<Relative path>]|Gibt an, der relative Pfad vom Ordner "RemoteInstall" für das Startimage, das diesem Computer erhalten soll.|
## <a name="BKMK_examples"></a>Beispiele für
So genehmigen Sie den Computer mit einem Anforderungs-ID von 12, geben Sie Folgendes ein:
```
wdsutil /Approve-AutoaddDevices /RequestId:12
```
Um Computer mit einem Anforderungs-ID 20 genehmigen und Bereitstellen des Abbilds mit den angegebenen Einstellungen, geben Sie Folgendes ein:
```
wdsutil /Approve-AutoaddDevices /RequestId:20 /MachineName:computer1 /OU:"OU=Test,CN=company,DC=Domain,DC=Com" /User:Domain\User1 
/JoinRights:Full /ReferralServer:MyWDSServer /BootProgram:boot\x86\pxeboot.n12 /WdsClientUnattend:WDSClientUnattend\Unattend.xml /BootImagepath:boot\x86\images\boot.wim
```
So genehmigen Sie alle ausstehenden Computer, geben Sie Folgendes ein:
```
wdsutil /verbose /Approve-AutoaddDevices /RequestId:ALL
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl Delete-AutoaddDevices](using-the-delete-autoadddevices-command.md)
[mit dem Befehl Get-AutoaddDevices](using-the-get-autoadddevices-command.md) 
 [Mithilfe des Befehls Reject-AutoaddDevices](using-the-reject-autoadddevices-command.md)
