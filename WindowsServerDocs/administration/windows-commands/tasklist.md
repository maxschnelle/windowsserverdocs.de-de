---
title: tasklist
description: Referenz Artikel für den tasklist-Befehl, der eine Liste der Prozesse anzeigt, die auf dem lokalen Computer oder dem Remote Computer ausgeführt werden.
ms.topic: reference
ms.assetid: 8dbe30ee-1484-46be-917b-5ca3ff4fdc9c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: af89112d98cb7799a2fa910d562ac8c2a35bba19
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91718057"
---
# <a name="tasklist"></a>tasklist

Zeigt eine Liste der aktuell auf dem lokalen Computer oder auf einem Remotecomputer ausgeführten Prozesse an. **Tasklist** ersetzt das **tlist** -Tool.

> [!NOTE]
> Dieser Befehl ersetzt das **tlist** -Tool.

## <a name="syntax"></a>Syntax

```
tasklist [/s <computer> [/u [<domain>\]<username> [/p <password>]]] [{/m <module> | /svc | /v}] [/fo {table | list | csv}] [/nh] [/fi <filter> [/fi <filter> [ ... ]]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /s `<computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer. |
| /u `<domain>\<username>` | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der von `<username>` oder angegeben wird `<domain>\<username>` . Der **/u** -Parameter kann nur angegeben werden, wenn **/s** ebenfalls angegeben wird. Der Standardwert sind die Berechtigungen des Benutzers, der zurzeit an dem Computer angemeldet ist, der den Befehl ausgibt. |
| /p `<password>` | Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| /m `<module>` | Listet alle Tasks mit geladenen DLL-Modulen auf, die mit dem angegebenen Muster Namen identisch sind. Wenn der Modulname nicht angegeben ist, zeigt diese Option Alle Module an, die von den einzelnen Tasks geladen werden. |
| SVC | Listet alle Dienst Informationen für jeden Prozess ohne Abschneiden auf. Gültig, wenn der **/FO** -Parameter auf **Table**festgelegt ist. |
| /v | Zeigt ausführliche Aufgabeninformationen in der Ausgabe an. Verwenden Sie **/v** und **/svc ein** , um die ausführliche Ausgabe ohne Abschneiden zu vervollständigen. |
| /FO `{table | list | csv}` | Gibt das Format an, das für die Ausgabe verwendet werden soll. Gültige Werte sind " **Table**", " **List**" und " **CSV**". Das Standardformat für die Ausgabe ist **Table**. |
| /nh | Unterdrückt die Spaltenüberschriften in der Ausgabe. Gültig, wenn der **/FO** -Parameter auf **Table** oder **CSV**festgelegt ist. |
| /fi `<filter>` | Gibt die Typen von Prozessen an, die in die Abfrage eingeschlossen bzw. von dieser ausgeschlossen werden sollen. Sie können mehr als einen Filter verwenden oder das Platzhalter Zeichen ( `\` ) verwenden, um alle Aufgaben oder Bildnamen anzugeben. Die gültigen Filter sind im Abschnitt **Filter Namen, Operatoren und Werte** dieses Artikels aufgeführt.  |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="filter-names-operators-and-values"></a>Filter Namen, Operatoren und Werte

| Filter Name | Gültige Operatoren | Gültiger Wert (e) |
|--|--|--|
| STATUS | eq, ne | `RUNNING | NOT RESPONDING | UNKNOWN`. Dieser Filter wird nicht unterstützt, wenn Sie ein Remote System angeben. |
| ImageName | eq, ne | Imagename |
| PID | eq, ne, gt, lt, ge, le | PID-Wert |
| SESSION | eq, ne, gt, lt, ge, le | Sitzungsnummer |
| Sessionname | eq, ne | Sitzungsname |
| CPUtime | eq, ne, gt, lt, ge, le | CPU-Zeit im Format *hh: mm: SS*, wobei *mm* und *SS* zwischen 0 und 59 liegen und *HH* eine beliebige Zahl ohne Vorzeichen ist. |
| MEMUSAGE | eq, ne, gt, lt, ge, le | Speicherauslastung in KB |
| USERNAME | eq, ne | Beliebiger gültiger Benutzername ( `<user>` oder `<domain\user>` ) |
| DIENSTE | eq, ne | Dienstname |
| WindowTitle | eq, ne | Fenstertitel. Dieser Filter wird nicht unterstützt, wenn Sie ein Remote System angeben. |
| Modulen | eq, ne | DLL-Name |

## <a name="examples"></a>Beispiele

Wenn Sie alle Aufgaben mit einer *Prozess-ID größer als 1000*auflisten und *im CSV-Format anzeigen*möchten, geben Sie Folgendes ein:

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

Geben Sie Folgendes ein, um alle Dienst Informationen für Prozesse auf dem Remote Computer *srvmain*aufzulisten, der einen DLL-Namen hat, der *mit ntdll beginnt*:

```
tasklist /s srvmain /svc /fi "MODULES eq ntdll*"
```

Um die Prozesse auf dem Remote Computer *srvmain*mithilfe der Anmelde Informationen des aktuell angemeldeten Benutzerkontos aufzulisten, geben Sie Folgendes ein:

```
tasklist /s srvmain
```

Um die Prozesse auf dem Remote Computer *srvmain*mithilfe der Anmelde Informationen des *Benutzerkontos hiropln*aufzulisten, geben Sie Folgendes ein:

```
tasklist /s srvmain /u maindom\hiropln /p p@ssW23
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
