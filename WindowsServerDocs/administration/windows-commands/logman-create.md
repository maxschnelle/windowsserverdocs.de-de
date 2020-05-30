---
title: logman create
description: Referenz Thema für den Befehl logman Create, der einen Counter, eine Ablauf Verfolgung, einen Konfigurationsdaten Sammler oder eine API erstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 972f0126-7bc4-4b14-9265-062864f3ffd4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c4a68be098f868cdd9cd48c1e7c68fc183fa1fab
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222954"
---
# <a name="logman-create"></a>logman create

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt einen Counter, eine Ablauf Verfolgung, einen Konfigurationsdaten Sammler oder eine API.

## <a name="syntax"></a>Syntax

```
logman create <counter | trace | alert | cfg | api> <[-n] <name>> [options]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| [logman Create Counter](logman-create-counter.md) | Erstellt einen Counter-Datensammler. |
| [logman Create Trace](logman-create-trace.md) | Erstellt einen Ablauf Verfolgungs Datensammler. |
| [Warnung zu logman Create](logman-create-alert.md) | Erstellt einen Warnungs Datensammler. |
| [logman Create cfg](logman-create-cfg.md) | Erstellt einen Konfigurationsdaten Sammler. |
| [logman Create-API](logman-create-api.md) | Erstellt einen API-Ablauf Verfolgungs Datensammler. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [logman-Befehl](logman.md)