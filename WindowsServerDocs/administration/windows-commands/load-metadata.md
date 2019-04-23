---
title: Laden von Metadaten
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2c535487-668b-44fc-babb-ff59cf7d190e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b52b5040fc8c834b04cad83ca4b0cfab103fdc43
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871331"
---
# <a name="load-metadata"></a>Laden von Metadaten



Lädt eine Metadaten-CAB-Datei vor dem Importieren der übertragbarer Schattenkopien oder lädt die Metadaten im Fall einer Wiederherstellung. Wenn Sie ohne Angabe von Parametern **Laden von Metadaten** zeigt die Hilfe an der Eingabeaufforderung.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
load metadata [<Drive>:][<Path>]<MetaData.cab>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<Drive>:][<Path>]|Gibt den Speicherort der Metadatendatei.|
|MetaData.cab|Gibt an, die Metadaten-CAB-Datei zu laden.|

## <a name="remarks"></a>Hinweise

-   Können Sie die **importieren** Befehl zum Importieren von übertragbarer Schattenkopien auf Grundlage der Metadaten gemäß **Laden von Metadaten**.
-   Mit diesem Befehl ist erforderlich, bevor Sie die **beginnen Wiederherstellung** Befehl aus, um die ausgewählten Writer und die Komponenten für die Wiederherstellung zu laden.

## <a name="BKMK_examples"></a>Beispiele für

Um eine Metadatendatei namens metafile.cab aus dem Standardspeicherort zu laden, geben Sie Folgendes ein:
```
load metadata metafile.cab
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)