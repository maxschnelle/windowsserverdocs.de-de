---
title: irftp
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e15c60a7-546d-4e9f-9871-43aaa1b569d6 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 34f912878b97bd00fb1c4ea539c7ea4c1423ea59
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724816"
---
# <a name="irftp"></a>irftp

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet Dateien über einen Infrarot Link.    
## <a name="syntax"></a>Syntax  
```  
irftp [<Drive>:\] [[<path>] <FileName>] [/h][/s]  
```  

#### <a name="parameters"></a>Parameter  
|Parameter|BESCHREIBUNG|  
|-------|--------|  
|Laufwerk:\|gibt das Laufwerk an, das die Dateien enthält, die über einen Infrarot Link gesendet werden sollen.|  
|ADS Einfügen|Gibt den Speicherort und den Namen der Datei oder des Satzes von Dateien an, die über einen Infrarot Link gesendet werden sollen. Wenn Sie einen Satz von Dateien angeben, müssen Sie den vollständigen Pfad für jede Datei angeben.|  
|/h|Gibt den verborgenen Modus an. Wenn der verborgene Modus verwendet wird, werden die Dateien gesendet, ohne dass das Dialogfeld drahtlos Verbindung angezeigt wird.|  
|/s|Öffnet das Dialogfeld drahtlos Verbindung, sodass Sie die Datei oder den Satz von Dateien, die Sie senden möchten, ohne die Befehlszeile zum Angeben von Laufwerk, Pfad und Dateinamen auswählen können.|  

## <a name="remarks"></a>Bemerkungen  
-   Vergewissern Sie sich vor der Verwendung dieses Befehls, dass die Geräte, für die Sie über eine Infrarot Verbindung kommunizieren möchten, über eine aktivierte und ordnungsgemäße Funktion verfügen und eine Infrarot Verbindung zwischen den Geräten hergestellt wird.  
-   Wenn Sie ohne Parameter verwendet oder mit **/s**verwendet wird **, wird das** Dialogfeld **drahtlos Verbindung** geöffnet, in dem Sie die Dateien, die Sie senden möchten, ohne die Befehlszeile auswählen können.  

## <a name="examples"></a>Beispiele  
Senden Sie "example. txt" über den Infrarot Link.  
```  
irftp c:\example.txt  
```  

## <a name="additional-references"></a>Zusätzliche Referenzen  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
