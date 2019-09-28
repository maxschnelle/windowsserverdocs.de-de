---
title: bearbeiten
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e0ff2e8-3518-47c1-8c69-5e93f895fa0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a51a81a0ed2d28a30e8ec221d5719968dce48ac
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377616"
---
# <a name="edit"></a>bearbeiten



Startet den MS-DOS-Editor, mit dem ASCII-Textdateien erstellt und geändert werden.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
edit [/b] [/h] [/r] [/s] [/<NNN>] [[<Drive>:][<Path>]<FileName> [<FileName2> [...]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<laufwerk >:] [<Path>] <FileName> [<FileName2> [...]]|Gibt den Speicherort und den Namen einer oder mehrerer ASCII-Textdateien an. Wenn die Datei nicht vorhanden ist, wird Sie vom MS-DOS-Editor erstellt. Wenn die Datei vorhanden ist, wird Sie vom MS-DOS-Editor geöffnet, und der Inhalt wird auf dem Bildschirm angezeigt. *Filename* kann Platzhalter Zeichen ( **&#42;** und **?** ) enthalten. Trennen Sie mehrere Dateinamen mit Leerzeichen.|
|/b|Erzwingt den Monochrom-Modus, sodass der MS-DOS-Editor in schwarz und weiß angezeigt wird.|
|/h|Zeigt die maximale Anzahl von Zeilen an, die für den aktuellen Monitor möglich sind.|
|/r|Lädt Dateien im schreibgeschützten Modus.|
|/s|Erzwingt die Verwendung von kurzen Dateinamen.|
|\<NNN >|Lädt Binärdateien und umwickelt Zeilen in *nnn* -Zeichen breit.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Wenn Sie weitere Hilfe benötigen, öffnen Sie den MS-DOS-Editor, und drücken Sie dann die F1-Taste.
-   Einige Monitore unterstützen standardmäßig nicht die Anzeige von Tastenkombinationen. Wenn der Monitor keine Tastenkombinationen anzeigt, verwenden Sie **/b**.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie zum Öffnen des MS-DOS-Editors Folgendes ein:
```
edit
```
Geben Sie Folgendes ein, um eine Datei mit dem Namen newtextfile. txt im aktuellen Verzeichnis zu erstellen und zu bearbeiten:
```
edit newtextfile.txt
```