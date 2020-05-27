---
title: FTP-Typ
description: Referenz Thema für den Befehl FTP Type, mit dem der Datei Übertragungstyp festgelegt oder angezeigt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6e96dcd4-08f8-4e7b-90b7-1e1761fea4c7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 02b6d5b4bd7944c9f4126ba4877360de02586cfb
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820270"
---
# <a name="ftp-type"></a>FTP-Typ

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt den Datei Übertragungstyp fest oder zeigt ihn an. Der **FTP** -Befehl unterstützt sowohl ASCII-(Standard) als auch binäre Bilddatei-Übertragungs Typen:

- Beim Übertragen von Textdateien empfiehlt es sich, ASCII zu verwenden. Im ASCII-Modus werden Zeichen Konvertierungen in und aus dem Netzwerkstandard-Zeichensatz ausgeführt. Beispielsweise werden zeitzeiendezeichen nach Bedarf auf Grundlage des Ziel Betriebssystems konvertiert.

- Beim Übertragen von ausführbaren Dateien wird die Verwendung von Binary empfohlen. Im Binärmodus werden Dateien in 1-Byte-Einheiten übertragen.

## <a name="syntax"></a>Syntax

```
type [<typename>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `[<typename>]` | Gibt den Dateiübertragungstyp an. Wenn Sie diesen Parameter nicht angeben, wird der aktuelle Typ angezeigt.|

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Datei Übertragungstyp auf ASCII festzulegen:

```
type ascii
```

Geben Sie Folgendes ein, um den Dateityp für die Übertragung auf Binär

```
type binary
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Zusätzlicher FTP-Leitfaden](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
