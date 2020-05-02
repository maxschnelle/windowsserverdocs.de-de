---
title: FTP-ls_1
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5e03c7db-1e2b-419c-acb2-8a68f3db9615 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0dd661742288bdd43299f379f4eb04016b2ac799
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725240"
---
# <a name="ftp-ls_1"></a>FTP: ls_1

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
> 
> 
> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine abgekürzte Liste von Dateien und Unterverzeichnissen vom Remote Computer an.   
## <a name="syntax"></a>Syntax  
```  
ls [<remotedirectory>] [<LocalFile>]  
```  
#### <a name="parameters"></a>Parameter  

|      Parameter      |                                                                       BESCHREIBUNG                                                                        |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<remotedirectory>] | Gibt das Verzeichnis an, für das eine Auflistung angezeigt werden soll. Wenn kein Verzeichnis angegeben ist, wird das aktuelle Arbeitsverzeichnis auf dem Remote Computer verwendet. |
|    [<LocalFile>]    |               Gibt eine lokale Datei an, in der die Auflistung gespeichert werden soll. Wenn keine lokale Datei angegeben wird, werden die Ergebnisse auf dem Bildschirm angezeigt.               |

## <a name="examples"></a>Beispiele  
Hiermit wird eine abgekürzte Liste von Dateien und Unterverzeichnissen vom Remote Computer angezeigt.  
```  
ls  
```  
Verschaffen Sie sich auf dem Remote Computer eine abgekürzte Verzeichnis Auflistung von **dir1** , und speichern Sie Sie in einer lokalen Datei namens **dirlist. txt.**  
```  
ls dir1 dirlist.txt   
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
