---
title: tasklist
description: Erfahren Sie, wie Sie eine Liste der Prozesse anzeigen, die auf dem lokalen Computer oder Remote Computer ausgeführt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8dbe30ee-1484-46be-917b-5ca3ff4fdc9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b43f4c9a89fa60f2244253d48d3dca646fe8e02d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833433"
---
# <a name="tasklist"></a>tasklist

Zeigt eine Liste der aktuell auf dem lokalen Computer oder auf einem Remotecomputer ausgeführten Prozesse an. **Tasklist** ersetzt das **tlist** -Tool.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
tasklist [/s <Computer> [/u [<Domain>\]<UserName> [/p <Password>]]] [{/m <Module> | /svc | /v}] [/fo {table | list | csv}] [/nh] [/fi <Filter> [/fi <Filter> [ ... ]]]
```

### <a name="parameters"></a>Parameter

|          Parameter           |                                                                                                                                            Beschreibung                                                                                                                                             |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        /s \<Computer >        |                                                                                         Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Der Standardwert ist der lokale Computer.                                                                                         |
| /u [\<Domänen >\\\]\<Benutzername > | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch *username* oder *Domain*\*username angegeben wird<em>. \*\*/u</em> -\* kann nur angegeben werden, wenn **/s** angegeben wird. Der Standardwert sind die Berechtigungen des Benutzers, der zurzeit an dem Computer angemeldet ist, der den Befehl ausgibt. |
|        /p \<Kennwort >        |                                                                                                       Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                                                                        |
|         /m \<-Modul >         |                                                               Listet alle Tasks mit geladenen DLL-Modulen auf, die mit dem angegebenen Muster Namen identisch sind. Wenn der Modulname nicht angegeben ist, zeigt diese Option Alle Module an, die von den einzelnen Tasks geladen werden.                                                                |
|             /SVC ein             |                                                                                    Listet alle Dienst Informationen für jeden Prozess ohne Abschneiden auf. Gültig, wenn der **/FO** -Parameter auf **Table**festgelegt ist.                                                                                    |
|              /v              |                                                                                 Zeigt ausführliche Aufgabeninformationen in der Ausgabe an. Verwenden Sie **/v** und **/svc ein** , um die ausführliche Ausgabe ohne Abschneiden zu vervollständigen.                                                                                 |
|  /FO {Table \| Liste \| CSV}  |                                                                             Gibt das Format an, das für die Ausgabe verwendet werden soll. Gültige Werte sind " **Table**", " **List**" und " **CSV**". Das Standardformat für die Ausgabe ist **Table**.                                                                             |
|             /nh              |                                                                                             Unterdrückt die Spaltenüberschriften in der Ausgabe. Gültig, wenn der **/FO** -Parameter auf **Table** oder **CSV**festgelegt ist.                                                                                              |
|        /fi \<Filter >         |                                                                          Gibt die Typen von Prozessen an, die in die Abfrage eingeschlossen bzw. von dieser ausgeschlossen werden sollen. Gültige Filternamen, Operatoren und Werte finden Sie in der folgenden Tabelle.                                                                          |
|              /?              |                                                                                                                                Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                |

### <a name="filter-names-operators-and-values"></a>Filter Namen, Operatoren und Werte

| Filter Name |    Gültige Operatoren     |                                                                 Gültige Werte                                                                 |
|-------------|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|   STATUS    |         eq, ne         |                                                                   WIRD AUSGEFÜHRT                                                                    |
|  ImageName  |         eq, ne         |                                                                  Bildname                                                                  |
|     PID     | eq, ne, gt, lt, ge, le |                                                                  PID-Wert                                                                   |
|   SITZUNG   | eq, ne, gt, lt, ge, le |                                                                Sitzungsnummer                                                                |
| Sessionname |         eq, ne         |                                                                 Sitzungsname                                                                 |
|   CPUTIME   | eq, ne, gt, lt, ge, le | CPU-Zeit im Format <em>HH</em> **:** <em>mm</em> **:** <em>SS</em>, wobei *mm* und *SS* zwischen 0 und 59 liegen und *HH* eine beliebige Zahl ohne Vorzeichen ist. |
|  MEMUSAGE   | eq, ne, gt, lt, ge, le |                                                              Speicherauslastung in KB                                                              |
|  BENUTZERNAME   |         eq, ne         |                                                             Gültiger Benutzername                                                              |
|  DIENSTE   |         eq, ne         |                                                                 Dienstname                                                                 |
| WindowTitle |         eq, ne         |                                                                 Fenstertitel                                                                 |
|   Modulen   |         eq, ne         |                                                                   DLL-Name                                                                   |

## <a name="remarks"></a>Hinweise

Die Filter WindowTitle und Status werden nicht unterstützt, wenn ein Remote System angegeben wird.

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele

Wenn Sie alle Aufgaben mit einer Prozess-ID größer als 1000 auflisten und im CSV-Format anzeigen möchten, geben Sie Folgendes ein:
```
tasklist /v /fi "PID gt 1000" /fo csv
```
Geben Sie Folgendes ein, um die System Prozesse aufzulisten, die zurzeit ausgeführt werden:
```
tasklist /fi "USERNAME ne NT AUTHORITY\SYSTEM" /fi "STATUS eq running"
```
Geben Sie Folgendes ein, um ausführliche Informationen zu allen derzeit laufenden Prozessen aufzulisten:
```
tasklist /v /fi "STATUS eq running"
```
Um alle Dienst Informationen für Prozesse auf dem Remote Computer "srvmain" aufzulisten, die einen DLL-Namen aufweisen, der mit "Ntdll" beginnt, geben Sie Folgendes ein:
```
tasklist /s srvmain /svc /fi "MODULES eq ntdll*"
```
Um die Prozesse auf dem Remote Computer "srvmain" mit den Anmelde Informationen Ihres aktuell angemeldeten Benutzerkontos aufzulisten, geben Sie Folgendes ein:
```
tasklist /s srvmain 
```
Um die Prozesse auf dem Remote Computer "srvmain" mit den Anmelde Informationen des Benutzerkontos "hiropln" aufzulisten, geben Sie Folgendes ein:
```
tasklist /s srvmain /u maindom\hiropln /p p@ssW23
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)