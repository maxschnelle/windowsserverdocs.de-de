---
title: FTP-Verzeichnis
description: Windows-Befehls Thema für FTP-dir
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: c47971c52135d79ce62f935bfed981f6eefcecaa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376445"
---
# <a name="ftp-dir"></a>FTP: dir

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine Liste der Verzeichnis Dateien und Unterverzeichnisse auf einem Remote Computer an.   
## <a name="syntax"></a>Syntax  
```  
dir [<remotedirectory>] [<LocalFile>]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|[<remotedirectory>]|Gibt das Verzeichnis an, für das eine Auflistung angezeigt werden soll. Wenn kein Verzeichnis angegeben ist, wird das aktuelle Arbeitsverzeichnis auf dem Remote Computer verwendet.|  
|[<LocalFile>]|Gibt eine lokale Datei an, in der die Verzeichnis Auflistung gespeichert werden soll. Wenn keine lokale Datei angegeben wird, werden die Ergebnisse auf dem Bildschirm angezeigt.|  
## <a name="BKMK_Examples"></a>Beispiele  
Zeigen Sie eine Verzeichnis Auflistung für **dir1** auf dem Remote Computer an.  
```  
dir dir1  
```  
Speichern Sie eine Liste mit dem aktuellen Verzeichnis auf dem Remote Computer in der lokalen Datei " **dirlist. txt**".  
```  
dir . dirlist.txt  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
