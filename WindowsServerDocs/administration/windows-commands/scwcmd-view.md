---
title: Scwcmd-Ansicht
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 2ef1dd72903108edd6c5fb450c536a9325fcf546
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889551"
---
# <a name="scwcmd-view"></a>scwcmd: view

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Rendert eine XML-Datei mit einer angegebenen XSL-Transformation. Dieser Befehl kann zum Anzeigen von XML-Dateien (Security Configuration Wizard, SCW) mit anderen Ansichten nützlich sein.

## <a name="syntax"></a>Syntax

```
scwcmd view /x:<Xmlfile.xml> [/s:<Xslfile.xsl>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ x:\<Xmlfile.xml >|Gibt die XML-Datei angezeigt werden. Dieser Parameter muss angegeben werden.|
|/s:\<Xslfile.xsl>|Gibt an, die XSL-Transformation, die für die XML-Datei als Teil des Renderingprozesses gelten. Dieser Parameter ist optional, für die SCW-XML-Dateien. Wenn die **Ansicht** Befehl wird verwendet, um eine XML-Datei mit dem Sicherheitskonfigurations-Assistenten zu rendern, wird automatisch versucht, die richtige Standard-Transformation für die angegebene XML-Datei zu laden. Wenn eine XSL-Transformation angegeben ist, muss die Transformation unter der Annahme geschrieben werden, die die XML-Datei im gleichen Verzeichnis wie die XSL-Transformation ist.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Scwcmd.exe ist nur auf Computern unter Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 verfügbar.

## <a name="BKMK_Examples"></a>Beispiele für

Um mit der Transformation für Policyview.xsl Policyfile.xml anzeigen, geben Sie Folgendes ein:
```
scwcmd view /x:C:\policies\Policyfile.xml /s:C:\viewers\Policyview.xsl
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)