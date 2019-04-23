---
title: nfsstat
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 9db8b903d4c3681b2b3bae3424f8af83696ae2c7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853291"
---
# <a name="nfsstat"></a>nfsstat



Sie können **Nfsstat** zum Anzeigen oder Zurücksetzen der Anzahl der Aufrufe, die an den Server für NFS.

## <a name="syntax"></a>Syntax

```
nfsstat [-z]
```

## <a name="description"></a>Beschreibung

Bei der Verwendung ohne die **- Z** -Option der **Nfsstat** Befehlszeilen-Hilfsprogramm zeigt die Anzahl der NFS-V2 und NFS V3 Mount-V3-Aufrufe, die auf dem Server vorgenommen werden, da die Leistungsindikatoren auf 0 (null) festgelegt wurden Wenn entweder den Dienst gestartet, oder wenn die Indikatoren zurückgesetzt wurden mithilfe von **Nfsstat - Z**.