---
title: Unterbefehl Set-Image
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: e63c67210764de76edae18a1897a68d763f9d695
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856481"
---
# <a name="subcommand-set-image"></a>Unterbefehl: Set-Image

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ändert die Attribute eines Bilds.
## <a name="syntax"></a>Syntax
für Startabbilder:
```
wdsutil /Set-Imagmedia:<Image name> [/Server:<Server name>mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>] [/Name:<Name>] 
[/Description:<Description>] [/Enabled:{Yes | No}]
```
bei Installationsabbildern:
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
Medien:<Image name>|Gibt den Namen des Bilds.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
mediatype:{Boot &#124; Install}|Gibt den Typ des Bilds an.|
|/Architecture:{x86 &#124; ia64 &#124; x64}|Gibt die Architektur des Bilds. Da Sie den imagenamen für verschiedene Startabbilder in verschiedenen Architekturen verfügen können, wird sichergestellt, die die Architektur angibt, dass das richtige Bild geändert wird.|
|[/Filename:<File name>]|Wenn das Bild kann nicht eindeutig anhand des Namens identifiziert werden, müssen Sie diese Option verwenden, um den Dateinamen angeben.|
|[/Name]|Gibt den Namen des Bilds.|
|[/ Description:<Description>]|Legt die Beschreibung des Images fest.|
|[/ Aktiviert: {Yes &#124; No}]|Aktiviert oder deaktiviert das Bild.|
|\mediaGroup:<Image group name>]|Gibt die Image-Gruppe, die das Bild enthält. Wenn kein Bild-Gruppenname angegeben und nur eine Abbildgruppe auf dem Server vorhanden ist, wird diese Abbildgruppe verwendet. Wenn mehr als eine Abbildgruppe auf dem Server vorhanden ist, müssen Sie diese Option verwenden, um die Abbildgruppe angeben.|
|[/UserFilter:<SDDL>]|Legt den Benutzerfilter für das Bild fest. Die Filterzeichenfolge muss im Security Descriptor Definition Language (SDDL)-Format vorliegen. Beachten Sie, dass im Gegensatz zu den **/Sicherheit** Option für Abbildgruppen, diese Option nur beschränkt, die die imagedefinition und nicht die eigentlichen Bild-Datei-Ressourcen anzeigen können. Zum Einschränken des Zugriffs auf die Ressourcen, und daher Zugriff auf alle Abbilder in einer Abbildgruppe enthalten, müssen Sie beim Festlegen der Sicherheit für die Abbildgruppe selbst.|
|[/UnattendFile:<Unattend file path>]|Legt den vollständigen Pfad zur Datei für die unbeaufsichtigte Installation mit dem Image zugeordnet werden soll. Zum Beispiel: **D:\Files\Unattend\Img1Unattend.xml**|
|[/OverwriteUnattend:{Yes &#124; No}]|Sie können angeben, **/Overwrite** , die für die unbeaufsichtigte Installation-Datei zu überschreiben, wenn bereits eine Datei für unbeaufsichtigte Installation, die dem Bild zugeordneten vorhanden ist. Beachten Sie, dass die Standardeinstellung **keine**.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie eine der folgenden Schritte aus, um Werte für ein Startimage festzulegen:
```
wdsutil /Set-Imagmedia:"WinPE boot imagemediatype:Boot /Architecture:x86 /Description:"New description"
wdsutil /verbose /Set-Imagmedia:"WinPE boot image" /Server:MyWDSServemediatype:Boot /Architecture:x86 /Filename:boot.wim 
/Name:"New Name" /Description:"New Description" /Enabled:Yes
```
Geben Sie eine der folgenden Schritte aus, um Werte bei einem Installationsabbild festzulegen:
```
wdsutil /Set-Imagmedia:"Windows Vista with Officemediatype:Install /Description:"New description" 
wdsutil /verbose /Set-Imagmedia:"Windows Vista with Office" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /Name:"New name" /Description:"New description" /UserFilter:"O:BAG:DUD:AI(A;ID;FA;;;SY)(A;ID;FA;;;BA)(A;ID;0x1200a9;;;AU)" /Enabled:Yes /UnattendFile:\\server\share\unattend.xml /OverwriteUnattend:Yes
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl-Add-Image](using-the-add-image-command.md)
[mit dem Befehl-Kopieren-Image](using-the-copy-image-command.md)
[mithilfe der Export-Image-Befehl](using-the-export-image-command.md)
[mit dem Get-Image-Befehl](using-the-get-image-command.md)
[mit dem Remove-Image-Befehl](using-the-remove-image-command.md) 
 [ Verwenden die Replace-Image-Befehl](using-the-replace-image-command.md)
