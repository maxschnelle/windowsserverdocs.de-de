---
title: FTP-MLS
description: Referenz Thema für den FTP-MLS-Befehl, der eine abgekürzte Liste von Dateien und Unterverzeichnissen in einem Remote Verzeichnis anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4738fd49-0e80-4bdf-a773-0f973db3a710
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 372c0b9a42fdfb8600083a301b71c37ada43c014
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820393"
---
# <a name="ftp-mls"></a>FTP-MLS

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine abgekürzte Liste von Dateien und Unterverzeichnissen in einem Remote Verzeichnis an.

## <a name="syntax"></a>Syntax

```
mls <remotefile>[ ] <localfile>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<remotefile>` | Gibt die Datei an, für die eine Auflistung angezeigt werden soll. Verwenden Sie bei der Angabe von *remotefiles*einen Bindestrich, um das aktuelle Arbeitsverzeichnis auf dem Remote Computer darzustellen. |
| `<localfile>` | Gibt eine lokale Datei an, in der die Auflistung gespeichert werden soll. Verwenden Sie beim Angeben von *LocalFile*einen Bindestrich, um die Auflistung auf dem Bildschirm anzuzeigen. |

### <a name="examples"></a>Beispiele

Wenn Sie eine abgekürzte Liste von Dateien und Unterverzeichnissen für *dir1* und *dir2*anzeigen möchten, geben Sie Folgendes ein:

```
mls dir1 dir2 -
```

Geben Sie Folgendes ein, um eine abgekürzte Liste von Dateien und Unterverzeichnissen für *dir1* und *dir2* in der lokalen Datei " *dirlist. txt*" zu speichern:

```
mls dir1 dir2 dirlist.txt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
