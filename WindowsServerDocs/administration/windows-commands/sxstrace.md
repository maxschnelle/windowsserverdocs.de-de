---
title: sxstrace
description: Referenz Artikel für den systrace-Befehl, der Sie bei der Diagnose paralleler Probleme unterstützt.
ms.topic: reference
ms.assetid: fcd26eeb-fbd9-4a86-b6a9-dfa5e9c6e4fc
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 95f52993db56e61b3a1cd4d26a0ef36626421a15
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91718207"
---
# <a name="sxstrace"></a>sxstrace

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Diagnostizieren paralleler Probleme

## <a name="syntax"></a>Syntax

```
sxstrace [{[trace -logfile:<filename> [-nostop]|[parse -logfile:<filename> -outfile:<parsedfile>  [-filter:<appname>]}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| Ablaufverfolgung | Aktiviert die Ablauf Verfolgung für nebeneinander. |
| -Logfile | Gibt die unformatierte Protokolldatei an. |
| `<filename>` | Speichert das Ablauf Verfolgungs Protokoll in `<filename` . |
| -nostoppt | Gibt an, dass Sie keine Aufforderung zum Abbrechen der Ablauf Verfolgung erhalten sollten. |
| parse | Übersetzt die RAW-Ablauf Verfolgungs Datei. |
| -outfile | Gibt den Ausgabe Dateinamen an. |
| `<parsedfile>` | Gibt den Dateinamen der analysierten Datei an. |
| -filter | Ermöglicht das Filtern der Ausgabe. |
| `<appname>` | Gibt den Namen der Anwendung an. |
| stoptrace | Beendet die Ablauf Verfolgung, wenn Sie nicht zuvor beendet wurde. |
| -? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Um die Ablauf Verfolgung zu aktivieren und die Ablauf Verfolgungs Datei in *sxstrace. ETL*zu speichern, geben Sie Folgendes ein:

```
sxstrace trace -logfile:sxstrace.etl
```

Um die unformatierte Ablauf Verfolgungs Datei in ein lesbares Format zu übersetzen und das Ergebnis in *sxstrace.txt*zu speichern, geben Sie Folgendes ein:

```
sxstrace parse -logfile:sxstrace.etl -outfile:sxstrace.txt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
