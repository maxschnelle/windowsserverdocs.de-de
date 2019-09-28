---
title: reg entladen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d07791d-ca27-454e-9797-27d7e84c5048
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 32df397b597291269dcfb1449d00e86b2f4f5836
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384619"
---
# <a name="reg-unload"></a>reg entladen



Entfernt einen Abschnitt der Registrierung, der mit dem reg- **Lade** Vorgang geladen wurde.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
reg unload <KeyName>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<keyname >|Gibt den vollständigen Pfad des zu entladenden unter Schlüssels an. Wenn Sie Remote Computer angeben, schließen Sie den Computernamen (im Format \\ @ no__t-1computername @ no__t-2 als Teil des *keyName*-Steuerelement ein. Wenn \\ @ no__t-1computername \ weggelassen wird, wird der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind "HKLM", "HKCU", "HKCR", "HKU" und "HKCC". Wenn ein Remote Computer angegeben wird, lauten gültige Stamm Schlüssel HKLM und HKU.|
|/?|Zeigt die Hilfe zum **Entladen von reg** an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

In der folgenden Tabelle sind die Rückgabewerte für die Option zum **Entladen von reg** aufgeführt.

|Wert|Description|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="BKMK_examples"></a>Beispiele

Zum Entladen der Hive-temphive in der Datei HKLM geben Sie Folgendes ein:
```
REG UNLOAD HKLM\TempHive
```

> [!CAUTION]
> Bearbeiten Sie die Registrierung nur dann direkt, wenn Sie keine Alternative haben. Der Registrierungs-Editor umgeht Standard-Sicherheitsvorkehrungen und ermöglicht Einstellungen, die die Leistung beeinträchtigen, das System beschädigen oder sogar die Neuinstallation von Windows erfordern. Sie können die meisten Registrierungs Einstellungen sicher ändern, indem Sie die Programme in der Systemsteuerung oder Microsoft Management Console (MMC) verwenden. Wenn Sie die Registrierung direkt bearbeiten müssen, sichern Sie Sie zuerst.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)