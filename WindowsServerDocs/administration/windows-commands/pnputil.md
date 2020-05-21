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
ms.openlocfilehash: 4c6bcb138e8bd7308c01c2c53fba83b69362298a
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436365"
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
|-E|Gibt an, dass alle INF-Dateien von Drittanbietern aufgelistet werden.|
|-f|Gibt an, dass das Löschen der identifizierten INF-Datei erzwungen werden soll. Kann nicht in Verbindung mit dem **– i** -Parameter verwendet werden.|
|-i|Gibt an, dass die identifizierte INF-Datei installiert werden soll. Kann nicht in Verbindung mit dem **-f-** Parameter verwendet werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|


## <a name="examples"></a>Beispiele

-   pnputil. exe-a a:\. INF fügt die von "Start" angegebene INF-Datei hinzu. INF
-   pnputil. exe: ein c:\drivers \* . inf fügt alle INF-Dateien in "c:\drivers\" hinzu.
-   pnputil. exe-i-a a:\herbcam\ebcam. INF fügt den angegebenen Treiber hinzu und installiert ihn.
-   pnputil. exe – e listet alle Treiber von Drittanbietern auf.
-   pnputil. exe-d oem0. inf löscht die angegebene.
-   pnputil. exe-f-d oem0. inf erzwingt das Löschen der angegebenen INF-Datei.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Popd](popd.md)