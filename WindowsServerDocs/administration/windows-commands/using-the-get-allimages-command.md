---
title: Get-allimages
description: Windows-Befehls Thema für Get-allimages, das Informationen zu allen Images auf einem Server abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 19de3720-4315-415a-8dc6-486caa0b2100
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f1358d7ae4a86b6439b9a304e10e3aa569112d5a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831303"
---
# <a name="get-allimages"></a>Get-allimages

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen zu allen Images auf einem Server ab.

## <a name="syntax"></a>Syntax
```
wdsutil /Get-AllImages [/Server:<Server name>] /Show:{Boot | Install | LegacyRis | All} [/detailed]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Show: {Boot &#124; install &#124; legacyris &#124; all}|beim -   **Start** werden nur Start Abbilder zurückgegeben.<br />-   **Installation** gibt sowohl Installations Abbilder als auch Informationen zu den Abbild Gruppen zurück, in denen Sie enthalten sind.<br />-   **legacyris** gibt nur Remoteinstallations Dienste (RIS) zurück.<br />-   **alle** Informationen zum Start Abbild zurück, zum Installieren von Image Informationen (einschließlich Informationen zu den Abbild Gruppen) und zum RIS-Image.|
|/Detailed|Gibt an, dass alle Bild Metadaten aus jedem Bild zurückgegeben werden sollen. Wenn diese Option nicht verwendet wird, besteht das Standardverhalten darin, nur den Bildnamen, die Beschreibung und den Dateinamen zurückzugeben.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Wenn Sie Informationen zu den Bildern anzeigen möchten, geben Sie eine der folgenden Informationen ein:
```
wdsutil /Get-AllImages /Show:Install
wdsutil /verbose /Get-AllImages /Server:MyWDSServer /Show:All /detailed
```
## <a name="additional-references"></a>Weitere Verweise
- Der [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls "Add-Image](using-the-add-image-command.md) "
[mithilfe des Befehls "Copy-](using-the-copy-image-command.md) Image"
[mithilfe des Befehls "Export-](using-the-export-image-command.md) Image"
mithilfe des Befehls " [Remove](using-the-remove-image-command.md) -Image"
mit dem Befehl " [Replace](using-the-replace-image-command.md) -Image"
[Unterbefehl: Set-Image](subcommand-set-image.md)
