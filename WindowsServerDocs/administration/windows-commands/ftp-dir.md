---
title: FTP-Verzeichnis
description: Windows-Befehls Thema für FTP-dir
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a29a92a5-7b79-4e6e-95cf-2ccb38bb6fb2 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 64f227ea9806f169c2df1698382cfce6e7ac3257
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843573"
---
# <a name="ftp-dir"></a>FTP: dir

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine Liste der Verzeichnis Dateien und Unterverzeichnisse auf einem Remote Computer an.   
## <a name="syntax"></a>Syntax  
```  
dir [<remotedirectory>] [<LocalFile>]  
```  
#### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|[<remotedirectory>]|Gibt das Verzeichnis an, für das eine Auflistung angezeigt werden soll. Wenn kein Verzeichnis angegeben ist, wird das aktuelle Arbeitsverzeichnis auf dem Remote Computer verwendet.|  
|[<LocalFile>]|Gibt eine lokale Datei an, in der die Verzeichnis Auflistung gespeichert werden soll. Wenn keine lokale Datei angegeben wird, werden die Ergebnisse auf dem Bildschirm angezeigt.|  
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Zeigen Sie eine Verzeichnis Auflistung für **dir1** auf dem Remote Computer an.  
```  
dir dir1  
```  
Speichern Sie eine Liste mit dem aktuellen Verzeichnis auf dem Remote Computer in der lokalen Datei " **dirlist. txt**".  
```  
dir . dirlist.txt  
```  
## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
