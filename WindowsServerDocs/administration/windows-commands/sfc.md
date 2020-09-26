---
title: sfc
description: Referenz Artikel für den SFC-Befehl, der die Integrität aller geschützten Systemdateien scannt und überprüft und falsche Versionen durch korrekte Versionen ersetzt.
ms.topic: reference
ms.assetid: c58c25da-e028-42a6-9e10-973484a4b953
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 829c6e328ad0ea993e11cb5eb5d96d99f0d52476
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388940"
---
# <a name="sfc"></a>sfc

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überprüft und überprüft die Integrität aller geschützten Systemdateien und ersetzt falsche Versionen durch korrekte Versionen. Wenn mit diesem Befehl ermittelt wird, dass eine geschützte Datei überschrieben wurde, ruft Sie die korrekte Version der Datei aus dem Ordner **systemroot\system32\dllcache** ab und ersetzt dann die falsche Datei.

> [!IMPORTANT]
> Sie müssen als Mitglied der Gruppe "Administratoren" angemeldet sein, um diesen Befehl ausführen zu können.

## <a name="syntax"></a>Syntax

```
sfc [/scannow] [/verifyonly] [/scanfile=<file>] [/verifyfile=<file>] [/offwindir=<offline windows directory> /offbootdir=<offline boot directory>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /scannow | Überprüft die Integrität aller geschützten Systemdateien und repariert Dateien mit Problemen, wenn möglich. |
| /verifyonly | Überprüft die Integrität aller geschützten Systemdateien, ohne dass Reparaturen durchgeführt werden. |
| /scanfile `<file>` | Scannt die Integrität der angegebenen Datei (vollständiger Pfad und Dateiname) und versucht, etwaige Probleme zu beheben, wenn Sie erkannt werden. |
| /verifyfile `<file>` | Überprüft die Integrität der angegebenen Datei (vollständiger Pfad und Dateiname), ohne dass Reparaturen durchgeführt werden. |
| /offwindir `<offline windows directory>` | Gibt den Speicherort des Windows-offline Verzeichnisses für die Offline Reparatur an. |
| /offbootdir `<offline boot directory>` | Gibt den Speicherort des Offline-Start Verzeichnisses für die Offline Reparatur an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Um die *kernel32.dll Datei*zu überprüfen, geben Sie

```
sfc /verifyfile=c:\windows\system32\kernel32.dll
```

Geben Sie Folgendes ein, um die Offline Reparatur der *kernel32.dll* Datei mit einem Offline-Start Verzeichnis festzulegen, das auf * D: \* und einem Offline-Windows-Verzeichnis auf " *d:\Windows*" festgelegt ist:

```
sfc /scanfile=D:\windows\system32\kernel32.dll /offbootdir=D:\ /offwindir=d:\windows
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
