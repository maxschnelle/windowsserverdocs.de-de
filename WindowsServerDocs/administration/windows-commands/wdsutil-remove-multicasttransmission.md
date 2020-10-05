---
title: WDSUTIL Remove-MulticastTransmission
description: Referenz Artikel für WDSUTIL Remove-MulticastTransmission, der die Multicast Übertragung für ein Bild deaktiviert.
ms.topic: reference
ms.assetid: 9a7f5c31-bfbf-425d-9129-a6f9173fe83d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a7ed8d9ef26deb0a50baa8511cd07f250561d579
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730595"
---
# <a name="wdsutil-remove-multicasttransmission"></a>WDSUTIL Remove-MulticastTransmission

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Deaktiviert die Multicast Übertragung für ein Bild. Wenn Sie **/Force**nicht angeben, wird die Abbild Übertragung durch vorhandene Clients beendet, der Beitritt neuer Clients ist jedoch nicht gestattet.

## <a name="syntax"></a>Syntax
**Windows Server 2008**
```
wdsutil /remove-MulticastTransmission:<Image name> [/Server:<Server name> mediatype:Install Group:<Image Group>] [/Filename:<File name>] [/force]
```
**Windows Server 2008 R2** für Start Abbilder:
```
wdsutil [Options] /remove-MulticastTransmissiomedia:<Image name>
\x20    [/Server:<Server name>]
\x20  mediatype:Boot
\x20    /Architecture:{x86 | ia64 | x64}
\x20    [/Filename:<File name>]
```
für Installations Images:
```
wdsutil [Options] /remove-MulticastTransmissiomedia:<Image name>
        [/Server:<Server name>]
      mediatype:Install
       mediaGroup:<Image Group
        [/Filename:<File name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|Medien<Image name>|Gibt den Namen des Images an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
MediaType: {Install&#124;Boot}|Gibt den Bildtyp an. Beachten Sie, dass diese Option für die **Installation** von für Windows Server 2008 festgelegt werden muss.|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Start Abbilds an, das mit der zu startenden Übertragung verknüpft ist. Da es möglich ist, den gleichen Image Namen für Start Images in verschiedenen Architekturen zu verwenden, sollten Sie die Architektur angeben, um sicherzustellen, dass die richtige Übertragung verwendet wird.|
|\mediagroup: <Image group name> ]|Gibt die Bild Gruppe an, die das Bild enthält. Wenn kein Bildgruppen Name angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe verwendet. Wenn auf dem Server mehr als eine Abbild Gruppe vorhanden ist, müssen Sie diese Option verwenden, um den Namen der Abbild Gruppe anzugeben.|
|[/Filename:<File name>]|Gibt den Dateinamen an. Wenn das Quell Image nicht anhand des Namens eindeutig identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.|
|/Force|entfernt die Übertragung und beendet alle Clients. Wenn Sie keinen Wert für die Option **/Force** angeben, können vorhandene Clients die Abbild Übertragung beenden, aber neue Clients können nicht beitreten.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um einen Namespace zu beenden (aktuelle Clients schließen die Übertragung ab, aber neue Clients können nicht beitreten). Geben Sie Folgendes ein:
```
wdsutil /remove-MulticastTransmission:Vista with Office
/Imagetype:Install
```
```
wdsutil /remove-MulticastTransmission:x64 Boot Image
/Imagetype:Boot /Architecture:x64
```
Wenn Sie die Beendigung aller Clients erzwingen möchten, geben Sie Folgendes ein:
```
wdsutil /remove-MulticastTransmission /Server:MyWDSServer
/Image:Vista with Officemediatype:InstalmediaGroup:ImageGroup1
/Filename:install.wim /force
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL Get-allmulticasttransmissions-Befehl](wdsutil-get-allmulticasttransmissions.md)
- [WDSUTIL Get-MulticastTransmission-Befehl](wdsutil-get-multicasttransmission.md)
- [WDSUTIL New-MulticastTransmission-Befehl](wdsutil-new-multicasttransmission.md)
- [WDSUTIL Start-MulticastTransmission-Befehl](wdsutil-start-multicasttransmission.md)
