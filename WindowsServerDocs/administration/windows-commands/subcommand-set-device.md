---
title: Unterbefehls Satz-Gerät
description: Referenz Artikel für den Unterbefehl Set-Device, mit dem die Attribute eines vorab bereitgestellten Computers geändert werden.
ms.topic: reference
ms.assetid: 401567f8-eaeb-4a2d-b811-140bb007028d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f2eef4d1061e0cd78e4fbb53ae276368318b6d26
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640906"
---
# <a name="subcommand-set-device"></a>Unterbefehl: Set-Device

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert die Attribute eines vorab bereitgestellten Computers. Ein vorab bereitgestellter Computer ist ein Computer, der mit einem Computer Konto Objekt in Active Directory-Domänen Servern (AD DS) verknüpft ist. Vorab bereitgestellte Clients werden auch als bekannte Computer bezeichnet. Sie können Eigenschaften für das Computer Konto konfigurieren, um die Installation für den-Client zu steuern. Beispielsweise können Sie das Netzwerkstart Programm und die Datei für die unbeaufsichtigte Installation konfigurieren, die vom Client empfangen werden soll, sowie den Server, von dem der Client das Netzwerkstart Programm herunterladen soll.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Set-Device /Device:<Device name> [/ID:<UUID | MAC address>] [/ReferralServer:<Server name>] [/BootProgram:<Relative path>]
[/WdsClientUnattend:<Relative path>] [/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/BootImagepath:<Relative path>] [/Domain:<Domain>] [/resetAccount]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|Schutz<computer name>|Gibt den Namen des Computers an (Sam-Account-Name).|
|[/ID: <UUID &#124; Mac-Adresse>]|Gibt entweder die GUID/UUID oder die Mac-Adresse des Computers an. Dieser Wert muss einem der folgenden drei Formate aufweisen:<p>-Binäre Zeichenfolge: **/ID: ACEFA3E81F20694E953EB2DAA1E8B1B6**<br />-GUID/UUID-Zeichenfolge:/ID:**E8A3EFAC-201F-4E69-953E-B2DAA1E8B1B6**<br />-Mac-Adresse: **00b056882(** keine Bindestriche) oder **00-B0-56-88-2F-DC** (mit Bindestrichen)|
|[/ReferralServer: <Server name> ]|Gibt den Namen des Servers an, für den eine Verbindung hergestellt werden soll, um das Netzwerkstart Programm und das Start Abbild mit Trivial File Transfer Protocol (TFTP) herunterzuladen.|
|[/BootProgram: <Relative path> ]|Gibt den relativen Pfad vom Ordner RemoteInstall zum Netzwerkstart Programm an, das vom angegebenen Computer empfangen wird. Beispiel: **boot\x86\pxeboot.com**|
|[/WdsClientUnattend: <Relative path> ]|Gibt den relativen Pfad vom Ordner "RemoteInstall" zur Datei für die unbeaufsichtigte Installation an, mit der die Installations Bildschirme für den Windows-Bereitstellungsdiensteclient automatisiert werden.|
|[/User: <Domäne \ Benutzer &#124; User@Domain>]|Legt Berechtigungen für das Computer Konto Objekt fest, um dem angegebenen Benutzer die erforderlichen Rechte zum Hinzufügen des Computers zur Domäne zu übergeben.|
|[/JoinRights: {joinonly &#124; Full}]|Gibt den Typ der Rechte an, die dem Benutzer zugewiesen werden sollen.<p>-   Für **joinonly** muss der Administrator das Computer Konto zurücksetzen, bevor der Benutzer den Computer der Domäne hinzufügen kann.<br />-   **Full** bietet vollen Zugriff auf den Benutzer, einschließlich der Berechtigung, den Computer der Domäne hinzuzufügen.|
|[/JoinDomain: {yes &#124; No}]|Gibt an, ob der Computer während der Installation der Windows-Bereitstellungs Dienste der Domäne als dieses Computer Konto beitreten soll. Der Standardwert für diese Einstellung ist **Ja**.|
|[/BootImagepath: <Relative path> ]|Gibt den relativen Pfad vom Ordner RemoteInstall zum Start Abbild an, das vom Computer verwendet wird.|
|[/Domain: <Domain> ]|Gibt die Domäne an, die nach dem vorab bereitgestellten Computer durchsucht werden soll. Der Standardwert ist die lokale Domäne.|
|[/resetAccount]|setzt die Berechtigungen für den angegebenen Computer zurück, sodass jeder Benutzer mit den entsprechenden Berechtigungen mithilfe dieses Kontos der Domäne beitreten kann.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um das Netzwerkstart Programm und den Verweis Server für einen Computer festzulegen:
```
wdsutil /Set-Device /Device:computer1 /ReferralServer:MyWDSServer
/BootProgram:boot\x86\pxeboot.n12
```
Geben Sie Folgendes ein, um verschiedene Einstellungen für einen Computer festzulegen:
```
wdsutil /verbose /Set-Device /Device:computer2 /ID:00-B0-56-88-2F-DC /WdsClientUnattend:WDSClientUnattend\unattend.xml
/User:Domain\user /JoinRights:JoinOnly /JoinDomain:No /BootImagepath:boot\x86\images\boot.wim /Domain:NorthAmerica /resetAccount
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-add-device-command.md) 
 "Add-Device" [Verwenden des Befehls](using-the-get-alldevices-command.md) 
 Get-alldevices [Verwenden des Befehls Get-Device](using-the-get-device-command.md)
