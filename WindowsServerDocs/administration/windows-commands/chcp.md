---
title: chcp
description: Referenz Artikel für den CHCP-Befehl, durch den die Codepage der aktiven Konsole geändert wird.
ms.topic: reference
ms.assetid: dc7b1c71-7b80-443d-9cf1-9bcf305aa1fd
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ef70d73253782528bcd54f7cfd6f98de9d941702
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89629829"
---
# <a name="chcp"></a>chcp

Ändert die aktive Konsolen Codepage. Bei Verwendung ohne Parameter zeigt **chcp** die Nummer der aktiven Konsolen Codepage an.

## <a name="syntax"></a>Syntax

```
chcp [<nnn>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<nnn>` | Gibt die Codepage an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

In der folgenden Tabelle werden die einzelnen unterstützten Codeseiten und deren Land/Region oder Sprache aufgeführt:

| Codepage | Land/Region oder Sprache |
| --------- | -------------------------- |
| 437 | USA |
| 850 | Mehrsprachig (lateinisch I) |
| 852 | Slawisch (Lateinisch II) |
| 855 | Kyrillisch (Russisch) |
| 857 | Türkisch |
| 860 | Portugiesisch |
| 861 | Isländisch |
| 863 | Französisch (Kanada) |
| 865 | Nordischen |
| 866 | Russisch |
| 869 | Modernes Griechisch |
| 936 | Chinesisch |

#### <a name="remarks"></a>Hinweise

- Nur die mit Windows installierte OEM-Codepage (Original Equipment Manufacturer) wird in einem Eingabe Aufforderungs Fenster, in dem Raster Schriftarten verwendet werden, ordnungsgemäß angezeigt. Andere Codepages werden im Vollbildmodus oder in Eingabe Aufforderungs Fenstern, die TrueType-Schriftarten verwenden, ordnungsgemäß angezeigt.

- Sie müssen keine Codepages vorbereiten (wie in MS MS-DOS).

- Programme, die Sie starten, nachdem Sie eine neue Codepage zugewiesen haben, verwenden die neue Codepage. Programme (mit Ausnahme von Cmd.exe), die Sie vor dem Zuweisen der neuen Codepage gestartet haben, verwenden jedoch weiterhin die ursprüngliche Codepage.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Einstellung der aktiven Codepage anzuzeigen:

```
chcp
```

Eine Meldung ähnlich der folgenden wird angezeigt: `Active code page: 437`

Um die aktive Codepage in 850 (mehrsprachig) zu ändern, geben Sie Folgendes ein:

```
chcp 850
```

Wenn die angegebene Codepage ungültig ist, wird die folgende Fehlermeldung angezeigt: `Invalid code page`

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
