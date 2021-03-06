---
title: nslookup set search
description: Referenz Artikel für den Befehl nslookup Set Search, der Domain Name System die DNS-Domänen Namen (DNS) in der DNS-Domänen Suchliste an die Anforderung anfügt, bis eine Antwort empfangen wird.
ms.topic: reference
ms.assetid: 064ac660-8b04-4af9-8b2c-e4e0549771b8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 91efbb50ab54a920be4c2942db1ea8b9cea71fbe
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637450"
---
# <a name="nslookup-set-search"></a>nslookup set search

Fügt Domain Name System die DNS-Domänen Namen (DNS) in der DNS-Domänen Suchliste an die Anforderung an, bis eine Antwort empfangen wird. Dies gilt, wenn die Set-und die Suche-Anforderung mindestens einen Zeitraum enthalten, aber nicht mit einem nachfolgenden Zeitraum enden.

## <a name="syntax"></a>Syntax

```
set [no]search
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| noSearch | Beendet das Anfügen der DNS-Domänen Namen (Domain Name System) in der DNS-Domänen Suchliste für die Anforderung. |
| search | Fügt Domain Name System die DNS-Domänen Namen (DNS) in der DNS-Domänen Suchliste für die Anforderung an, bis eine Antwort empfangen wird. Dies ist der Standardwert. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
