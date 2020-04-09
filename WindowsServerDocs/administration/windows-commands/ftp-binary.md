---
title: FTP-Binärdatei
description: Windows-Befehls Thema für FTP-Binärdatei
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ee925b4d-85d2-47b1-b7d6-3832b7ec5505 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 20b2f72517826576cfee643eda0c54063b162c94
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843723"
---
# <a name="ftp-binary"></a>FTP: binär

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt den Datei Übertragungstyp auf Binary fest.   
## <a name="syntax"></a>Syntax  
```  
binary  
```  
#### <a name="parameters"></a>Parameter  
none  
## <a name="remarks-optional-section"></a>Hinweise <optional section>  
**FTP** unterstützt sowohl ASCII-als auch binäre Bilddatei-Übertragungs Typen. Verwenden Sie Binärdateien beim Übertragen von ausführbaren Dateien. Im Binärmodus werden Dateien in 1-Byte-Einheiten übertragen. Weitere Informationen zum Übertragen von ASCII-Dateien finden Sie unter **FTP: ASCII** in additional References.  
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Legen Sie den Datei Übertragungstyp auf Binär fest.  
```  
binary  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [FTP: ASCII](ftp-ascii.md)  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
