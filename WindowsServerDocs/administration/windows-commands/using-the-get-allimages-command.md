---
title: Get-allimages
description: Referenz Artikel zu Get-allimages, der Informationen zu allen Images auf einem Server abruft.
ms.topic: reference
ms.assetid: 19de3720-4315-415a-8dc6-486caa0b2100
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 79b28d3649e18b192504bf6eb012984cb43218e2
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626386"
---
# <a name="get-allimages"></a>Get-allimages

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen zu allen Images auf einem Server ab.

## <a name="syntax"></a>Syntax
```
wdsutil /Get-AllImages [/Server:<Server name>] /Show:{Boot | Install | LegacyRis | All} [/detailed]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Show: {Boot &#124; Installation &#124; legacyris &#124; alle}|-   Beim **Start** werden nur Start Abbilder zurückgegeben.<br />-   Bei der **Installation** werden Installations Images sowie Informationen zu den Abbild Gruppen zurückgegeben, in denen Sie enthalten sind.<br />-   **Legacyris** gibt nur Remoteinstallations Dienste (Remote Installation Services, RIS) zurück.<br />-   **Alle** gibt Informationen zum Start Abbild zurück, zum Installieren von Image Informationen (einschließlich Informationen zu den Abbild Gruppen) und zum RIS-Image.|
|/Detailed|Gibt an, dass alle Bild Metadaten aus jedem Bild zurückgegeben werden sollen. Wenn diese Option nicht verwendet wird, besteht das Standardverhalten darin, nur den Bildnamen, die Beschreibung und den Dateinamen zurückzugeben.|
## <a name="examples"></a>Beispiele
Wenn Sie Informationen zu den Bildern anzeigen möchten, geben Sie eine der folgenden Informationen ein:
```
wdsutil /Get-AllImages /Show:Install
wdsutil /verbose /Get-AllImages /Server:MyWDSServer /Show:All /detailed
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-add-image-command.md) 
 "Add-Image" [Verwenden des Befehls](using-the-copy-image-command.md) 
 "Copy-Image" [Verwenden des Befehls](using-the-export-image-command.md) 
 "Export-Image" [Verwenden des Remove-Image-Befehls](using-the-remove-image-command.md) 
 [Verwenden des "Replace-Image"-Befehls](using-the-replace-image-command.md) 
 [Unterbefehl: Set-Image](subcommand-set-image.md)
