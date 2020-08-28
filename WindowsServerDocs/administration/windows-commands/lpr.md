---
title: lpr
description: Referenz Artikel für den LPR-Befehl, der eine Datei an einen Computer oder ein Druckerfreigabe Gerät sendet, auf dem der LPD-Dienst (Line Printer Daemon) ausgeführt wird, um den Druck vorzubereiten.
ms.topic: reference
ms.assetid: afc8790b-8b52-45c4-acdf-be0ffa9da534
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5ab663ab089c6727e7354accda5dc43b2d94c946
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89036338"
---
# <a name="lpr"></a>lpr

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet eine Datei an einen Computer oder ein Druckerfreigabe Gerät, auf dem der LPD-Dienst (Line Printer Daemon) ausgeführt wird, um den Druck vorzubereiten.

## <a name="syntax"></a>Syntax

```
lpr [-S <servername>] -P <printername> [-C <bannercontent>] [-J <jobname>] [-o | -o l] [-x] [-d] <filename>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| -S `<servername>` | Gibt (anhand des Namens oder der IP-Adresse) das Computer-oder Druckerfreigabe Gerät an, das die LPD-Drucker Warteschlange mit einem Status hostet, den Sie anzeigen möchten.  Dieser Parameter ist erforderlich und muss groß geschrieben werden. |
| -P `<printername> `| Gibt (nach Name) den Drucker für die Druck Warteschlange mit einem Status an, den Sie anzeigen möchten. Um den Namen des Druckers zu ermitteln, öffnen Sie den Ordner **Drucker** . Dieser Parameter ist erforderlich und muss groß geschrieben werden. |
| -C `<bannercontent>` | Gibt den Inhalt an, der auf der Seite Banner des Druckauftrags gedruckt werden soll. Wenn Sie diesen Parameter nicht angeben, wird der Name des Computers, von dem der Druckauftrag gesendet wurde, auf der Seite Banner angezeigt. Dieser Parameter muss groß geschrieben werden. |
| -J `<jobname>` | Gibt den Druckauftrags Namen an, der auf der Bannerseite gedruckt wird. Wenn Sie diesen Parameter nicht einschließen, wird der Name der zu druckenden Datei auf der Seite Banner angezeigt. Dieser Parameter muss groß geschrieben werden. |
| `[-o | -o l]` | Gibt den Dateityp an, den Sie drucken möchten. Der Parameter **-o** gibt an, dass Sie eine Textdatei drucken möchten. Der Parameter **-o l** gibt an, dass Sie eine Binärdatei (z. b. eine PostScript-Datei) drucken möchten. |
| -d | Gibt an, dass die Datendatei vor der Steuerungs Datei gesendet werden muss. Verwenden Sie diesen Parameter, wenn für den Drucker die Datendatei zuerst gesendet werden muss. Weitere Informationen finden Sie in der Druckerdokumentation. |
| -X | Gibt an, dass der **LPR** -Befehl mit dem Sun Microsystems-Betriebssystem (als SunOS bezeichnet) für Releases bis einschließlich 4.1.4_u1 kompatibel sein muss. |
| `<filename>` | Gibt (nach Name) die Datei an, die gedruckt werden soll. Dieser Parameter ist erforderlich. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die *Document.txt* Textdatei in der *Laserprinter1* -Drucker Warteschlange auf einem LPD-Host unter *10.0.0.45*auszugeben:

```
lpr -S 10.0.0.45 -P Laserprinter1 -o Document.txt
```

Geben Sie Folgendes ein, um die Adobe PostScript-Datei *PostScript_file. PS* in der *Laserprinter1* -Drucker Warteschlange auf einem LPD-Host unter *10.0.0.45*auszugeben:

```
lpr -S 10.0.0.45 -P Laserprinter1 -o l PostScript_file.ps
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Druckbefehlsreferenz](print-command-reference.md)
