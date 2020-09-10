---
title: ftp dir
description: Referenz Artikel für den Befehl FTP dir, mit dem eine Liste der Verzeichnis Dateien und Unterverzeichnisse auf einem Remote Computer angezeigt wird.
ms.topic: reference
ms.assetid: a29a92a5-7b79-4e6e-95cf-2ccb38bb6fb2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8641fdca55976eb5998cdfbba58eddd3e6d8f286
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89621780"
---
# <a name="ftp-dir"></a>ftp dir

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine Liste der Verzeichnis Dateien und Unterverzeichnisse auf einem Remote Computer an.

## <a name="syntax"></a>Syntax

```
dir [<remotedirectory>] [<localfile>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| ------- | -------- |
| `[<remotedirectory>]` | Gibt das Verzeichnis an, für das eine Auflistung angezeigt werden soll. Wenn kein Verzeichnis angegeben ist, wird das aktuelle Arbeitsverzeichnis auf dem Remote Computer verwendet. |
| `[<localfile>]` | Gibt eine lokale Datei an, in der die Verzeichnis Auflistung gespeichert werden soll. Wenn keine lokale Datei angegeben wird, werden die Ergebnisse auf dem Bildschirm angezeigt. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Verzeichnis Auflistung für *dir1* auf dem Remote Computer anzuzeigen:

```
dir dir1
```

Geben Sie Folgendes ein, um eine Liste mit dem aktuellen Verzeichnis auf dem Remote Computer *dirlist.txt*in der lokalen Datei zu speichern:

```
dir . dirlist.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
