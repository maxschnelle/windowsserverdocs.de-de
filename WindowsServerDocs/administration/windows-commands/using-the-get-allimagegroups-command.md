---
title: Mithilfe des Befehls Get-AllImageGroups
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ca06533-bcf5-4590-ac8e-263d6c9874f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 917f61327a3d39ee97c5fd59072884f7844c487e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822351"
---
# <a name="using-the-get-allimagegroups-command"></a>Mithilfe des Befehls Get-AllImageGroups

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ruft Informationen über alle imagegruppen auf einem Server und alle zugehörigen Images in diesen imagegruppen ab.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-AllImageGroups [/Server:<Server name>] [/detailed]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
|[/detailed]|Gibt die Metadaten zu Bildern von jedes Image zurück. Wenn dieser Parameter nicht verwendet wird, ist das Standardverhalten, um nur die Image-Name, Beschreibung und Dateinamen für jedes Bild zurückzugeben.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie eine der folgenden Schritte aus, zum Anzeigen von Informationen zu den imagegruppen:
```
wdsutil /Get-AllImageGroups
wdsutil /verbose /Get-AllImageGroups /Server:MyWDSServer /detailed
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Add-ImageGroup](using-the-add-imagegroup-command.md)
[mit dem Befehl Get-ImageGroup](using-the-get-imagegroup-command.md)
[mithilfe der Remove-ImageGroup Befehl](using-the-remove-imagegroup-command.md)
[Unterbefehl: Set-ImageGroup](subcommand-set-imagegroup.md)
