---
title: ftp dir
description: Referenz Artikel für den Befehl FTP dir, mit dem eine Liste der Verzeichnis Dateien und Unterverzeichnisse auf einem Remote Computer angezeigt wird.
ms.topic: article
ms.assetid: a29a92a5-7b79-4e6e-95cf-2ccb38bb6fb2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0a4f65cee67ec91b6871649fece4f580684c2e3f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889475"
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
