---
title: reg entladen
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1d07791d-ca27-454e-9797-27d7e84c5048
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5fd1436ed1122a09eea11d358a3711aedddf2c1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836273"
---
# <a name="reg-unload"></a>reg entladen



Entfernt einen Abschnitt der Registrierung, der mit dem reg- **Lade** Vorgang geladen wurde.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
reg unload <KeyName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName >|Gibt den vollständigen Pfad des zu entladenden unter Schlüssels an. Zum Angeben von Remote Computern müssen Sie den Computernamen (im Format \\\\Computername als Teil des *keyName*-\) einschließen. Wenn \\\\Computername \ weggelassen wird, wird der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind "HKLM", "HKCU", "HKCR", "HKU" und "HKCC". Wenn ein Remote Computer angegeben wird, lauten gültige Stamm Schlüssel HKLM und HKU.|
|/?|Zeigt die Hilfe zum **Entladen von reg** an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

In der folgenden Tabelle sind die Rückgabewerte für die Option zum **Entladen von reg** aufgeführt.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Zum Entladen der Hive-temphive in der Datei HKLM geben Sie Folgendes ein:
```
REG UNLOAD HKLM\TempHive
```

> [!CAUTION]
> Bearbeiten Sie die Registrierung nur dann direkt, wenn Sie keine Alternative haben. Der Registrierungs-Editor umgeht Standard-Sicherheitsvorkehrungen und ermöglicht Einstellungen, die die Leistung beeinträchtigen, das System beschädigen oder sogar die Neuinstallation von Windows erfordern. Sie können die meisten Registrierungs Einstellungen sicher ändern, indem Sie die Programme in der Systemsteuerung oder Microsoft Management Console (MMC) verwenden. Wenn Sie die Registrierung direkt bearbeiten müssen, sichern Sie Sie zuerst.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)