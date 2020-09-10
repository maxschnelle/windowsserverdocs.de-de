---
title: recover
description: Referenz Artikel für den Wiederherstellungs Befehl, der lesbare Informationen von einem fehlerhaften oder fehlerhaften Datenträger wiederherstellt.
ms.topic: reference
ms.assetid: cf9be2e3-90c8-4773-a201-dc503b91948e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9bb402c5821ae8caa0a83d132a7fbeef9c88b4bd
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637299"
---
# <a name="recover"></a>recover

Stellt lesbare Informationen von einem ungültigen oder fehlerhaften Datenträger wieder her Mit diesem Befehl wird eine Datei (sektorweise) gelesen und Daten aus den guten Sektoren wieder hergestellt. Daten in fehlerhaften Sektoren gehen verloren. Da alle Daten in fehlerhaften Sektoren verloren gehen, wenn Sie eine Datei wiederherstellen, sollten Sie jeweils nur eine Datei wiederherstellen.

Ungültige, vom **chkdsk** -Befehl gemeldete Sektoren wurden als schlecht gekennzeichnet, als der Datenträger für den Betrieb vorbereitet wurde. Sie stellen keine Gefahr dar, und die **Wiederherstellung** wirkt sich nicht auf diese aus.

## <a name="syntax"></a>Syntax

```
recover [<drive>:][<path>]<filename>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `[<drive>:][<path>]<filename>` | Gibt den Dateinamen (und den Speicherort der Datei an, wenn er sich nicht im aktuellen Verzeichnis befindet), die Sie wiederherstellen möchten. *Dateiname* ist erforderlich, und Platzhalter werden nicht unterstützt. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Wenn Sie die Datei *story.txt* im Verzeichnis " *\fiction* " auf Laufwerk D wiederherstellen möchten, geben Sie Folgendes ein:

```
recover d:\fiction\story.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
