---
title: FTP-umbenennen
description: Referenz Thema für den Befehl FTP rename, mit dem Remote Dateien umbenannt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a8d3ea25e48266db6a4a282f2ea395bd8b8d5fd9
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820310"
---
# <a name="ftp-rename"></a>FTP-umbenennen

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

Wenn Sie die Remote Datei *example. txt* in *"example1". txt*umbenennen möchten, geben Sie Folgendes ein:

```
rename example.txt example1.txt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
