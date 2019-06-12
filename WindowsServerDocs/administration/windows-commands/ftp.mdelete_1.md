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
ms.openlocfilehash: 7b342f9d728e91085d5edf2f8e1ece00b48bec8d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438327"
---
# <a name="ftp-mdelete1"></a>ftp: mdelete_1

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Löscht Dateien auf dem Remotecomputer.   
## <a name="syntax"></a>Syntax  
```  
mdelete <remoteFile>[ ]  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |             Beschreibung              |
|--------------|--------------------------------------|
| <remoteFile> | Gibt an, der remote-Datei zu löschen. |

## <a name="BKMK_Examples"></a>Beispiele für  
Remotedateien löschen **a.exe** und **b.exe**.  
```  
mdelete a.exe b.exe  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
