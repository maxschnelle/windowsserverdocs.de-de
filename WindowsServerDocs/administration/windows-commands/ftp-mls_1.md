---
title: ftp mls_1
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4738fd49-0e80-4bdf-a773-0f973db3a710 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6cf81018fa590d38e55778d60b0cb0e849ab83de
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835701"
---
# <a name="ftp-mls1"></a>ftp: mls_1

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt eine verkürzte Liste der Dateien und Unterverzeichnisse in einem Remoteverzeichnis.   
## <a name="syntax"></a>Syntax  
```  
mls <remoteFile>[ ] <LocalFile>  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|<remoteFile>|Gibt die Datei, die für die eine Liste angezeigt werden sollen.|  
|<LocalFile>|Gibt eine lokale Datei in dem die Auflistung gespeichert.|  
## <a name="remarks"></a>Hinweise  
-   Angeben von *Remotedateien*  
    Geben Sie einen Bindestrich (**-**) auf das aktuelle Arbeitsverzeichnis auf dem Remotecomputer zu verwenden.  
-   Angeben von *LocalFile*  
    Geben Sie einen Bindestrich (**-**) um die Auflistung auf dem Bildschirm anzuzeigen.  
## <a name="BKMK_Examples"></a>Beispiele für  
Anzeigen eine verkürzte Liste von Dateien und Unterverzeichnisse für **dir1** und **dir2**.  
```  
mls dir1 dir2 -  
```  
Speichern eine verkürzte Liste von Dateien und Unterverzeichnisse für **dir1** und **dir2** in der lokalen Datei **Verliste.txt**  
```  
mls dir1 dir2 dirlist.txt   
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
