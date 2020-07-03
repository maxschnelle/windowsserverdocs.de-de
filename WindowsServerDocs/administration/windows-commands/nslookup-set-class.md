---
title: nslookup set class
description: Referenz Artikel für den Befehl "nslookup Set Class", durch den die Abfrage Klasse geändert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 073f27f6f10721b11e6d0889d1cb8c16f15db283
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934423"
---
# <a name="nslookup-set-class"></a>nslookup set class

Ändert die Query-Klasse. Die-Klasse gibt die Protokoll Gruppe der Informationen an.

## <a name="syntax"></a>Syntax

```
set class=<class>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<class>` | Gültige Werte sind:<ul><li>**In:** Gibt die Internet Klasse an. Dies ist der Standardwert.</li><li>**Chaos:** Gibt die Chaos-Klasse an.</li><li>**Hesiod:** Gibt die mit-Athena-Hesiod-Klasse an.</li><li>**Beliebig:** Gibt an, dass die zuvor aufgelisteten Werte verwendet werden sollen.</li></ul> |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
