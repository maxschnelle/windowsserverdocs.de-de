---
title: FTP-Anfüge Ende
description: Referenz Thema für den Befehl FTP anfügen, bei dem eine lokale Datei mithilfe der aktuellen Dateityp Einstellung an eine Datei auf dem Remote Computer angefügt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c1a133c-31dc-41a4-9eb9-258efd79804d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d1b6ab4a6ae0c1654d4335d24f135b2893bdcb7
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83819140"
---
# <a name="ftp-append"></a>FTP-Anfüge Ende

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt eine lokale Datei mithilfe der aktuellen Dateityp Einstellung an eine Datei auf dem Remote Computer an.

## <a name="syntax"></a>Syntax

```
append <localfile> [remotefile]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<localfile>` | Gibt die hinzu zufügende lokale Datei an. |
| [remotefile] | Gibt die Datei auf dem Remote Computer an, der <localfile> hinzugefügt wird. Wenn Sie diesen Parameter nicht verwenden, `<localfile>` wird der Name anstelle des Remote Dateinamens verwendet. |

### <a name="examples"></a>Beispiele

Um *File1. txt* an *File2. txt* auf dem Remote Computer anzufügen, geben Sie Folgendes ein:

```
append file1.txt file2.txt
```

Um die lokale Datei " *File1. txt* " an eine Datei mit dem Namen " *File1. txt* " auf dem Remote Computer anzufügen.

```
append file1.txt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
