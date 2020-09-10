---
title: ftp rename
description: Referenz Artikel für den Befehl FTP rename, der Remote Dateien umbenennt.
ms.topic: reference
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ea7862a759779a5f767b8e18cdd5a0b36db2a6a1
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627633"
---
# <a name="ftp-rename"></a>ftp rename

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Benennt Remote Dateien um.

## <a name="syntax"></a>Syntax

```
rename <filename> <newfilename>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<filename>` | Gibt die Datei an, die Sie umbenennen möchten. |
| `<newfilename>` | Gibt den neuen Dateinamen an. |

### <a name="examples"></a>Beispiele

Um die Remote Datei *example.txt* in *example1.txt*umzubenennen, geben Sie Folgendes ein:

```
rename example.txt example1.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
