---
title: nslookup set class
description: Referenz Thema für den Befehl "nslookup Set Class", mit dem die Abfrage Klasse geändert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e939be13eedcab557dc6dcbe16f2e83f810c20d5
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721563"
---
# <a name="nslookup-set-class"></a>nslookup set class

Ändert die Query-Klasse. Die-Klasse gibt die Protokoll Gruppe der Informationen an.

## <a name="syntax"></a>Syntax

```
set class=<class>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<class>` | Gültige Werte sind:<ul><li>**In:** Gibt die Internet Klasse an. Dies ist der Standardwert.</li><li>**Chaos:** Gibt die Chaos-Klasse an.</li><li>**Hesiod:** Gibt die mit-Athena-Hesiod-Klasse an.</li><li>**Beliebig:** Gibt an, dass die zuvor aufgelisteten Werte verwendet werden sollen.</li></ul> |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
