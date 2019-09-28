---
title: reg laden
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3b0b2b1b-f510-4108-9e9d-7057e924aa6e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: db661e311e3fe8c393750716de5dab375e7817f4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384697"
---
# <a name="reg-load"></a>reg laden



Schreibt gespeicherte Unterschlüssel und Einträge in einen anderen Unterschlüssel in der Registrierung. Vorgesehen für die Verwendung mit temporären Dateien, die für die Problembehandlung oder Bearbeitung von Registrierungs Einträgen verwendet werden.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
reg load KeyName FileName
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<keyname >|Gibt den vollständigen Pfad des zu ladenden unter Schlüssels an. Wenn Sie Remote Computer angeben, schließen Sie den Computernamen (im Format \\ @ no__t-1computername @ no__t-2 als Teil des *keyName*-Steuerelement ein. Wenn \\ @ no__t-1computername \ weggelassen wird, wird der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: "HKLM", "HKCU", "HKCR", "HKU" und "HKCC" Wenn ein Remote Computer angegeben wird, sind gültige Stamm Schlüssel: HKLM und HKU.|
|\<Dateiname >|Gibt den Namen und den Pfad der Datei an, die geladen werden soll. Diese Datei muss im Voraus mit dem Registrierungsvorgang " **reg** " und der Erweiterung ". HIV" erstellt werden.|
|/?|Zeigt die Hilfe für den **reg Load** -Befehl an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

In der folgenden Tabelle sind die Rückgabewerte für den **reg-Lade** Vorgang aufgeführt.

|Wert|Description|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="BKMK_examples"></a>Beispiele

Wenn Sie die Datei mit dem Namen temphive. HIV in den Schlüssel hklm\temphive laden möchten, geben Sie Folgendes ein:
```
REG LOAD HKLM\TempHive TempHive.hiv
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)