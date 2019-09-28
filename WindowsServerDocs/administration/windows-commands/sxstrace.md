---
title: sxstrace
description: Erfahren Sie, wie Sie parallele Probleme diagnostizieren können.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 66326943bf1b056951ae5824df5a4f60892492cb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370713"
---
# <a name="sxstrace"></a>sxstrace

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Diagnostizieren paralleler Probleme    

## <a name="syntax"></a>Syntax  
```  
sxstrace [{[trace -logfile:<FileName> [-nostop]|[parse -logfile:<FileName> -outfile:<ParsedFile>  [-filter:<AppName>]}]  
```  

### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|Ablauf Verfolgungs|Aktiviert die Ablauf Verfolgung für SxS (Seite an Seite).|  
|-Logfile|Gibt die unformatierte Protokolldatei an.|  
|\<Dateiname >|Speichert das Ablauf Verfolgungs Protokoll in *filename*.|  
|-nostoppt|Gibt keine Aufforderung zum Abbrechen der Ablauf Verfolgung an.|  
|Analysieren|Übersetzt die RAW-Ablauf Verfolgungs Datei.|  
|-outfile|Gibt den Ausgabe Dateinamen an.|  
|\<> Für das von Dateien|Gibt den Dateinamen der analysierten Datei an.|  
|-Filter|Ermöglicht das Filtern der Ausgabe.|  
|\<AppName->|Gibt den Namen der Anwendung an.|  
|stoptrace|Beenden Sie die Ablauf Verfolgung, wenn Sie noch nicht beendet wurde.|  
|-?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="BKMK_Examples"></a>Beispiele  
Aktivieren Sie die Ablauf Verfolgung, und speichern Sie die Ablauf Verfolgungs Datei in **sxstrace. ETL**:  
```  
sxstrace trace -logfile:sxstrace.etl  
```  
Übersetzen Sie die unformatierte Ablauf Verfolgungs Datei in ein lesbares Format, und speichern Sie das Ergebnis in **sxstrace. txt**:  
```  
sxstrace parse -logfile:sxstrace.etl -outfile:sxstrace.txt  
```  

## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
