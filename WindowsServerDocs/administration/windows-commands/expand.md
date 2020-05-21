---
title: Erweitern
description: Referenz Thema für den Expand-Befehl, mit dem eine oder mehrere komprimierte Dateien erweitert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 66de0488-a0c4-40c2-9b03-e40c107ba343
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a25507b83c17100c579f00d10c94e20c6be2aa4e
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437215"
---
# <a name="expand"></a>Erweitern

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erweitert eine oder mehrere komprimierte Dateien. Sie können diesen Befehl auch verwenden, um komprimierte Dateien von Verteilungs Datenträgern abzurufen.

Der **Erweiterungs Befehl kann** auch in der Windows-Wiederherstellungskonsole mit unterschiedlichen Parametern ausgeführt werden. Weitere Informationen finden Sie in der [Windows-Wiederherstellungs Umgebung (WinRE)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference).

## <a name="syntax"></a>Syntax

```
expand [/r] <source> <destination>
expand /r <source> [<destination>]
expand /i <source> [<destination>]
expand /d <source>.cab [/f:<files>]
expand <source>.cab /f:<files> <destination>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /r | Benennt Erweiterte Dateien um. |
| Quelle | Gibt die Dateien an, die erweitert werden sollen. Die *Quelle* kann aus einem Laufwerk Buchstaben und einem Doppelpunkt, einem Verzeichnisnamen, einem Dateinamen oder einer Kombination aus diesen bestehen. Sie können Platzhalter (**&#42;** oder **?**) verwenden. |
| destination | Gibt an, wo Dateien erweitert werden sollen.<p>Wenn die *Quelle* aus mehreren Dateien besteht und Sie **/r**nicht angeben, muss es sich bei dem *Ziel* um ein Verzeichnis handeln. Das *Ziel* kann aus einem Laufwerk Buchstaben und einem Doppelpunkt, einem Verzeichnisnamen, einem Dateinamen oder einer Kombination aus diesen bestehen. Ziel `file | path` Spezifikation. |
| /i | Benennt Erweiterte Dateien um, ignoriert jedoch die Verzeichnisstruktur. |
| /d | Zeigt eine Liste der Dateien am Quell Speicherort an. Die Dateien werden nicht erweitert oder extrahiert. |
| /f`<files>` | Gibt die Dateien in einer CAB-Datei an, die Sie erweitern möchten. Sie können Platzhalter (**&#42;** oder **?**) verwenden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

