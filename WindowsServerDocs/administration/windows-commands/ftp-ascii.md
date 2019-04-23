---
title: ftp-ascii
description: 'Windows-Befehle-Thema für den ftp-ascii '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 523be48e-eab0-4237-8fb5-ca222824f0b6 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b7bcca3f29cec8ff5c30256dfd123acc7fbb804d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849191"
---
# <a name="ftp-ascii"></a>ftp: ascii

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Legt den Dateiübertragungstyp auf ASCII fest.   
## <a name="syntax"></a>Syntax  
```  
ascii  
```  
### <a name="parameters"></a>Parameter  
none  
## <a name="remarks"></a>Hinweise  
-   Der Standardtyp ist ASCII.  
-   Im ASCII-Modus werden zeichenkonvertierungen in und aus dem Netzwerk-standard-Zeichensatz ausgeführt. End-of-Line-Zeichen werden z. B. nach Bedarf konvertiert basierend auf dem Zielbetriebssystem bereit.  
-   **FTP** unterstützt sowohl ASCII-als auch binäre Übertragung für Bilddateitypen. Verwenden Sie ASCII aus, bei der Übertragung von Textdateien. Weitere Informationen zur Übertragung von binären Dateien finden Sie unter **ftp: binäre** in zusätzliche Verweise.  
## <a name="BKMK_Examples"></a>Beispiele für  
Den Dateityp für die Übertragung auf ASCII festgelegt.  
```  
ascii  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [FTP: binär](ftp-binary.md)  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
