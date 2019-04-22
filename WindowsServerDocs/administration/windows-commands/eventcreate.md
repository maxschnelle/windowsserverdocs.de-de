---
title: eventcreate
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f2b1b26d-a70e-49a6-832b-91eb5a1a159a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 80d575364adbeba9d9ea4da75a0a866bcc02acea
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818711"
---
# <a name="eventcreate"></a>eventcreate



Kann ein Administrator ein benutzerdefiniertes Ereignis in ein bestimmtes Ereignisprotokoll zu erstellen. Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
eventcreate [/s <Computer> [/u <Domain\User> [/p <Password>]] {[/l {APPLICATION|SYSTEM}]|[/so <SrcName>]} /t {ERROR|WARNING|INFORMATION|SUCCESSAUDIT|FAILUREAUDIT} /id <EventID> /d <Description>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ s \<Computer >|Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer.|
|/ u \<"Domäne\Benutzer" >|Führt den Befehl mit den Berechtigungen des Benutzers gemäß \<Benutzer > oder < Domäne\Benutzername >. Der Standardwert ist die Berechtigungen von der aktuell angemeldete Benutzer auf dem Computer, die der Befehl ausgegeben wird.|
|/ p \<Kennwort >|Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.|
|/ l {Anwendung\|SYSTEM}|Gibt den Namen des Ereignisprotokolls, in dem das Ereignis erstellt wird. Die Namen gültiger sind ANWENDUNGS- und SYSTEMPROTOKOLL.|
|/ So \<SrcName >|Gibt die Quelle für das Ereignis an. Eine gültige Quelle kann eine beliebige Zeichenfolge sein und sollte darstellen, die Anwendung oder Komponente, die das Ereignis generiert.|
|/ t / {Fehler\|Warnung\|Informationen\|</br>SUCCESSAUDIT\|FAILUREAUDIT%}|Gibt den Typ des Ereignisses erstellen. Die gültigen Typen sind Fehler, Warnung, INFORMATION, SUCCESSAUDIT und FAILUREAUDIT%.|
|/ ID \<EventID >|Gibt die Ereignis-ID für das Ereignis an. Eine gültige ID ist eine beliebige Zahl zwischen 1 und 1000.|
|/ d \<Beschreibung >|Gibt die Beschreibung für die neu erstellte Ereignis.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Benutzerdefinierte Ereignisse können nicht in das Sicherheitsprotokoll geschrieben werden.

## <a name="BKMK_examples"></a>Beispiele für

Die folgenden Beispiele zeigen, wie Sie die Eventcreate-Befehl verwenden können:
```
eventcreate /t error /id 100 /l application /d "Create event in application log"
eventcreate /t information /id 1000 /so winmgmt /d "Create event in WinMgmt source"
eventcreate /t error /id 2001 /so winword /l application /d "new src Winword in application log"
eventcreate /s server /t error /id 100 /l application /d "Remote machine without user credentials"
eventcreate /s server /u user /p password /id 100 /t error /l application /d "Remote machine with user credentials"
eventcreate /s server1 /s server2 /u user /p password /id 100 /t error /so winmgmt /d "Creating events on Multiple remote machines"
eventcreate /s server /u user /id 100 /t warning /so winmgmt /d "Remote machine with partial user credentials"
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)
