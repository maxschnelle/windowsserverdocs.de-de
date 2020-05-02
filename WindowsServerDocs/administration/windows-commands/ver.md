---
title: ver
description: Referenz Thema für Ver, in dem die Versionsnummer des Betriebssystems angezeigt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5a9c6cd4-b67d-4b30-8c56-5f9798eafd2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7050dddda6cc27c50980f2e44f40e1f682c1d375
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720314"
---
# <a name="ver"></a>ver



Zeigt die Versionsnummer des Betriebssystems an.

Dieser Befehl wird in der Windows-Eingabeaufforderung (cmd. exe) unterstützt, jedoch nicht in PowerShell.



## <a name="syntax"></a>Syntax

```
ver
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a>Beispiele

Zum Abrufen der Versionsnummer des Betriebssystems von der Befehlsshell (cmd. exe) geben Sie Folgendes ein:

```
ver
```

Der Befehl "Ver" funktioniert nicht in PowerShell. Geben Sie Folgendes ein, um die Betriebssystemversion von PowerShell zu erhalten:

```powershell
$PSVersionTable.BuildVersion
````


## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
