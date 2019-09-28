---
title: assoc
description: 'Thema Windows-Befehle für **Assoc** : zeigt die Zuordnungen von Dateinamen Erweiterungen an oder ändert diese.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 237bedda-b24c-4fec-a39c-9b7eacf96417
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e4a6fd700cbe66897a24f01f66387e76e07b568b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382669"
---
# <a name="assoc"></a>assoc



Zeigt Zuordnungen für Dateinamen Erweiterungen an oder ändert diese. Bei Verwendung ohne Parameter zeigt **Assoc** eine Liste aller aktuellen Zuordnungen für Dateinamen Erweiterungen an.

> [!NOTE]
> Dieser Befehl wird nur in cmd unterstützt. EXE und ist in PowerShell nicht verfügbar.
>

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
assoc [<.ext>[=[<FileType>]]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|<. ext >|Gibt die Dateinamenerweiterung an.|
|\<filetype >|Gibt den Dateityp an, der der angegebenen Dateinamenerweiterung zugeordnet werden soll.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Um die Dateityp Zuordnung für eine Dateinamenerweiterung zu entfernen, fügen Sie nach dem Gleichheitszeichen ein Leerzeichen hinzu, indem Sie die Leertaste drücken.
-   Verwenden Sie den **ftype** -Befehl, um aktuelle Dateitypen anzuzeigen, für die geöffnete Befehls Zeichenfolgen definiert sind.
-   Um die Ausgabe von **Assoc** in eine Textdatei umzuleiten, verwenden Sie den **>-** Umleitungs Operator.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um die aktuelle Dateityp Zuordnung für die Dateinamenerweiterung. txt anzuzeigen:
```
assoc .txt
```
Um die Dateityp Zuordnung für die Dateinamenerweiterung. bak zu entfernen, geben Sie Folgendes ein:
```
assoc .bak= 
```

> [!NOTE]
> Achten Sie darauf, nach dem Gleichheitszeichen ein Leerzeichen hinzuzufügen.

Geben Sie Folgendes ein, um die Ausgabe von **Assoc** auf einem Bildschirm anzuzeigen:
```
assoc | more
```
Geben Sie Folgendes ein, um die Ausgabe von **Assoc** an die Datei "Assoc. txt" zu senden:
```
assoc>assoc.txt
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
