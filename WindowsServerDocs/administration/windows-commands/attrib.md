---
title: attrib
description: Thema Windows-Befehle für **atungb** -zeigt Attribute an, die Dateien oder Verzeichnissen zugewiesen sind, oder entfernt Sie.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e763ca5-21a2-45d2-b26d-a9c44c99091a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 702bad9e48456898d38ba9094910b1419e724a76
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382606"
---
# <a name="attrib"></a>attrib



Hiermit werden Attribute angezeigt, festgelegt oder entfernt, die Dateien oder Verzeichnissen zugewiesen sind. Bei Verwendung ohne Parameter zeigt **atyb** Attribute aller Dateien im aktuellen Verzeichnis an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
attrib [{+|-}r] [{+|-}a] [{+|-}s] [{+|-}h] [{+|-}i] [<Drive>:][<Path>][<FileName>] [/s [/d] [/l]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|{+ \|-} r|Legt ( **+** ) oder löscht ( **-** ) das schreibgeschützte Datei Attribut.|
|{+ \|-} a|Legt ( **+** ) oder löscht ( **-** ) das Archivdatei Attribut.|
|{+ \|-} s|Legt ( **+** ) oder löscht ( **-** ) das System Datei Attribut.|
|{+ \|-} h|Legt ( **+** ) oder löscht ( **-** ) das ausgeblendete Datei Attribut.|
|{+ \|-} i|Legt ( **+** ) oder löscht ( **-** ) das Attribut not Content indizierte Datei.|
|[\<laufwerk >:] [<Path>] [<FileName>]|Gibt den Speicherort und den Namen des Verzeichnisses, der Datei oder der Gruppe von Dateien an, für die Sie Attribute anzeigen oder ändern möchten. Sie können den **?** und **&#42;** Platzhalter Zeichen im *filename* -Parameter, um die Attribute für eine Gruppe von Dateien anzuzeigen oder zu ändern.|
|/s|Wendet **atungb** und alle Befehlszeilenoptionen auf übereinstimmende Dateien im aktuellen Verzeichnis und allen Unterverzeichnissen an.|
|/d|Wendet **attrb** und alle Befehlszeilenoptionen auf Verzeichnisse an.|
|/l|Wendet **atungb** und alle Befehlszeilenoptionen auf die symbolische Verknüpfung anstelle des Ziels der symbolischen Verknüpfung an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Sie können Platzhalter Zeichen verwenden ( **?** und **&#42;** ) mit dem *filename* -Parameter, um die Attribute für eine Gruppe von Dateien anzuzeigen oder zu ändern.
-   Wenn für eine Datei das System (**s**) oder Hidden (**h**)-Attribut festgelegt ist, müssen Sie das-Attribut löschen, bevor Sie andere Attribute für diese Datei ändern können.
-   Das Archive-Attribut (**a**) markiert Dateien, die sich seit der letzten Sicherung geändert haben. Beachten Sie, dass der **xcopy** -Befehl Archiv Attribute verwendet.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um die Attribute einer Datei mit dem Namen News86 anzuzeigen, die sich im aktuellen Verzeichnis befindet:
```
attrib news86 
```
Wenn Sie das Attribut "schreibgeschützt" der Datei "Report. txt" zuweisen möchten, geben Sie Folgendes ein:
```
attrib +r report.txt 
```
Um das schreibgeschützte Attribut aus den Dateien im öffentlichen Verzeichnis und seinen Unterverzeichnissen auf einem Datenträger auf Laufwerk B zu entfernen, geben Sie Folgendes ein:
```
attrib -r b:\public\*.* /s 
```
Um das Archive-Attribut für alle Dateien auf Laufwerk A festzulegen, und löschen Sie dann das Archiv Attribut für Dateien mit der Erweiterung. bak, geben Sie Folgendes ein:
```
attrib +a a:*.* & attrib -a a:*.bak 
```
