---
title: FTP-mdelete_1
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9390f8e5b0bded92a553b3057d122dace3fc665a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851611"
---
# <a name="ftp-mdelete1"></a>ftp: mdelete_1

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Löscht Dateien auf dem Remotecomputer.   
## <a name="syntax"></a>Syntax  
```  
mdelete <remoteFile>[ ]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|<remoteFile>|Gibt an, der remote-Datei zu löschen.|  
## <a name="BKMK_Examples"></a>Beispiele für  
Remotedateien löschen **a.exe** und **b.exe**.  
```  
mdelete a.exe b.exe  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
