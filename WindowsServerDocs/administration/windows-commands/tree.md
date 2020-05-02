---
title: Struktur
description: Referenz Thema für die Struktur, in der die Verzeichnisstruktur eines Pfads oder des Datenträgers auf einem Laufwerk grafisch angezeigt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 345d3192-401e-4a3b-a8ac-36a85c7be79d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 94b0429dadc3965c7e41ad5aa881fc902988ec9b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721282"
---
# <a name="tree"></a>Struktur

Zeigt die Verzeichnisstruktur eines Pfads oder des Datenträgers auf einem Laufwerk grafisch an.



## <a name="syntax"></a>Syntax

```
tree [<Drive>:][<Path>] [/f] [/a]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Laufwerk>:|Gibt das Laufwerk an, das den Datenträger enthält, für den Sie die Verzeichnisstruktur anzeigen möchten.|
|\<Pfad>|Gibt das Verzeichnis an, für das Sie die Verzeichnisstruktur anzeigen möchten.|
|/f|Zeigt die Namen der Dateien in jedem Verzeichnis an.|
|/a|Gibt an **, dass die** Struktur Textzeichen anstelle von Grafikzeichen verwendet, um die Zeilen anzuzeigen, die Unterverzeichnisse verknüpfen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

Die Struktur, die von **Tree** angezeigt wird, hängt von den Parametern ab, die Sie an der Eingabeaufforderung angeben. Wenn Sie kein Laufwerk oder einen Pfad angeben, wird die Baumstruktur von **Tree** beginnend mit dem aktuellen Verzeichnis des aktuellen Laufwerks angezeigt.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Namen aller Unterverzeichnisse auf dem Datenträger auf dem aktuellen Laufwerk anzuzeigen:
```
tree \
```
Geben Sie Folgendes ein, um die Dateien in allen Verzeichnissen auf Laufwerk C anzuzeigen:
```
tree c:\ /f | more 
```
Geben Sie Folgendes ein, um eine Liste aller Verzeichnisse auf Laufwerk C zu drucken:
```
tree c:\ /f  prn 
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)