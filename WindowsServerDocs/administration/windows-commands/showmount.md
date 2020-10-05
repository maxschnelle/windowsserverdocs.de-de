---
title: showmount
description: Referenz Artikel für den Befehl showmount, der Informationen zu bereitgestellten Dateisystemen anzeigt, die vom Server für NFS auf einem angegebenen Computer exportiert wurden.
ms.topic: reference
ms.assetid: a6dd562e-e3bd-4ee6-be3b-6d29e29fd20e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3af87ba4ed42789cf07a2ae63ce9e720043a196e
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91718327"
---
# <a name="showmount"></a>showmount

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mit **showmount** können Sie Informationen zu bereitgestellten Dateisystemen anzeigen, die vom Server für NFS auf einem angegebenen Computer exportiert wurden. Wenn Sie keinen Server angeben, werden mit diesem Befehl Informationen zu dem Computer angezeigt, auf dem der **showmount** -Befehl ausgeführt wird.

## <a name="syntax"></a>Syntax

```
showmount {-e|-a|-d} <server>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -E | Zeigt alle auf dem Server exportierten Dateisysteme an. |
| -a | Zeigt alle NFS-Clients (Network File System) und die Verzeichnisse auf dem Server an, die jeweils bereitgestellt wurden. |
| -d | Zeigt alle Verzeichnisse auf dem Server an, die zurzeit von NFS-Clients bereitgestellt werden. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Dienste für Network File System-Befehlsreferenz](services-for-network-file-system-command-reference.md)