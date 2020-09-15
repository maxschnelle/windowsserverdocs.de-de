---
title: tzutil
description: Referenz Artikel zu "TZUtil", in dem das Windows-Zeit Zonen Dienstprogramm angezeigt wird.
ms.topic: reference
ms.assetid: bcf6e007-c9b6-4df5-83c5-ed7b4b1b5913
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3640da68f48944fd9d67486dface4cfd77531d57
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90078457"
---
# <a name="tzutil"></a>tzutil

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt das Windows-Zeit Zonen Dienstprogramm an.

## <a name="syntax"></a>Syntax

```
tzutil [/?] [/g] [/s <timezoneID>[_dstoff]] [/l]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /g | Zeigt die aktuelle Zeit Zonen-ID an. |
| /s `<timezoneID>[_dstoff]` | Legt die aktuelle Zeitzone mithilfe der angegebenen Zeit Zonen-ID fest. Mit dem **_dstoff** Suffix werden die Anpassungen der Sommerzeit für die Zeitzone deaktiviert (falls zutreffend). Ihr Wert muss in Anführungszeichen eingeschlossen werden. |
| /l | Listet alle gültigen Zeit Zonen-IDs und anzeigen Amen auf. Die Ausgabe wird wie folgt angezeigt:<ul><li>`<display name>`</li><li>`<time zone ID>`</li></ul> |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

Der Exitcode **0** gibt an, dass der Befehl erfolgreich abgeschlossen wurde.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die aktuelle Zeit Zonen-ID anzuzeigen:

```
tzutil /g
```

Um die aktuelle Zeitzone auf Pacific Normalzeit festzulegen, geben Sie Folgendes ein:

```
tzutil /s "Pacific Standard time"
```

Geben Sie Folgendes ein, um die aktuelle Zeitzone auf Pacific Normalzeit festzulegen und die Anpassungen der Sommerzeit zu deaktivieren:

```
tzutil /s "Pacific Standard time_dstoff"
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
