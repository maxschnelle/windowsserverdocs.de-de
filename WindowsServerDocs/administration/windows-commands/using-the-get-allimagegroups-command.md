---
title: Get-allimagegroups
description: Referenz Thema für Get-allimagegroups, das Informationen zu allen Image Gruppen auf einem Server und alle Images in diesen Abbild Gruppen abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ca06533-bcf5-4590-ac8e-263d6c9874f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 204618955e91f1c9c9659d37ac3dfe2a01897c51
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720029"
---
# <a name="get-allimagegroups"></a>Get-allimagegroups

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ruft Informationen zu allen Abbild Gruppen auf einem Server und alle Images in diesen Abbild Gruppen ab.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-AllImageGroups [/Server:<Server name>] [/detailed]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Detailed|Gibt die Bild Metadaten aus jedem Bild zurück. Wenn dieser Parameter nicht verwendet wird, besteht das Standardverhalten darin, nur den Bildnamen, die Beschreibung und den Dateinamen für jedes Image zurückzugeben.|
## <a name="examples"></a>Beispiele
Zum Anzeigen von Informationen zu den Bildgruppen geben Sie eine der folgenden Informationen ein:
```
wdsutil /Get-AllImageGroups
wdsutil /verbose /Get-AllImageGroups /Server:MyWDSServer /detailed
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
mithilfe des Befehls "[Add-ImageGroup](using-the-add-imagegroup-command.md)
" mithilfe des Befehls "[Get-ImageGroup](using-the-get-imagegroup-command.md)
" mit dem Befehl "[Remove-ImageGroup Command](using-the-remove-imagegroup-command.md)
[unter Command: Set-ImageGroup](subcommand-set-imagegroup.md) "
