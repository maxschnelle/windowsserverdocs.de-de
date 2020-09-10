---
title: diskperf
description: Referenz Artikel für den diskperf-Befehl, der verwendet werden kann, um Leistungsindikatoren für physische oder logische Datenträger auf Windows-Computern Remote zu aktivieren oder zu deaktivieren.
ms.topic: reference
ms.assetid: f06916e8-069b-4ec8-a6eb-59f1d9f77111
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f0e7700b3fbe1cec79aa9cf2b5c93eab9bd8372d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624814"
---
# <a name="diskperf"></a>diskperf

Der **diskperf** -Befehl aktiviert oder deaktiviert die Leistungsindikatoren physischer oder logischer Datenträger auf Computern, auf denen Windows ausgeführt wird.

## <a name="syntax"></a>Syntax

```
diskperf [-y[d|v] | -n[d|v]] [\\computername]
```

## <a name="options"></a>Tastatur

| Option | BESCHREIBUNG |
| ------ | ----------- |
| -y | Startet alle Datenträger Leistungsindikatoren, wenn der Computer neu gestartet wird. |
| -Yd | Aktiviert Datenträger-Leistungsindikatoren für physische Laufwerke, wenn der Computer neu gestartet wird. |
| -YV | Aktiviert Datenträger-Leistungsindikatoren für logische Laufwerke oder Speichervolumes, wenn der Computer neu gestartet wird. |
| -n | Deaktiviert alle Leistungsindikatoren für Datenträger, wenn der Computer neu gestartet wird. |
| -ND | Deaktivieren Sie die Datenträger Leistungsindikatoren für physische Laufwerke, wenn der Computer neu gestartet wird. |
| -NV | Deaktivieren Sie die Datenträger Leistungsindikatoren für logische Laufwerke oder Speichervolumes, wenn der Computer neu gestartet wird. |
| `\\<computername>` | Gibt den Namen des Computers an, auf dem Sie die Datenträger-Leistungsindikatoren aktivieren bzw. deaktivieren möchten. |
| -? | Zeigt kontextabhängige Hilfe an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
