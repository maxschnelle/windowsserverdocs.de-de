---
title: diantz
description: Referenz Artikel für den diantz-Befehl, mit dem vorhandene Dateien in eine CAB-Datei (CAB-Datei) verpackt werden.
ms.topic: reference
ms.assetid: 218ed5d7-1203-4d68-ad9b-65cdd022d54f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 033bfb59bbd33fee44bb307d1a905dc6c8d658c7
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635017"
---
# <a name="diantz"></a>diantz

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verpacken vorhandener Dateien in eine CAB-Datei. Dieser Befehl führt dieselben Aktionen aus wie der aktualisierte [makecab-Befehl](makecab.md).

## <a name="syntax"></a>Syntax

```
diantz [/v[n]] [/d var=<value> ...] [/l <dir>] <source> [<destination>]
diantz [/v[<n>]] [/d var=<value> ...] /f <directives_file> [...]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<source>` | Die zu komprimierende Datei. |
| `<destination>` | Dateiname, der komprimierte Dateien zugewiesen werden soll. Wenn der Name ausgelassen wird, wird das letzte Zeichen des Quell Dateinamens durch einen Unterstrich (_) ersetzt und als Ziel verwendet. |
| /f `<directives_file>` | Eine Datei mit **diantz** -Direktiven (kann wiederholt werden). |
| /d var =`<value>` | Definiert die Variable mit dem angegebenen Wert. |
| /l `<dir>` | Speicherort für das Ziel (Standard ist Aktuelles Verzeichnis). |
| /v [ `<n>` ] | Ausführlichkeits Grad für das Debuggen festlegen (0 = keine,..., 3 = vollständig). |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Microsoft-CAB-Format](/previous-versions/bb417343(v=msdn.10))
