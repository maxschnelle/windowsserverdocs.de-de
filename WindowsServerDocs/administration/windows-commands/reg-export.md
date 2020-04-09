---
title: reg-Export
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ad9526f-1e29-4fa5-9d2d-feaa92f12d7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5901014511fed0c17a641e1ed183ddbf40dd44c8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836493"
---
# <a name="reg-export"></a>reg-Export



Kopiert die angegebenen Unterschlüssel, Einträge und Werte des lokalen Computers in eine Datei für die Übertragung an andere Server.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Reg export KeyName FileName [/y]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName >|Gibt den vollständigen Pfad des unter Schlüssels an. Der Export Vorgang funktioniert nur mit dem lokalen Computer. Der KeyName muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel sind: HKLM, HKCU, HKCR, HKU und HKCC.|
|\<Dateiname >|Gibt den Namen und Pfad der Datei an, die während des Vorgangs erstellt werden soll. Die Datei muss die Erweiterung ". reg" aufweisen.|
|/y|Überschreibt alle vorhandenen Dateien mit dem Namen *filename* , ohne zur Bestätigung aufzufordern.|
|/?|Zeigt die Hilfe für den **reg-Export** an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

In der folgenden Tabelle sind die Rückgabewerte für den **reg-Export** Vorgang aufgeführt.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um den Inhalt aller Unterschlüssel und Werte des Schlüssels "MyApp" in die Datei "appbkup. reg" zu exportieren:
```
reg export HKLM\Software\MyCo\MyApp AppBkUp.reg
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)