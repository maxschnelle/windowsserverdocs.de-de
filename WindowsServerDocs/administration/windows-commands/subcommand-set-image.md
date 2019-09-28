---
title: Unterbefehls Satz-Image
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ae03c86-7a13-4e38-9182-32e55fffd504
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4584bd6253b1991aba7e87fc42ff484101681081
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383865"
---
# <a name="subcommand-set-image"></a>Unterbefehl: Set-Image

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ändert die Attribute eines Bilds.
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
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien: <Image name>|Gibt den Namen des Bilds an.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
MediaType: {Boot &#124; install}|Gibt den Typ des Bilds an.|
|/Architecture: {x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Bilds an. Da Sie den gleichen Image Namen für verschiedene Start Images in verschiedenen Architekturen haben können, wird durch die Angabe der Architektur sichergestellt, dass das richtige Image geändert wird.|
|[/Filename:<File name>]|Wenn das Bild nicht eindeutig anhand des Namens identifiziert werden kann, müssen Sie diese Option verwenden, um den Dateinamen anzugeben.|
|/Name|Gibt den Namen des Bilds an.|
|/Description<Description>]|Legt die Beschreibung des Bilds fest.|
|[/Enabled: {Yes &#124; No}]|Aktiviert oder deaktiviert das Bild.|
|\mediagroup: <Image group name>]|Gibt die Bild Gruppe an, die das Bild enthält. Wenn kein Bildgruppen Name angegeben wird und nur eine Abbild Gruppe auf dem Server vorhanden ist, wird diese Abbild Gruppe verwendet. Wenn auf dem Server mehr als eine Abbild Gruppe vorhanden ist, müssen Sie diese Option verwenden, um die Abbild Gruppe anzugeben.|
|[/UserFilter: <SDDL>]|Legt den Benutzer Filter für das Bild fest. Die Filter Zeichenfolge muss im SDDL-Format (Security Descriptor Definition Language) vorliegen. Beachten Sie, dass diese Option im Gegensatz zur **/Security** -Option für Bildgruppen nur die Benutzer einschränkt, die die Bilddefinition sehen können, und nicht die eigentlichen Bild Datei Ressourcen. Um den Zugriff auf die Datei Ressourcen einzuschränken und damit auf alle Images in einer Abbild Gruppe zuzugreifen, müssen Sie die Sicherheit für die Image Gruppe selbst festlegen.|
|[/UnattendFile:<Unattend file path>]|Legt den vollständigen Pfad zur Datei für die unbeaufsichtigte Installation fest, die dem Image zugeordnet werden soll. Zum Beispiel: **D:\dateien\unattend\img1unattend.XML**|
|[/OverwriteUnattend: {Yes &#124; No}]|Sie können **/overwrite** angeben, um die Datei für die unbeaufsichtigte Installation zu überschreiben, wenn dem Image bereits eine Datei für die unbeaufsichtigte Installation zugeordnet ist. Beachten Sie, dass die Standardeinstellung **Nein**lautet.|
## <a name="BKMK_examples"></a>Beispiele
Um Werte für ein Start Abbild festzulegen, geben Sie einen der folgenden Werte ein:
```
wdsutil /Set-Imagmedia:"WinPE boot imagemediatype:Boot /Architecture:x86 /Description:"New description"
wdsutil /verbose /Set-Imagmedia:"WinPE boot image" /Server:MyWDSServemediatype:Boot /Architecture:x86 /Filename:boot.wim 
/Name:"New Name" /Description:"New Description" /Enabled:Yes
```
Geben Sie einen der folgenden Werte ein, um Werte für ein Installations Image festzulegen:
```
wdsutil /Set-Imagmedia:"Windows Vista with Officemediatype:Install /Description:"New description" 
wdsutil /verbose /Set-Imagmedia:"Windows Vista with Office" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /Name:"New name" /Description:"New description" /UserFilter:"O:BAG:DUD:AI(A;ID;FA;;;SY)(A;ID;FA;;;BA)(A;ID;0x1200a9;;;AU)" /Enabled:Yes /UnattendFile:\\server\share\unattend.xml /OverwriteUnattend:Yes
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
 mithilfe des Befehls "[Add-Image](using-the-add-image-command.md)" 
 mithilfe des Befehls "[Copy-Image](using-the-copy-image-command.md)" 
 mithilfe des Befehls "[Export-](using-the-export-image-command.md)Image" 
 mithilfe des Befehls "[Get-](using-the-get-image-command.md)Image" 
 mithilfe[der Befehl "Remove-Image](using-the-remove-image-command.md)" 1[mit dem Befehl "Replace-Image](using-the-replace-image-command.md) "
