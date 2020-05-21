---
title: sxstrace
description: Erfahren Sie, wie Sie parallele Probleme diagnostizieren können.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fcd26eeb-fbd9-4a86-b6a9-dfa5e9c6e4fc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e56b190c96633c5f9ee62328429abdbbf181434f
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436945"
---
# <a name="sxstrace"></a>sxstrace

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Diagnostizieren paralleler Probleme

## <a name="syntax"></a>Syntax
```
sxstrace [{[trace -logfile:<FileName> [-nostop]|[parse -logfile:<FileName> -outfile:<ParsedFile>  [-filter:<AppName>]}]
```

#### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|Ablaufverfolgung|Aktiviert die Ablauf Verfolgung für SxS (Seite an Seite).|
|-Logfile|Gibt die unformatierte Protokolldatei an.|
|\<Dateiname>|Speichert das Ablauf Verfolgungs Protokoll in *filename*.|
|-nostoppt|Gibt keine Aufforderung zum Abbrechen der Ablauf Verfolgung an.|
|parse|Übersetzt die RAW-Ablauf Verfolgungs Datei.|
|-outfile|Gibt den Ausgabe Dateinamen an.|
|\<> für das von Dateien|Gibt den Dateinamen der analysierten Datei an.|
|-filter|Ermöglicht das Filtern der Ausgabe.|
|\<AppName->|Gibt den Namen der Anwendung an.|
|stoptrace|Beenden Sie die Ablauf Verfolgung, wenn Sie noch nicht beendet wurde.|
|-?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a>Beispiele
Aktivieren Sie die Ablauf Verfolgung, und speichern Sie die Ablauf Verfolgungs Datei in **sxstrace. ETL**:
```
sxstrace trace -logfile:sxstrace.etl
```
Übersetzen Sie die unformatierte Ablauf Verfolgungs Datei in ein lesbares Format, und speichern Sie das Ergebnis in **sxstrace. txt**:
```
sxstrace parse -logfile:sxstrace.etl -outfile:sxstrace.txt
```

## <a name="additional-references"></a>Zusätzliche Referenzen
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

