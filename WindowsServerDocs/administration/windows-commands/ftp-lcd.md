---
title: ftp lcd
description: Referenz Artikel für den Befehl FTP LCD, der das Arbeitsverzeichnis auf dem lokalen Computer ändert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 60a25808-6abb-408b-8373-0bbdcd0994b4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d98b300de74ec537dedd3f43ccc2404c7350ac0c
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957782"
---
# <a name="ftp-lcd"></a>ftp lcd

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert das Arbeitsverzeichnis auf dem lokalen Computer. Standardmäßig ist das Arbeitsverzeichnis das Verzeichnis, in dem der **FTP** -Befehl gestartet wurde.

## <a name="syntax"></a>Syntax

```
lcd [<directory>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `[<directory>]` | Gibt das Verzeichnis auf dem lokalen Computer an, in dem die Änderung vorgenommen werden soll. Wenn das *Verzeichnis* nicht angegeben wird, wird das aktuelle Arbeitsverzeichnis in das Standardverzeichnis geändert. |

### <a name="examples"></a>Beispiele

Wenn Sie das Arbeitsverzeichnis auf dem lokalen Computer in " *c:\dir1*" ändern möchten, geben Sie Folgendes ein:

```
lcd c:\dir1
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
