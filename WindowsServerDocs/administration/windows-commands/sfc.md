---
title: sfc
description: Windows-Befehls Thema für SFC, das die Integrität aller geschützten Systemdateien scannt und überprüft und falsche Versionen durch korrekte Versionen ersetzt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c58c25da-e028-42a6-9e10-973484a4b953
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7663c8e3527995e2d3ec874dff6fa972e7e83ddd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834323"
---
# <a name="sfc"></a>sfc

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überprüft und überprüft die Integrität aller geschützten Systemdateien und ersetzt falsche Versionen durch korrekte Versionen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax
```
sfc [/scannow] [/verifyonly] [/scanfile=<file>] [/verifyfile=<file>] [/offwindir=<offline windows directory> /offbootdir=<offline boot directory>]
```

#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/scannow|Überprüft die Integrität aller geschützten Systemdateien und repariert Dateien mit Problemen, wenn möglich.|
|/verifyonly|Überprüft die Integrität aller geschützten Systemdateien. Es wird kein Reparaturvorgang durchgeführt.|
|/scanfile|Überprüft die Integrität der angegebenen Datei und repariert die Datei nach Möglichkeit, wenn Probleme erkannt werden.|
|\<Datei >|Angegebene vollständiger Pfad und Dateiname|
|/verifyfile|überprüft die Integrität der angegebenen Datei. Es wird kein Reparaturvorgang durchgeführt.|
|/offwindir|Gibt den Speicherort des Windows-offline Verzeichnisses für die Offline Reparatur an.|
|/offbootdir|Gibt den Speicherort des Offline-Start Verzeichnisses für Offline an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Sie müssen als Mitglied der Gruppe "Administratoren" angemeldet sein, um " **sfc. exe**" ausführen zu können.
-   Wenn **sfc** ermittelt, dass eine geschützte Datei überschrieben wurde, ruft Sie die korrekte Version der Datei aus dem Ordner **systemroot\system32\dllcache** ab und ersetzt dann die falsche Datei.
-   Es gibt funktionale Unterschiede zwischen **sfc** unter Windows Server 2003, Windows Server 2008 und Windows Server 2008 R2:
-   Weitere Informationen zu **sfc** unter Windows Server 2003 finden Sie im [Artikel 310747](https://go.microsoft.com/fwlink/?LinkId=227069) der Microsoft Knowledge Base.
-   Weitere Informationen zu **sfc** unter Windows Server 2008 und Windows Server 2008 R2 finden Sie unter [System File Checker](https://go.microsoft.com/fwlink/?LinkId=227071).

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Geben Sie Folgendes ein, um die **Datei kernel32. dll**zu überprüfen:
```
sfc /verifyfile=c:\windows\system32\kernel32.dll
```
Geben Sie Folgendes ein, um die Offline Reparatur der Datei **Kernel32. dll** mit einem Offline-Start Verzeichnis festzulegen, das auf **d:** und dem Offline-Windows-Verzeichnis **d:\Windows aus**festgelegt ist:
```
sfc /scanfile=d:\windows\system32\kernel32.dll /offbootdir=d:\ /offwindir=d:\windows
```

## <a name="additional-references"></a>Weitere Verweise
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

