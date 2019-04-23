---
title: showmount
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a6dd562e-e3bd-4ee6-be3b-6d29e29fd20e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 26acf24922e6ac53a5c902d65eb0f23bff0af93b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852351"
---
# <a name="showmount"></a>showmount

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sie können **Showmount** bereitgestellten Verzeichnisse angezeigt.  
  
## <a name="syntax"></a>Syntax  
```
showmount {-e|-a|-d} <Server>  
```

## <a name="description"></a>Beschreibung  
Die **Showmount** Befehl\-Befehlszeilen-Hilfsprogramm zeigt Informationen zu bereitgestellten Dateisystemen, die auf dem Computer, die anhand des vom Server für NFS exportiert *Server*. Wenn *Server* nicht angegeben wird, **Showmount** zeigt Informationen über den Computer, auf dem die **Showmount** ausgeführt wird.  
  
Sie müssen eine der folgenden Optionen angeben:  
  
- **\-e** -zeigt alle Dateisysteme, die auf dem Server exportiert.  
- **\-eine** -zeigt alle Network File System \(NFS\) Clients und die Verzeichnisse auf dem Server, die jeweils bereitgestellt wurde.  
- **\-d** -zeigt alle Verzeichnisse auf dem Server, der derzeit von NFS-Clients bereitgestellt werden.  
  
## <a name="see-also"></a>Siehe auch  
[Dienste für Network File System-Befehlsreferenz](services-for-network-file-system-command-reference.md)  