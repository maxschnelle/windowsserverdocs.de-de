---
title: Unterbefehls Satz-Image
description: Windows-Befehls Thema für Unterbefehls Satz-Image, das die Attribute eines Bilds ändert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ae03c86-7a13-4e38-9182-32e55fffd504
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9564c489c1c3abced839ba27cbfe2841cd5894b0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833933"
---
# <a name="subcommand-set-image"></a>Unterbefehl: Set-Image

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert die Attribute eines Bilds.

## <a name="syntax"></a>Syntax
für Start Abbilder:
```
wdsutil /Set-Imagmedia:<Image name> [/Server:<Server name>mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>] [/Name:<Name>] 
[/Description:<Description>] [/Enabled:{Yes | No}]
```
für Installations Images:
```
wdsutil /Set-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:InstallmediaGroup:<Image group name>]
     [/Filename:<File name>]
     [/Name:<Name>]
     [/Description:<Description>]
     [/UserFilter:<SDDL>]
     [/Enabled:{Yes | No}]
     [/UnattendFile:<Unattend file path>]
         [/OverwriteUnattend:{Yes | No}]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien:<Image name>|Gibt den Namen des Images an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
MediaType: {Boot &#124; install}|Gibt den Typ des Bilds an.|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Bilds an. Da Sie den gleichen Image Namen für verschiedene Start Images in verschiedenen Architekturen haben können, wird durch die Angabe der Architektur sichergestellt, dass das richtige Image geändert wird.|
|[/Filename:<File name>]|Wenn das Bild nicht eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.|
|/Name|Gibt den Namen des Images an.|
|/Description<Description>]|Legt die Beschreibung des Bilds fest.|
|[/Enabled: {Yes &#124; No}]|Aktiviert oder deaktiviert das Bild.|
|\mediagroup:<Image group name>]|Gibt die Bild Gruppe an, die das Bild enthält. Wenn kein Bildgruppen Name angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe verwendet. Wenn auf dem Server mehr als eine Abbild Gruppe vorhanden ist, müssen Sie diese Option verwenden, um die Abbild Gruppe anzugeben.|
|[/UserFilter:<SDDL>]|Legt den Benutzer Filter für das Bild fest. Die Filter Zeichenfolge muss im SDDL-Format (Security Descriptor Definition Language) vorliegen. Beachten Sie, dass diese Option im Gegensatz zur **/Security** -Option für Bildgruppen nur die Benutzer einschränkt, die die Bilddefinition sehen können, und nicht die eigentlichen Bild Datei Ressourcen. Um den Zugriff auf die Datei Ressourcen einzuschränken und damit auf alle Images in einer Abbild Gruppe zuzugreifen, müssen Sie die Sicherheit für die Image Gruppe selbst festlegen.|
|[/UnattendFile:<Unattend file path>]|Legt den vollständigen Pfad zur Datei für die unbeaufsichtigte Installation fest, die dem Image zugeordnet werden soll. Beispiel: **d:\dateien\unattend\img1unattend.XML**|
|[/OverwriteUnattend: {Yes &#124; No}]|Sie können **/overwrite** angeben, um die Datei für die unbeaufsichtigte Installation zu überschreiben, wenn dem Image bereits eine Datei für die unbeaufsichtigte Installation zugeordnet ist. Beachten Sie, dass die Standardeinstellung **Nein**lautet.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Um Werte für ein Start Abbild festzulegen, geben Sie einen der folgenden Werte ein:
```
wdsutil /Set-Imagmedia:WinPE boot imagemediatype:Boot /Architecture:x86 /Description:New description
wdsutil /verbose /Set-Imagmedia:WinPE boot image /Server:MyWDSServemediatype:Boot /Architecture:x86 /Filename:boot.wim 
/Name:New Name /Description:New Description /Enabled:Yes
```
Geben Sie einen der folgenden Werte ein, um Werte für ein Installations Image festzulegen:
```
wdsutil /Set-Imagmedia:Windows Vista with Officemediatype:Install /Description:New description 
wdsutil /verbose /Set-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /Name:New name /Description:New description /UserFilter:O:BAG:DUD:AI(A;ID;FA;;;SY)(A;ID;FA;;;BA)(A;ID;0x1200a9;;;AU) /Enabled:Yes /UnattendFile:\\server\share\unattend.xml /OverwriteUnattend:Yes
```
## <a name="additional-references"></a>Weitere Verweise
- [Der Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls "Add-Image](using-the-add-image-command.md) "
[mithilfe des Befehls "Copy-Image](using-the-copy-image-command.md) "
[mithilfe des Befehls "Export-Image](using-the-export-image-command.md) "
mithilfe des Befehls " [Get-Image](using-the-get-image-command.md) "
mithilfe [des](using-the-remove-image-command.md) Befehls "Remove-Image"
mit dem Befehl " [Replace](using-the-replace-image-command.md) -Image"
