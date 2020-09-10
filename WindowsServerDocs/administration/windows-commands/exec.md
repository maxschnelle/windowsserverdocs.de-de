---
title: exec
description: Referenz Artikel für den Befehl "exec", der eine Skriptdatei auf dem lokalen Computer ausführt.
ms.topic: reference
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 668dc3cf3d93d11066d7dece4309f586b3a5b964
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635962"
---
# <a name="exec"></a>exec

Führt eine Skriptdatei auf dem lokalen Computer aus. Mit diesem Befehl werden auch Daten im Rahmen einer Sicherungs-oder Wiederherstellungs Sequenz dupliziert oder wieder hergestellt. Wenn das Skript fehlschlägt, wird ein Fehler zurückgegeben, und DiskShadow wird beendet.

Bei der Datei kann es sich um ein **cmd** -Skript handeln.

## <a name="syntax"></a>Syntax

```
exec <scriptfile.cmd>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<scriptfile.cmd>` | Gibt die Skriptdatei an, die ausgeführt werden soll. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [DiskShadow-Befehl](diskshadow.md)
