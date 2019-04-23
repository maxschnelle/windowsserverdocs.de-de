---
title: FTP-dir
description: Windows-Befehle-Thema für FTP-dir
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a29a92a5-7b79-4e6e-95cf-2ccb38bb6fb2 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 78ac8ac5e9fc4894f55401bb234aa98de981adf7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835251"
---
# <a name="ftp-dir"></a>FTP: Dir

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt eine Liste der Dateien und Unterverzeichnisse auf einem Remotecomputer befindet.   
## <a name="syntax"></a>Syntax  
```  
dir [<remotedirectory>] [<LocalFile>]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|[<remotedirectory>]|Gibt das Verzeichnis für das eine Liste angezeigt werden sollen. Wenn kein Verzeichnis angegeben ist, wird das aktuelle Arbeitsverzeichnis auf dem Remotecomputer verwendet.|  
|[<LocalFile>]|Gibt eine lokale Datei in dem Sie die Verzeichnisliste zu speichern. Wenn eine lokale Datei nicht angegeben ist, werden die Ergebnisse auf dem Bildschirm angezeigt.|  
## <a name="BKMK_Examples"></a>Beispiele für  
Zeigt eine Verzeichnisliste für **dir1** auf dem Remotecomputer.  
```  
dir dir1  
```  
Speichern Sie eine Liste der im aktuellen Verzeichnis auf dem Remotecomputer in der lokalen Datei **Verliste.txt**.  
```  
dir . dirlist.txt  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
