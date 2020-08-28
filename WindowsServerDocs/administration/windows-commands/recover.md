---
title: recover
description: Referenz Artikel für den Wiederherstellungs Befehl, der lesbare Informationen von einem fehlerhaften oder fehlerhaften Datenträger wiederherstellt.
ms.topic: reference
ms.assetid: cf9be2e3-90c8-4773-a201-dc503b91948e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad9d2f665bccca1413830e29c082c05a37d93a26
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037138"
---
# <a name="recover"></a>recover

Stellt lesbare Informationen von einem ungültigen oder fehlerhaften Datenträger wieder her Mit diesem Befehl wird eine Datei (sektorweise) gelesen und Daten aus den guten Sektoren wieder hergestellt. Daten in fehlerhaften Sektoren gehen verloren. Da alle Daten in fehlerhaften Sektoren verloren gehen, wenn Sie eine Datei wiederherstellen, sollten Sie jeweils nur eine Datei wiederherstellen.

Ungültige, vom **chkdsk** -Befehl gemeldete Sektoren wurden als schlecht gekennzeichnet, als der Datenträger für den Betrieb vorbereitet wurde. Sie stellen keine Gefahr dar, und die **Wiederherstellung** wirkt sich nicht auf diese aus.

## <a name="syntax"></a>Syntax

```
recover [<drive>:][<path>]<filename>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
