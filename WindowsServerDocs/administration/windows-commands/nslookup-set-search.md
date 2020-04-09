---
title: nslookup set search
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 064ac660-8b04-4af9-8b2c-e4e0549771b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9972919eae1be21d5dd30820d64dd1576b935666
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838303"
---
# <a name="nslookup-set-search"></a>nslookup set search



Fügt Domain Name System die DNS-Domänen Namen (DNS) in der DNS-Domänen Suchliste an die Anforderung an, bis eine Antwort empfangen wird. Dies gilt, wenn die Set-und die Suche-Anforderung mindestens einen Zeitraum enthalten, aber nicht mit einem nachfolgenden Zeitraum enden.

## <a name="syntax"></a>Syntax

```
set [no]search
```

### <a name="parameters"></a>Parameter

|  Parameter   |                                                                          Beschreibung                                                                          |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **noSearch** |                            Beendet das Anfügen der Domain Name System (DNS)-Domänen Namen in der DNS-Domänen Suchliste an die Anforderung.                            |
|  **Such**  | Fügt Domain Name System die DNS-Domänen Namen (DNS) in der DNS-Domänen Suchliste an die Anforderung an, bis eine Antwort empfangen wird. Die Standard Syntax lautet **Search**. |
|    {Hilfe     |                                                                              ?}                                                                               |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)