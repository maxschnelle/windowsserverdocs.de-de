---
title: irftp
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e15c60a7-546d-4e9f-9871-43aaa1b569d6 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d469270b744a9de881efd9b0cfa6f1105f70519a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848421"
---
# <a name="irftp"></a>irftp

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sendet Dateien über eine infrarote Verbindung.    
## <a name="syntax"></a>Syntax  
```  
irftp [<Drive>:\] [[<path>] <FileName>] [/h][/s]  
```  

### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|Laufwerk:\|gibt an, das Laufwerk, das Dateien enthält, die über eine infrarotverbindung gesendet werden sollen.|  
|[path]FileName|Gibt den Speicherort und Namen der Datei oder den Satz von Dateien, die über eine infrarotverbindung gesendet werden sollen. Wenn Sie einen Satz von Dateien angeben, müssen Sie den vollständigen Pfad für jede Datei angeben.|  
|/h|Gibt die ausgeblendeten Modus an. Wenn ausgeblendeten Modus verwendet wird, werden die Dateien gesendet, ohne das Dialogfeld für die drahtlose Verbindung anzuzeigen.|  
|/s|Wird das Dialogfeld drahtlose Verbindung geöffnet, sodass Sie auswählen können, die Datei oder einer Gruppe von Dateien, die Sie senden, ohne über die Befehlszeile auf dem Laufwerk, Pfad und Dateinamen angeben möchten.|  

## <a name="remarks"></a>Hinweise  
-   Stellen Sie sicher, dass die Geräte, die Sie über eine infrarotverbindung kommunizieren möchten Infrarot-Funktionalität aktiviert und ordnungsgemäß funktioniert, und dass eine infrarotverbindung zwischen den Geräten hergestellt wird, bevor Sie mit diesem Befehl.  
-   Ohne Parameter oder mit verwendet **/s**, **Irftp** öffnet die **drahtlose Verbindung** Dialogfeld, in dem Sie die Dateien, die zu senden, ohne über die Befehlszeile auswählen können.  

## <a name="BKMK_Examples"></a>Beispiele für  
Senden Sie Example.txt, über die infrarote Verbindung.  
```  
irftp c:\example.txt  
```  

## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
