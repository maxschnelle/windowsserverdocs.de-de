---
title: showmount
description: Referenz Artikel zu showmount, in dem eingebundene Verzeichnisse angezeigt werden.
ms.topic: reference
ms.assetid: a6dd562e-e3bd-4ee6-be3b-6d29e29fd20e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ba118e711af040bba7dd6c1e63a14405b3116743
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024794"
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