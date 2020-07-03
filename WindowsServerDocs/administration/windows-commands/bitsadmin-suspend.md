---
title: bitsadmin suspend
description: Referenz Artikel für den Befehl "bizadmin Suspend", der den angegebenen Auftrag anhält.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f9d42500-7bea-4aa8-a9f0-c22f6ed3e73b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 42257d31dbada2badc12b44b6375702ac41a91ca
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927472"
---
# <a name="bitsadmin-suspend"></a>bitsadmin suspend

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hält den angegebenen Auftrag an. Wenn Sie den Auftrag versehentlich angehalten haben, können Sie den Auftrag mit dem Umschalter [bigsadmin Resume](bitsadmin-resume.md) neu starten.

## <a name="syntax"></a>Syntax

```
bitsadmin /suspend <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ---------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="example"></a>Beispiel

So brechen Sie den Auftrag mit dem Namen *mydownloadjob*ab:


```
bitsadmin /suspend myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "biout admin Resume"](bitsadmin-resume.md)

- [Bider admin-Befehl](bitsadmin.md)
