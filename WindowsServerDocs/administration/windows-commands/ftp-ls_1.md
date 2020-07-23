---
title: ftp ls
description: Referenz Artikel für den Befehl FTP ls, bei dem eine abgekürzte Liste von Dateien und Unterverzeichnissen vom Remote Computer angezeigt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5e03c7db-1e2b-419c-acb2-8a68f3db9615
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6895886b8a18575f5e7c1f93c65f37a58ad3ad45
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957742"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
