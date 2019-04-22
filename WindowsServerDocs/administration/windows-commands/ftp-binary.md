---
title: binäre FTP
description: Windows-Befehle-Thema für FTP-Binärdatei
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ee925b4d-85d2-47b1-b7d6-3832b7ec5505 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cadd59bff3bd2acf5c6d700caef66ca5c871b523
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821921"
---
# <a name="ftp-binary"></a>FTP: binär

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Legt den Dateiübertragungstyp in einen Binärwert.   
## <a name="syntax"></a>Syntax  
```  
binary  
```  
### <a name="parameters"></a>Parameter  
none  
## <a name="remarks-optional-section"></a>"Hinweise" <optional section>  
**FTP** unterstützt sowohl ASCII-als auch binäre Übertragung für Bilddateitypen. Verwenden Sie Binary, bei der Übertragung von ausführbarer Dateien. In diesem Modus werden die Dateien in ein-Byte-Einheiten übertragen. Weitere Informationen zur Übertragung von ASCII-Dateien finden Sie unter **ftp: Ascii** in zusätzliche Verweise.  
## <a name="BKMK_Examples"></a>Beispiele für  
Legen Sie den Dateityp für die Übertragung in das Binärformat.  
```  
binary  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [ftp: ascii](ftp-ascii.md)  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
