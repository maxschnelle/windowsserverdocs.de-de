---
title: wmic
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6c68866fbe0c8f5b16dae77e2121331f06cdc726
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885841"
---
# <a name="wmic"></a>wmic



Zeigt die WMI-Informationen in eine interaktive Befehlsshell.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
command </parameter>
```

## <a name="sub-commands"></a>Unterbefehle

Die folgenden Unterbefehle stehen immer zur Verfügung:

|Unterbefehl|Beschreibung|
|-----------|-----------|
|Klasse|Escapezeichen aus der Alias-Standardmodus von WMIC Klassen im WMI-Schema direkt zugreifen.|
|path|Der Alias-Standardmodus von WMIC im WMI-Schema direkt den Zugriff auf Instanzen beendet.|
|Kontext|Zeigt die aktuellen Werte aller globalen Schalter.|
|[beenden \| beenden]|Beendet die WMIC-Befehlsshell.|

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|</parameter>|\<Präzise Beschreibung, beginnt mit einem Verb. >|
|</param2>|\<Eine andere präzise Beschreibung, beginnt mit einem Verb. >|


## <a name="BKMK_examples"></a>Beispiele für

Um die aktuellen Werte aller globalen Schalter anzuzeigen, geben Sie Folgendes ein:
```
wmic context
```
Eine Ausgabe ähnlich der folgenden angezeigt:
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
Zum Ändern der Sprache verwendet die ID mithilfe der Befehlszeile auf Englisch (Gebietsschema-ID-409), Typ:
```
wmic /locale:ms_409
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)