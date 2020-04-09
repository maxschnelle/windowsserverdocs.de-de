---
title: exec
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d39fbf948050dd00f329e461c34c2365030cb05d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844993"
---
# <a name="exec"></a>exec



Führt eine Datei auf dem lokalen Computer aus. Bei der Datei kann es sich um ein **cmd** -Skript handeln.

## <a name="syntax"></a>Syntax

```
exec <ScriptFile.cmd>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<scriptfile. cmd >|Gibt die auszuführende Skriptdatei an.|

## <a name="remarks"></a>Hinweise

-   Dieser Befehl wird verwendet, um Daten im Rahmen einer Sicherungs-oder Wiederherstellungs Sequenz zu duplizieren oder wiederherzustellen.
-   Wenn das Skript fehlschlägt, wird ein Fehler zurückgegeben, und DiskShadow wird beendet.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)