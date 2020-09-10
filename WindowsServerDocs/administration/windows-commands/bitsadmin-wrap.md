---
title: bitsadmin wrap
description: Referenz Artikel für den Befehl bizadmin Wrap, der jede Zeile von Ausgabetext umschließt, die über den rechten Rand des Befehls Fensters zur nächsten Zeile hinausgeht.
ms.topic: reference
ms.assetid: 14e57522-539d-4621-ad15-09f7a44ccab7
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 24fa50e153d52ec74ab728a132aadd1b95c7a9da
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630383"
---
# <a name="bitsadmin-wrap"></a>bitsadmin wrap

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Umschließt eine beliebige Zeile von Ausgabetext, der über den rechten Rand des Befehls Fensters zur nächsten Zeile erweitert wird. Dieser Switch muss vor allen anderen Schaltern angegeben werden.

Standardmäßig umschließen alle Switches außer dem Schalter [bizadmin Monitor](bitsadmin-monitor.md) den Ausgabetext.

## <a name="syntax"></a>Syntax

```
bitsadmin /wrap <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ---------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

Zum Abrufen von Informationen für den Auftrag mit dem Namen *mydownloadjob* und zum Einschließen des Ausgabe Texts:

```
bitsadmin /wrap /info myDownloadJob /verbose
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
