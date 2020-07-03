---
title: ftp ascii
description: Referenz Artikel für den FTP-ASCII-Befehl, mit dem der Datei Übertragungstyp auf ASCII festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 523be48e-eab0-4237-8fb5-ca222824f0b6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e3ba10ba6498b48a19aacf6235c84a890c7db63a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933324"
---
# <a name="ftp-ascii"></a>ftp ascii

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt den Datei Übertragungstyp auf ASCII fest. Der **FTP** -Befehl unterstützt sowohl ASCII-(Standard) als auch binäre Bilddatei-Übertragungs Typen, aber wir empfehlen die Verwendung von ASCII beim Übertragen von Textdateien. Im ASCII-Modus werden Zeichen Konvertierungen in und aus dem Netzwerkstandard-Zeichensatz ausgeführt. Beispielsweise werden zeitzeiendezeichen nach Bedarf auf Grundlage des Ziel Betriebssystems konvertiert.

## <a name="syntax"></a>Syntax

```
ascii
```

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Datei Übertragungstyp auf ASCII festzulegen:

```
ascii
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [FTP-Binär Befehl](ftp-binary.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
