---
title: ftp dir
description: Referenz Artikel für den Befehl FTP dir, mit dem eine Liste der Verzeichnis Dateien und Unterverzeichnisse auf einem Remote Computer angezeigt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a29a92a5-7b79-4e6e-95cf-2ccb38bb6fb2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1c3ec103797a1683c6f2810da375b00b56b87414
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957872"
---
# <a name="ftp-dir"></a>ftp dir

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine Liste der Verzeichnis Dateien und Unterverzeichnisse auf einem Remote Computer an.

## <a name="syntax"></a>Syntax

```
dir [<remotedirectory>] [<localfile>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
