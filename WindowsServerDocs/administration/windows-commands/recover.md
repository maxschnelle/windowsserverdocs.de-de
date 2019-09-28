---
title: recover
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf9be2e3-90c8-4773-a201-dc503b91948e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 415efe2d1e60ca70d68059b5702108440da735f3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371769"
---
# <a name="recover"></a>recover



Stellt lesbare Informationen von einem ungültigen oder fehlerhaften Datenträger wieder her

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
recover [<Drive>:][<Path>]<FileName>
```

## <a name="parameters"></a>Parameter

|           Parameter           |                                          Beschreibung                                          |
|-------------------------------|-----------------------------------------------------------------------------------------------|
| [\<laufwerk >:] [<Path>] <FileName> | Gibt den Speicherort und den Namen der Datei an, die Sie wiederherstellen möchten. *Dateiname* ist erforderlich. |
|              /?               |                             Zeigt die Hilfe an der Eingabeaufforderung an.                              |

## <a name="remarks"></a>Hinweise

-   Mit dem Befehl "Wiederherstellen" wird eine Datei sektorweise gelesen und Daten aus den guten Sektoren **wieder hergestellt** . Daten in fehlerhaften Sektoren gehen verloren.
-   Ungültige von **chkdsk** gemeldete Sektoren wurden als "schlecht" gekennzeichnet, als der Datenträger für den Betrieb vorbereitet wurde. Sie stellen keine Gefahr dar, und die **Wiederherstellung** wirkt sich nicht auf diese aus.
-   Da alle Daten in fehlerhaften Sektoren verloren gehen, wenn Sie eine Datei wiederherstellen, sollten Sie jeweils nur eine Datei wiederherstellen.
-   Mit dem **Wiederherstellungs** Befehl können **&#42;** keine Platzhalter Zeichen (und **?** ) verwendet werden. Sie müssen eine Datei angeben (und den Speicherort der Datei, wenn Sie sich nicht im aktuellen Verzeichnis befindet).

## <a name="BKMK_examples"></a>Beispiele

Um die Datei Story. txt im Verzeichnis "\fiction" auf Laufwerk D wiederherzustellen, geben Sie Folgendes ein:
```
recover d:\fiction\story.txt 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)