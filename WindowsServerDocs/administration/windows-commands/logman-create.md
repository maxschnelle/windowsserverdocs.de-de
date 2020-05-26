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
ms.openlocfilehash: 1d4bffd68d5b74d1d6f36750967911dfec3f299a
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820590"
---
# <a name="logman-create"></a>logman create

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt einen Counter, eine Ablauf Verfolgung, einen Konfigurationsdaten Sammler oder eine API.

## <a name="syntax"></a>Syntax

```
logman create <counter | trace | alert | cfg | api> <[-n] <name>> [options]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| [logman Create Counter](logman-create-counter.md) | Erstellt einen Counter-Datensammler. |
| [logman Create Trace](logman-create-trace.md) | Erstellt einen Ablauf Verfolgungs Datensammler. |
| [Warnung zu logman Create](logman-create-alert.md) | Erstellt einen Warnungs Datensammler. |
| [logman Create cfg](logman-create-cfg.md) | Erstellt einen Konfigurationsdaten Sammler. |
| [logman Create-API](logman-create-api.md) | Erstellt einen API-Ablauf Verfolgungs Datensammler. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)