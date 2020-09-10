---
title: sxstrace
description: Erfahren Sie, wie Sie parallele Probleme diagnostizieren können.
ms.topic: reference
ms.assetid: fcd26eeb-fbd9-4a86-b6a9-dfa5e9c6e4fc
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7afcb79bf12cf23a66ac564362012c4424e5bbe6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626775"
---
# <a name="sxstrace"></a>sxstrace

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Diagnostizieren paralleler Probleme

## <a name="syntax"></a>Syntax
```
sxstrace [{[trace -logfile:<FileName> [-nostop]|[parse -logfile:<FileName> -outfile:<ParsedFile>  [-filter:<AppName>]}]
```

#### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|Ablaufverfolgung|Aktiviert die Ablauf Verfolgung für SxS (Seite an Seite).|
|-Logfile|Gibt die unformatierte Protokolldatei an.|
|\<FileName>|Speichert das Ablauf Verfolgungs Protokoll in *filename*.|
|-nostoppt|Gibt keine Aufforderung zum Abbrechen der Ablauf Verfolgung an.|
|parse|Übersetzt die RAW-Ablauf Verfolgungs Datei.|
|-outfile|Gibt den Ausgabe Dateinamen an.|
|\<ParsedFile>|Gibt den Dateinamen der analysierten Datei an.|
|-filter|Ermöglicht das Filtern der Ausgabe.|
|\<AppName>|Gibt den Namen der Anwendung an.|
|stoptrace|Beenden Sie die Ablauf Verfolgung, wenn Sie noch nicht beendet wurde.|
|-?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a>Beispiele
Aktivieren Sie die Ablauf Verfolgung, und speichern Sie die Ablauf Verfolgungs Datei in **sxstrace. ETL**:
```
sxstrace trace -logfile:sxstrace.etl
```
Übersetzen Sie die unformatierte Ablauf Verfolgungs Datei in ein lesbares Format, und speichern Sie das Ergebnis in **sxstrace.txt**:
```
sxstrace parse -logfile:sxstrace.etl -outfile:sxstrace.txt
```

## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

