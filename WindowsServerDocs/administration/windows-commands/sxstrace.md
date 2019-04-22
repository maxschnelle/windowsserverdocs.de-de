---
title: sxstrace
description: Erfahren Sie, wie Sie die Seite-an-Seite Probleme zu diagnostizieren.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fcd26eeb-fbd9-4a86-b6a9-dfa5e9c6e4fc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 396d06bf079c0cfa8ba4864f71333eec39f7b255
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814101"
---
# <a name="sxstrace"></a>sxstrace

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Seite-an-Seite-Probleme diagnostizieren.    

## <a name="syntax"></a>Syntax  
```  
sxstrace [{[trace /logfile:<FileName> [/nostop]|[parse /logfile:<FileName> /outfile:<ParsedFile>  [/filter:<AppName>]}]  
```  

### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|Ablaufverfolgung|Aktiviert die Ablaufverfolgung für Sxs (Seite-an-Seite)|  
|/logfile|Gibt die reinen Log-Datei.|  
|\<FileName>|Protokoll für die speichert *FileName*.|  
|/nostop|Gibt an, keine Aufforderung zum Beenden der Ablaufverfolgung.|  
|Analysieren|Übersetzt die unformatierten Ablaufverfolgungsdatei an.|  
|/outfile|Gibt an, der Name der Ausgabedatei.|  
|\<ParsedFile>|Gibt den Dateinamen der analysierten Datei.|  
|/filter|Kann die Ausgabe gefiltert werden sollen.|  
|\<AppName>|Gibt den Namen der Anwendung.|  
|stoptrace|Beenden Sie die Ablaufverfolgung aus, wenn sie nicht vor dem beendet wurde.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="BKMK_Examples"></a>Beispiele für  
Aktivieren der Ablaufverfolgung, und speichern Sie die Ablaufverfolgungsdatei **sxstrace.etl**:  
```  
sxstrace trace /logfile:sxstrace.etl  
```  
Die unformatierten Ablaufverfolgungsdatei in einem vom Menschen lesbaren Format übersetzen, und Speichern des Ergebnisses, **sxstrace.txt**:  
```  
sxstrace parse /logfile:sxstrace.etl /outfile:sxstrace.txt  
```  

## <a name="additional-references"></a>Weitere Verweise  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
  
