---
title: FTP-Binärdatei
description: Windows-Befehls Thema für FTP-Binärdatei
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 48579523f44232dec3357a20e8082050cc5175e6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376580"
---
# <a name="ftp-binary"></a>FTP: binär

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt den Datei Übertragungstyp auf Binary fest.   
## <a name="syntax"></a>Syntax  
```  
binary  
```  
### <a name="parameters"></a>Parameter  
none  
## <a name="remarks-optional-section"></a>Hinweise <optional section>  
**FTP** unterstützt sowohl ASCII-als auch binäre Bilddatei-Übertragungs Typen. Verwenden Sie Binärdateien beim Übertragen von ausführbaren Dateien. Im Binärmodus werden Dateien in 1-Byte-Einheiten übertragen. Weitere Informationen zum Übertragen von ASCII-Dateien finden Sie unter **FTP: ASCII** in additional References.  
## <a name="BKMK_Examples"></a>Beispiele  
Legen Sie den Datei Übertragungstyp auf Binär fest.  
```  
binary  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [FTP: ASCII](ftp-ascii.md)  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
