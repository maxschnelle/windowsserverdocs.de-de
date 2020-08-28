---
title: exec
description: Referenz Artikel für den Befehl "exec", der eine Skriptdatei auf dem lokalen Computer ausführt.
ms.topic: reference
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e0e4cd876fe5c6abcf909f20e330ff347db1113b
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89023994"
---
# <a name="exec"></a>exec

Führt eine Skriptdatei auf dem lokalen Computer aus. Mit diesem Befehl werden auch Daten im Rahmen einer Sicherungs-oder Wiederherstellungs Sequenz dupliziert oder wieder hergestellt. Wenn das Skript fehlschlägt, wird ein Fehler zurückgegeben, und DiskShadow wird beendet.

Bei der Datei kann es sich um ein **cmd** -Skript handeln.

## <a name="syntax"></a>Syntax

```
exec <scriptfile.cmd>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<scriptfile.cmd>` | Gibt die Skriptdatei an, die ausgeführt werden soll. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [DiskShadow-Befehl](diskshadow.md)
