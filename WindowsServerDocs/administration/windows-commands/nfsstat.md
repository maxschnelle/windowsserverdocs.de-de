---
title: nfsstat
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da7a9768-44bd-404b-97ee-c388d00dc395
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e2c02fdfeb9923993a1d4471862a6c8487c9d86
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723751"
---
# <a name="nfsstat"></a>nfsstat



Mit **nfsstat** können Sie die Anzahl der Aufrufe von Server für NFS anzeigen oder zurücksetzen.

## <a name="syntax"></a>Syntax

```
nfsstat [-z]
```

## <a name="description"></a>BESCHREIBUNG

Bei Verwendung ohne die Option **-z** zeigt das Befehlszeilen-Hilfsprogramm **nfsstat** die Anzahl der Aufrufe des NFS v2-, NFS V3-und Mount V3 an, seit die Zähler auf 0 festgelegt wurden, entweder wenn der Dienst gestartet wurde oder die Indikatoren mithilfe von **nfsstat-z**zurückgesetzt wurden.