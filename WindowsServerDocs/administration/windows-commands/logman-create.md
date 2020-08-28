---
title: logman create
description: Referenz Artikel für den Befehl logman Create, der einen Counter, eine Ablauf Verfolgung, einen Konfigurationsdaten Sammler oder eine API erstellt.
ms.topic: reference
ms.assetid: 972f0126-7bc4-4b14-9265-062864f3ffd4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8635bfef8e9a82175348bdc06b5b722c8a1e733d
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89023814"
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
| [logman create counter](logman-create-counter.md) | Erstellt einen Counter-Datensammler. |
| [logman create trace](logman-create-trace.md) | Erstellt einen Ablauf Verfolgungs Datensammler. |
| [logman create alert](logman-create-alert.md) | Erstellt einen Warnungs Datensammler. |
| [logman create cfg](logman-create-cfg.md) | Erstellt einen Konfigurationsdaten Sammler. |
| [logman create api](logman-create-api.md) | Erstellt einen API-Ablauf Verfolgungs Datensammler. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [logman-Befehl](logman.md)