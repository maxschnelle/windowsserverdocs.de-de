---
title: Scwcmd-Ansicht
description: Referenz Artikel für * * * *-
ms.topic: reference
ms.assetid: 7995959a-d93e-4865-a6a0-2ab18c2bb47f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 985b8edb2ef6a99abeb9545dfe62fa5255080b2c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89636905"
---
# <a name="scwcmd-view"></a>Scwcmd: Ansicht

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Rendert eine XML-Datei mithilfe einer angegebenen XSL-Transformation. Dieser Befehl kann nützlich sein, um SCW (Security Configuration Wizard). XML-Dateien unter Verwendung verschiedener Ansichten anzuzeigen.

## <a name="syntax"></a>Syntax

```
scwcmd view /x:<Xmlfile.xml> [/s:<Xslfile.xsl>]
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/x\<Xmlfile.xml>|Gibt die XML-Datei an, die angezeigt werden soll. Dieser Parameter muss angegeben werden.|
|/s\<Xslfile.xsl>|Gibt die XSL-Transformation an, die als Teil des Renderingprozesses auf die XML-Datei angewendet werden soll. Dieser Parameter ist für SCW. XML-Dateien optional. Wenn der **View** -Befehl verwendet wird, um eine SCW. XML-Datei zu rendieren, wird automatisch versucht, die richtige Standard Transformation für die angegebene XML-Datei zu laden. Wenn eine XSL-Transformation angegeben ist, muss die Transformation unter der Annahme geschrieben werden, dass sich die XML-Datei im gleichen Verzeichnis wie die XSL-Transformation befindet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Scwcmd.exe ist nur auf Computern verfügbar, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird.

## <a name="examples"></a>Beispiele

Wenn Sie Policyfile.xml mithilfe der Transformation policyview. xsl anzeigen möchten, geben Sie Folgendes ein:
```
scwcmd view /x:C:\policies\Policyfile.xml /s:C:\viewers\Policyview.xsl
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)