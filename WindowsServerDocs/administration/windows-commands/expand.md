---
title: Erweitern
description: Referenz Artikel für den Expand-Befehl, mit dem eine oder mehrere komprimierte Dateien erweitert werden.
ms.topic: reference
ms.assetid: 66de0488-a0c4-40c2-9b03-e40c107ba343
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b64303d2a7cd38c86d8f5c99d319e46f837f2970
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635889"
---
# <a name="expand"></a>Erweitern

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erweitert eine oder mehrere komprimierte Dateien. Sie können diesen Befehl auch verwenden, um komprimierte Dateien von Verteilungs Datenträgern abzurufen.

Der **Erweiterungs Befehl kann** auch in der Windows-Wiederherstellungskonsole mit unterschiedlichen Parametern ausgeführt werden. Weitere Informationen finden Sie in der [Windows-Wiederherstellungs Umgebung (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference).

## <a name="syntax"></a>Syntax

```
expand [/r] <source> <destination>
expand /r <source> [<destination>]
expand /i <source> [<destination>]
expand /d <source>.cab [/f:<files>]
expand <source>.cab /f:<files> <destination>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /r | Benennt Erweiterte Dateien um. |
| source | Gibt die Dateien an, die erweitert werden sollen. Die *Quelle* kann aus einem Laufwerk Buchstaben und einem Doppelpunkt, einem Verzeichnisnamen, einem Dateinamen oder einer Kombination aus diesen bestehen. Sie können Platzhalter (**&#42;** oder **?**) verwenden. |
| destination | Gibt an, wo Dateien erweitert werden sollen.<p>Wenn die *Quelle* aus mehreren Dateien besteht und Sie **/r**nicht angeben, muss es sich bei dem *Ziel* um ein Verzeichnis handeln. Das *Ziel* kann aus einem Laufwerk Buchstaben und einem Doppelpunkt, einem Verzeichnisnamen, einem Dateinamen oder einer Kombination aus diesen bestehen. Ziel `file | path` Spezifikation. |
| /i | Benennt Erweiterte Dateien um, ignoriert jedoch die Verzeichnisstruktur. |
| /d | Zeigt eine Liste der Dateien am Quell Speicherort an. Die Dateien werden nicht erweitert oder extrahiert. |
| /f`<files>` | Gibt die Dateien in einer CAB-Datei an, die Sie erweitern möchten. Sie können Platzhalter (**&#42;** oder **?**) verwenden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
