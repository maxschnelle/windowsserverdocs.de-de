---
title: Mithilfe des Befehls Get-AllImages
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19de3720-4315-415a-8dc6-486caa0b2100
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 57b81dd3dd3a24876c4401e80d08130ed5243888
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872561"
---
# <a name="using-the-get-allimages-command"></a>Mithilfe des Befehls Get-AllImages

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ruft Informationen über alle Bilder auf einem Server ab.
## <a name="syntax"></a>Syntax
```
wdsutil /Get-AllImages [/Server:<Server name>] /Show:{Boot | Install | LegacyRis | All} [/detailed]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
|/Show: {Boot &#124; Install &#124; LegacyRis &#124; All}|-   **Start** nur Startabbilder gibt.<br />-   **Installieren Sie** gibt installieren, Bilder sowie Informationen zu den imagegruppen, die sie enthalten.<br />-   **LegacyRis** nur remote Installation Services (RIS) Images zurückgegeben.<br />-   **Alle** gibt Image-Informationen, Informationen zur Installation Image (einschließlich Informationen zu den imagegruppen) und RIS-Image-Informationen zu starten.|
|[/detailed]|Gibt an, dass alle Metadaten zu Bildern von jedes Bild zurückgegeben werden sollen. Wenn diese Option nicht verwendet wird, ist das Standardverhalten, um nur die Image-Name, Beschreibung und Dateinamen zurückzugeben.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie einen der folgenden Schritte aus, zum Anzeigen von Informationen zu den Images:
```
wdsutil /Get-AllImages /Show:Install
wdsutil /verbose /Get-AllImages /Server:MyWDSServer /Show:All /detailed
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl-Add-Image](using-the-add-image-command.md)
[mit dem Befehl-Kopieren-Image](using-the-copy-image-command.md)
[mithilfe der Export-Image-Befehl](using-the-export-image-command.md)
[mit dem Remove-Image-Befehl](using-the-remove-image-command.md)
[mit dem Replace-Image-Befehl](using-the-replace-image-command.md) 
 [Unterbefehl: Set-Image](subcommand-set-image.md)
