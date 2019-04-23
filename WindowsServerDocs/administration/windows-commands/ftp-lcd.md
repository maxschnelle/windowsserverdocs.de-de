---
title: FTP-LCD-Anzeige
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60a25808-6abb-408b-8373-0bbdcd0994b4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eac028c8aa675e680dedefcfe9f0b8da18ce7179
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826891"
---
# <a name="ftp-lcd"></a>ftp: lcd

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ändert das Arbeitsverzeichnis auf dem lokalen Computer. Das Arbeitsverzeichnis wird standardmäßig das Verzeichnis, in dem **ftp** wurde gestartet.   
## <a name="syntax"></a>Syntax  
```  
lcd [<directory>]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|[<directory>]|Gibt das Verzeichnis auf dem lokalen Computer, um zu ändern. Wenn *Directory* nicht angegeben ist, wird das aktuelle Arbeitsverzeichnis in das Standardverzeichnis geändert wird.|  
## <a name="BKMK_Examples"></a>Beispiele für  
Ändern Sie das Arbeitsverzeichnis auf dem lokalen Computer **C:\dir1**  
```  
lcd C:\dir1  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
