---
title: New-MulticastTransmission
description: Windows-Befehle für New-MulticastTransmission, das eine neue Multicast Übertragung für ein Abbild erstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c1f1dc46-dd50-4eb9-9f72-cf0e5d71bd3d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a94aa4cd944b655a0f81153ff3bd0ab0d0b9c1f9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830663"
---
# <a name="new-multicasttransmission"></a>New-MulticastTransmission

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt eine neue Multicast Übertragung für ein Bild. Dieser Befehl entspricht der Erstellung einer Übertragung über das MMC-Snap-in "Windows-Bereitstellungs Dienste" (Klicken Sie mit der rechten Maustaste auf den Knoten **Multicast Übertragungen** , und klicken Sie dann auf **Multicast Übertragung erstellen**). Verwenden Sie diesen Befehl, wenn Sie sowohl den Rollen Dienst "Bereitstellungs Server" als auch den Transport Server-Rollen Dienst installiert haben (Dies ist die Standardinstallation). Wenn Sie nur den Transport Server-Rollen Dienst installiert haben, verwenden Sie [den Befehl New-Namespace](using-the-new-namespace-command.md).
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
      mediatype:Install
       mediaGroup:<Image Group>]
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
      mediatype:Boot
        /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien:<Image name>|Gibt den Namen des Abbilds an, das mithilfe von Multicasting übertragen werden soll.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/FriendlyName:<Friendly name>|Gibt den anzeigen amen der Übertragung an.|
|/Description<Description>]|Gibt die Beschreibung der Übertragung an.|
MediaType: {Boot&#124;install}|Gibt den Typ des Bilds an, das mithilfe von Multicasting übertragen werden soll. Beachten Sie, dass der **Start** nur für Windows Server 2008 R2 unterstützt wird.|
|\mediagroup:<Image group name>]|Gibt die Bild Gruppe an, die das Bild enthält. Wenn kein Bildgruppen Name angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe verwendet. Wenn auf dem Server mehr als eine Abbild Gruppe vorhanden ist, müssen Sie diese Option verwenden, um den Namen der Abbild Gruppe anzugeben.|
|[/Filename:<File name>]|Gibt den Dateinamen an. Wenn das Quell Image nicht anhand des Namens eindeutig identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.|
|/TransmissionType: {AutoCast &#124; ScheduledCast}|Gibt an, ob die Übertragung automatisch (AutoCast) oder basierend auf den angegebenen Start Kriterien (ScheduledCast) gestartet werden soll.<p><ul><li>**Automatische**Umwandlung. Dieser Übertragungstyp gibt an, dass die Multicast Übertragung des ausgewählten Images beginnt, sobald ein anwendbarer Client ein Installations Abbild anfordert. Wenn andere Clients dasselbe Abbild anfordern, werden Sie mit der Übertragung verknüpft, die bereits gestartet wurde.</li><li>**Geplante**Umwandlung. Mit diesem Übertragungstyp werden die Start Kriterien für die Übertragung basierend auf der Anzahl von Clients, von denen ein Abbild angefordert wird, bzw. an einem bestimmten Tag und einer bestimmten Uhrzeit festgelegt Sie können die folgenden Optionen angeben:<p><ul><li>[/Time: <time>]: legt fest, wie lange die Übertragung beginnen soll, indem Sie das folgende Format verwendet: yyyy/mm/dd: hh: mm.</li><li>[/Clients: <Number of clients>]: legt die Mindestanzahl von Clients fest, auf die gewartet werden soll, bevor die Übertragung beginnt.</li></ul></li></ul>|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Start Abbilds an, das mithilfe von Multicasting übertragen wird. Da es möglich ist, den gleichen Namen für Start Abbilder verschiedener Architekturen zu verwenden, sollten Sie die Architektur angeben, um sicherzustellen, dass das richtige Image verwendet wird.|
|[/Filename:<File name>]|Gibt den Dateinamen an. Wenn das Quell Image nicht anhand des Namens eindeutig identifiziert werden kann, müssen Sie den Dateinamen angeben.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Geben Sie Folgendes ein, um eine automatische Cast Übertragung eines Start Abbilds in Windows Server 2008 R2 zu erstellen:
```
wdsutil /New-MulticastTransmission /FriendlyName:WDS Boot Transmission
/Image:X64 Boot Imagemediatype:Boot /Architecture:x64 /Transmissiontype:AutoCast
```
Geben Sie Folgendes ein, um eine automatische Cast Übertragung eines Installations Abbilds zu erstellen:
```
wdsutil /New-MulticastTransmission /FriendlyName:WDS AutoCast Transmission
/Image:Vista with Officemediatype:Install /Transmissiontype:AutoCast
```
Geben Sie Folgendes ein, um eine Übertragung mit geplanter Umwandlung eines Installations Abbilds zu erstellen:
```
wdsutil /New-MulticastTransmission /FriendlyName:WDS SchedCast Transmission /Server:MyWDSServemedia:Vista with Officemediatype:Install 
/Transmissiontype:ScheduledCast /time:2006/11/20:17:00 /Clients:100
```
## <a name="additional-references"></a>Weitere Verweise
- Der [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Get-allmulticasttransmission](using-the-get-allmulticasttransmissions-command.md)
[mithilfe des Befehls Get-MulticastTransmission](using-the-get-multicasttransmission-command.md)
[mit dem Befehl Remove-MulticastTransmission](using-the-remove-multicasttransmission-command.md)
[Unterbefehl: Start-MulticastTransmission](subcommand-start-multicasttransmission.md)
