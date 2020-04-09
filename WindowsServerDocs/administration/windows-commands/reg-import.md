---
title: reg-Import
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0be103de-08fc-4f02-b590-361782680b3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0816297e837bbce91ca069e3506405cbdb53c51a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836423"
---
# <a name="reg-import"></a>reg-Import



Kopiert den Inhalt einer Datei, die exportierte Registrierungs Unterschlüssel, Einträge und Werte enthält, in die Registrierung des lokalen Computers.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Reg import FileName
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Dateiname >|Gibt den Namen und Pfad der Datei an, die Inhalte enthält, die in die Registrierung des lokalen Computers kopiert werden sollen. Diese Datei muss im Voraus mit dem reg- **Export**erstellt werden.|
|/?|Zeigt die Hilfe für den **reg-Import** an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

In der folgenden Tabelle sind die Rückgabewerte für den **reg-Import** Vorgang aufgeführt.

|Wert|Beschreibung|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um Registrierungseinträge aus der Datei mit dem Namen appbkup. reg zu importieren:
```
reg import AppBkUp.reg
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)