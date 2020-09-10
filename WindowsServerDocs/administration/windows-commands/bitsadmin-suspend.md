---
title: bitsadmin suspend
description: Referenz Artikel für den Befehl "bizadmin Suspend", der den angegebenen Auftrag anhält.
ms.topic: reference
ms.assetid: f9d42500-7bea-4aa8-a9f0-c22f6ed3e73b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0827f7fe42a41d981c165e41b1a8af71ec5d7472
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630595"
---
# <a name="bitsadmin-suspend"></a>bitsadmin suspend

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hält den angegebenen Auftrag an. Wenn Sie den Auftrag versehentlich angehalten haben, können Sie den Auftrag mit dem Umschalter [bigsadmin Resume](bitsadmin-resume.md) neu starten.

## <a name="syntax"></a>Syntax

```
bitsadmin /suspend <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
