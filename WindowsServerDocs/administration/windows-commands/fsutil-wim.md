---
title: fsutil wim
description: Referenz Artikel für den WIM-Befehl fsutil, der Funktionen zum Ermitteln und Verwalten von Dateien mit Windows-Abbildern (WIM) bereitstellt.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 6c6ff819-f349-4aea-b0be-1f637f631736
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 791eb80942187b0a0309097b2b785fb3dcea88ec
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931417"
---
# <a name="fsutil-wim"></a>fsutil wim

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10

Stellt Funktionen zum Ermitteln und Verwalten von Dateien mit Windows-Abbildern (WIM) bereit.

## <a name="syntax"></a>Syntax

```
fsutil wim [enumfiles] <drive name> <data source>
fsutil wim [enumwims] <drive name>
fsutil wim [queryfile] <filename>
fsutil wim [removewim] <drive name> <data source>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| EnumFiles | Listet WIM-gestützte Dateien auf. |
| `<drive name>` | Gibt den Namen des Laufwerks an. |
| `<data source>` | Gibt die Datenquelle an. |
| enumwims | Listet die unterstützten WIM-Dateien auf. |
| QueryFile | Fragt ab, ob die Datei durch WIM unterstützt wird, und zeigt ggf. Details zur WIM-Datei an. |
| `<filename>` | Gibt den Dateinamen an. |
| removewim | Entfernt eine WIM-Datei aus Unterstützungs Dateien. |

### <a name="examples"></a>Beispiele

Zum Auflisten der Dateien für Laufwerk C: Geben Sie aus der Datenquelle 0 Folgendes ein:

```
fsutil wim enumfiles C: 0
```

Geben Sie Folgendes ein, um die zugrunde liegenden WIM-Dateien für Laufwerk C: aufzuzählen:

```
fsutil wim enumwims C:
```

Um festzustellen, ob eine Datei durch WIM unterstützt wird, geben Sie Folgendes ein:

```
fsutil wim C:\Windows\Notepad.exe
```

Geben Sie Folgendes ein, um die WIM-Datei aus den Unterstützungs Dateien für Volume C: und Data Source 2 zu entfernen:

```
fsutil wim removewims C: 2
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)
