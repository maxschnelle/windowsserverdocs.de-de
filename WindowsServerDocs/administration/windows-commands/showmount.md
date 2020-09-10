---
title: showmount
description: Referenz Artikel zu showmount, in dem eingebundene Verzeichnisse angezeigt werden.
ms.topic: reference
ms.assetid: a6dd562e-e3bd-4ee6-be3b-6d29e29fd20e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e0a03c7e08c80e4cf0b99bbcb74aeff1deccdb1e
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640953"
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