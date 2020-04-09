---
title: irftp
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e15c60a7-546d-4e9f-9871-43aaa1b569d6 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 28cf722a5e630cb05b0348ebf2d4f582217b5497
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841983"
---
# <a name="irftp"></a>irftp

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet Dateien über einen Infrarot Link.    
## <a name="syntax"></a>Syntax  
```  
irftp [<Drive>:\] [[<path>] <FileName>] [/h][/s]  
```  

#### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|Laufwerk:\|gibt das Laufwerk an, das die Dateien enthält, die über einen Infrarot Link gesendet werden sollen.|  
|ADS Einfügen|Gibt den Speicherort und den Namen der Datei oder des Satzes von Dateien an, die über einen Infrarot Link gesendet werden sollen. Wenn Sie einen Satz von Dateien angeben, müssen Sie den vollständigen Pfad für jede Datei angeben.|  
|/h|Gibt den verborgenen Modus an. Wenn der verborgene Modus verwendet wird, werden die Dateien gesendet, ohne dass das Dialogfeld drahtlos Verbindung angezeigt wird.|  
|/s|Öffnet das Dialogfeld drahtlos Verbindung, sodass Sie die Datei oder den Satz von Dateien, die Sie senden möchten, ohne die Befehlszeile zum Angeben von Laufwerk, Pfad und Dateinamen auswählen können.|  

## <a name="remarks"></a>Hinweise  
-   Vergewissern Sie sich vor der Verwendung dieses Befehls, dass die Geräte, für die Sie über eine Infrarot Verbindung kommunizieren möchten, über eine aktivierte und ordnungsgemäße Funktion verfügen und eine Infrarot Verbindung zwischen den Geräten hergestellt wird.  
-   Wenn Sie ohne Parameter verwendet oder mit **/s**verwendet wird **, wird das** Dialogfeld **drahtlos Verbindung** geöffnet, in dem Sie die Dateien, die Sie senden möchten, ohne die Befehlszeile auswählen können.  

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Senden Sie "example. txt" über den Infrarot Link.  
```  
irftp c:\example.txt  
```  

## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
