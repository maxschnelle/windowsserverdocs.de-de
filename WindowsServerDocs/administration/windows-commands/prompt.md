---
title: prompt
description: Referenz Artikel für den Prompt-Befehl, mit dem die Cmd.exe Eingabeaufforderung angepasst wird.
ms.topic: reference
ms.assetid: 3d98e965-02eb-46ad-9d0a-5dc44830373e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: 8cf91a2a2e78191f035545bc897eceae4c897457
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640327"
---
# <a name="prompt"></a>prompt

Ändert die Cmd.exe Eingabeaufforderung, einschließlich der Anzeige eines beliebigen Texts, z. b. des Namens des aktuellen Verzeichnisses, der Uhrzeit und des Datums oder der Microsoft Windows-Versionsnummer. Bei Verwendung ohne Parameter setzt dieser Befehl die Eingabeaufforderung auf die Standardeinstellung zurück. Hierbei handelt es sich um den aktuellen Laufwerk Buchstaben und das Verzeichnis, gefolgt vom größer-als-Symbol ( **>** ).

## <a name="syntax"></a>Syntax

```
prompt [<text>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<text>` | Gibt den Text und die Informationen an, die Sie in die Eingabeaufforderung einschließen möchten. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Die Zeichenkombinationen, die Sie anstelle von oder zusätzlich zu einer oder mehreren Zeichen folgen im *Text* Parameter einschließen können:

    | Zeichen | BESCHREIBUNG |
    |--|--|
    | $q | = (Gleichheitszeichen) |
    | $$ | $ (Dollar Zeichen) |
    | $t | Die aktuelle Zeit |
    | $d | Aktuelles Datum |
    | $p | Aktuelles Laufwerk und Pfad |
    | $v | Windows-Versionsnummer |
    | $n | Aktuelles Laufwerk |
    | $g | > (größer als-Zeichen) |
    | $l | < (kleiner als Vorzeichen) |
    | $b | `|` (Pipe-Symbol) |
    | $_ | Eingabe-Zeilenvorschub |
    | $e | ANSI-Escapecode (Code 27) |
    | $h | Rücktaste (zum Löschen eines Zeichens, das in die Befehlszeile geschrieben wurde) |
    | $a | & (kaufmännisches und-Paar) |
    | $c | ((Linke Klammer) |
    | $f | ) (Schließende Klammer) |
    | $s | LeerZchn |

- Wenn Befehls Erweiterungen aktiviert sind, unterstützt der **prompt** -Befehl die folgenden Formatierungszeichen:

    | Zeichen | BESCHREIBUNG |
    |--|--|
    | $+ | 0 (null) oder mehr Pluszeichen ( **+** ), abhängig von der Tiefe des **pushd-** Verzeichnis Stapels (ein Zeichen für jede Ebene wird per Push abgelegt). |
    | $m | Der Remote Name, der dem aktuellen Laufwerk Buchstaben oder der leeren Zeichenfolge zugeordnet ist, wenn das aktuelle Laufwerk kein Netzwerklaufwerk ist. |

- Wenn Sie das **$p** Zeichen in den Text Parameter einschließen, wird der Datenträger gelesen, nachdem Sie jeden Befehl eingegeben haben (um das aktuelle Laufwerk und den Pfad zu bestimmen). Dies kann zusätzliche Zeit in Anspruch nehmen, insbesondere bei Diskettenlaufwerken.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine zweizeilige Eingabeaufforderung mit der aktuellen Uhrzeit und dem aktuellen Datum in der ersten Zeile und dem größer-als-Zeichen in der nächsten Zeile festzulegen:

```
prompt $d$s$s$t$_$g
```

Die Eingabeaufforderung wird wie folgt geändert, wobei Datum und Uhrzeit aktuell sind:

```
Fri 06/01/2007  13:53:28.91
```

Geben Sie Folgendes ein, um die Eingabeaufforderung als Pfeil ( `-->` ) anzuzeigen:

```
prompt --$g
```

Geben Sie Folgendes ein, um die Eingabeaufforderung manuell in die Standardeinstellung (das aktuelle Laufwerk und den Pfad gefolgt von dem größer-als-Zeichen) zu ändern:

```
prompt $p$g
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
