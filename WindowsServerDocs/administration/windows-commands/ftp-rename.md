---
title: ftp rename
description: Referenz Artikel für den Befehl FTP rename, der Remote Dateien umbenennt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f46caa4394be9edc80da018d88809a0dd6e91862
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925739"
---
# <a name="ftp-rename"></a>ftp rename

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Benennt Remote Dateien um.

## <a name="syntax"></a>Syntax

```
rename <filename> <newfilename>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
