---
title: graftabl
description: Referenz Artikel für den graftabl-Befehl, mit dem Windows-Betriebssysteme einen erweiterten Zeichensatz im Grafikmodus anzeigen können.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b08351d4-3d24-490c-86f6-1252da11d923
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9259833856ec5c6de402b0db0a4de4636a66f508
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924593"
---
# <a name="graftabl"></a>graftabl

Ermöglicht Windows-Betriebssystemen das Anzeigen eines erweiterten Zeichensatzes im Grafikmodus. Bei Verwendung ohne Parameter zeigt **graftabl** die vorherige und die aktuelle Codepage an.

## <a name="syntax"></a>Syntax

```
graftabl <codepage>
graftabl /status
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<codepage>` | Gibt eine Codepage an, um die Darstellung erweiterter Zeichen im Grafikmodus zu definieren. Gültige Codepage-Identifikationsnummern sind:<ul><li>**437** -USA</li><li>**850** -mehrsprachig (lateinisch I)</li><li>**852** -slawisch (Lateinisch II)</li><li>**855** -Kyrillisch (Russisch)</li><li>**857** -Türkisch</li><li>**860** -Portugiesisch</li><li>**861** -Isländisch</li><li>**863** -Französisch (Kanada)</li><li>**865** -Nordisch</li><li>**866** -Russisch</li><li>**869** -modern Griechisch</li></ul> |
| /status | Zeigt die aktuelle Codepage an, die von diesem Befehl verwendet wird. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Der **graftabl** -Befehl wirkt sich nur auf die Anzeige von erweiterten Zeichen der von Ihnen angegebenen Codepage aus. Die tatsächliche Konsolen Eingabe Codepage wird nicht geändert. Zum Ändern der Konsolen Eingabe Codepage verwenden Sie den Befehl [Mode](mode.md) oder [chcp](chcp.md) .

- Jeder Exitcode und eine kurze Beschreibung:

    | Exitcode | BESCHREIBUNG |
    | --------- | ----------- |
    | 0 | Der Zeichensatz wurde erfolgreich geladen. Es wurde keine vorherige Codepage geladen. |
    | 1 | Es wurde ein falscher Parameter angegeben. Es wurde keine Aktion ausgeführt. |
    | 2 | Ein Datei Fehler ist aufgetreten. |

- Mit der ERRORLEVEL-Umgebungsvariablen in einem Batch-Programm können Sie Exitcodes verarbeiten, die von **graftabl**zurückgegeben werden.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die von **graftabl**verwendete aktuelle Codepage anzuzeigen:

```
graftabl /status
```

Geben Sie Folgendes ein, um den Grafikzeichen Satz für die Codepage 437 (USA) in den Arbeitsspeicher zu laden:

```
graftabl 437
```

Geben Sie Folgendes ein, um den Grafikzeichen Satz für Codepage 850 (mehrsprachig) in den Arbeitsspeicher zu laden:

```
graftabl 850
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "freiplatte"](freedisk.md)

- [Mode-Befehl](mode.md)

- [CHCP-Befehl](chcp.md)
