---
title: eventcreate
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f2b1b26d-a70e-49a6-832b-91eb5a1a159a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 79b10963abef9918e5962fdaf7d387a129873452
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845093"
---
# <a name="eventcreate"></a>eventcreate



Ermöglicht es einem Administrator, ein benutzerdefiniertes Ereignis in einem angegebenen Ereignisprotokoll zu erstellen. Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
eventcreate [/s <Computer> [/u <Domain\User> [/p <Password>]] {[/l {APPLICATION|SYSTEM}]|[/so <SrcName>]} /t {ERROR|WARNING|INFORMATION|SUCCESSAUDIT|FAILUREAUDIT} /id <EventID> /d <Description>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/s \<Computer >|Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.|
|/u \<Domäne \ Benutzer >|Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch \<Benutzer > oder < Domäne \ Benutzer > angegeben wird. Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird.|
|/p \<Kennwort >|Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.|
|/l {Application\|System}|Gibt den Namen des Ereignis Protokolls an, in dem das Ereignis erstellt wird. Gültige Protokollnamen sind Application und System.|
|/so \<SrcName >|Gibt die Quelle an, die für das Ereignis verwendet werden soll. Eine gültige Quelle kann eine beliebige Zeichenfolge sein und die Anwendung oder Komponente darstellen, die das Ereignis erzeugt.|
|/t {Fehler\|Warnung\|Informationen\|</br>Erfolgreiches Audit\|FAILUREAUDIT}|Gibt den Typ des zu erstellenden Ereignisses an. Gültige Typen sind "Error", "Warning", "Information", "Success Audit" und "FAILUREAUDIT".|
|/ID \<EventID >|Gibt die Ereignis-ID für das Ereignis an. Eine gültige ID ist eine beliebige Zahl zwischen 1 und 1000.|
|/d \<Beschreibung >|Gibt die Beschreibung an, die für das neu erstellte Ereignis verwendet werden soll.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Benutzerdefinierte Ereignisse können nicht in das Sicherheitsprotokoll geschrieben werden.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

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

#### <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
