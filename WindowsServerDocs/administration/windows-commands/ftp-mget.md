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
ms.openlocfilehash: 1160ec742dde318141da720bd35b7d60ab805bb1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888421"
---
# <a name="ftp-mget"></a>ftp: mget

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Kopiert die Remotedateien auf dem lokalen Computer mithilfe der aktuellen Datei Übertragungstyp auswählen.   
## <a name="syntax"></a>Syntax  
```  
mget <remoteFile>[ ]  
```  
### <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|<remoteFile>|Gibt an, die Remotedateien auf dem lokalen Computer kopiert.|  
## <a name="BKMK_Examples"></a>Beispiele für  
Kopieren Sie Remotedateien **a.exe** und **b.exe** auf dem lokalen Computer, die den aktuellen Dateityp für die Übertragung verwenden.  
```  
mget a.exe b.exe  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [ftp: ascii](ftp-ascii.md)  
-   [FTP: binär](ftp-binary.md)  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
