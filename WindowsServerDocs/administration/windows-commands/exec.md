---
title: exec
description: Referenz Artikel für den Befehl "exec", der eine Skriptdatei auf dem lokalen Computer ausführt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b4c9ff71b886bd84120bd3af7c1f8d8c143425da
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932314"
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
