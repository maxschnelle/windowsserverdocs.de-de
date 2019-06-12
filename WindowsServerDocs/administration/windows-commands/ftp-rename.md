---
title: FTP-umbenennen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 80d1a15f038017444c7654a44748bfd22be8e487
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438378"
---
# <a name="ftp-rename"></a>FTP: Umbenennen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Benennt die Remotedateien.   
## <a name="syntax"></a>Syntax  
```  
rename <FileName> <NewFileName>  
```  
### <a name="parameters"></a>Parameter  

|   Parameter   |                 Beschreibung                 |
|---------------|---------------------------------------------|
|  <FileName>   | Gibt die Datei, die Sie umbenennen möchten. |
| <NewFileName> |        Gibt den neuen Dateinamen an.         |

## <a name="BKMK_Examples"></a>Beispiele für  
Benennen Sie die Remotedatei **example.txt** zu **example1.txt**  
```  
rename example.txt example1.txt  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
