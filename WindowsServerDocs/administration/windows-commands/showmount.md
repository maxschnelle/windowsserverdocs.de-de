---
title: showmount
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: e1d197072db93130de880b5ec52d1875720b1d26
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383912"
---
# <a name="showmount"></a>showmount

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie können " **showmount** " verwenden, um eingebundene Verzeichnisse anzuzeigen.  
  
## <a name="syntax"></a>Syntax  
```
showmount {-e|-a|-d} <Server>  
```

## <a name="description"></a>Beschreibung  
Das\-Befehlszeilen-Hilfsprogramm " **showmount** " zeigt Informationen zu bereitgestellten Dateisystemen an, die vom Server für NFS auf dem vom *Server*angegebenen Computer exportiert wurden. Wenn kein *Server* bereitgestellt wird, zeigt **showmount** Informationen zu dem Computer an, auf dem der Befehl **showmount** ausgeführt wird.  
  
Sie müssen eine der folgenden Optionen angeben:  
  
- **\-e** -zeigt alle auf dem Server exportierten Dateisysteme an.  
- **\-a** : zeigt alle \(NFS-\) Clients und die Verzeichnisse auf dem Server an, die auf dem Server bereitgestellt wurden.  
- **\-d** : zeigt alle Verzeichnisse auf dem Server an, die zurzeit von NFS-Clients bereitgestellt werden.  
  
## <a name="see-also"></a>Weitere Informationen  
[Dienste für Network File System-Befehlsreferenz](services-for-network-file-system-command-reference.md)  