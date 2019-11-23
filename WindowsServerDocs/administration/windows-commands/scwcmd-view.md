---
title: Scwcmd-Ansicht
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7995959a-d93e-4865-a6a0-2ab18c2bb47f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a69db16696f42950af97b62ba6f28c4083954137
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371187"
---
# <a name="scwcmd-view"></a>scwcmd: view

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Rendert eine XML-Datei mithilfe einer angegebenen XSL-Transformation. Dieser Befehl kann nützlich sein, um SCW (Security Configuration Wizard). XML-Dateien unter Verwendung verschiedener Ansichten anzuzeigen.

## <a name="syntax"></a>Syntax

```
scwcmd view /x:<Xmlfile.xml> [/s:<Xslfile.xsl>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/x:\<xmlfile. XML >|Gibt die XML-Datei an, die angezeigt werden soll. Dieser Parameter muss angegeben werden.|
|/s:\<xslfile. xsl >|Gibt die XSL-Transformation an, die als Teil des Renderingprozesses auf die XML-Datei angewendet werden soll. Dieser Parameter ist für SCW. XML-Dateien optional. Wenn der **View** -Befehl verwendet wird, um eine SCW. XML-Datei zu rendieren, wird automatisch versucht, die richtige Standard Transformation für die angegebene XML-Datei zu laden. Wenn eine XSL-Transformation angegeben ist, muss die Transformation unter der Annahme geschrieben werden, dass sich die XML-Datei im gleichen Verzeichnis wie die XSL-Transformation befindet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Scwcmd. exe ist nur auf Computern verfügbar, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird.

## <a name="BKMK_Examples"></a>Beispiele

Wenn Sie policyFile. XML mithilfe der Transformation policyview. xsl anzeigen möchten, geben Sie Folgendes ein:
```
scwcmd view /x:C:\policies\Policyfile.xml /s:C:\viewers\Policyview.xsl
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)