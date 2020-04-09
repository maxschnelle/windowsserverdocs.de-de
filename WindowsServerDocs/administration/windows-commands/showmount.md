---
title: showmount
description: Windows-Befehls Thema für showmount, das bereitgestellte Verzeichnisse anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a6dd562e-e3bd-4ee6-be3b-6d29e29fd20e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6fa61d47bb14cf21d93beec0a6e9257b9f66737b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834223"
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