---
title: reg laden
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3b0b2b1b-f510-4108-9e9d-7057e924aa6e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 140c6b51b9f88081a8686ebebbc9400f241b5ef6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836383"
---
# <a name="reg-load"></a>reg laden



Schreibt gespeicherte Unterschlüssel und Einträge in einen anderen Unterschlüssel in der Registrierung. Vorgesehen für die Verwendung mit temporären Dateien, die für die Problembehandlung oder Bearbeitung von Registrierungs Einträgen verwendet werden.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
reg load KeyName FileName
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName >|Gibt den vollständigen Pfad des zu ladenden unter Schlüssels an. Zum Angeben von Remote Computern müssen Sie den Computernamen (im Format \\\\Computername als Teil des *keyName*-\) einschließen. Wenn \\\\Computername \ weggelassen wird, wird der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: HKLM, HKCU, HKCR, HKU und HKCC. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: HKLM und HKU.|
|\<Dateiname >|Gibt den Namen und den Pfad der Datei an, die geladen werden soll. Diese Datei muss im Voraus mit dem Registrierungsvorgang " **reg** " und der Erweiterung ". HIV" erstellt werden.|
|/?|Zeigt die Hilfe für den **reg Load** -Befehl an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

In der folgenden Tabelle sind die Rückgabewerte für den **reg-Lade** Vorgang aufgeführt.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Wenn Sie die Datei mit dem Namen temphive. HIV in den Schlüssel hklm\temphive laden möchten, geben Sie Folgendes ein:
```
REG LOAD HKLM\TempHive TempHive.hiv
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)