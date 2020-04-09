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
ms.openlocfilehash: ece727b68eb620e839cbfb8efe02dbe775666498
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833613"
---
# <a name="sxstrace"></a>sxstrace

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Diagnostizieren paralleler Probleme    

## <a name="syntax"></a>Syntax  
```  
sxstrace [{[trace -logfile:<FileName> [-nostop]|[parse -logfile:<FileName> -outfile:<ParsedFile>  [-filter:<AppName>]}]  
```  

#### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|Ablauf Verfolgungs|Aktiviert die Ablauf Verfolgung für SxS (Seite an Seite).|  
|-Logfile|Gibt die unformatierte Protokolldatei an.|  
|\<Dateiname >|Speichert das Ablauf Verfolgungs Protokoll in *filename*.|  
|-nostoppt|Gibt keine Aufforderung zum Abbrechen der Ablauf Verfolgung an.|  
|analysieren|Übersetzt die RAW-Ablauf Verfolgungs Datei.|  
|-outfile|Gibt den Ausgabe Dateinamen an.|  
|> der \<-Datei|Gibt den Dateinamen der analysierten Datei an.|  
|-Filter|Ermöglicht das Filtern der Ausgabe.|  
|\<appname >|Gibt den Namen der Anwendung an.|  
|stoptrace|Beenden Sie die Ablauf Verfolgung, wenn Sie noch nicht beendet wurde.|  
|-?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="examples"></a><a name="BKMK_Examples"></a>Beispiele  
Aktivieren Sie die Ablauf Verfolgung, und speichern Sie die Ablauf Verfolgungs Datei in **sxstrace. ETL**:  
```  
sxstrace trace -logfile:sxstrace.etl  
```  
Übersetzen Sie die unformatierte Ablauf Verfolgungs Datei in ein lesbares Format, und speichern Sie das Ergebnis in **sxstrace. txt**:  
```  
sxstrace parse -logfile:sxstrace.etl -outfile:sxstrace.txt  
```  

## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
