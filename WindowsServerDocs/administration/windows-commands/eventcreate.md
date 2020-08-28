---
title: eventcreate
description: Referenz Artikel für den eventcreate-Befehl, der es einem Administrator ermöglicht, ein benutzerdefiniertes Ereignis in einem angegebenen Ereignisprotokoll zu erstellen.
ms.topic: reference
ms.assetid: f2b1b26d-a70e-49a6-832b-91eb5a1a159a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 374dd015cdccbac308fa099854e46765a672ef9f
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89035198"
---
# <a name="eventcreate"></a>eventcreate

Ermöglicht es einem Administrator, ein benutzerdefiniertes Ereignis in einem angegebenen Ereignisprotokoll zu erstellen.

> [!IMPORTANT]
> Benutzerdefinierte Ereignisse können nicht in das Sicherheitsprotokoll geschrieben werden.

## <a name="syntax"></a>Syntax

```
eventcreate [/s <computer> [/u <domain\user> [/p <password>]] {[/l {APPLICATION|SYSTEM}]|[/so <srcname>]} /t {ERROR|WARNING|INFORMATION|SUCCESSAUDIT|FAILUREAUDIT} /id <eventID> /d <description>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- |------------ |
| /s `<computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| /u `<domain\user>` | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der von oder angegeben wird `<user>` `<domain\user>` . Der Standardwert sind die Berechtigungen des aktuell angemeldeten Benutzers auf dem Computer, von dem der Befehl ausgegeben wird. |
| /p `<password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| /l `{APPLICATION | SYSTEM}` | Gibt den Namen des Ereignis Protokolls an, in dem das Ereignis erstellt wird. Gültige Protokollnamen sind " **Application** " oder " **System**". |
| /so `<srcname>` | Gibt die Quelle an, die für das Ereignis verwendet werden soll. Eine gültige Quelle kann eine beliebige Zeichenfolge sein und die Anwendung oder Komponente darstellen, die das Ereignis erzeugt. |
| /t `{ERROR | WARNING | INFORMATION | SUCCESSAUDIT | FAILUREAUDIT}` | Gibt den Typ des zu erstellenden Ereignisses an. Gültige Typen sind " **Error**", " **Warning**", " **Information**", " **Success Audit**" und " **FAILUREAUDIT**". |
| /ID `<eventID>` | Gibt die Ereignis-ID für das Ereignis an. Eine gültige ID ist eine beliebige Zahl zwischen 1 und 1000. |
| /d `<description>` | Gibt die Beschreibung an, die für das neu erstellte Ereignis verwendet werden soll. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

In den folgenden Beispielen wird gezeigt, wie Sie den **eventcreate** -Befehl verwenden können:

```
eventcreate /t error /id 100 /l application /d Create event in application log
eventcreate /t information /id 1000 /so winmgmt /d Create event in WinMgmt source
eventcreate /t error /id 2001 /so winword /l application /d new src Winword in application log
eventcreate /s server /t error /id 100 /l application /d Remote machine without user credentials
eventcreate /s server /u user /p password /id 100 /t error /l application /d Remote machine with user credentials
eventcreate /s server1 /s server2 /u user /p password /id 100 /t error /so winmgmt /d Creating events on Multiple remote machines
eventcreate /s server /u user /id 100 /t warning /so winmgmt /d Remote machine with partial user credentials
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
