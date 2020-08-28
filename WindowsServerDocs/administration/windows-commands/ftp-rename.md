---
title: ftp rename
description: Referenz Artikel für den Befehl FTP rename, der Remote Dateien umbenennt.
ms.topic: reference
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a722605e451fff3ea8d4a758434a7509deaf355c
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89035738"
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

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
