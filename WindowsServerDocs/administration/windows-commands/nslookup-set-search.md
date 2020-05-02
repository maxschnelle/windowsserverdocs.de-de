---
title: nslookup set search
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 064ac660-8b04-4af9-8b2c-e4e0549771b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2e3f5bce42d3614b535b2dfb00c4c9ea9cac2346
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723566"
---
# <a name="nslookup-set-search"></a>nslookup set search



Fügt Domain Name System die DNS-Domänen Namen (DNS) in der DNS-Domänen Suchliste an die Anforderung an, bis eine Antwort empfangen wird. Dies gilt, wenn die Set-und die Suche-Anforderung mindestens einen Zeitraum enthalten, aber nicht mit einem nachfolgenden Zeitraum enden.

## <a name="syntax"></a>Syntax

```
set [no]search
```

### <a name="parameters"></a>Parameter

|  Parameter   |                                                                          BESCHREIBUNG                                                                          |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **noSearch** |                            Beendet das Anfügen der Domain Name System (DNS)-Domänen Namen in der DNS-Domänen Suchliste an die Anforderung.                            |
|  **search**  | Fügt Domain Name System die DNS-Domänen Namen (DNS) in der DNS-Domänen Suchliste an die Anforderung an, bis eine Antwort empfangen wird. Die Standard Syntax lautet **Search**. |
|    {Hilfe     |                                                                              ?}                                                                               |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)