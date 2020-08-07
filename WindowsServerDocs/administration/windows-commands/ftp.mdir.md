---
title: ftp mdir
description: Referenz Artikel für den FTP-mdir-Befehl, der eine Verzeichnisliste von Dateien und Unterverzeichnissen in einem Remote Verzeichnis anzeigt.
ms.topic: article
ms.assetid: 90eec45b-558b-4b8d-bbe4-b56d98e1ca70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ddd4a5adb282464d2b5a202ea8ed2838be7a4676
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888725"
---
# <a name="ftp-mdir"></a>ftp mdir

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine Verzeichnisliste von Dateien und Unterverzeichnissen in einem Remote Verzeichnis an.

## <a name="syntax"></a>Syntax

```
mdir <remotefile>[...] <localfile>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<remotefile>` | Gibt das Verzeichnis oder die Datei an, für das eine Auflistung angezeigt werden soll. Sie können mehrere *remotefiles*angeben. Geben Sie einen Bindestrich (-) ein, um das aktuelle Arbeitsverzeichnis auf dem Remote Computer zu verwenden. |
| `<localfile>` | Gibt eine lokale Datei zum Speichern der Auflistung an. Dieser Parameter ist erforderlich. Geben Sie einen Bindestrich (-) ein, um die Auflistung auf dem Bildschirm anzuzeigen. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Verzeichnis Auflistung von *dir1* und *dir2* auf dem Bildschirm anzuzeigen:

```
mdir dir1 dir2 -
```

Um die kombinierte Verzeichnis Auflistung von *dir1* und *dir2* in einer lokalen Datei namens *dirlist.txt*zu speichern, geben Sie Folgendes ein:

```
mdir dir1 dir2 dirlist.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
