---
title: tree
description: Referenz Artikel für Tree, der die Verzeichnisstruktur eines Pfads oder des Datenträgers auf einem Laufwerk grafisch anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 345d3192-401e-4a3b-a8ac-36a85c7be79d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dea885a8149c8231f3cb8e24c2128622131206e7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932393"
---
# <a name="tree"></a>tree

Zeigt die Verzeichnisstruktur eines Pfads oder des Datenträgers auf einem Laufwerk grafisch an.



## <a name="syntax"></a>Syntax

```
tree [<Drive>:][<Path>] [/f] [/a]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Drive>:|Gibt das Laufwerk an, das den Datenträger enthält, für den Sie die Verzeichnisstruktur anzeigen möchten.|
|\<Path>|Gibt das Verzeichnis an, für das Sie die Verzeichnisstruktur anzeigen möchten.|
|/f|Zeigt die Namen der Dateien in jedem Verzeichnis an.|
|/a|Gibt an **, dass die** Struktur Textzeichen anstelle von Grafikzeichen verwendet, um die Zeilen anzuzeigen, die Unterverzeichnisse verknüpfen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)