---
title: FTP-löschen
description: Windows-Befehle-Thema zum Löschen von ftp
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 067c45f3-e4e8-4450-b8b6-836994f6adfe vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1c8af4beb83b789be1456d5556a0aa07749590fb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438726"
---
# <a name="ftp-delete"></a>FTP: Löschen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Löscht Dateien auf Remotecomputern.   
## <a name="syntax"></a>Syntax  
```  
delete <remoteFile>  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |          Beschreibung          |
|--------------|-------------------------------|
| <remoteFile> | Gibt die zu löschende Datei an. |

## <a name="BKMK_Examples"></a>Beispiele für  
Löschen Sie die Datei "Test.txt" auf dem Remotecomputer.  
```  
delete test.txt  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
