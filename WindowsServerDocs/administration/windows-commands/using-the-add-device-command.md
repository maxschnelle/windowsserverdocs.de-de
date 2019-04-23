---
title: Mithilfe des Befehls Hinzufügen von Geräten
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e599cc4-464a-421b-b6bb-c101af154131
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 85e9ef4445b4dabbe85c2397d62b06756e17879d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878541"
---
# <a name="using-the-add-device-command"></a>Mithilfe des Befehls Hinzufügen von Geräten

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Fortschrittsdialogfeld einen Computer in active Directory-Domänendienste. Vorab bereitgestellte Computer werden auch bekannte Computer bezeichnet. Dadurch können Sie so konfigurieren Sie die Eigenschaften, um die Installation des Clients zu steuern. Beispielsweise können Sie konfigurieren, das Netzwerkstartprogramm und die für die unbeaufsichtigte Installation-Datei, die der Client erhalten soll, als auch der Server, von dem der Client das Netzwerkstartprogramm herunterladen soll.
Beispiele, wie Sie diesen Befehl verwenden können, finden Sie unter [Beispiele](#BKMK_examples).
## <a name="syntax"></a>Syntax
```
wdsutil /add-Device /Device:<Device name> /ID:<UUID | MAC address> [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] [/WdsClientUnattend:<Relative path>] 
[/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/BootImagepath:<Relative path>] [/OU:<DN of OU>] [/Domain:<Domain>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/ Gerät:<computer name>|Gibt den Namen des Computers hinzugefügt werden.|
|/-ID: < UUID &#124; MAC-Adresse >|Gibt entweder die GUID/UUID oder die MAC-Adresse des Computers. Eine GUID/UUID muss in einem der zwei Formate Binärzeichenfolge oder einem GUID-Zeichenfolge sein. Zum Beispiel:<br /><br />Binäre Zeichenfolge: **/ID:ACEFA3E81F20694E953EB2DAA1E8B1B6**<br /><br />GUID-Zeichenfolge: **/ID:E8A3EFAC-201F-4E69-953E-B2DAA1E8B1B6**<br /><br />Eine MAC-Adresse muss im folgenden Format sein: **00B056882FDC** (ohne Bindestriche) oder **00-B0-56-88-2F-DC** (mit Bindestrichen)|
|[/ReferralServer:<Server name>]|Gibt den Namen des Servers kontaktiert werden, um das Netzwerkstartprogramm und das Startabbild mit Trivial File Transfer Protocol (Tftp) herunterzuladen.|
|[/BootProgram:<Relative path>]|Gibt an, der relative Pfad vom Ordner "RemoteInstall", um das Netzwerkstartprogramm an, dem diesem Computer erhalten soll. Zum Beispiel: "boot\x86\pxeboot.com"|
|[/WdsClientUnattend:<Relative path>]|Gibt an, der relative Pfad vom Ordner "RemoteInstall" zur Datei für die unbeaufsichtigte Installation, die die Installationsbildschirme des Windows-Bereitstellungsdiensteclients automatisiert.|
|[/User:<Domain\User &#124; User@Domain>]|Legt Berechtigungen für das Computerkonto-Objekt, das dem angegebenen Benutzer die erforderlichen Rechte für den Beitritt zur Domäne geben fest.|
|[/JoinRights:{JoinOnly &#124; Full}]|Gibt den Typ von rechten, dem Benutzer zugewiesen werden soll.<br /><br />-   **JoinOnly** muss der Administrator das Computerkonto zurückgesetzt werden, bevor der Benutzer den Computer der Domäne beitreten kann.<br />-   **Vollständige** erhalten Sie Vollzugriff für den Benutzer das Recht zum Beitritt zur Domäne gehört.|
|[/JoinDomain:{Yes &#124; No}]|Gibt an, und zwar unabhängig davon, ob der Computer der Domäne als dieses Computerkonto während Betriebssysteminstallation hinzugefügt werden soll. Der Standardwert ist **Ja**.|
|[/BootImagepath:<Relative path>]|Gibt an, der relative Pfad vom Ordner "RemoteInstall" für das Startimage, das diesem Computer verwenden soll.|
|[/OU:<DN of OU>]|Der distinguished Name der Organisationseinheit, in dem das Computerkontoobjekt erstellt werden soll. Zum Beispiel: **OU = MyOU, CN = Test, DC = Domain, DC = com**. Der Standardspeicherort ist der Standard-Computer-Container.|
|[/ Domain:<Domain>]|Die Domäne, in dem das Computerkontoobjekt erstellt werden soll. Der Standardspeicherort ist der lokalen Domäne.|
## <a name="BKMK_examples"></a>Beispiele für
Um einen Computer mit einer MAC-Adresse hinzuzufügen, geben Sie Folgendes ein:
```
wdsutil /add-Device /Device:computer1 /ID:00-B0-56-88-2F-DC
```
Um einen Computer mit der eine GUID-Zeichenfolge hinzuzufügen, geben Sie Folgendes ein:
```
wdsutil /add-Device /Device:computer1 /ID:{E8A3EFAC-201F-4E69-953F-B2DAA1E8B1B6} /ReferralServer:WDSServer1 /BootProgram:boot\x86\pxeboot.com 
/WDSClientUnattend:WDSClientUnattend\unattend.xml /User:Domain\MyUser/JoinRights:Full /BootImagepath:boot\x86\images\boot.wim /OU:"OU=MyOU,CN=Test,DC=Domain,DC=com"
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl Get-AllDevices](using-the-get-alldevices-command.md)
[mithilfe des Get-Geräte-Befehl](using-the-get-device-command.md)
[Unterbefehl: Set-Device-](subcommand-set-device.md)
[WdsClient-neu](https://technet.microsoft.com/library/dn283430.aspx)
