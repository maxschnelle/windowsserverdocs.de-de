---
title: shift
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b56574e8-570a-4cc9-bbac-1b94fbf6a47a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 52b3012a39409f9d48ae8aa7608e7bd0af5787d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858821"
---
# <a name="shift"></a>shift



Ändert die Position der Batchparameter in einer Batchdatei.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
shift [/n <N>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/n \<N>|Gibt an, dass das Starten der Verschiebung auf der *N*th-Argument, in denen *N* ein Wert zwischen 0 und 8 ist. Erfordert befehlserweiterungen, die standardmäßig aktiviert sind.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Die **UMSCHALT** Befehl ändert die Werte der Parameter **%0** über **%9** jeden Parameter in dem vorherigen Beispiel kopieren, den Wert der **%1** in kopiert **%0**, den Wert der **%2** in kopiert **%1**und so weiter. Dies ist nützlich für das Schreiben von einer Batchdatei, die den gleichen Vorgang auf einer beliebigen Anzahl von Parametern ausführt.
-   Wenn der befehlserweiterungen aktiviert sind, die **UMSCHALT** Befehl unterstützt die **/n** Befehlszeilenoption. Die **/n** Option zum Starten der Verschiebung auf der n-te Argument gibt an, in denen **N** ein Wert zwischen 0 und 8 ist. Z. B. **UMSCHALT /2** verschoben würde **%3** zu **%2**, **%4** zu **%3**, und so weiter, und lassen Sie **%0** und **%1** nicht betroffen. Befehlserweiterungen sind standardmäßig aktiviert.
-   Können Sie die **UMSCHALT** Befehl aus, um eine Batchdatei erstellen, die mehr als 10 Batchparameter akzeptieren kann. Wenn Sie mehr als 10 Parameter in der Befehlszeile angeben, die, die angezeigt werden nach der zehnten (**%9**) werden die verschobenen einzeln nacheinander in **%9**.
-   Die **UMSCHALT** Befehl hat keine Auswirkungen auf die **% \*** batch-Parameter.
-   Es ist nicht abwärtskompatibel **UMSCHALT** Befehl. Nach dem Implementieren der **UMSCHALT** Befehl, den Batchparameter kann nicht wiederhergestellt werden (**%0**), die vorhanden waren, bevor Sie die UMSCHALTTASTE.

## <a name="BKMK_examples"></a>Beispiele für

Die folgenden Zeilen aus einer Beispiel-Batchdatei namens kopieren.bat veranschaulichen, wie **UMSCHALT** mit einer beliebigen Anzahl von Batchparameter. In diesem Beispiel kopiert kopieren.bat eine Liste der Dateien in ein bestimmtes Verzeichnis. Die Batchparameter werden durch die Namensargumente Verzeichnis- und Dateinamen dargestellt.
```
@echo off 
rem MYCOPY.BAT copies any number of files
rem to a directory.
rem The command uses the following syntax:
rem mycopy dir file1 file2 ... 
set todir=%1
:getfile
shift
if "%1"=="" goto end
copy %1 %todir%
goto getfile
:end
set todir=
echo All done
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)