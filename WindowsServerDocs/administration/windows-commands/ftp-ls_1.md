---
title: ftp ls
description: Referenz Artikel für den Befehl FTP ls, bei dem eine abgekürzte Liste von Dateien und Unterverzeichnissen vom Remote Computer angezeigt wird.
ms.topic: reference
ms.assetid: 5e03c7db-1e2b-419c-acb2-8a68f3db9615
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 845d8fed8dbb637a241d4b1c4491ef9f037eceb8
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89621613"
---
# <a name="ftp-ls"></a>ftp ls

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine abgekürzte Liste von Dateien und Unterverzeichnissen vom Remote Computer an.

## <a name="syntax"></a>Syntax

```
ls [<remotedirectory>] [<localfile>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- |------------ |
| `[<remotedirectory>]` | Gibt das Verzeichnis an, für das eine Auflistung angezeigt werden soll. Wenn kein Verzeichnis angegeben ist, wird das aktuelle Arbeitsverzeichnis auf dem Remote Computer verwendet. |
| `[<localfile>]` | Gibt eine lokale Datei an, in der die Auflistung gespeichert werden soll. Wenn keine lokale Datei angegeben wird, werden die Ergebnisse auf dem Bildschirm angezeigt. |

### <a name="examples"></a>Beispiele

Wenn Sie eine abgekürzte Liste von Dateien und Unterverzeichnissen vom Remote Computer anzeigen möchten, geben Sie Folgendes ein:

```
ls
```

Um eine abgekürzte Verzeichnis Auflistung von *dir1* auf dem Remote Computer zu erhalten und in einer lokalen Datei namens *dirlist.txt*zu speichern, geben Sie Folgendes ein:

```
ls dir1 dirlist.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
