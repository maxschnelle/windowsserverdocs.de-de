---
title: ftp lcd
description: Referenz Artikel für den Befehl FTP LCD, der das Arbeitsverzeichnis auf dem lokalen Computer ändert.
ms.topic: reference
ms.assetid: 60a25808-6abb-408b-8373-0bbdcd0994b4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 344d0ba14c552315504fc16b109500141c341f97
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038921"
---
# <a name="ftp-lcd"></a>ftp lcd

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert das Arbeitsverzeichnis auf dem lokalen Computer. Standardmäßig ist das Arbeitsverzeichnis das Verzeichnis, in dem der **FTP** -Befehl gestartet wurde.

## <a name="syntax"></a>Syntax

```
lcd [<directory>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `[<directory>]` | Gibt das Verzeichnis auf dem lokalen Computer an, in dem die Änderung vorgenommen werden soll. Wenn das *Verzeichnis* nicht angegeben wird, wird das aktuelle Arbeitsverzeichnis in das Standardverzeichnis geändert. |

### <a name="examples"></a>Beispiele

Wenn Sie das Arbeitsverzeichnis auf dem lokalen Computer in " *c:\dir1*" ändern möchten, geben Sie Folgendes ein:

```
lcd c:\dir1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
