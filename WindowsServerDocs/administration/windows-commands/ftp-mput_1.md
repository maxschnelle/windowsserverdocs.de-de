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
ms.openlocfilehash: 99b938618deb2d1e779fd20c504c01a13a2d3f8a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868161"
---
# <a name="ftp-mput1"></a>FTP: mput_1

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Lokale Dateien auf dem Remotecomputer über die aktuelle Datei kopiert Übertragungstyp auswählen.   
## <a name="syntax"></a>Syntax  
```  
mput <LocalFile>[ ]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|<LocalFile>|Gibt an, die lokale Datei auf den Remotecomputer kopiert.|  
## <a name="BKMK_Examples"></a>Beispiele für  
Kopie **Program1.exe** und **Program2.exe** an den Remotecomputer, der den aktuellen Dateityp für die Übertragung verwenden.  
```  
mput Program1.exe Program2.exe  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [ftp: ascii](ftp-ascii.md)  
-   [FTP: binär](ftp-binary.md)  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
