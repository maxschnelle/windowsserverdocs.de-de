---
title: sfc
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c58c25da-e028-42a6-9e10-973484a4b953
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1db0ab81c9469c88ddb64a367a9dc98a1fd9b70c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832391"
---
# <a name="sfc"></a>sfc

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Überprüft, und überprüft die Integrität des Systems für alle geschützten Dateien und falsche Versionen mit entsprechenden Versionen ersetzt.
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax
```
sfc [/scannow] [/verifyonly] [/scanfile=<file>] [/verifyfile=<file>] [/offwindir=<offline windows directory> /offbootdir=<offline boot directory>]
```

### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/scannow|Überprüft die Integrität aller geschützten Systemdateien und Reparatur von Dateien mit Problemen, wenn möglich.|
|/verifyonly|Überprüft die Integrität aller geschützten Systemdateien. Ohne Reparaturvorgang wird ausgeführt.|
|/scanfile|Überprüft die Integrität der angegebenen Datei und die Datei repariert, wenn Probleme erkannt werden, wenn möglich.|
|\<file>|Angegebene vollständiger Pfad und Dateiname|
|/verifyfile|überprüft die Integrität der angegebenen Datei. Ohne Reparaturvorgang wird ausgeführt.|
|/offwindir|Gibt den Speicherort des offline Windows-Verzeichnisses, für die offline-Reparatur.|
|/offbootdir|Gibt an, den Speicherort der offline Startverzeichnis nach offline|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Sie müssen als Mitglied der Gruppe "Administratoren" Ausführen angemeldet sein **sfc.exe**.
-   Wenn **sfc** ermittelt, dass eine geschützte Datei überschrieben, ruft es ab, die richtige Version der Datei, aus der **systemroot\system32\dllcache** Ordner, und klicken Sie dann die falsche Datei ersetzt.
-   Es sind die Funktionsunterschiede zwischen **sfc** unter Windows Server 2003, Windows Server 2008 und Windows Server 2008 R2:
-   Weitere Informationen zu **sfc** unter Windows Server 2003 finden Sie unter [Artikel 310747](https://go.microsoft.com/fwlink/?LinkId=227069) in der Microsoft Knowledge Base.
-   Weitere Informationen zu **sfc** unter Windows Server 2008 und Windows Server 2008 R2, finden Sie unter [Systemdatei-Überprüfungsprogramm](https://go.microsoft.com/fwlink/?LinkId=227071).

## <a name="BKMK_examples"></a>Beispiele für
So überprüfen die **Datei "Kernel32.dll"**, Typ:
```
sfc /verifyfile=c:\windows\system32\kernel32.dll
```
Zum Setup Offlinereparatur von der **"Kernel32.dll"** -Datei mit einer offline-Startverzeichnis festgelegt **"d:"** und offline Windowsverzeichnis festgelegt **d:\windows**, Typ:
```
sfc /scanfile=d:\windows\system32\kernel32.dll /offbootdir=d:\ /offwindir=d:\windows
```

## <a name="additional-references"></a>Weitere Verweise
-   [Befehlszeilensyntax](command-line-syntax-key.md)

