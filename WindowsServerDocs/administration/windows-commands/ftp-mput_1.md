---
title: FTP-mput_1
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 980f15e7-7cf1-4813-9946-a8cc4edfb198 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dd19a97246aa6155182cb055deceb4b5a5019f6c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438583"
---
# <a name="ftp-mput1"></a>FTP: mput_1

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Lokale Dateien auf dem Remotecomputer über die aktuelle Datei kopiert Übertragungstyp auswählen.   
## <a name="syntax"></a>Syntax  
```  
mput <LocalFile>[ ]  
```  
### <a name="parameters"></a>Parameter  

|  Parameter  |                       Beschreibung                        |
|-------------|----------------------------------------------------------|
| <LocalFile> | Gibt an, die lokale Datei auf den Remotecomputer kopiert. |

## <a name="BKMK_Examples"></a>Beispiele für  
Kopie **Program1.exe** und **Program2.exe** an den Remotecomputer, der den aktuellen Dateityp für die Übertragung verwenden.  
```  
mput Program1.exe Program2.exe  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [ftp: ascii](ftp-ascii.md)  
-   [FTP: binär](ftp-binary.md)  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
