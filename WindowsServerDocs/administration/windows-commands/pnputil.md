---
title: pnputil
description: Erfahren Sie, wie Sie den Treiber Speicher mit dem Hilfsprogramm "PnPUtil. exe" verwalten.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fab686b8-09d3-4f6c-afa2-630e6036f44c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 134e6ce4b1fc44450047de3287b7daac67da4b6a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837513"
---
# <a name="pnputil"></a>pnputil

"PnPUtil. exe" ist ein Befehlszeilen-Hilfsprogramm, das Sie zum Verwalten des Treiber Speichers verwenden können. Sie können PnPUtil zum Hinzufügen von Treiber Paketen, zum Entfernen von Treiber Paketen und zum Auflisten von Treiber Paketen im Speicher verwenden.

## <a name="syntax"></a>Syntax

```
pnputil.exe [-f | -i] [ -? | -a | -d | -e ] <INF name>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-a|Gibt an, dass die identifizierte INF-Datei hinzugefügt wird.|
|-d|Gibt an, dass die identifizierte INF-Datei gelöscht werden soll.|
|-e|Gibt an, dass alle INF-Dateien von Drittanbietern aufgelistet werden.|
|-f|Gibt an, dass das Löschen der identifizierten INF-Datei erzwungen werden soll. Kann nicht in Verbindung mit dem **– i** -Parameter verwendet werden.|
|-i|Gibt an, dass die identifizierte INF-Datei installiert werden soll. Kann nicht in Verbindung mit dem **-f-** Parameter verwendet werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|


## <a name="examples"></a>Beispiele

-   pnputil. exe-a a:\. INF fügt die von "Start" angegebene INF-Datei hinzu. INF
-   pnputil. exe: ein c:\drivers\*. inf fügt alle INF-Dateien in "c:\drivers\" hinzu.
-   pnputil. exe-i-a a:\herbcam\ebcam. INF fügt den angegebenen Treiber hinzu und installiert ihn.
-   pnputil. exe – e listet alle Treiber von Drittanbietern auf.
-   pnputil. exe-d oem0. inf löscht die angegebene.
-   pnputil. exe-f-d oem0. inf erzwingt das Löschen der angegebenen INF-Datei.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Popd](popd.md)