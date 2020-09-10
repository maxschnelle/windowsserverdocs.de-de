---
title: makecab
description: Referenz Artikel für den makecab-Befehl, mit dem vorhandene Dateien in eine CAB-Datei (CAB-Datei) verpackt werden.
ms.topic: reference
ms.assetid: 4da95297-c593-427b-9f76-2f389c46cbf4
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3ba4adf0d1cc94fc3fc1c5d4db15f641a5c30b90
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640178"
---
# <a name="makecab"></a>makecab

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verpacken vorhandener Dateien in eine CAB-Datei.


> [!NOTE]
> Dieser Befehl ist mit dem Befehl " [diantz](diantz.md)" identisch.

## <a name="syntax"></a>Syntax

```
makecab [/v[n]] [/d var=<value> ...] [/l <dir>] <source> [<destination>]
makecab [/v[<n>]] [/d var=<value> ...] /f <directives_file> [...]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<source>` | Die zu komprimierende Datei. |
| `<destination>` | Dateiname, der komprimierte Dateien zugewiesen werden soll. Wenn der Name ausgelassen wird, wird das letzte Zeichen des Quell Dateinamens durch einen Unterstrich (_) ersetzt und als Ziel verwendet. |
| /f `<directives_file>` | Eine Datei mit **makecab** -Direktiven (kann wiederholt werden). |
| /d var =`<value>` | Definiert die Variable mit dem angegebenen Wert. |
| /l `<dir>` | Speicherort für das Ziel (Standard ist Aktuelles Verzeichnis). |
| /v [ `<n>` ] | Ausführlichkeits Grad für das Debuggen festlegen (0 = keine,..., 3 = vollständig). |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [diantz-Befehl](diantz.md)

- [Microsoft-CAB-Format](/previous-versions/bb417343(v=msdn.10))
