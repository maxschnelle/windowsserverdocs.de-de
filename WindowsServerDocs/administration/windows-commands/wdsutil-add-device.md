---
title: WDSUTIL-Add-Device
description: Referenz Artikel für den Befehl "WDSUTIL Add-Device", der einen Computer in Active Directory Domain Services vorab eingibt.
ms.topic: reference
ms.assetid: 1e599cc4-464a-421b-b6bb-c101af154131
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: de05d5510e61f5cba0813a7e11215935fd380968
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524636"
---
# <a name="wdsutil-add-device"></a>WDSUTIL-Add-Device

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Vorab Stufen eines Computers in Active Directory Domain Services (AD DS). Vorab bereitgestellte Computer werden auch als *bekannte Computer*bezeichnet. Dadurch können Sie Eigenschaften konfigurieren, um die Installation für den Client zu steuern. Beispielsweise können Sie das Netzwerkstart Programm und die Datei für die unbeaufsichtigte Installation konfigurieren, die vom Client empfangen werden soll, sowie den Server, von dem der Client das Netzwerkstart Programm herunterladen soll.

## <a name="syntax"></a>Syntax

```
wdsutil /add-Device /Device:<Devicename> /ID:<UUID | MAC address> [/ReferralServer:<Servername>] [/BootProgram:<Relativepath>] [/WdsClientUnattend:<Relativepath>] [/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/BootImagepath:<Relativepath>] [/OU:<DN of OU>] [/Domain:<Domain>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| Schutz`<Devicename>` | Gibt den Namen des hinzu zufügenden Geräts an. |
| Name`<UUID|MAC address>` | Gibt entweder die GUID/UUID oder die Mac-Adresse des Computers an. Eine GUID/UUID muss eines von zwei Formaten aufweisen: binäre Zeichenfolge ( `/ID:ACEFA3E81F20694E953EB2DAA1E8B1B6` ) oder GUID-Zeichenfolge ( `/ID:E8A3EFAC-201F-4E69-953E-B2DAA1E8B1B6` ). Eine Mac-Adresse muss folgendes Format aufweisen: **00b056882(** keine Bindestriche) oder **00-B0-56-88-2F-DC** (mit Bindestrichen) |
| [/ReferralServer: `<Servername>` ] | Gibt den Namen des Servers an, für den eine Verbindung hergestellt werden soll, um das Netzwerkstart Programm und das Start Abbild mit Trivial File Transfer Protocol (TFTP) herunterzuladen. |
| [/BootProgram: `<Relativepath>` ] | Gibt den relativen Pfad vom Ordner **RemoteInstall** zum Netzwerkstart Programm an, das von diesem Computer empfangen werden soll. Beispiel: `boot\x86\pxeboot.com` |
| [/WdsClientUnattend: `<Relativepath>` ] | Gibt den relativen Pfad vom Ordner **RemoteInstall** zur unbeaufsichtigten Installationsdatei an, mit der die Installations Bildschirme des Windows-Bereitstellungsdiensteclient automatisiert werden. |
| [/User: `<Domain\User|User@Domain>` ] | Legt Berechtigungen für das Computer Konto Objekt fest, um dem angegebenen Benutzer die erforderlichen Rechte zum Hinzufügen des Computers zur Domäne zu übergeben. |
| [/JoinRights: `{JoinOnly|Full}` ] | Gibt den Typ der Rechte an, die dem Benutzer zugewiesen werden sollen.<ul><li>**Joinonly** : der Administrator muss das Computer Konto zurücksetzen, bevor der Benutzer den Computer der Domäne hinzufügen kann.</li><li>**Full** : bietet vollständigen Zugriff auf den Benutzer, der über das Recht zum Hinzufügen des Computers zur Domäne verfügt. |
| [/JoinDomain: `{Yes|No}` ] | Gibt an, ob der Computer während der Installation des Betriebssystems mit der Domäne verknüpft werden soll. Der Standardwert ist **Ja**. |
| [/BootImagepath: `<Relativepath>` ] | Gibt den relativen Pfad vom Ordner **RemoteInstall** zum Start Abbild an, das von diesem Computer verwendet werden soll. |
| [/Ou: `<DN of OU>` ] | Der Distinguished Name der Organisationseinheit, in der das Computer Konto Objekt erstellt werden soll. Beispiel: **OU = MyOU, CN = Test, DC = Domain, DC = com**. Der Standard Speicherort ist der Container des Standard Computers. |
| [/Domain: `<Domain>` ] | Die Domäne, in der das Computer Konto Objekt erstellt werden soll. Der Standard Speicherort ist die lokale Domäne. |

## <a name="examples"></a>Beispiele

Wenn Sie einen Computer mit einer Mac-Adresse hinzufügen möchten, geben Sie Folgendes ein:

```
wdsutil /add-Device /Device:computer1 /ID:00-B0-56-88-2F-DC
```

Um einen Computer mithilfe einer GUID-Zeichenfolge hinzuzufügen, geben Sie Folgendes ein:

```
wdsutil /add-Device /Device:computer1 /ID:{E8A3EFAC-201F-4E69-953F-B2DAA1E8B1B6} /ReferralServer:WDSServer1 /BootProgram:boot\x86\pxeboot.com/WDSClientUnattend:WDSClientUnattend\unattend.xml /User:Domain\MyUser/JoinRights:Full /BootImagepath:boot\x86\images\boot.wim /OU:OU=MyOU,CN=Test,DC=Domain,DC=com
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [WDSUTIL-Befehl "Get-alldevices"](wdsutil-get-alldevices.md)

- [WDSUTIL-Befehl "Get-Device"](wdsutil-get-device.md)

- [WDSUTIL Set-Device-Befehl](wdsutil-set-device.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)

- [New-wdsclient](/powershell/module/wds/New-WdsClient)
