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
ms.openlocfilehash: fb613810e764f3dd486ea79869607d68e7f009df
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957442"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
