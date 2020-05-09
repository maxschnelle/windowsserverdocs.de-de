---
title: makecab
description: Referenz Thema für den makecab-Befehl, mit dem vorhandene Dateien in eine CAB-Datei (CAB-Datei) verpackt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4da95297-c593-427b-9f76-2f389c46cbf4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f3d5e778ee78d812a3ec8c3683b01e0b304a127e
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2020
ms.locfileid: "82992338"
---
# <a name="makecab"></a>makecab

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verpacken vorhandener Dateien in eine CAB-Datei. Dieser Befehl führt dieselben Aktionen aus wie der **diantz** -Befehl.

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
| /l`<dir>` | Speicherort für das Ziel (Standard ist Aktuelles Verzeichnis). |
| /v [`<n>`] | Ausführlichkeits Grad für das Debuggen festlegen (0 = keine,..., 3 = vollständig). |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Microsoft-CAB-Format](https://docs.microsoft.com/previous-versions/bb417343(v=msdn.10))
