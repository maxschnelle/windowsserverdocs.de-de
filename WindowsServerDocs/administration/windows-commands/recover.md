---
title: recover
description: Referenz Artikel für den Wiederherstellungs Befehl, der lesbare Informationen von einem fehlerhaften oder fehlerhaften Datenträger wiederherstellt.
ms.topic: article
ms.assetid: cf9be2e3-90c8-4773-a201-dc503b91948e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0c3d709d76743df4c1a653f0f0a19e8319b0e0f1
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884315"
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
