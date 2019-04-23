---
title: taskkill
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2b71e792-08b6-46d4-95a5-cb6336a79524
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: db264181ef8e5e3632f3312ade61183cac3fc8f5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853081"
---
# <a name="taskkill"></a>taskkill

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Beendet eine oder mehrere Aufgaben oder Prozesse. Prozesse können nach Prozess-ID oder Imagename beendet werden. **Taskkill** ersetzt die **kill** Tool.
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax
```
taskkill [/s <computer> [/u [<Domain>\]<UserName> [/p [<Password>]]]] {[/fi <Filter>] [...] [/pid <ProcessID> | /im <ImageName>]} [/f] [/t]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/s \<computer>|Gibt den Namen oder die IP-Adresse eines Remotecomputers (umgekehrte Schrägstriche nicht verwenden). Der Standardwert ist der lokale Computer.|
|/ u \<Domäne >\\\<Benutzername >|Führt den Befehl mit den Berechtigungen des Benutzers, der angegebenen *Benutzername* oder *Domäne*\\*Benutzername*. **/ u** können angegeben werden, wenn **/s** angegeben ist. Der Standardwert ist die Berechtigungen des Benutzers, der derzeit auf dem Computer angemeldet ist, die den Befehl ausgegeben wird.|
|/ p \<Kennwort >|Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.|
|/fi \<Filter>|Wendet einen Filter, um eine Reihe von Aufgaben auszuwählen. Sie können mehr als ein Filter oder verwenden Sie das Platzhalterzeichen (**\***) Geben Sie alle Aufgaben oder Namen von Images. Finden Sie in der folgenden [Tabelle gültiger Filternamen](#BKMK_table), Operatoren und Werten.|
|"/ PID" \<Prozess-ID >|Gibt die Prozess-ID des Prozesses beendet werden soll.|
|/im \<ImageName >|Gibt den imagenamen des Prozesses beendet werden soll. Verwenden Sie das Platzhalterzeichen (**\***) an alle Namen von Images.|
|/f|Gibt an, dass Prozesse beendet werden. Dieser Parameter wird bei ignoriert; Alle remote-Prozesse werden beendet.|
|/t|Beendet den angegebenen Prozess und alle untergeordneten Prozesse werden gestartet.|

#### <a name="BKMK_table"></a>Filternamen, Operatoren und Werte
|Filtername|Gültige Operatoren|Gültige Werte|
|--------|----------|----------|
|STatUS|eq, ne|AUSFÜHRUNG &AMP;#124; REAGIERT NICHT &AMP;#124; UNBEKANNT|
|IMAGENAME|eq, ne|Name des Images|
|PID|eq, ne, gt, lt, ge, le|PID-Wert|
|SITZUNG|eq, ne, gt, lt, ge, le|Sitzungsnummer|
|CPUtime|eq, ne, gt, lt, ge, le|CPU-Zeit im Format *HH ***:*** MM ***:*** SS*, wobei *MM* und *SS* liegen zwischen 0 und 59 und *HH* ist ein vorzeichenloser Anzahl|
|MEMUSAGE|eq, ne, gt, lt, ge, le|Speicherverwendung in KB|
|BENUTZERNAME|eq, ne|Beliebiger gültiger Benutzername (*Benutzer* oder *Domäne*\\*Benutzer*)|
|DIENSTE|eq, ne|Dienstname|
|WINDOWTITLE|eq, ne|Fenstertitel|
|MODULE|eq, ne|DLL-Name|

## <a name="remarks"></a>Hinweise
* Die Filter WINDOWTITLE und STatUS werden nicht unterstützt, wenn einem Remotesystem angegeben wird.
* Das Platzhalterzeichen (**\***) wird akzeptiert, die **/im** option nur, wenn ein Filter angewendet wird.
* Beenden von Remoteprozessen immer durchgeführt wird erzwungen, unabhängig davon, ob die **/f** angegeben wird.
* Bereitstellen eines Computernamens zu dem hostnamensfilter führt dazu, dass das Herunterfahren und alle Prozesse beendet werden.
* Sie können **Tasklist** um zu bestimmen, den Prozess-ID (PID) für den Prozess beendet wird.

## <a name="examples"></a>Beispiele
Geben zum Beenden der Prozesse mit dem Prozess-IDs 1230 1241 und 1253, ein:
```
taskkill /pid 1230 /pid 1241 /pid 1253
```
Geben Sie Folgendes ein, um das Beenden des Prozesses "Notepad.exe". wenn er vom System gestartet wurde:
```
taskkill /f /fi "USERNAME eq NT AUTHORITY\SYSTEM" /im notepad.exe
```
Geben Sie Folgendes ein, um alle Prozesse auf dem Remotecomputer "Srvmain" mit einem Image Name mit "Note" beginnt und mit den Anmeldeinformationen für das Benutzerkonto, das Hiropln zu beenden:
```
taskkill /s srvmain /u maindom\hiropln /p p@ssW23 /fi "IMAGENAME eq note*" /im *
```
Beendet den Prozess mit der Prozess-ID 2134 sowie vorhandene untergeordnete verarbeitet, die gestartet, sondern nur, wenn die Prozesse gestartet wurden, durch das Administratorkonto, geben Sie folgende Aktionen ausführen:
```
taskkill /pid 2134 /t /fi "username eq administrator"
```
Um alle Prozesse zu beenden, die Prozess-ID größer als oder gleich 1000, unabhängig von deren imagenamen aus, geben Sie Folgendes ein:
```
taskkill /f /fi "PID ge 1000" /im *
```

#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilensyntax](command-line-syntax-key.md)
