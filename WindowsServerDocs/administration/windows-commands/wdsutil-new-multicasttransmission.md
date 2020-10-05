---
title: WDSUTIL New-MulticastTransmission
description: Referenz Artikel für WDSUTIL New-MulticastTransmission, das eine neue Multicast Übertragung für ein Abbild erstellt.
ms.topic: reference
ms.assetid: c1f1dc46-dd50-4eb9-9f72-cf0e5d71bd3d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4b02668a6e714ce090a013a34d9dee73121f7a89
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730176"
---
# <a name="wdsutil-new-multicasttransmission"></a>WDSUTIL New-MulticastTransmission

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt eine neue Multicast Übertragung für ein Bild. Dieser Befehl entspricht der Erstellung einer Übertragung über das MMC-Snap-in "Windows-Bereitstellungs Dienste" (Klicken Sie mit der rechten Maustaste auf den Knoten **Multicast Übertragungen** , und klicken Sie dann auf **Multicast Übertragung erstellen**). Verwenden Sie diesen Befehl, wenn Sie sowohl den Rollen Dienst "Bereitstellungs Server" als auch den Transport Server-Rollen Dienst installiert haben (Dies ist die Standardinstallation). Wenn Sie nur den Transport Server-Rollen Dienst installiert haben, verwenden Sie den [Befehl wdsutilnew-Namespace](wdsutil-new-namespace.md).
## <a name="syntax"></a>Syntax
für Installations Abbild Übertragungen:
```
wdsutil [Options] /New-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
        /FriendlyName:<Friendly name>
        [/Description:<Description>]
        /Transmissiontype: {AutoCast | ScheduledCast}
            [/time:<YYYY/MM/DD:hh:mm>]
            [/Clients:<Num of Clients>]
      imagetype:Install
       ImageGroup:<Image Group>]
        [/Filename:<File name>]
```
für Start Abbild Übertragungen (nur unterstützt für Windows Server 2008 R2):
```
wdsutil [Options] /New-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
        /FriendlyName:<Friendly name>
        [/Description:<Description>]
        /Transmissiontype: {AutoCast | ScheduledCast}
            [/time:<YYYY/MM/DD:hh:mm>]
            [/Clients:<Num of Clients>]
      imagetype:Boot
        /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
| /Image<Image name>|Gibt den Namen des Abbilds an, das mithilfe von Multicasting übertragen werden soll.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|FriendlyName<Friendly name>|Gibt den anzeigen amen der Übertragung an.|
|/Description<Description>]|Gibt die Beschreibung der Übertragung an.|
| /ImageType: {Boot&#124;Installation}|Gibt den Typ des Bilds an, das mithilfe von Multicasting übertragen werden soll. Beachten Sie, dass der **Start** nur für Windows Server 2008 R2 unterstützt wird.|
| /ImageGroup: <Image group name> ]|Gibt die Bild Gruppe an, die das Bild enthält. Wenn kein Bildgruppen Name angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe verwendet. Wenn auf dem Server mehr als eine Abbild Gruppe vorhanden ist, müssen Sie diese Option verwenden, um den Namen der Abbild Gruppe anzugeben.|
|[/Filename:<File name>]|Gibt den Dateinamen an. Wenn das Quell Image nicht anhand des Namens eindeutig identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.|
|/TransmissionType: {AutoCast &#124; ScheduledCast}|Gibt an, ob die Übertragung automatisch (AutoCast) oder basierend auf den angegebenen Start Kriterien (ScheduledCast) gestartet werden soll.<p><ul><li>**Automatische**Umwandlung. Dieser Übertragungstyp gibt an, dass die Multicast Übertragung des ausgewählten Images beginnt, sobald ein anwendbarer Client ein Installations Abbild anfordert. Wenn andere Clients dasselbe Abbild anfordern, werden Sie mit der Übertragung verknüpft, die bereits gestartet wurde.</li><li>**Geplante**Umwandlung. Mit diesem Übertragungstyp werden die Start Kriterien für die Übertragung basierend auf der Anzahl von Clients, von denen ein Abbild angefordert wird, bzw. an einem bestimmten Tag und einer bestimmten Uhrzeit festgelegt Sie können die folgenden Optionen angeben:<p><ul><li>[/Time: <time> ] : Legt fest, wie lange die Übertragung beginnen soll, indem Sie das folgende Format verwendet: yyyy/mm/dd: hh: mm.</li><li>[/Clients: <Number of clients> ] : Legt die Mindestanzahl von Clients fest, auf die gewartet werden soll, bevor die Übertragung beginnt.</li></ul></li></ul>|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Start Abbilds an, das mithilfe von Multicasting übertragen wird. Da es möglich ist, den gleichen Namen für Start Abbilder verschiedener Architekturen zu verwenden, sollten Sie die Architektur angeben, um sicherzustellen, dass das richtige Image verwendet wird.|
|[/Filename:<File name>]|Gibt den Dateinamen an. Wenn das Quell Image nicht anhand des Namens eindeutig identifiziert werden kann, müssen Sie den Dateinamen angeben.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um eine automatische Cast Übertragung eines Start Abbilds in Windows Server 2008 R2 zu erstellen:
```
wdsutil /New-MulticastTransmission /FriendlyName:WDS Boot Transmission
/Image:X64 Boot imagetype:Boot /Architecture:x64 /Transmissiontype:AutoCast
```
Geben Sie Folgendes ein, um eine automatische Cast Übertragung eines Installations Abbilds zu erstellen:
```
wdsutil /New-MulticastTransmission /FriendlyName:WDS AutoCast Transmission
/Image:Vista with Officeimage imagetype:Install /Transmissiontype:AutoCast
```
Geben Sie Folgendes ein, um eine Übertragung mit geplanter Umwandlung eines Installations Abbilds zu erstellen:
```
wdsutil /New-MulticastTransmission /FriendlyName:WDS SchedCast Transmission /Server:MyWDSServer Image:Vista with Office imagetype:Install
/Transmissiontype:ScheduledCast /time:2006/11/20:17:00 /Clients:100
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL Get-allmulticasttransmissions-Befehl](wdsutil-get-allmulticasttransmissions.md)
- [WDSUTIL Get-MulticastTransmission-Befehl](wdsutil-get-multicasttransmission.md)
- [WDSUTIL Remove-MulticastTransmission-Befehl](wdsutil-remove-multicasttransmission.md)
- [WDSUTIL Start-MulticastTransmission-Befehl](wdsutil-start-multicasttransmission.md)
