---
title: nfsstat
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da7a9768-44bd-404b-97ee-c388d00dc395
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4f9db119596b5602f18acfa10af6aa1b7cbbc9b2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373176"
---
# <a name="nfsstat"></a>nfsstat



Mit **nfsstat** können Sie die Anzahl der Aufrufe von Server für NFS anzeigen oder zurücksetzen.

## <a name="syntax"></a>Syntax

```
nfsstat [-z]
```

## <a name="description"></a>Beschreibung

Bei Verwendung ohne die Option **-z** zeigt das Befehlszeilen-Hilfsprogramm **nfsstat** die Anzahl der Aufrufe des NFS v2-, NFS V3-und Mount V3 an, seit die Zähler auf 0 festgelegt wurden, entweder wenn der Dienst gestartet wurde oder die Indikatoren mithilfe **von zurückgesetzt wurden. nfsstat-z**.