---
title: Mithilfe des Befehls new-MulticastTransmission
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1f1dc46-dd50-4eb9-9f72-cf0e5d71bd3d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 84f5aa69f2d4a875995ac6c18fa43bd68518fba3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875141"
---
# <a name="using-the-new-multicasttransmission-command"></a>Mithilfe des Befehls new-MulticastTransmission

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

erstellt eine neue Multicastübertragung für ein Bild an. Dieser Befehl ist äquivalent zum Erstellen einer Übertragung mithilfe der Windows-Bereitstellungsdienste-Mmc-Snap-in (mit der rechten Maustaste die **Multicastübertragungen** Knoten, und klicken Sie dann auf **erstellen Multicast-Übertragung**). Sie sollten diesen Befehl verwenden, wenn Sie sowohl den Rollendienst Bereitstellung als auch der Transportserver-Rollendienst installiert (d.h. die Standardinstallation) haben. Wenn Sie lediglich der Transportserver-Rollendienst installiert haben, verwenden Sie [mit dem neuen Namespace-Befehl](using-the-new-namespace-command.md).
## <a name="syntax"></a>Syntax
für Übertragungen für Install-Images:
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
für Boot Image-Übertragungen (nur für Windows Server 2008 R2 unterstützt):
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
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien:<Image name>|Gibt den Namen des Images über Multicasting übertragen werden.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollständig qualifizierten Domänennamen (FQDN) sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
|/FriendlyName:<Friendly name>|Gibt den Anzeigenamen der Übertragung an.|
|[/ Description:<Description>]|Gibt die Beschreibung der Übertragung.|
mediatype:{Boot&#124;Install}|Gibt den Typ des Images über Multicasting übertragen werden. Beachten Sie **Boot** wird nur für Windows Server 2008 R2 unterstützt.|
|\mediaGroup:<Image group name>]|Gibt die Image-Gruppe, die das Bild enthält. Wenn kein Bild-Gruppenname angegeben und nur eine Abbildgruppe auf dem Server vorhanden ist, wird diese Abbildgruppe verwendet. Wenn mehr als eine Abbildgruppe auf dem Server vorhanden ist, müssen Sie diese Option verwenden, den Namen des Abbilds an.|
|[/Filename:<File name>]|Gibt den Dateinamen an. Wenn das Quellbild eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen angeben.|
|/Transmissiontype:{AutoCast &#124; ScheduledCast}|Gibt an, ob die Übertragung automatisch gestartet (AutoCast) oder basierend auf den angegebenen Kriterien (ScheduledCast).<br /><br /><ul><li>**Ein automatischer Cast**. Diese Übertragung-Typ gibt an, dass, sobald ein zutreffende Client ein Installationsabbild anfordert, eine Multicastübertragung des ausgewählten Images beginnt. Wie andere Clients das gleiche Image anfordern, werden sie zur Übertragung verknüpft, die bereits gestartet ist.</li><li>**Ein geplanter Cast**. Solche Übertragung legt die Startkriterien für die Übermittlung basierend auf der Anzahl von Clients, von die ein Bild bzw. einem bestimmten Datum und Uhrzeit anfordert. Sie können die folgenden Optionen angeben:<br /><br /><ul><li>[/ time: <time>] – die Zeit, die die Übertragung gestartet werden soll, mithilfe des folgenden Formats: YYYY/MM/DD:hh:mm.</li><li>[/ Clients: <Number of clients>]-legt die minimale Anzahl von Clients warten, bevor die Übertragung gestartet wird.</li></ul></li></ul>|
|/Architecture:{x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Startabbilds zum Übertragen von über Multicasting. Da es möglich, dass den gleichen Namen für Startabbilder mit verschiedenen Architekturen handelt, sollten Sie angeben, die Architektur, um sicherzustellen, dass das richtige Image verwendet wird.|
|[/Filename:<File name>]|Gibt den Dateinamen an. Wenn das Quellbild eindeutig anhand des Namens identifiziert werden kann, müssen Sie den Dateinamen angeben.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie zum Erstellen einer Autocast-Übertragung eines Startabbilds in Windows Server 2008 R2 Folgendes ein:
```
wdsutil /New-MulticastTransmission /FriendlyName:"WDS Boot Transmission"
/Image:"X64 Boot Imagemediatype:Boot /Architecture:x64 /Transmissiontype:AutoCast
```
Um eine Übertragung mit automatischer Umwandlung eines Installationsimages erstellen möchten, geben Sie Folgendes ein:
```
wdsutil /New-MulticastTransmission /FriendlyName:"WDS AutoCast Transmission"
/Image:"Vista with Officemediatype:Install /Transmissiontype:AutoCast
```
Zum Erstellen einer Scheduledcast-Übertragung eines Installationsabbilds Geben Sie Folgendes ein:
```
wdsutil /New-MulticastTransmission /FriendlyName:"WDS SchedCast Transmission" /Server:MyWDSServemedia:"Vista with Officemediatype:Install 
/Transmissiontype:ScheduledCast /time:"2006/11/20:17:00" /Clients:100
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl Get-AllMulticastTransmissions](using-the-get-allmulticasttransmissions-command.md)
[mit dem Befehl Get-MulticastTransmission](using-the-get-multicasttransmission-command.md) 
 [Mit dem Befehl Remove-MulticastTransmission](using-the-remove-multicasttransmission-command.md)
[Unterbefehl: Start-MulticastTransmission](subcommand-start-multicasttransmission.md)
