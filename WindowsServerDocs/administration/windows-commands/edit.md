---
title: bearbeiten
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4e0ff2e8-3518-47c1-8c69-5e93f895fa0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4dfffefbe113bc5df242a00357c769aaa9c1c787
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845223"
---
# <a name="edit"></a>bearbeiten



Startet den MS-DOS-Editor, mit dem ASCII-Textdateien erstellt und geändert werden.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
edit [/b] [/h] [/r] [/s] [/<NNN>] [[<Drive>:][<Path>]<FileName> [<FileName2> [...]]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<Laufwerk >:] [<Path>]<FileName> [<FileName2> [...]]|Gibt den Speicherort und den Namen einer oder mehrerer ASCII-Textdateien an. Wenn die Datei nicht vorhanden ist, wird Sie vom MS-DOS-Editor erstellt. Wenn die Datei vorhanden ist, wird Sie vom MS-DOS-Editor geöffnet, und der Inhalt wird auf dem Bildschirm angezeigt. *Filename* kann Platzhalter Zeichen ( **&#42;** und **?** ) enthalten. Trennen Sie mehrere Dateinamen mit Leerzeichen.|
|/b|Erzwingt den Monochrom-Modus, sodass der MS-DOS-Editor in schwarz und weiß angezeigt wird.|
|/h|Zeigt die maximale Anzahl von Zeilen an, die für den aktuellen Monitor möglich sind.|
|/r|Lädt Dateien im schreibgeschützten Modus.|
|/s|Erzwingt die Verwendung von kurzen Dateinamen.|
|\<nnn >|Lädt Binärdateien und umwickelt Zeilen in *nnn* -Zeichen breit.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Wenn Sie weitere Hilfe benötigen, öffnen Sie den MS-DOS-Editor, und drücken Sie dann die F1-Taste.
-   Einige Monitore unterstützen standardmäßig nicht die Anzeige von Tastenkombinationen. Wenn der Monitor keine Tastenkombinationen anzeigt, verwenden Sie **/b**.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie zum Öffnen des MS-DOS-Editors Folgendes ein:
```
edit
```
Geben Sie Folgendes ein, um eine Datei mit dem Namen newtextfile. txt im aktuellen Verzeichnis zu erstellen und zu bearbeiten:
```
edit newtextfile.txt
```