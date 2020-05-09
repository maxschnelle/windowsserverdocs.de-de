---
title: diskperf
description: Referenz Thema für den diskperf-Befehl, der verwendet werden kann, um Leistungsindikatoren für physische oder logische Datenträger auf Windows-Computern Remote zu aktivieren bzw. zu deaktivieren.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f06916e8-069b-4ec8-a6eb-59f1d9f77111
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 092518f414d6e27436c46ffd6f9f15b6e6c0407e
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2020
ms.locfileid: "82992426"
---
# <a name="diskperf"></a>diskperf

Der **diskperf** -Befehl aktiviert oder deaktiviert die Leistungsindikatoren physischer oder logischer Datenträger auf Computern, auf denen Windows ausgeführt wird.

## <a name="syntax"></a>Syntax

```
diskperf [-y[d|v] | -n[d|v]] [\\computername]
```

## <a name="options"></a>Optionen

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
