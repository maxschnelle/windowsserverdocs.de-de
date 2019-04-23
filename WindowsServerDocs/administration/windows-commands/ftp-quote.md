---
title: FTP-Angebot
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4500a1d3-c091-42c7-a909-f61df7f2e993 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0b1aaf9eadfd9c51048ad41106ce6532f6f9588b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865881"
---
# <a name="ftp-quote"></a>FTP: Anführungszeichen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sendet wörtliche Argumente an den remote-ftp-Server an. Es wird ein einzelnes FTP-Antwortcode zurückgegeben.   
## <a name="syntax"></a>Syntax  
```  
quote <Argument>[ ]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|<Argument>|Gibt das Argument an den ftp-Server senden.|  
## <a name="remarks"></a>Hinweise  
Die **Anführungszeichen** Befehl ist identisch mit der **literal** Befehl.  
## <a name="BKMK_Examples"></a>Beispiele für  
Senden einer **beenden** Befehl zum remote-ftp-Server.  
```  
quote quit  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [FTP: literal_1](ftp-literal_1.md)  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
