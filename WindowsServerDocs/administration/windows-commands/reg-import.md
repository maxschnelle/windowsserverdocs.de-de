---
title: REG import
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0be103de-08fc-4f02-b590-361782680b3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d1dd1b61848671b528c62fd22fe656e14fda7b1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861841"
---
# <a name="reg-import"></a>REG import



Kopiert den Inhalt der Datei, die enthält exportiert Registrierungsunterschlüssel, Einträge und Werte in die Registrierung des lokalen Computers.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Reg import FileName
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<FileName>|Gibt den Namen und Pfad der Datei, die Inhalte der Registrierung des lokalen Computers kopiert werden soll. Diese Datei muss im Voraus erstellt werden, mithilfe von **Reg Export**.|
|/?|Zeigt die Hilfe für **Reg Import** an der Eingabeaufforderung.|

## <a name="remarks"></a>Hinweise

Die folgende Tabelle enthält die Rückgabewerte für die **Reg Import** Vorgang.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="BKMK_examples"></a>Beispiele für

Um Einträge in der Registrierung aus der Datei mit dem Namen AppBkUp.reg zu importieren, geben Sie Folgendes ein:
```
reg import AppBkUp.reg
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)