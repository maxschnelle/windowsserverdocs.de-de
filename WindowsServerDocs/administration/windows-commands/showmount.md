---
title: showmount
description: Referenz Artikel zu showmount, in dem eingebundene Verzeichnisse angezeigt werden.
ms.topic: article
ms.assetid: a6dd562e-e3bd-4ee6-be3b-6d29e29fd20e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0be623eadd56a55a87f2df57fec9b4c6558770c9
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882401"
---
# <a name="showmount"></a>showmount

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie können " **showmount** " verwenden, um eingebundene Verzeichnisse anzuzeigen.

## <a name="syntax"></a>Syntax
```
showmount {-e|-a|-d} <Server>
```

## <a name="description"></a>BESCHREIBUNG
Das Befehlszeilen-Hilfsprogramm **showmount** \- zeigt Informationen zu bereitgestellten Dateisystemen an, die vom Server für NFS auf dem vom *Server*angegebenen Computer exportiert wurden. Wenn kein *Server* bereitgestellt wird, zeigt **showmount** Informationen zu dem Computer an, auf dem der Befehl **showmount** ausgeführt wird.

Sie müssen eine der folgenden Optionen angeben:

- ** \- e** -zeigt alle auf dem Server exportierten Dateisysteme an.
- ** \- a** : zeigt alle Network File System- \( NFS- \) Clients und die Verzeichnisse auf dem Server an, die jeweils bereitgestellt wurden.
- ** \- d** -zeigt alle Verzeichnisse auf dem Server an, die zurzeit von NFS-Clients bereitgestellt werden.

## <a name="see-also"></a>Weitere Informationen
[Dienste für Network File System-Befehlsreferenz](services-for-network-file-system-command-reference.md)