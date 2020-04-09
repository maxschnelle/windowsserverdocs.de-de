---
title: ver
description: Windows-Befehls Thema für Ver, in dem die Versionsnummer des Betriebssystems angezeigt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5a9c6cd4-b67d-4b30-8c56-5f9798eafd2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d0d0676dcfa6546e4bbf74c4c58a24f51744d00f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830193"
---
# <a name="ver"></a>ver



Zeigt die Versionsnummer des Betriebssystems an.

Dieser Befehl wird in der Windows-Eingabeaufforderung (cmd. exe) unterstützt, jedoch nicht in PowerShell.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
ver
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Zum Abrufen der Versionsnummer des Betriebssystems von der Befehlsshell (cmd. exe) geben Sie Folgendes ein:

```
ver
```

Der Befehl "Ver" funktioniert nicht in PowerShell. Geben Sie Folgendes ein, um die Betriebssystemversion von PowerShell zu erhalten:

```powershell
$PSVersionTable.BuildVersion
````


## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
