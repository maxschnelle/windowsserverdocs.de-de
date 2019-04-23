---
title: append
description: 'Windows-Befehle Thema '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c3fea20-9502-40ad-a442-7a927aad88eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: abf7713b3fd5bbb6172969ca1cc39cbbbbafafc6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881981"
---
# <a name="append"></a>append



Ermöglicht Programmen, die Datendateien in den angegebenen Verzeichnissen zu öffnen, als wären sie im aktuellen Verzeichnis. Wenn Sie ohne Angabe von Parametern **Anfügen** zeigt die Liste der hinzugefügten Verzeichnisse.

> [!NOTE]
> Dieser Befehl in Windows 10 nicht unterstützt.
>

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
append [[<Drive>:]<Path>[;...]] [/x[:on|:off]] [/path:[:on|:off] [/e] 
append ;
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<Drive>:]<Path>|Gibt an, als Laufwerk und Verzeichnis, angefügt werden soll.|
|/x:on|Wendet angefügten Verzeichnisse Dateisuchen und beim Starten von Anwendungen.|
|/x:off|Wendet angefügten Verzeichnisse nur auf Anforderungen zum Öffnen von Dateien.</br>**/ x: off** ist die Standardeinstellung.|
|/path:on|Wendet angefügten Verzeichnisse für dateianforderungen, die bereits über einen Pfad angeben. **/ Path: auf** ist die Standardeinstellung.|
|/path:off|Deaktiviert die Auswirkungen der **/Path: auf**.|
|/ e|Speichert eine Kopie der Liste der hinzugefügten Verzeichnisse in einer Umgebungsvariablen mit dem Namen ANFÜGEN. **/ e** herangezogen werden nur beim ersten Mal Sie verwenden **Anfügen** nach Start des Systems.|
|;|Löscht die Liste der hinzugefügten Verzeichnisse.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="BKMK_examples"></a>Beispiele für

Um die Liste der hinzugefügten Verzeichnisse zu löschen, geben Sie Folgendes ein:
```
append ;
```
Um eine Kopie des angefügten Verzeichnisses, das eine Umgebungsvariable namens ANFÜGEN zu speichern, geben Sie Folgendes ein:
```
append /e
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)
