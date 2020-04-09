---
title: nfsstat
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da7a9768-44bd-404b-97ee-c388d00dc395
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 94eb389fdd694c08dcd1d77325f145a81e59ea0f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838883"
---
# <a name="nfsstat"></a>nfsstat



Mit **nfsstat** können Sie die Anzahl der Aufrufe von Server für NFS anzeigen oder zurücksetzen.

## <a name="syntax"></a>Syntax

```
nfsstat [-z]
```

## <a name="description"></a>Beschreibung

Bei Verwendung ohne die Option **-z** zeigt das Befehlszeilen-Hilfsprogramm **nfsstat** die Anzahl der Aufrufe des NFS v2-, NFS V3-und Mount V3 an, seit die Zähler auf 0 festgelegt wurden, entweder wenn der Dienst gestartet wurde oder die Indikatoren mithilfe von **nfsstat-z**zurückgesetzt wurden.