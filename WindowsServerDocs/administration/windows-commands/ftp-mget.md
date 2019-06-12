---
title: FTP-mget
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6c85ae96-ec51-48a9-a227-7f02c7332c69 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e43bf8b6e7067a31b3ec51336b0b43845ab88f63
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438600"
---
# <a name="ftp-mget"></a>ftp: mget

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Kopiert die Remotedateien auf dem lokalen Computer mithilfe der aktuellen Datei Übertragungstyp auswählen.   
## <a name="syntax"></a>Syntax  
```  
mget <remoteFile>[ ]  
```  
### <a name="parameters"></a>Parameter  

|  Parameter   |                        Beschreibung                        |
|--------------|-----------------------------------------------------------|
| <remoteFile> | Gibt an, die Remotedateien auf dem lokalen Computer kopiert. |

## <a name="BKMK_Examples"></a>Beispiele für  
Kopieren Sie Remotedateien **a.exe** und **b.exe** auf dem lokalen Computer, die den aktuellen Dateityp für die Übertragung verwenden.  
```  
mget a.exe b.exe  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [ftp: ascii](ftp-ascii.md)  
-   [FTP: binär](ftp-binary.md)  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
