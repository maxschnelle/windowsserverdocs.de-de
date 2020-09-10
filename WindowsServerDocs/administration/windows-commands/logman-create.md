---
title: logman create
description: Referenz Artikel für den Befehl logman Create, der einen Counter, eine Ablauf Verfolgung, einen Konfigurationsdaten Sammler oder eine API erstellt.
ms.topic: reference
ms.assetid: 972f0126-7bc4-4b14-9265-062864f3ffd4
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1115591f097c81b9b23dedbf3739c10346d4932e
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640371"
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
| [logman create counter](logman-create-counter.md) | Erstellt einen Counter-Datensammler. |
| [logman create trace](logman-create-trace.md) | Erstellt einen Ablauf Verfolgungs Datensammler. |
| [logman create alert](logman-create-alert.md) | Erstellt einen Warnungs Datensammler. |
| [logman create cfg](logman-create-cfg.md) | Erstellt einen Konfigurationsdaten Sammler. |
| [logman create api](logman-create-api.md) | Erstellt einen API-Ablauf Verfolgungs Datensammler. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [logman-Befehl](logman.md)