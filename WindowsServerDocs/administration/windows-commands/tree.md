---
title: tree
description: Referenz Artikel für Tree, der die Verzeichnisstruktur eines Pfads oder des Datenträgers auf einem Laufwerk grafisch anzeigt.
ms.topic: article
ms.assetid: 345d3192-401e-4a3b-a8ac-36a85c7be79d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44e3e54f986cc4bd4459d4e007c5111b664a6a45
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87897091"
---
# <a name="tree"></a>tree

Zeigt die Verzeichnisstruktur eines Pfads oder des Datenträgers auf einem Laufwerk grafisch an.



## <a name="syntax"></a>Syntax

```
tree [<Drive>:][<Path>] [/f] [/a]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Drive>:|Gibt das Laufwerk an, das den Datenträger enthält, für den Sie die Verzeichnisstruktur anzeigen möchten.|
|\<Path>|Gibt das Verzeichnis an, für das Sie die Verzeichnisstruktur anzeigen möchten.|
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)