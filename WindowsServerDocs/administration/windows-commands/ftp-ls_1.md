---
title: FTP-ls_1
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5e03c7db-1e2b-419c-acb2-8a68f3db9615 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5ff63272fe3c5e59965b04bef258a06fee2da0c4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843363"
---
# <a name="ftp-ls_1"></a>FTP: ls_1

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
> 
> 
> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine abgekürzte Liste von Dateien und Unterverzeichnissen vom Remote Computer an.   
## <a name="syntax"></a>Syntax  
```  
ls [<remotedirectory>] [<LocalFile>]  
```  
#### <a name="parameters"></a>Parameter  

|      Parameter      |                                                                       Beschreibung                                                                        |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<remotedirectory>] | Gibt das Verzeichnis an, für das eine Auflistung angezeigt werden soll. Wenn kein Verzeichnis angegeben ist, wird das aktuelle Arbeitsverzeichnis auf dem Remote Computer verwendet. |
|    [<LocalFile>]    |               Gibt eine lokale Datei an, in der die Auflistung gespeichert werden soll. Wenn keine lokale Datei angegeben wird, werden die Ergebnisse auf dem Bildschirm angezeigt.               |

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Hiermit wird eine abgekürzte Liste von Dateien und Unterverzeichnissen vom Remote Computer angezeigt.  
```  
ls  
```  
Verschaffen Sie sich auf dem Remote Computer eine abgekürzte Verzeichnis Auflistung von **dir1** , und speichern Sie Sie in einer lokalen Datei namens **dirlist. txt.**  
```  
ls dir1 dirlist.txt   
```  
## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
