---
title: eventcreate
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f2b1b26d-a70e-49a6-832b-91eb5a1a159a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 797298622ba1021caef3d04e2f2f06f016ef6a70
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725762"
---
# <a name="eventcreate"></a>eventcreate



Ermöglicht es einem Administrator, ein benutzerdefiniertes Ereignis in einem angegebenen Ereignisprotokoll zu erstellen. 

## <a name="syntax"></a>Syntax

```
eventcreate [/s <Computer> [/u <Domain\User> [/p <Password>]] {[/l {APPLICATION|SYSTEM}]|[/so <SrcName>]} /t {ERROR|WARNING|INFORMATION|SUCCESSAUDIT|FAILUREAUDIT} /id <EventID> /d <Description>
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/s \<Computer>|Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.|
|/u \<Domäne \ Benutzer>|Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der \<durch die Benutzer> oder <Domäne \ Benutzer> angegeben ist. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird.|
|/p \<Password>|Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.|
|/l {Anwendungs\|System}|Gibt den Namen des Ereignis Protokolls an, in dem das Ereignis erstellt wird. Gültige Protokollnamen sind Application und System.|
|/so \<SrcName>|Gibt die Quelle an, die für das Ereignis verwendet werden soll. Eine gültige Quelle kann eine beliebige Zeichenfolge sein und die Anwendung oder Komponente darstellen, die das Ereignis erzeugt.|
|/t {Fehler\|Warnungs\|Informationen\|</br>\|FAILUREAUDIT} erfolgreich überwachen|Gibt den Typ des zu erstellenden Ereignisses an. Gültige Typen sind "Error", "Warning", "Information", "Success Audit" und "FAILUREAUDIT".|
|/ID \<EventID>|Gibt die Ereignis-ID für das Ereignis an. Eine gültige ID ist eine beliebige Zahl zwischen 1 und 1000.|
|/d \<Description>|Gibt die Beschreibung an, die für das neu erstellte Ereignis verwendet werden soll.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

-   Benutzerdefinierte Ereignisse können nicht in das Sicherheitsprotokoll geschrieben werden.

## <a name="examples"></a>Beispiele

In den folgenden Beispielen wird gezeigt, wie Sie den eventcreate-Befehl verwenden können:
```
eventcreate /t error /id 100 /l application /d Create event in application log
eventcreate /t information /id 1000 /so winmgmt /d Create event in WinMgmt source
eventcreate /t error /id 2001 /so winword /l application /d new src Winword in application log
eventcreate /s server /t error /id 100 /l application /d Remote machine without user credentials
eventcreate /s server /u user /p password /id 100 /t error /l application /d Remote machine with user credentials
eventcreate /s server1 /s server2 /u user /p password /id 100 /t error /so winmgmt /d Creating events on Multiple remote machines
eventcreate /s server /u user /id 100 /t warning /so winmgmt /d Remote machine with partial user credentials
```

#### <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
