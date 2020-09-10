---
title: ftp append
description: Referenz Artikel für den Befehl FTP anfügen, bei dem eine lokale Datei mithilfe der aktuellen Dateityp Einstellung an eine Datei auf dem Remote Computer angefügt wird.
ms.topic: reference
ms.assetid: 7c1a133c-31dc-41a4-9eb9-258efd79804d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 42270b8f3633158e12d472a234fcf1904cee86de
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89638574"
---
# <a name="ftp-append"></a>ftp append

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

Um *file1.txt* an *file2.txt* auf dem Remote Computer anzufügen, geben Sie Folgendes ein:

```
append file1.txt file2.txt
```

Fügen Sie den lokalen *file1.txt* an eine Datei mit dem Namen *file1.txt* auf dem Remote Computer an.

```
append file1.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
