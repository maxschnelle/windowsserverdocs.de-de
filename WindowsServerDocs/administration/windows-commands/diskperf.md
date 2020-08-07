---
title: diskperf
description: Referenz Artikel für den diskperf-Befehl, der verwendet werden kann, um Leistungsindikatoren für physische oder logische Datenträger auf Windows-Computern Remote zu aktivieren oder zu deaktivieren.
ms.topic: article
ms.assetid: f06916e8-069b-4ec8-a6eb-59f1d9f77111
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 81cefe217abaa7b2d4ee843f3887076f66484422
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890867"
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
