---
title: nslookup set class
description: Referenz Artikel für den Befehl "nslookup Set Class", durch den die Abfrage Klasse geändert wird.
ms.topic: reference
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5f4eb309c3972230247bf231b0e731e146d8159a
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634034"
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
