---
title: FTP-literal_1
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fb81aa2d-07fa-4e79-bf44-1fb5526fdf14 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d50c6356dfa56a4a1c22c09b08dffc6b3a514c4a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879261"
---
# <a name="ftp-literal1"></a>FTP: literal_1

>Gilt für: Windows Server (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012-sendet wörtliche Argumente an den remote-ftp-Server. Es wird ein einzelnes FTP-Antwortcode zurückgegeben.   

## <a name="syntax"></a>Syntax  
```  
literal <Argument> [ ]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|<Argument>|Gibt das Argument an den ftp-Server senden.|  
## <a name="remarks"></a>Hinweise  
Die **literal** Befehl ist identisch mit der **Anführungszeichen** Befehl.  
## <a name="BKMK_Examples"></a>Beispiele für  
Senden einer **beenden** Befehl zum remote-ftp-Server.  
```  
literal quit  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [ftp: quote](ftp-quote.md)  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
