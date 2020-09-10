---
title: ftp lcd
description: Referenz Artikel für den Befehl FTP LCD, der das Arbeitsverzeichnis auf dem lokalen Computer ändert.
ms.topic: reference
ms.assetid: 60a25808-6abb-408b-8373-0bbdcd0994b4
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 91b2990495c91033c1bc885ec9d19142640f55b5
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89621673"
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
