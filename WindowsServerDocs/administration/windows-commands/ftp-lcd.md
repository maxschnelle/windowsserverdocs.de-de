---
title: FTP-LCD
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 60a25808-6abb-408b-8373-0bbdcd0994b4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 646cbfe3feadb63388694218758dae165ffb49c4
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725265"
---
# <a name="ftp-lcd"></a>FTP: LCD

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ändert das Arbeitsverzeichnis auf dem lokalen Computer. Standardmäßig ist das Arbeitsverzeichnis das Verzeichnis, in dem **FTP** gestartet wurde.   
## <a name="syntax"></a>Syntax  
```  
lcd [<directory>]  
```  
#### <a name="parameters"></a>Parameter  
|Parameter|BESCHREIBUNG|  
|-------|--------|  
|[<directory>]|Gibt das Verzeichnis auf dem lokalen Computer an, in dem die Änderung vorgenommen werden soll. Wenn *Directory* nicht angegeben wird, wird das aktuelle Arbeitsverzeichnis in das Standardverzeichnis geändert.|  
## <a name="examples"></a>Beispiele  
Ändern Sie das Arbeitsverzeichnis auf dem lokalen Computer in **c:\dir1** .  
```  
lcd C:\dir1  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
