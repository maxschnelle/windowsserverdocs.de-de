---
title: ftp mdir
description: Referenz Artikel für den FTP-mdir-Befehl, der eine Verzeichnisliste von Dateien und Unterverzeichnissen in einem Remote Verzeichnis anzeigt.
ms.topic: reference
ms.assetid: 90eec45b-558b-4b8d-bbe4-b56d98e1ca70
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 40c64d82f07a763dec3dd690780438eb2db35753
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89636666"
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
