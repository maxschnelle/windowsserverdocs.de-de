---
title: WDSUTIL genehmigen-AutoAddDevices
description: Referenz Artikel zu "WDSUTIL genehmigen-AutoAddDevices", mit dem Computer genehmigt werden, für die die administrative Genehmigung aussteht.
ms.topic: reference
ms.assetid: 8d76e8d3-ab35-429c-be7b-904f95d0782d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 30074d7b92898e579bbd0cc8f963fc3d8b56c59a
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730413"
---
# <a name="wdsutil-approve-autoadddevices"></a>WDSUTIL genehmigen-AutoAddDevices

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Genehmigt Computer, für die die administrative Genehmigung aussteht. Wenn die Richtlinie zum automatischen hinzufügen aktiviert ist, ist eine administrative Genehmigung erforderlich, bevor unbekannte Computer (die nicht vorab bereitgestellt werden) ein Abbild installieren können. Sie können diese Richtlinie mithilfe der Registerkarte **PXE-Antwort** auf der Seite Server s-Eigenschaften aktivieren.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Approve-AutoaddDevices [/Server:<Server name>] /RequestId:{<Request ID>| ALL} [/MachineName:<Device name>] [/OU:<DN of OU>]
[/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] [/WdsClientUnattend:<Relative path>] [/BootImagepath:<Relative path>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn Sie keinen Servernamen angeben, wird der lokale Server verwendet.|
|/RequestId: {Anforderungs-ID &#124; alle}|Gibt die Anforderungs-ID an, die dem ausstehenden Computer zugewiesen ist. Geben Sie **all** an, um alle ausstehenden Computer zu genehmigen.|
|[/MachineName: <Device name> ]|Gibt den Namen des hinzu zufügenden Computers an. Sie können diese Option nicht verwenden, wenn Sie alle Computer genehmigen.|
|[/Ou: <DN of OU> ]|Gibt den Distinguished Name der Organisationseinheit (OU) an, in der das Computer Konto Objekt erstellt werden soll. Beispiel: **OU = MyOU, CN = Test, DC = Domain, DC = com**. Der Standard Speicherort ist der Container des Standard Computers.|
|[/User: <Domäne \ Benutzer &#124; User@Domain>]|Legt Berechtigungen für das Computer Konto Objekt fest, um dem angegebenen Benutzer die erforderlichen Rechte zuzuweisen.|
|[/JoinRights: {joinonly &#124; Full}]|Gibt den Typ der Rechte an, die dem angegebenen Benutzer zugewiesen werden sollen.<p>-   Für **joinonly** muss der Administrator das Computer Konto zurücksetzen, bevor der Benutzer den Computer der Domäne hinzufügen kann.<br />-   **Full** bietet vollen Zugriff auf den Benutzer, der das Recht zum Hinzufügen des Computers zur Domäne umfasst.|
|[/JoinDomain: {yes &#124; No}]|Gibt an, ob der Computer während der Installation des Betriebssystems mit der Domäne verknüpft werden soll oder nicht. Der Standardwert ist **Ja**.|
|[/ReferralServer: <Server name> ]|Gibt den Namen des Servers an, für den eine Verbindung hergestellt werden soll, um das Netzwerkstart Programm und das Start Abbild mit Trivial File Transfer Protocol (TFTP) herunterzuladen.|
|[/BootProgram: <Relative path> ]|Gibt den relativen Pfad vom Ordner RemoteInstall zum Netzwerkstart Programm an, das von diesem Computer empfangen werden soll. Beispiel: **boot\x86\pxeboot.com**.|
|[/WdsClientUnattend: <Relative path> ]|Gibt den relativen Pfad vom Ordner RemoteInstall zur Datei für die unbeaufsichtigte Installation an, mit der der Windows-Bereitstellungsdiensteclient automatisiert wird.|
|[/BootImagepath: <Relative path> ]|Gibt den relativen Pfad vom Ordner RemoteInstall zum Start Abbild an, das von diesem Computer empfangen werden soll.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um den Computer mit der RequestId 12 zu genehmigen:
```
wdsutil /Approve-AutoaddDevices /RequestId:12
```
Geben Sie Folgendes ein, um den Computer mit einer RequestId von 20 zu genehmigen und das Abbild mit den angegebenen Einstellungen bereitzustellen:
```
wdsutil /Approve-AutoaddDevices /RequestId:20 /MachineName:computer1 /OU:OU=Test,CN=company,DC=Domain,DC=Com /User:Domain\User1
/JoinRights:Full /ReferralServer:MyWDSServer /BootProgram:boot\x86\pxeboot.n12 /WdsClientUnattend:WDSClientUnattend\Unattend.xml /BootImagepath:boot\x86\images\boot.wim
```
Geben Sie Folgendes ein, um alle ausstehenden Computer zu genehmigen:
```
wdsutil /verbose /Approve-AutoaddDevices /RequestId:ALL
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL DELETE-AutoAddDevices-Befehl](wdsutil-delete-autoadddevices.md)
- [Befehl "WDSUTIL Get-AutoAddDevices"](wdsutil-get-autoadddevices.md)
- [WDSUTIL ablehnen-AutoAddDevices-Befehl](wdsutil-reject-autoadddevices.md)
