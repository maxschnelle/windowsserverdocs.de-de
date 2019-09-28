---
title: ver
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a9c6cd4-b67d-4b30-8c56-5f9798eafd2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e48b3b1061edf793c88693b3353753c6a4cedcfc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362722"
---
# <a name="ver"></a>ver



Zeigt die Versionsnummer des Betriebssystems an.

Dieser Befehl wird in der Windows-Eingabeaufforderung (cmd. exe) unterstützt, jedoch nicht in PowerShell.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
ver
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_examples"></a>Beispiele

Zum Abrufen der Versionsnummer des Betriebssystems von der Befehlsshell (cmd. exe) geben Sie Folgendes ein:

```
ver
```

Der Befehl "Ver" funktioniert nicht in PowerShell. Geben Sie Folgendes ein, um die Betriebssystemversion von PowerShell zu erhalten:

```powershell
$PSVersionTable.BuildVersion
````


#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
