---
title: wmic
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76397c72-d06f-4cea-88cf-c7603315a983
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e9840bc20ddf6193241fe36055698e2bd3222496
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361878"
---
# <a name="wmic"></a>wmic



Zeigt WMI-Informationen in einer interaktiven Befehlsshell an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
command </parameter>
```

## <a name="sub-commands"></a>Unterbefehle

Die folgenden Unterbefehle sind jederzeit verfügbar:

|Unterbefehl|Beschreibung|
|-----------|-----------|
|Klasse|Schützt den Standardalias Modus von WMIC, um direkt auf Klassen im WMI-Schema zuzugreifen.|
|path|Gibt einen Escapezeichen aus dem Standardalias Modus von WMIC für den direkten Zugriff auf Instanzen im WMI-Schema aus.|
|Kontext|Zeigt die aktuellen Werte aller globalen Switches an.|
|[beenden \| beenden]|Beendet die WMIC-Befehlsshell.|

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|</parameter>|\<concise Description, beginnt mit einem Verb. >|
|</param2>|\<eine kurze Kurzbeschreibung, beginnt mit einem Verb. >|


## <a name="BKMK_examples"></a>Beispiele

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

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)