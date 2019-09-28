---
title: path
description: Erfahren Sie, wie Sie die PATH-Umgebungsvariable festlegen.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1bfa1349-e79a-472b-a9e6-d7a91149ae8f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 81e8441e7c67e42bdf929e703c8fe780a6f8aff8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372423"
---
# <a name="path"></a>path



Legt den Befehlspfad in der PATH-Umgebungsvariablen fest (der Satz von Verzeichnissen, der zum Suchen nach ausführbaren Dateien verwendet wird). Bei Verwendung ohne Parameter zeigt **path** den aktuellen Befehlspfad an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
path [[<Drive>:]<Path>[;...][;%PATH%]]
path ;
```

## <a name="parameters"></a>Parameter

|     Parameter     |                                                                                                     Beschreibung                                                                                                      |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [\<laufwerk >:] <Path> |                                                                            Gibt das Laufwerk und das Verzeichnis an, die im Befehlspfad festgelegt werden sollen.                                                                             |
|         ;         | Trennt Verzeichnisse im Befehlspfad. Wenn es ohne andere Parameter verwendet wird, löscht die vorhandenen Befehls Pfade aus der PATH-Umgebungsvariablen und leitet "cmd. exe" so **um, dass** Sie nur im aktuellen Verzeichnis suchen. |
|      ADS       |                                                         Fügt den Befehlspfad an den vorhandenen Satz von Verzeichnissen an, der in der PATH-Umgebungsvariablen aufgelistet ist.                                                         |
|        /?         |                                                                                         Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                         |

## <a name="remarks"></a>Hinweise

-   Wenn Sie " **% path%** " in die Syntax einschließen, ersetzt "cmd. exe" diese durch die in der PATH-Umgebungsvariablen gefundenen Befehlspfad Werte, sodass diese Werte in der Eingabeaufforderung nicht manuell eingegeben werden müssen.
-   Das aktuelle Verzeichnis wird immer vor den im Befehlspfad angegebenen Verzeichnissen durchsucht.
-   Möglicherweise verfügen Sie über Dateien in einem Verzeichnis, das denselben Dateinamen hat, aber über unterschiedliche Erweiterungen verfügt. Angenommen, Sie verfügen über eine Datei mit dem Namen accnt.com, die ein Buchhaltungsprogramm und eine weitere Datei mit dem Namen accnt. bat startet, die Ihren Server mit dem Kontoführungs System-Netzwerk verbindet.

    Das Windows-Betriebssystem sucht nach einer Datei mithilfe von standardmäßigen Dateinamen Erweiterungen in der folgenden Rangfolge:. exe,. com,. bat und. cmd. Um "accnt. bat" auszuführen, wenn accnt.com im gleichen Verzeichnis vorhanden ist, müssen Sie die Erweiterung ". bat" an der Eingabeaufforderung einschließen.
-   Wenn zwei oder mehr Dateien im Befehlspfad den gleichen Dateinamen und die gleiche Erweiterung aufweisen, sucht der **Pfad** zuerst nach dem angegebenen Dateinamen im aktuellen Verzeichnis. Anschließend werden die Verzeichnisse im Befehlspfad in der Reihenfolge durchsucht, in der Sie in der PATH-Umgebungsvariablen aufgelistet sind.
-   Wenn Sie den **Pfad** Befehl in der Datei Autoexec. NT platzieren, fügt das Windows-Betriebssystem jedes Mal, wenn Sie sich an Ihrem Computer angemeldet haben, automatisch den angegebenen Pfad des MS-DOS-subsystemsuchpfades an. "Cmd. exe" verwendet nicht die Datei "Autoexec. NT". Beim Starten über eine Verknüpfung erbt cmd. exe die Umgebungsvariablen, die in Arbeitsplatz/Properties/Advanced/Environment festgelegt sind.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um die Pfade c:\user\steuern, b:\user\invest und b:\bin für externe Befehle zu durchsuchen:

`path c:\user\taxes;b:\user\invest;b:\bin`

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)