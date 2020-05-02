---
title: recover
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cf9be2e3-90c8-4773-a201-dc503b91948e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b316ed26f008a62f88aaeb4a7a7f3030d08f1588
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722623"
---
# <a name="recover"></a>recover



Stellt lesbare Informationen von einem ungültigen oder fehlerhaften Datenträger wieder her



## <a name="syntax"></a>Syntax

```
recover [<Drive>:][<Path>]<FileName>
```

### <a name="parameters"></a>Parameter

|           Parameter           |                                          BESCHREIBUNG                                          |
|-------------------------------|-----------------------------------------------------------------------------------------------|
| [\<Laufwerk>:] [<Path>]<FileName> | Gibt den Speicherort und den Namen der Datei an, die Sie wiederherstellen möchten. *Dateiname* ist erforderlich. |
|              /?               |                             Zeigt die Hilfe an der Eingabeaufforderung an.                              |

## <a name="remarks"></a>Bemerkungen

-   Mit dem Befehl "Wiederherstellen" wird eine Datei sektorweise gelesen und Daten aus den guten Sektoren **wieder hergestellt** . Daten in fehlerhaften Sektoren gehen verloren.
-   Ungültige von **chkdsk** gemeldete Sektoren wurden als schlecht gekennzeichnet, als der Datenträger für den Betrieb vorbereitet wurde. Sie stellen keine Gefahr dar, und die **Wiederherstellung** wirkt sich nicht auf diese aus.
-   Da alle Daten in fehlerhaften Sektoren verloren gehen, wenn Sie eine Datei wiederherstellen, sollten Sie jeweils nur eine Datei wiederherstellen.
-   Mit dem **Wiederherstellungs** Befehl können keine Platzhalter Zeichen (**&#42;** und **?**) verwendet werden. Sie müssen eine Datei angeben (und den Speicherort der Datei, wenn Sie sich nicht im aktuellen Verzeichnis befindet).

## <a name="examples"></a>Beispiele

Um die Datei Story. txt im Verzeichnis "\fiction" auf Laufwerk D wiederherzustellen, geben Sie Folgendes ein:
```
recover d:\fiction\story.txt 
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)