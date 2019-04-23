---
title: tasklist
description: Erfahren Sie, wie Sie eine Liste der auf dem lokalen Computer oder Remotecomputer ausgeführten Prozesse anzuzeigen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8dbe30ee-1484-46be-917b-5ca3ff4fdc9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: abb36c8c794836387af5547f3706e910dc06fa42
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843001"
---
# <a name="tasklist"></a>tasklist

Zeigt eine Liste der aktuell auf dem lokalen Computer oder auf einem Remotecomputer ausgeführten Prozesse an. **TaskList** ersetzt die **Tlist** Tool.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
tasklist [/s <Computer> [/u [<Domain>\]<UserName> [/p <Password>]]] [{/m <Module> | /svc | /v}] [/fo {table | list | csv}] [/nh] [/fi <Filter> [/fi <Filter> [ ... ]]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ s \<Computer >|Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer.|
|/ u [\<Domäne >\\\]\<Benutzername >|Führt den Befehl mit den Berechtigungen des Benutzers, der angegebenen *Benutzername* oder *Domäne*\*Benutzername *. **/ u** können angegeben werden, wenn **/s** angegeben ist. Der Standardwert ist die Berechtigungen des Benutzers, der derzeit auf dem Computer angemeldet ist, die den Befehl ausgegeben wird.|
|/ p \<Kennwort >|Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.|
|/ m \<Modul >|Führt alle Aufgaben mit geladenen DLL-Module, die mit dem angegebenen Muster übereinstimmen. Wenn Sie der Namen des Moduls nicht angegeben ist, zeigt diese Option alle Module, die von jeder Aufgabe geladen werden.|
|/svc|Listet alle Dienstinformationen für jeden Prozess ohne abschneiden. Gültig, wenn die **/Fo** Parametersatz zu **Tabelle**.|
|/v|Zeigt Informationen zum verbose-Vorgang in der Ausgabe. Verwenden Sie für die vollständige ausführliche Ausgabe ungekürzt **/v** und **/svc** zusammen.|
|/ Fo {Tabelle \| Liste \| Csv}|Gibt das Format für die Ausgabe verwendet. Gültige Werte sind **Tabelle**, **Liste**, und **Csv**. Das Standardformat für die Ausgabe ist **Tabelle**.|
|/nh|Unterdrückt die Spaltenüberschriften in der Ausgabe. Gültig, wenn die **/Fo** Parametersatz zu **Tabelle** oder **Csv**.|
|/fi \<Filter>|Gibt die Typen von Prozessen ein- oder Ausschließen aus der Abfrage. Finden Sie unter der folgenden Tabelle gültiger Filter, Operatoren und Werte.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

### <a name="filter-names-operators-and-values"></a>Filternamen, Operatoren und Werte

|Filtername|Gültige Operatoren|Gültige Werte|
|-----------|---------------|------------|
|STATUS|eq, ne|AUSFÜHREN VON | KEINE RÜCKMELDUNG | UNBEKANNT|
|IMAGENAME|eq, ne|Name des Images|
|PID|eq, ne, gt, lt, ge, le|PID-Wert|
|SITZUNG|eq, ne, gt, lt, ge, le|Sitzungsnummer|
|SESSIONNAME|eq, ne|Sitzungsname|
|CPUTIME|eq, ne, gt, lt, ge, le|CPU-Zeit im Format *HH ***:*** MM ***:*** SS*, wobei *MM* und *SS* liegen zwischen 0 und 59 und *HH* ist ein vorzeichenloser Anzahl|
|MEMUSAGE|eq, ne, gt, lt, ge, le|Speicherverwendung in KB|
|BENUTZERNAME|eq, ne|Beliebiger gültiger Benutzername|
|DIENSTE|eq, ne|Dienstname|
|WINDOWTITLE|eq, ne|Fenstertitel|
|MODULE|eq, ne|DLL-Name|

## <a name="remarks"></a>Hinweise

Die Filter WINDOWTITLE und STATUS werden nicht unterstützt, wenn einem Remotesystem angegeben wird.

## <a name="BKMK_examples"></a>Beispiele für

Zum Auflisten aller Aufgaben mit einer Prozess-ID, die größer als 1000 und in der CSV-Format anzuzeigen, geben Sie Folgendes ein:
```
tasklist /v /fi "PID gt 1000" /fo csv
```
Um Systemprozesse aufzulisten, die derzeit ausgeführt werden, geben Sie Folgendes ein:
```
tasklist /fi "USERNAME ne NT AUTHORITY\SYSTEM" /fi "STATUS eq running"
```
Um detaillierte Informationen für alle Prozesse aufzulisten, die derzeit ausgeführt werden, geben Sie Folgendes ein:
```
tasklist /v /fi "STATUS eq running"
```
Zum Auflisten alle Dienstinformationen für Prozesse, die auf dem Remotecomputer "Srvmain", die eine DLL-Namen mit "Ntdll" beginnt, geben Sie Folgendes ein:
```
tasklist /s srvmain /svc /fi "MODULES eq ntdll*"
```
Geben Sie Folgendes ein, um die Prozesse auf dem Remotecomputer "Srvmain," mit den Anmeldeinformationen Ihres Kontos derzeit angemeldeten Benutzers aufzulisten:
```
tasklist /s srvmain 
```
Geben Sie Folgendes ein, um die Prozesse auf dem Remotecomputer "Srvmain," mit den Anmeldeinformationen des Benutzerkontos Hiropln, aufzulisten:
```
tasklist /s srvmain /u maindom\hiropln /p p@ssW23
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)