---
title: Verwenden die Copy-Image-Befehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bea41cf4-36e6-4181-afa5-00170ebd4fdc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 52c9c0bb45e60e76077bf90534e93f2c6fc1df18
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884041"
---
# <a name="using-the-copy-image-command"></a>Verwenden die Copy-Image-Befehl

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Kopiert Images, die innerhalb der gleichen Image-Gruppe sind. Verwenden Sie zum Kopieren von Images zwischen Abbildgruppen der [mithilfe des Export-Image-Befehls](using-the-export-image-command.md) Befehl und klicken Sie dann die [mit dem Befehl-Add-Image](using-the-add-image-command.md) Befehl.
Beispiele, wie Sie diesen Befehl verwenden können, finden Sie unter [Beispiele](#BKMK_examples).
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /copy-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Install
    mediaGroup:<Image group name>]
     [/Filename:<File name>]
     /DestinationImage
         /Name:<Name>
         /Filename:<File name>
         [/Description:<Description>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
Medien:<Image name>|Gibt den Namen des Bildes, das kopiert werden.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
mediatype:Install|Gibt den Typ der zu kopierende Bild. Diese Option muss festgelegt werden, um **installieren**.|
|\mediaGroup:<Image group name>]|Gibt die Image-Gruppe, die die zu kopierende Bild enthält. Wenn keine Abbildgruppe angegeben ist, und nur eine Gruppe, die auf dem Server vorhanden ist, wird standardmäßig diese Abbildgruppe verwendet werden. Wenn auf dem Server mehr als eine Abbildgruppe vorhanden ist, müssen Sie die Abbildgruppe angeben.|
|[/Filename:<Filename>]|Gibt den Dateinamen des Bildes, das kopiert werden. Wenn das Quellbild eindeutig anhand des Namens identifiziert werden kann, müssen Sie den Dateinamen angeben.|
|/DestinationImage|Gibt die Einstellungen für das Zielabbild an, wie in der folgenden Tabelle beschrieben.<br /><br />-/ Name:<Name> -legt den Anzeigenamen des Bildes, das kopiert werden.<br />-/ FileName:<Filename> -legt den Namen der Ziel-Bilddatei, die die imagekopie enthält.<br />-[/ Description: <Description>]-Legt die Beschreibung des Kopiervorgangs Image fest.|
## <a name="BKMK_examples"></a>Beispiele für
Erstellen eine Kopie des angegebenen Bilds, und nennen Sie sie WindowsVista.wim, geben Sie Folgendes ein:
```
wdsutil /copy-Imagmedia:"Windows Vista with Officemediatype:Install /DestinationImage /Name:"copy of Windows Vista with Office" /Filename:"WindowsVista.wim"
```
Um eine Kopie des angegebenen Bilds zu erstellen, Anwenden der angegebenen Einstellungen, und nennen Sie die Kopie WindowsVista.wim, Typ:
```
wdsutil /verbose /Progress /copy-Imagmedia:"Windows Vista with Office" /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/Filename:install.wim /DestinationImage /Name:"copy of Windows Vista with Office" /Filename:"WindowsVista.wim" /Description:"This is a copy of the original Windows image with Office installed"
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl-Add-Image](using-the-add-image-command.md)
[mithilfe des Export-Image-Befehls](using-the-export-image-command.md)
[mithilfe der Get-Image-Befehl](using-the-get-image-command.md)
[mit dem Remove-Image-Befehl](using-the-remove-image-command.md)
[mit dem Replace-Image-Befehl](using-the-replace-image-command.md) 
 [ Unterbefehl: Set-Image](subcommand-set-image.md)
