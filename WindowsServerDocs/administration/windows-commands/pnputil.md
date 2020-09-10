---
title: pnputil
description: Referenz Artikel für den PnPUtil-Befehl, der Treiber Pakete hinzufügt, Treiber Pakete entfernt und Treiber Pakete im Treiber Speicher mithilfe des pnputil.exe Hilfsprogramms auflistet.
ms.topic: reference
ms.assetid: fab686b8-09d3-4f6c-afa2-630e6036f44c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: d88d48fe1fc5aa838bbe04f320ea4cac55e09eaa
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628620"
---
# <a name="pnputil"></a>pnputil

Pnputil.exe ist ein Befehlszeilen-Hilfsprogramm, das Sie zum Verwalten des Treiber Speichers verwenden können. Mit diesem Befehl können Sie Treiber Pakete hinzufügen, Treiber Pakete entfernen und Treiber Pakete auflisten, die sich im Speicher befinden.

## <a name="syntax"></a>Syntax

```
pnputil.exe [-f | -i] [ -? | -a | -d | -e ] <INF name>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -a | Gibt an, dass die identifizierte INF-Datei hinzugefügt wird. |
| -d | Gibt an, dass die identifizierte INF-Datei gelöscht werden soll. |
| -E | Gibt an, dass alle INF-Dateien von Drittanbietern aufgelistet werden. |
| -f | Gibt an, dass das Löschen der identifizierten INF-Datei erzwungen werden soll. Kann nicht in Verbindung mit dem **– i** -Parameter verwendet werden. |
| -i | Gibt an, dass die identifizierte INF-Datei installiert werden soll. Kann nicht in Verbindung mit dem **-f-** Parameter verwendet werden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Zum Hinzufügen einer INF-Datei mit dem Namen "". Inf, geben Sie Folgendes ein:

```
pnputil.exe -a a:\usbcam\USBCAM.INF
```

Um alle INF-Dateien hinzuzufügen, die sich in c:\drivers befinden, geben Sie Folgendes ein:

```
pnputil.exe -a c:\drivers\*.inf
```

Zum Hinzufügen und Installieren von "". INF-Treiber, geben Sie Folgendes ein:

```
pnputil.exe -i -a a:\usbcam\USBCAM.INF
```

Um alle Treiber von Drittanbietern aufzulisten, geben Sie Folgendes ein:

```
pnputil.exe –e
```

Geben Sie Folgendes ein, um die INF-Datei und den Treiber namens oem0. inf zu löschen:

```
pnputil.exe -d oem0.inf
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "POPD"](popd.md)
