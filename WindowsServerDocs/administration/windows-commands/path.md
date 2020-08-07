---
title: path
description: Referenz Artikel zum Festlegen des Befehls Pfads in der PATH-Umgebungsvariablen, der den Satz von Verzeichnissen angibt, die für die Suche nach ausführbaren Dateien (. exe) verwendet werden.
ms.topic: article
ms.assetid: 1bfa1349-e79a-472b-a9e6-d7a91149ae8f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4c81dfef09b4c9a411db9469ec851d4f92180f1d
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885106"
---
# <a name="path"></a>path

Legt den Befehlspfad in der PATH-Umgebungsvariablen fest und gibt den Satz von Verzeichnissen an, die für die Suche nach ausführbaren Dateien (. exe) verwendet werden. Bei Verwendung ohne Parameter zeigt dieser Befehl den aktuellen Befehlspfad an.

## <a name="syntax"></a>Syntax

```
path [[<drive>:]<path>[;...][;%PATH%]]
path ;
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `[<drive>:]<path>` | Gibt das Laufwerk und das Verzeichnis an, die im Befehlspfad festgelegt werden sollen. Das aktuelle Verzeichnis wird immer vor den im Befehlspfad angegebenen Verzeichnissen durchsucht. |
| ; | Trennt Verzeichnisse im Befehlspfad. Wenn es ohne andere Parameter verwendet wird, löscht die vorhandenen Befehls Pfade aus der PATH-Umgebungsvariablen und leitet **Cmd.exe, nur** im aktuellen Verzeichnis zu suchen. |
| `%PATH%` | Fügt den Befehlspfad an den vorhandenen Satz von Verzeichnissen an, der in der PATH-Umgebungsvariablen aufgelistet ist. Wenn Sie diesen Parameter einschließen, ersetzt Cmd.exe ihn durch die in der PATH-Umgebungsvariablen gefundenen Befehlspfad Werte, sodass diese Werte in der Eingabeaufforderung nicht manuell eingegeben werden müssen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Bemerkungen


- Das Windows-Betriebssystem sucht mithilfe von standardmäßigen Dateinamen Erweiterungen in der folgenden Rangfolge:. exe,. com,. bat und. cmd. Dies bedeutet, dass Sie die Erweiterung ". bat" an der Eingabeaufforderung einschließen müssen, wenn Sie nach einer Batchdatei mit dem Namen acct.bat suchen, aber eine APP mit dem Namen acct.exe im gleichen Verzeichnis haben.

- Wenn zwei oder mehr Dateien im Befehlspfad den gleichen Dateinamen und die gleiche Erweiterung aufweisen, sucht dieser Befehl zuerst im aktuellen Verzeichnis nach dem angegebenen Dateinamen. Anschließend werden die Verzeichnisse im Befehlspfad in der Reihenfolge durchsucht, in der Sie in der PATH-Umgebungsvariablen aufgelistet sind.

- Wenn Sie den **Pfad** Befehl in der Datei Autoexec. NT platzieren, fügt das Windows-Betriebssystem jedes Mal, wenn Sie sich an Ihrem Computer angemeldet haben, automatisch den angegebenen Pfad des MS-DOS-subsystemsuchpfades an. In Cmd.exe wird die Datei Autoexec. NT nicht verwendet. Beim Starten über eine Verknüpfung erbt Cmd.exe die Umgebungsvariablen, die in Arbeitsplatz/Properties/Advanced/Environment festgelegt sind.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Pfade *c:\user\steuern*, *b:\user\invest*und *b:\bin* für externe Befehle zu durchsuchen:

```
path c:\user\taxes;b:\user\invest;b:\bin
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
