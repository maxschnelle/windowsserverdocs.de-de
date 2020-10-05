---
title: taskkill
description: Referenz Artikel für taskkill, mit dem eine oder mehrere Tasks oder Prozesse beendet werden.
ms.topic: reference
ms.assetid: 2b71e792-08b6-46d4-95a5-cb6336a79524
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 71a443f4b588139a60b2330e668919a23250ba0f
ms.sourcegitcommit: 00406560a665a24d5a2b01c68063afdba1c74715
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91716891"
---
# <a name="taskkill"></a>taskkill

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beendet eine oder mehrere Aufgaben oder Prozesse. Prozesse können nach Prozess-ID oder Imagename beendet werden. **taskkill** ersetzt das **Kill** -Tool.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
taskkill [/s <computer> [/u [<Domain>\]<UserName> [/p [<Password>]]]] {[/fi <Filter>] [...] [/pid <ProcessID> | /im <ImageName>]} [/f] [/t]
```

### <a name="parameters"></a>Parameter

|         Parameter         |                                                                                                                                        BESCHREIBUNG                                                                                                                                        |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      /s \<computer>       |                                                                                    Gibt den Namen oder die IP-Adresse eines Remote Computers an (verwenden Sie keine umgekehrten Schrägstriche). Die Standardeinstellung ist der lokale Computer.                                                                                     |
| /u \<Domain>\\\<UserName> | Führt den Befehl mit den Konto Berechtigungen des Benutzers aus, der durch *Benutzername* oder *Domäne* \\ *Benutzername*angegeben ist. **/u** kann nur angegeben werden, wenn **/s** angegeben wird. Der Standardwert sind die Berechtigungen des Benutzers, der zurzeit an dem Computer angemeldet ist, der den Befehl ausgibt. |
|      /p \<Password>       |                                                                                                   Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                                                                   |
|       /fi \<Filter>       |          Wendet einen Filter an, um einen Satz von Tasks auszuwählen. Sie können mehr als einen Filter verwenden oder das Platzhalter Zeichen ( `*` ) verwenden, um alle Aufgaben oder Bildnamen anzugeben. [Gültige Filternamen](#filter-names-operators-and-values), Operatoren und Werte finden Sie in der folgenden Tabelle.           |
|     /PID \<ProcessID>     |                                                                                                                 Gibt die Prozess-ID des Prozesses an, der beendet werden soll.                                                                                                                 |
|     /im-Befehl \<ImageName>      |                                                                                Gibt den Bildnamen des Prozesses an, der beendet werden soll. Verwenden Sie das Platzhalter Zeichen ( `*` ), um alle Bildnamen anzugeben.                                                                                |
|            /f             |                                                                    Gibt an, dass Prozesse erzwungen werden. Dieser Parameter wird bei Remote Prozessen ignoriert. Alle Remote Prozesse werden erzwungen.                                                                     |
|            /t             |                                                                                                          Beendet den angegebenen Prozess und alle von ihm gestarteten untergeordneten Prozesse.                                                                                                          |

#### <a name="filter-names-operators-and-values"></a>Filter Namen, Operatoren und Werte

| Filter Name |    Gültige Operatoren     |                                                                Gültiger Wert (e)                                                                |
|-------------|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|   STATUS    |         eq, ne         |                                                 Ausführung &#124; antwortet &#124; unbekannt                                                 |
|  ImageName  |         eq, ne         |                                                                  Imagename                                                                  |
|     PID     | eq, ne, gt, lt, ge, le |                                                                  PID-Wert                                                                   |
|   SESSION   | eq, ne, gt, lt, ge, le |                                                                Sitzungsnummer                                                                |
|   CPUtime   | eq, ne, gt, lt, ge, le | CPU-Zeit im Format <em>HH</em>**:**<em>mm</em>**:**<em>SS</em>, wobei *mm* und *SS* zwischen 0 und 59 liegen und *HH* eine beliebige Zahl ohne Vorzeichen ist. |
|  MEMUSAGE   | eq, ne, gt, lt, ge, le |                                                              Speicherauslastung in KB                                                              |
|  USERNAME   |         eq, ne         |                                               Gültiger Benutzername (*Benutzer* oder *Domänen* \\ *Benutzer*)                                               |
|  DIENSTE   |         eq, ne         |                                                                 Dienstname                                                                 |
| WindowTitle |         eq, ne         |                                                                 Fenstertitel                                                                 |
|   Modulen   |         eq, ne         |                                                                   DLL-Name                                                                   |

## <a name="remarks"></a>Bemerkungen
* Die Filter WindowTitle und Status werden nicht unterstützt, wenn ein Remote System angegeben wird.
* Das Platzhalter Zeichen ( `*` ) wird für die **/im-Befehl** -Option nur akzeptiert, wenn ein Filter angewendet wird.
* Die Beendigung von Remote Prozessen wird immer erzwungen, unabhängig davon, ob die **/f** -Option angegeben ist.
* Wenn Sie einen Computernamen für den Host Namen Filter bereitstellen, wird ein Herunterfahren ausgelöst, und alle Prozesse werden beendet.
* Sie können **tasklist** verwenden, um die Prozess-ID (PID) für die Beendigung des Prozesses zu bestimmen.

## <a name="examples"></a>Beispiele

Um die Prozesse mit den Prozess-IDs 1230, 1241 und 1253 zu beenden, geben Sie Folgendes ein:

```
taskkill /pid 1230 /pid 1241 /pid 1253
```

Um den Prozess zu erzwingen Notepad.exe wenn er vom System gestartet wurde, geben Sie Folgendes ein:

```
taskkill /f /fi "USERNAME eq NT AUTHORITY\SYSTEM" /im notepad.exe
```

Um alle Prozesse auf dem Remote Computer srvmain mit einem Image Namen zu beenden, der mit Note beginnt, geben Sie bei Verwendung der Anmelde Informationen für das Benutzerkonto "hiropln" Folgendes ein:

```
taskkill /s srvmain /u maindom\hiropln /p p@ssW23 /fi "IMAGENAME eq note*" /im *
```

Um den Prozess mit der Prozess-ID 2134 und allen untergeordneten Prozessen zu beenden, die gestartet wurden, aber nur, wenn diese Prozesse vom Administrator Konto gestartet wurden, geben Sie Folgendes ein:

```
taskkill /pid 2134 /t /fi "username eq administrator"
```

Um alle Prozesse zu beenden, die eine Prozess-ID haben, die größer oder gleich 1000 ist, unabhängig von Ihren Image Namen, geben Sie Folgendes ein:

```
taskkill /f /fi "PID ge 1000" /im *
```

## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
