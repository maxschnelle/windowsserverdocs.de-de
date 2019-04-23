---
title: Set-Device-Unterbefehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 401567f8-eaeb-4a2d-b811-140bb007028d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 80bb9144936cf493784603bcbdb8a0d1e5c870bd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848061"
---
# <a name="subcommand-set-device"></a>Unterbefehl: Set-Device

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ändert die Attribute eines vorab bereitgestellten Computers. Kein vorab bereitgestellter Computer ist ein Computer, der mit einem Computerkontoobjekt in active Directory-Domänenserver (AD DS) verknüpft wurde. Vorab bereitgestellte Clients werden auch bekannte Computer bezeichnet. Sie können Eigenschaften für das Computerkonto zum Steuern der Installation für den Client konfigurieren. Beispielsweise können Sie konfigurieren, das Netzwerkstartprogramm und die für die unbeaufsichtigte Installation-Datei, die der Client erhalten soll, als auch der Server, von dem der Client das Netzwerkstartprogramm herunterladen soll.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Set-Device /Device:<Device name> [/ID:<UUID | MAC address>] [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] 
[/WdsClientUnattend:<Relative path>] [/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/BootImagepath:<Relative path>] [/Domain:<Domain>] [/resetAccount]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/ Gerät:<computer name>|Gibt den Namen des Computers (SAM-Account-Name).|
|[/ ID: < UUID &#124; MAC-Adresse >]|Gibt entweder die GUID/UUID oder die MAC-Adresse des Computers. Dieser Wert muss in einem der folgenden drei Formaten:<br /><br />-Binäre Zeichenfolge: **/ID:ACEFA3E81F20694E953EB2DAA1E8B1B6**<br />-GUID/UUID-Zeichenfolge: / ID:**E8A3EFAC-201F-4E69-953E-B2DAA1E8B1B6**<br />-MAC-Adresse: **00B056882FDC** (ohne Bindestriche) oder **00-B0-56-88-2F-DC** (mit Bindestrichen)|
|[/ReferralServer:<Server name>]|Gibt den Namen des Servers zu wenden, um das Netzwerk-Programm und Boot Startabbild mit Trivial File Transfer Protocol (Tftp) herunterladen.|
|[/BootProgram:<Relative path>]|Gibt an, der relative Pfad vom Ordner "RemoteInstall", um das Netzwerkstartprogramm an, dem der angegebene Computer erhält. Zum Beispiel: **boot\x86\pxeboot.com**|
|[/WdsClientUnattend:<Relative path>]|Gibt an, der relative Pfad vom Ordner "RemoteInstall" zur Datei für die unbeaufsichtigte Installation, die die Installationsbildschirme für den Windows-Bereitstellungsdiensteclient automatisiert.|
|[/User:<Domain\User &#124; User@Domain>]|Legt Berechtigungen für das Computerkonto-Objekt, das dem angegebenen Benutzer die erforderlichen Rechte für den Beitritt zur Domäne geben fest.|
|[/JoinRights:{JoinOnly &#124; Full}]|Gibt den Typ von rechten, dem Benutzer zugewiesen werden soll.<br /><br />-   **JoinOnly** muss der Administrator das Computerkonto zurückgesetzt werden, bevor der Benutzer den Computer der Domäne beitreten kann.<br />-   **Vollständige** erhalten Sie Vollzugriff für den Benutzer, einschließlich des rechts, um den Computer der Domäne zu verknüpfen.|
|[/JoinDomain:{Yes &#124; No}]|Gibt an, und zwar unabhängig davon, ob der Computer der Domäne als dieses Konto während einer Installation von Windows-Bereitstellungsdienste hinzugefügt werden soll. Die Standardeinstellung ist **Ja**.|
|[/BootImagepath:<Relative path>]|Gibt an, der relative Pfad vom Ordner "RemoteInstall" für das Startimage, das den Computer verwendet.|
|[/ Domain:<Domain>]|Gibt die Domäne, für den vorab bereitgestellten Computer gesucht werden soll. Der Standardwert ist der lokalen Domäne.|
|[/resetAccount]|setzt die Berechtigungen auf dem angegebenen Computer zurück, sodass jeder Benutzer mit den entsprechenden Berechtigungen auf der Domäne beitreten kann, mit diesem Konto.|
## <a name="BKMK_examples"></a>Beispiele für
Um das Programm und Weiterleitung netzwerkstartserver für einen Computer festzulegen, geben Sie Folgendes ein:
```
wdsutil /Set-Device /Device:computer1 /ReferralServer:MyWDSServer
/BootProgram:boot\x86\pxeboot.n12
```
Geben Sie Folgendes ein, um verschiedene Einstellungen für einen Computer festzulegen:
```
wdsutil /verbose /Set-Device /Device:computer2 /ID:00-B0-56-88-2F-DC /WdsClientUnattend:WDSClientUnattend\unattend.xml 
/User:Domain\user /JoinRights:JoinOnly /JoinDomain:No /BootImagepath:boot\x86\images\boot.wim /Domain:NorthAmerica /resetAccount
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl Hinzufügen von Geräten](using-the-add-device-command.md)
[mit dem Befehl Get-AllDevices](using-the-get-alldevices-command.md)
[mithilfe der Get-Device-Befehl](using-the-get-device-command.md)
