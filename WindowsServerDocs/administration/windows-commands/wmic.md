---
title: wmic
description: Referenz Artikel für WMIC, in dem WMI-Informationen in einer interaktiven Befehlsshell angezeigt werden.
ms.topic: reference
ms.assetid: 76397c72-d06f-4cea-88cf-c7603315a983
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6396f3e6ebc39722c3f1a79d32d629b206cceba2
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038088"
---
# <a name="wmic"></a>wmic



Zeigt WMI-Informationen in einer interaktiven Befehlsshell an.



## <a name="syntax"></a>Syntax

```
wmic </parameter>
```

## <a name="sub-commands"></a>Unterbefehle

Die folgenden Unterbefehle sind jederzeit verfügbar:

|Unterbefehl|Beschreibung|
|-----------|-----------|
|class|Schützt den Standardalias Modus von WMIC, um direkt auf Klassen im WMI-Schema zuzugreifen.|
|path|Gibt einen Escapezeichen aus dem Standardalias Modus von WMIC für den direkten Zugriff auf Instanzen im WMI-Schema aus.|
|context|Zeigt die aktuellen Werte aller globalen Switches an.|
|[Beenden Beenden \| ]|Beendet die WMIC-Befehlsshell.|

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die aktuellen Werte aller globalen Switches anzuzeigen:
```
wmic context
```
Ausgabe ähnlich der folgenden anzeigen:
```
NAMESPACE    : root\cimv2
ROLE         : root\cli
NODE(S)      : BOBENTERPRISE
IMPLEVEL     : IMPERSONATE
[AUTHORITY   : N/A]
AUTHLEVEL    : PKTPRIVACY
LOCALE       : ms_409
PRIVILEGES   : ENABLE
TRACE        : OFF
RECORD       : N/A
INTERACTIVE  : OFF
FAILFAST     : OFF
OUTPUT       : STDOUT
APPEND       : STDOUT
USER         : N/A
AGGREGATE    : ON
```
Wenn Sie die von der Befehlszeile verwendete Sprach-ID in Englisch (Gebiets Schema-ID 409) ändern möchten, geben Sie Folgendes ein:
```
wmic /locale:ms_409
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
