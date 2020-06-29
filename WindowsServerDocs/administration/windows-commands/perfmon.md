---
title: perfmon
description: Referenz Thema für den Perfmon-Befehl, der den Windows-Zuverlässigkeits-und Leistungs Monitor in einem bestimmten eigenständigen Modus startet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9a8d5eca-8473-463e-a6e0-7bbd590b18e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/25/2018
ms.openlocfilehash: 96d1589dcd75814c37c2ad295cf60887eb07739c
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472476"
---
# <a name="perfmon"></a>perfmon

Starten Sie die Windows-Zuverlässigkeits-und Leistungsüberwachung in einem bestimmten eigenständigen Modus.

## <a name="syntax"></a>Syntax

```
perfmon </res|report|rel|sys>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /res | Startet die Ressourcenansicht. |
| /Report ein | Startet den Datensammler Satz für die System Diagnose und zeigt einen Bericht der Ergebnisse an. |
| /rel | Startet den Zuverlässigkeits Monitor. |
| /sys | Startet den System Monitor. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Windows-Leistungsüberwachung](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc749154(v%3dws.11))
