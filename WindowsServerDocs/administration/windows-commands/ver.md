---
title: ver
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 384a5e8adb6c8304033f7dc645184ff2b674ae39
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887171"
---
# <a name="ver"></a>ver



Zeigt die Versionsnummer des Betriebssystems.

Mit diesem Befehl wird in der Windows-Eingabeaufforderung (Cmd.exe), aber nicht in PowerShell unterstützt.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
ver
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_examples"></a>Beispiele für

Um die Versionsnummer des Betriebssystems von der Befehlsshell (cmd.exe) zu erhalten, geben Sie Folgendes ein:

```
ver
```

Die Ver-Befehl funktioniert nicht in PowerShell. Um die Version von PowerShell zu erhalten, geben Sie Folgendes ein:

```powershell
$PSVersionTable.BuildVersion
````


#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)
