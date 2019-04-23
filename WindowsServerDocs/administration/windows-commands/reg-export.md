---
title: Reg export
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ad9526f-1e29-4fa5-9d2d-feaa92f12d7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d7aeddb4b069b1baf5b8f7aaea2730a2b25bdad7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889651"
---
# <a name="reg-export"></a>Reg export



Kopiert den angegebenen Unterschlüssel, Einträge und Werte des lokalen Computers in eine Datei für die Übertragung auf andere Server.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Reg export KeyName FileName [/y]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<KeyName>|Gibt den vollständigen Pfad des Unterschlüssels. Der Exportvorgang funktioniert nur mit dem lokalen Computer. Der Schlüsselname muss einen gültiges Stammzertifizierungsstellen-Schlüssel enthalten. Gültiges Stammzertifizierungsstellen-Schlüssel sind: HKLM, "HKCU", "HKCR", "HKU", und "HKCC".|
|\<FileName>|Gibt den Namen und Pfad der Datei, die während des Vorgangs erstellt werden. Die Datei muss es sich um eine Erweiterung REG aufweisen.|
|/y|Überschreibt eine vorhandene Datei mit dem Namen *FileName* ohne zur Bestätigung aufzufordern.|
|/?|Zeigt die Hilfe für **Reg Export** an der Eingabeaufforderung.|

## <a name="remarks"></a>Hinweise

Die folgende Tabelle enthält die Rückgabewerte für die **Reg Export** Vorgang.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie Folgendes ein, um den Inhalt aller Unterschlüssel und Werte des Schlüssels "MyApp" in einer Datenträgerdatei zu exportieren:
```
reg export HKLM\Software\MyCo\MyApp AppBkUp.reg
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)