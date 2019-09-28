---
title: irftp
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: ad8a0b9b49d90223f830081f5a99c40995d9e4ef
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375361"
---
# <a name="irftp"></a>irftp

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet Dateien über einen Infrarot Link.    
## <a name="syntax"></a>Syntax  
```  
irftp [<Drive>:\] [[<path>] <FileName>] [/h][/s]  
```  

### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|Laufwerk: \|gibt das Laufwerk an, das die Dateien enthält, die über einen Infrarot Link gesendet werden sollen.|  
|ADS Einfügen|Gibt den Speicherort und den Namen der Datei oder des Satzes von Dateien an, die über einen Infrarot Link gesendet werden sollen. Wenn Sie einen Satz von Dateien angeben, müssen Sie den vollständigen Pfad für jede Datei angeben.|  
|/h|Gibt den verborgenen Modus an. Wenn der verborgene Modus verwendet wird, werden die Dateien gesendet, ohne dass das Dialogfeld drahtlos Verbindung angezeigt wird.|  
|/s|Öffnet das Dialogfeld drahtlos Verbindung, sodass Sie die Datei oder den Satz von Dateien, die Sie senden möchten, ohne die Befehlszeile zum Angeben von Laufwerk, Pfad und Dateinamen auswählen können.|  

## <a name="remarks"></a>Hinweise  
-   Vergewissern Sie sich vor der Verwendung dieses Befehls, dass die Geräte, für die Sie über eine Infrarot Verbindung kommunizieren möchten, über eine aktivierte und ordnungsgemäße Funktion verfügen und eine Infrarot Verbindung zwischen den Geräten hergestellt wird.  
-   Wenn Sie ohne Parameter verwendet oder mit **/s**verwendet wird **, wird das** Dialogfeld **drahtlos Verbindung** geöffnet, in dem Sie die Dateien, die Sie senden möchten, ohne die Befehlszeile auswählen können.  

## <a name="BKMK_Examples"></a>Beispiele  
Senden Sie "example. txt" über den Infrarot Link.  
```  
irftp c:\example.txt  
```  

## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
