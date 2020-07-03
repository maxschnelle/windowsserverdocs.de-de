---
title: diskperf
description: Referenz Artikel für den diskperf-Befehl, der verwendet werden kann, um Leistungsindikatoren für physische oder logische Datenträger auf Windows-Computern Remote zu aktivieren oder zu deaktivieren.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f06916e8-069b-4ec8-a6eb-59f1d9f77111
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e1e33844849993c6d5a9f9330264f31e52af3b29
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922810"
---
# <a name="diskperf"></a>diskperf

Der **diskperf** -Befehl aktiviert oder deaktiviert die Leistungsindikatoren physischer oder logischer Datenträger auf Computern, auf denen Windows ausgeführt wird.

## <a name="syntax"></a>Syntax

```
diskperf [-y[d|v] | -n[d|v]] [\\computername]
```

## <a name="options"></a>Optionen

| Option | Beschreibung |
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
