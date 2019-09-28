---
title: FTP-ls_1
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e03c7db-1e2b-419c-acb2-8a68f3db9615 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d183f6a014273b78befd14c8d3208508948ffc54
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376253"
---
# <a name="ftp-ls_1"></a>FTP: ls_1

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
> 
> 
> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine abgekürzte Liste von Dateien und Unterverzeichnissen vom Remote Computer an.   
## <a name="syntax"></a>Syntax  
```  
ls [<remotedirectory>] [<LocalFile>]  
```  
### <a name="parameters"></a>Parameter  

|      Parameter      |                                                                       Beschreibung                                                                        |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<remotedirectory>] | Gibt das Verzeichnis an, für das eine Auflistung angezeigt werden soll. Wenn kein Verzeichnis angegeben ist, wird das aktuelle Arbeitsverzeichnis auf dem Remote Computer verwendet. |
|    [<LocalFile>]    |               Gibt eine lokale Datei an, in der die Auflistung gespeichert werden soll. Wenn keine lokale Datei angegeben wird, werden die Ergebnisse auf dem Bildschirm angezeigt.               |

## <a name="BKMK_Examples"></a>Beispiele  
Hiermit wird eine abgekürzte Liste von Dateien und Unterverzeichnissen vom Remote Computer angezeigt.  
```  
ls  
```  
Verschaffen Sie sich auf dem Remote Computer eine abgekürzte Verzeichnis Auflistung von **dir1** , und speichern Sie Sie in einer lokalen Datei namens **dirlist. txt.**  
```  
ls dir1 dirlist.txt   
```  
## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
