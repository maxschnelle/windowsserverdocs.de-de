---
title: tree
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 345d3192-401e-4a3b-a8ac-36a85c7be79d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de22de1c9d62ba79c1aa68248109cca88009703a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872631"
---
# <a name="tree"></a>tree



Zeigt die Verzeichnisstruktur eines Pfads oder des Datenträgers in ein Laufwerk grafisch an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
tree [<Drive>:][<Path>] [/f] [/a]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Laufwerk >:|Gibt an, das Laufwerk, das den Datenträger enthält, für den Verzeichnisstruktur angezeigt werden soll.|
|\<Pfad >|Gibt das Verzeichnis für das Verzeichnisstruktur angezeigt werden sollen.|
|/f|Zeigt den Namen der Dateien in jedem Verzeichnis an.|
|/a|Gibt an, dass **Struktur** besteht darin, Textzeichen statt grafische Zeichen verwenden, um die Zeilen anzuzeigen, die Unterverzeichnisse zu verknüpfen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Die Struktur angezeigt werden, indem **Struktur** richtet sich nach den Parametern, die Sie an der Eingabeaufforderung angeben. Wenn Sie kein Laufwerk oder einen Pfad angeben **Struktur** zeigt die Struktur beginnend mit dem aktuellen Verzeichnis für das aktuelle Laufwerk.

## <a name="BKMK_examples"></a>Beispiele für

Um die Namen aller Unterverzeichnisse in das aktuelle Laufwerk auf dem Datenträger anzuzeigen, geben Sie Folgendes ein:
```
tree \
```
Um anzuzeigen, einen Bildschirm zu einem Zeitpunkt, die Dateien in allen Verzeichnissen auf Laufwerk C, geben Sie Folgendes ein:
```
tree c:\ /f | more 
```
Geben Sie Folgendes ein, um eine Liste aller Verzeichnisse auf Laufwerk C zu drucken:
```
tree c:\ /f  prn 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)