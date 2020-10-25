---
title: WDSUTIL genehmigen-AutoAddDevices
description: Referenz Artikel für den Befehl "WDSUTIL genehmigen-AutoAddDevices", mit dem Computer genehmigt werden, für die die administrative Genehmigung aussteht.
ms.topic: reference
ms.assetid: 8d76e8d3-ab35-429c-be7b-904f95d0782d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 31dba6d0a0bb585f61433f86d1aa0ae4388fe484
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524935"
---
# <a name="wdsutil-approve-autoadddevices"></a>WDSUTIL genehmigen-AutoAddDevices

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Genehmigt Computer, für die die administrative Genehmigung aussteht. Wenn die Richtlinie zum automatischen hinzufügen aktiviert ist, ist eine administrative Genehmigung erforderlich, bevor unbekannte Computer (die nicht vorab bereitgestellt werden) ein Abbild installieren können. Sie können diese Richtlinie mithilfe der Registerkarte **PXE-Antwort** auf der Seite Server s-Eigenschaften aktivieren.

## <a name="syntax"></a>Syntax

```
wdsutil [Options] /Approve-AutoaddDevices [/Server:<Server name>] /RequestId:{<Request ID>| ALL} [/MachineName:<Device name>] [/OU:<DN of OU>] [/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] [/WdsClientUnattend:<Relative path>] [/BootImagepath:<Relative path>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| Servers`<Servername>` | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Namen handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |
| RequestId`{Request ID|ALL}` | Gibt die Anforderungs-ID an, die dem ausstehenden Computer zugewiesen ist. Geben Sie **all** an, um alle ausstehenden Computer zu genehmigen. |
| MachineName`<Devicename>` | Gibt den Namen des hinzu zufügenden Geräts an. Sie können diese Option nicht verwenden, wenn Sie alle Computer genehmigen. |
| [/Ou: `<DN of OU>` ] | Der Distinguished Name der Organisationseinheit, in der das Computer Konto Objekt erstellt werden soll. Beispiel: **OU = MyOU, CN = Test, DC = Domain, DC = com**. Der Standard Speicherort ist der Container des Standard Computers. |
| [/User: `<Domain\User|User@Domain>` ] | Legt Berechtigungen für das Computer Konto Objekt fest, um dem angegebenen Benutzer die erforderlichen Rechte zum Hinzufügen des Computers zur Domäne zu übergeben. |
| [/JoinRights: `{JoinOnly|Full}` ] | Gibt den Typ der Rechte an, die dem Benutzer zugewiesen werden sollen.<ul><li>**Joinonly** : der Administrator muss das Computer Konto zurücksetzen, bevor der Benutzer den Computer der Domäne hinzufügen kann.</li><li>**Full** : bietet vollständigen Zugriff auf den Benutzer, der über das Recht zum Hinzufügen des Computers zur Domäne verfügt. |
| [/JoinDomain: `{Yes|No}` ] | Gibt an, ob der Computer während der Installation des Betriebssystems mit der Domäne verknüpft werden soll. Der Standardwert ist **Ja**. |
| [/ReferralServer: `<Servername>` ] | Gibt den Namen des Servers an, der kontaktiert werden soll, um das Netzwerkstart Programm und das Start Abbild mit Trivial File Transfer Protocol (TFTP) herunterzuladen. |
| [/BootProgram: `<Relativepath>` ] | Gibt den relativen Pfad vom Ordner **RemoteInstall** zum Netzwerkstart Programm an, das von diesem Computer empfangen werden soll. Beispiel: **boot\x86\pxeboot.com**. |
| [/WdsClientUnattend: `<Relativepath>` ] | Gibt den relativen Pfad vom Ordner **RemoteInstall** zur Datei für die unbeaufsichtigte Installation an, mit der der Windows-Bereitstellungsdiensteclient automatisiert wird. |
| [/BootImagepath: `<Relativepath>` ] | Gibt den relativen Pfad vom Ordner RemoteInstall zum Start Abbild an, das von diesem Computer empfangen werden soll. |

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

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
