---
title: Verwenden des Befehls "genehmigen-AutoAddDevices"
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 5617837706a778bac2456647f40efd563d861722
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363663"
---
# <a name="using-the-approve-autoadddevices-command"></a>Verwenden des Befehls "genehmigen-AutoAddDevices"

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Genehmigt Computer, für die die administrative Genehmigung aussteht. Wenn die Richtlinie zum automatischen hinzufügen aktiviert ist, ist eine administrative Genehmigung erforderlich, bevor unbekannte Computer (die nicht vorab bereitgestellt werden) ein Abbild installieren können. Sie können diese Richtlinie mithilfe der Registerkarte **PXE-Antwort** auf der Seite Server s-Eigenschaften aktivieren.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Approve-AutoaddDevices [/Server:<Server name>] /RequestId:{<Request ID>| ALL} [/MachineName:<Device name>] [/OU:<DN of OU>] 
[/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] [/WdsClientUnattend:<Relative path>] [/BootImagepath:<Relative path>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn Sie keinen Servernamen angeben, wird der lokale Server verwendet.|
|/RequestId: {Anforderungs- &#124; ID alle}|Gibt die Anforderungs-ID an, die dem ausstehenden Computer zugewiesen ist. Geben Sie **all** an, um alle ausstehenden Computer zu genehmigen.|
|[/MachineName: <Device name>]|Gibt den Namen des hinzu zufügenden Computers an. Sie können diese Option nicht verwenden, wenn Sie alle Computer genehmigen.|
|[/OU: <DN of OU>]|Gibt den Distinguished Name der Organisationseinheit (OU) an, in der das Computer Konto Objekt erstellt werden soll. Zum Beispiel: **OU = MyOU, CN = Test, DC = Domain, DC = com**. Der Standard Speicherort ist der Container des Standard Computers.|
|[/User: < Domäne \ Benutzer &#124; User@Domain >]|Legt Berechtigungen für das Computer Konto Objekt fest, um dem angegebenen Benutzer die erforderlichen Rechte zuzuweisen.|
|[/JoinRights: {joinonly &#124; Full}]|Gibt den Typ der Rechte an, die dem angegebenen Benutzer zugewiesen werden sollen.<br /><br />-   **joinonly** erfordert, dass der Administrator das Computer Konto zurücksetzt, bevor der Benutzer den Computer der Domäne hinzufügen kann.<br />-   **Full** bietet vollen Zugriff auf den Benutzer, der über das Recht zum Hinzufügen des Computers zur Domäne verfügt.|
|[/JoinDomain: {Yes &#124; No}]|Gibt an, ob der Computer während der Installation des Betriebssystems mit der Domäne verknüpft werden soll oder nicht. Der Standardwert ist **Ja**.|
|[/ReferralServer: <Server name>]|Gibt den Namen des Servers an, für den eine Verbindung hergestellt werden soll, um das Netzwerkstart Programm und das Start Abbild mit Trivial File Transfer Protocol (TFTP) herunterzuladen.|
|[/BootProgram: <Relative path>]|Gibt den relativen Pfad vom Ordner RemoteInstall zum Netzwerkstart Programm an, das von diesem Computer empfangen werden soll. Beispiel: **boot\x86\pxeboot.com**.|
|[/WdsClientUnattend: <Relative path>]|Gibt den relativen Pfad vom Ordner RemoteInstall zur Datei für die unbeaufsichtigte Installation an, mit der der Windows-Bereitstellungsdiensteclient automatisiert wird.|
|[/BootImagepath: <Relative path>]|Gibt den relativen Pfad vom Ordner RemoteInstall zum Start Abbild an, das von diesem Computer empfangen werden soll.|
## <a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um den Computer mit der RequestId 12 zu genehmigen:
```
wdsutil /Approve-AutoaddDevices /RequestId:12
```
Geben Sie Folgendes ein, um den Computer mit einer RequestId von 20 zu genehmigen und das Abbild mit den angegebenen Einstellungen bereitzustellen:
```
wdsutil /Approve-AutoaddDevices /RequestId:20 /MachineName:computer1 /OU:"OU=Test,CN=company,DC=Domain,DC=Com" /User:Domain\User1 
/JoinRights:Full /ReferralServer:MyWDSServer /BootProgram:boot\x86\pxeboot.n12 /WdsClientUnattend:WDSClientUnattend\Unattend.xml /BootImagepath:boot\x86\images\boot.wim
```
Geben Sie Folgendes ein, um alle ausstehenden Computer zu genehmigen:
```
wdsutil /verbose /Approve-AutoaddDevices /RequestId:ALL
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
 mithilfe des Befehls "[Delete-AutoAddDevices](using-the-delete-autoadddevices-command.md)" 
 mithilfe des Befehls "[Get-AutoAddDevices](using-the-get-autoadddevices-command.md)" 
 mit dem Befehl "[ablehnen-AutoAddDevices](using-the-reject-autoadddevices-command.md) ".
