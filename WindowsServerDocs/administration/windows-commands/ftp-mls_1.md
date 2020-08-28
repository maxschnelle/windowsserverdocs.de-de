---
title: ftp mls
description: Referenz Artikel für den Befehl FTP MLS, der eine abgekürzte Liste von Dateien und Unterverzeichnissen in einem Remote Verzeichnis anzeigt.
ms.topic: reference
ms.assetid: 4738fd49-0e80-4bdf-a773-0f973db3a710
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b4eaf9a4b31fb233d281514bcc50ddc754d398a
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038028"
---
# <a name="ftp-mls"></a>ftp mls

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine abgekürzte Liste von Dateien und Unterverzeichnissen in einem Remote Verzeichnis an.

## <a name="syntax"></a>Syntax

```
mls <remotefile>[ ] <localfile>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<remotefile>` | Gibt die Datei an, für die eine Auflistung angezeigt werden soll. Verwenden Sie bei der Angabe von *remotefiles*einen Bindestrich, um das aktuelle Arbeitsverzeichnis auf dem Remote Computer darzustellen. |
| `<localfile>` | Gibt eine lokale Datei an, in der die Auflistung gespeichert werden soll. Verwenden Sie beim Angeben von *LocalFile*einen Bindestrich, um die Auflistung auf dem Bildschirm anzuzeigen. |

### <a name="examples"></a>Beispiele

Wenn Sie eine abgekürzte Liste von Dateien und Unterverzeichnissen für *dir1* und *dir2*anzeigen möchten, geben Sie Folgendes ein:

```
mls dir1 dir2 -
```

Zum Speichern einer abgekürzten Liste von Dateien und Unterverzeichnissen für *dir1* und *dir2* in der lokalen Datei *dirlist.txt*geben Sie Folgendes ein:

```
mls dir1 dir2 dirlist.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
