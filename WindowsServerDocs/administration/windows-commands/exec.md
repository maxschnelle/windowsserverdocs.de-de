---
title: exec
description: Referenz Thema für den exec-Befehl, der eine Skriptdatei auf dem lokalen Computer ausführt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 956f3d4a7c5992980aea0fc0f5933ee7def48381
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436106"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [DiskShadow-Befehl](diskshadow.md)
